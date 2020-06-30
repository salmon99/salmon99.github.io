---
title:  "컴퓨터시스템관리 기말과제"
excerpt: "스타트업에서 사용할 시스템 환경을 구축하는 과제를 수행했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-06-30T16:15:00
--- 
## 환경 구축 계획  
**Client**  
- 사설 네트워크에 존재하는 스타트업 직원이 사용하는 컴퓨터이다. 원격접속 환경을 구축하고, 아이피를 10.1.1.10으로 설정.  
**Server(B)**  
- 원격접속 환경을 구축하고, 외부 네트워크와 사설 네트워크를 연결하는 방화벽 서버를 설치할 것이다. ens35의 아이피를 10.1.1.1로 설정하고, ens32의 아이피는 192.168.117.131로 설정.  
**Server**  
- 원격접속 환경을 구축하고, 사설 네트워크에 존재하는 컴퓨터로, 이곳에 네임(dns)서버, 메일서버, 웹 서버(apache2), 클라우드 서버(pydio)를 설치할 것이다. 아이피를 10.1.1.20으로 설정.

## 1. 방화벽 서버 구축  
방화벽 서버를 구축하며 사설 네트워크에 존재하는 컴퓨터의 아이피를 바꿀 것이기 때문에, 가장 먼저 방화벽 서버를 구축하려고 했다.    
![](https://salmon99.github.io/assets/images/finals/1.PNG)    
우선 내부 컴퓨터인 Server와 Client의 아이피 주소를 각각 10.1.1.20/10.1.1.10 으로 바꾸고, 게이트웨이 주소를 방화벽 컴퓨터의 주소인 10.1.1.1로 설정한 후, 나중에 네임서버를 설치할 Server의 주소를 네임서버에 추가했다.  
![](https://salmon99.github.io/assets/images/finals/3.PNG)    
그리고 방화벽 컴퓨터로 사용할 Server(B)의 ens32의 주소는 192.168.117.131로 두고, ens35의 주소를 10.1.1.1로 설정하였다. (네트워크 어뎁터를 하나 더 추가했다.)  
![](https://salmon99.github.io/assets/images/finals/2.PNG)    
그리고 Server에서 Client, Server(B)와 통신할 수 있는지 확인해보니 잘 되었다.  
![](https://salmon99.github.io/assets/images/finals/4.PNG)    
마찬가지로 Client에서 Server, Server(B)와도 통신을 할 수 있었다.  
그 다음으로, 방화벽 컴퓨터인 Server(B)의 방화벽 정책을 설정하였다.  
![](https://salmon99.github.io/assets/images/finals/5.PNG)    
(패킷 포워딩 활성화 옵션)  
![](https://salmon99.github.io/assets/images/finals/6.PNG)    
(정책 초기화, Server(B)의 ens35와 ens32에 모든 패킷이 통과하도록 설정)  
![](https://salmon99.github.io/assets/images/finals/7.PNG)    
(ens32에 마스커레이드 허가, 설정 내용 저장)  
![](https://salmon99.github.io/assets/images/finals/8.PNG)    
이후 Client에서 인터넷에 접속이 되는지 확인을 해 보았더니 잘 되었다.  
방화벽 서버가 올바르게 동작하고 있는 것을 확인할 수 있었다.  
  
## 2. 원격 접속 환경 구축  
Client, Server, Server(B) 세 컴퓨터 모두 openssh를 설치하고 linux, linuxs, linuxb 사용자를 만들었다.  
![](https://salmon99.github.io/assets/images/finals/12.PNG)    
![](https://salmon99.github.io/assets/images/finals/11.PNG)    
![](https://salmon99.github.io/assets/images/finals/10.PNG)    
내부 컴퓨터인 Client와 Server에 접속하기 위해 외부 컴퓨터에서 ssh를 이용해 Server(B)에 원격 접속한 후 Client와 Server에 각각 원격 접속해 보았다.  
![](https://salmon99.github.io/assets/images/finals/13.PNG)    
(windows terminal을 이용해 ssh로 Server(B)에 접속함)  
![](https://salmon99.github.io/assets/images/finals/14.PNG)    
(Server(B)로 접속한 후 다시 Client에 원격으로 접속함)  
![](https://salmon99.github.io/assets/images/finals/15.PNG)    
(Client에서 로그아웃 한 후 Server에 원격으로 접속함)  
원격 접속이 올바르게 동작하는 것을 확인할 수 있었다.  

## 3. 네임 서버, 메일 서버 구축  
Server에 네임 서버와 메일 서버를 구축하려고 했다.  
메일 서버의 주소는 mail.ft.ac.kr로 할 것이다.  
먼저, Server에 네임 서버 환경을 설정해 주었다.   
![](https://salmon99.github.io/assets/images/finals/16.PNG)    
Server에 bind9 패키지를 설치 후 named.conf.local 파일과 ft.ac.kr.db 파일을 수정해 주었다.  
![](https://salmon99.github.io/assets/images/finals/17.PNG)    
설정 완료 후 nslookup으로 네임 서버가 올바르게 동작하는 것을 확인할 수 있었다.  
그 다음으로 Server에 메일 서버를 설치하고 설정했다.  
![](https://salmon99.github.io/assets/images/finals/24.PNG)    
sendmail이 올바르게 작동하는지 메일을 보내서 테스트 해보았다.  
![](https://salmon99.github.io/assets/images/finals/25.PNG)    
sendmail이 올바르게 작동하는 것을 확인할 수 있었다.  
그리고 Client에서, Evolution을 이용하여 내부 네트워크에서 메일서버가 올바르게 작동하는지 확인해보았다.  
![](https://salmon99.github.io/assets/images/finals/28.PNG)    
Server에 미리 만들어 두었던 사용자 계정 linuxs를 이용하여 접속해 보기로 했다.  
![](https://salmon99.github.io/assets/images/finals/29.PNG)    
다행히도 메일서버에 접속되어 비밀번호를 묻는 창이 떴다. linuxs 사용자의 비밀번호를 입력하여 로그인을 했다.  
![](https://salmon99.github.io/assets/images/finals/30.PNG)    
아까 Server 컴퓨터를 이용하여 보낸 메일을 확인할 수 있는 걸 보아, 메일 서버가 내부 네트워크에서 올바르게 동작하는 것을 알 수 있었다.  

## 4. 클라우드 서비스 설치  
먼저, 클라우드 서비스를 설치할 Server에 APM을 설치해 주었다. (apache2, php, mysql)  
![](https://salmon99.github.io/assets/images/finals/31.PNG)    
그리고 나서 설치형 클라우드 서비스인 pydio를 설치하고, mysql을 이용해 계정을 만들었다.    
![](https://salmon99.github.io/assets/images/finals/32.PNG)    
![](https://salmon99.github.io/assets/images/finals/34.PNG)    
pydio가 제대로 동작하는지 확인하기 위해 Client에서 pydio에 접속해 보았다.  
![](https://salmon99.github.io/assets/images/finals/35.PNG)    
![](https://salmon99.github.io/assets/images/finals/36.PNG)    
![](https://salmon99.github.io/assets/images/finals/37.PNG)    
![](https://salmon99.github.io/assets/images/finals/38.PNG)    
Client에 먼저 다운로드 해두었던 사진을 pydio에 서버에 올림으로서 클라우드 서비스가 제대로 동작하는 것을 확인할 수 있었다.  
  
## 5. 웹 서버 구축  
Server에 웹 서버(apache2)를 설치하려고 했다.
위의 클라우드 서비스를 설치하면서 apache2를 설치했으므로, 방화벽 설정을 하고 실제로 동작하는지 확인을 하였다.  
![](https://salmon99.github.io/assets/images/finals/40.PNG)    
![](https://salmon99.github.io/assets/images/finals/41.PNG)    
호스트 컴퓨터에서 접속했을 때 apache2 화면이 뜨는 것으로 웹서버가 제대로 설치된 것을 확인할 수 있었다.  