Telnet은 구식 잊어라
대신 SSH 씀
# 기본

![[Pasted image 20260306091644.png]]
```
enable: 관리 모드
conf t: 전역 설정 모드
```
![[Pasted image 20260306091925.png]]
>[!warning]
>"#"에서 end하면 렉 먹음!

![[Pasted image 20260306092101.png]]
```
password 금지. secret 권장
비번 입력할떄 원래 안보임 당황 ㄴㄴ

'솔트' 라고하는 $과 $ 사이에 들어가는 문자가 있음.
```
![[Pasted image 20260306094925.png]]

![[Pasted image 20260306092243.png]]
![[Pasted image 20260306092414.png]]
![[Pasted image 20260306095039.png]]

# SSH

>[!warning]
>telnet 금지!

![[Pasted image 20260306102558.png]]
```
crypto key generate rsa: private key
[512]: size==복잡도. 가능 범위는 <중략>에 적혀있음
SSH 1.99 : 버젼 1이나 2 사용. 1은 보안 취약점 있음
line vty의 가짓수는 보통 0~4로 5개
transport intput ssh: SSH만 허용
config)# ip ssh version 2: 버젼 2 만 사용
```
![[Pasted image 20260306104451.png]]
