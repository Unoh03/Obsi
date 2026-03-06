Telnet은 구식 잊어라
대신 SSH 씀
# 기본
![[강의 자료/CH03_Device configuration v1.3.pdf#page=15]]

```bash
enable: 관리 모드
conf t: 전역 설정 모드
```
![[강의 자료/CH03_Device configuration v1.3.pdf#page=16]]
>[!warning]
>"#"에서 end하면 렉 먹음!

![[강의 자료/CH03_Device configuration v1.3.pdf#page=17]]
```bash
password 금지. secret 권장
비번 입력할떄 원래 안보임 당황 ㄴㄴ

'솔트' 라고하는 $과 $ 사이에 들어가는 문자가 있음.
```
![[Pasted image 20260306094925.png]]

![[Pasted image 20260306092243.png]]
![[Pasted image 20260306092414.png]]
![[Pasted image 20260306095039.png]]

# [[SSH]]

>[!warning]
>telnet 금지!

![[Pasted image 20260306102558.png]]
```bash
crypto key generate rsa # private key 생성
# [512]: size==복잡도. 가능 범위는 <중략>에 적혀있음
# SSH 1.99 : 버젼 1이나 2 사용. 1은 보안 취약점 있음
# line vty의 가짓수는 보통 0~4로 5개
'(config-line)#'transport intput ssh # SSH만 허용
'(config)#' ip ssh version 2 # 버젼 2 만 사용
```
![[Pasted image 20260306104451.png]]

# [[실습 문제 1]]

![[Pasted image 20260306130934.png]]
```bash
1. 못하면 바보
2. en
   conf t
   ena sec 123
   user aaa sec 123
   lin con 0
   logi loc
   logg syn
   exec-time 5
   # 반대 라우터에도 동일하게
3. conf t
   int f0/0
   ip add 1.1.1.2 255.255.255.0
   no sh
   
   int f0/1
   ip add 12.12.12.1 255.255.255.0
   no sh
   # 반대 라우터 동일(ip 빼고)
4. #여기서 PC1에서 ping 2.2.2.1 하면 라우터1(1.1.1.2)에서 2.2.2.1을 몰라서 모른다고 응답 보냄(desti host unreach)
#PC1 에서 ping 12.12.12.2 하면 리퀘 탐 아웃. 이유는 까먹음
# 아직 1번 네트워크끼리, 2번 네트워크끼리, 라우터끼리만 통신 됨
5. # RSA(비대칭 키) 필요 상황
   conf t
   hostname '맘대로(라우터끼리 다르게)'
   ip domain-name '맘대로(둘이 같게)'
   cry k ge rsa
   2048 # 키 용량 설정. 보통 2048 많이 씀
   lin vty 0 4 
   logi loc
   transport input ssh
   logg syn
   exec-t 5
   exit
   ip ssh v 2
   
   #PC1에서
   ssh -l aaa 1.1.1.2
   #pc2에서
   ssh -l bbb 2.2.2.2
```

```bash
#하나의 네트워크가 있는 것처럼 하며 테스트를 하고싶을 땐 루프백 사용
conf t
int loopback 0
ip add 'ip 하고싶은거'
```

# [[실습 문제 2]]

![[Pasted image 20260306152834.png]]

```bash
# 라우터 기본 설정
en
conf t
no ip domain-lookup
ena sec cisco
username cisco sec cisco
lin con 0
logi loc
exec-t 10 30
logg syn
username cisco sec cisco
lin vty 0 4
logi loc
exec-t 5
logg syn
exit
hostname 

#인터페이스 설정
# 사용 가능 IP는 192.168.1.225, 192.168.1.226  섭넷 마스크 .252
en
conf t
int 
```