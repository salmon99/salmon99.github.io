---
title:  "컴퓨터시스템관리 8주차 실습일지"
excerpt: "중간고사 대체 실습과제와 네트워크 설정 실습을 했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-05-10T22:01:00
driveId1: 1_ERKFfLflT-7DOfqnduEQgwpEmZb2MDd/preview
driveId2: 1_6QjJRaZnzXTHXd4VH9j9tNTvtnLRzM8/preview
driveId3: 1m0TWBu9t674lITcryChW27mj7glqHG5J/preview
driveId4: 1lujvX1ZEw5ybAEnQHx8cwozX69a1j6_A/preview
--- 
## 실습 과제  
**1. 실무 환경의 우분투 설치**  
{% include googleDrivePlayer.html id=page.driveId1 %}  
  
**2. RAID 6 구성**  
{% include googleDrivePlayer.html id=page.driveId2 %}  
  
**3. 백업 자동화**  
{% include googleDrivePlayer.html id=page.driveId3 %}  
  
**4. 프로그램 개발 환경 구축**  
{% include googleDrivePlayer.html id=page.driveId4 %}  
  
## 새로 배운 내용  
**TCP/IP**  
- 통신의 송수신을 다루는 TCP(Transmission Control Protocol)(규약, 약속)  
- 데이터 통신을 다루는 IP(Internet Protocol)  
  
**Telnet**  
- 인터넷이나 로컬 영역 네트워크 연결에 쓰이는 네트워크 프로토콜  
- 1969년에 개발되었스며, TCP/IP 스택을 갖춘 대부분의 네트워크 장비와 운영체제에서 사용 가능  
- 보안 문제 때문에 SSH로 대체되고 있음  
  
**Telnet의 문제점**  
- 암호화되지 않은 데이터를 전송하여, 네트워크 스니핑(sniffing) , IP스푸핑(spoofing)과 같은 공격에 매우 취약  
- sniffing:네트워크 상의 패킷 삼청, 이 과정을 통해 패킷에 포함된 사용자의 아이디, 암호 같은 개인 정보를 탈취  
- spoofing: 호스트의 IP주소를 바꾸어 이를 통해 해커의 컴퓨터를 신뢰롭게 꾸며서 정보를 탈취  
   
**SSH(Secure SHell)**  
- 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해 주는 응용 프로그램 또는 그 프로토콜  
- 1995년 핀란드 헬싱키 공대 연구원인 Tatu Ylonen이 개발 및 공개하고, 이후 SSH Communication Security 사를 설립하여 상용화.  
- 기존 rsh, rlogin, telnet등을 대체하기 위해 설계  
- IP spoofing (호스트의 IP주소를 바꾸어 이를 통해 해킹)방지 기능 제공  
  
**Open SSH**  
-  SSH 프로토콜을 이용하여 암호화된 통신 세션을 컴퓨터 ㅔ트워크에 제공하는 컴퓨터 프로그램의 모임  
- 기존 상용화된 SSH 제품군을 대체할 목적으로 오픈소스로 작성 및 배포  
  
## 문제가 발생하거나 고민한 내용  
우분투 리눅스를 설치 후 존재하는 파티션을 모두 지우고 조건에 맞게 만드려고 하니 이미 사용중이라면서 오류 메세지가 떴다. 파티션을 만들고 리부트를 하니 응급모드로 들어가서 잘못된 걸 알아채고, 인터넷을 참고해서 리눅스 설치 전에 파티션을 나누었다.  
![](https://salmon99.github.io/assets/images/8week/1.PNG)  
![](https://salmon99.github.io/assets/images/8week/2.PNG)  
  
3번째 실습을 한 후에 인터넷에 접속하여 Visual Studio Code를 받으려고 하자가 뜨면서 로딩이 되지 않아서 오류 메세지를 검색해 보았다.  
오류 메세지: SEC_ERROR_OCSP_OLD_RESPONSE  
인터넷에 검색하니 시간 설정이 잘못되어 보안 문제가 있었다는 것을 알 수 있었다.  
  
## 참고할 만한 내용  
* [리눅스 파티션 관련 오류](https://unix.stackexchange.com/questions/477991/what-is-a-vfat-signature)  
* [SEC_ERROR_OCSP_OLD_RESPONSE 오류 해결 방법](https://support.mozilla.org/ko/kb/troubleshoot-time-errors-secure-websites)
  
## 회고  
처음에 실습 과제를 보며 지금까지 다 해봤던 것이지만 영구 마운트 설정 등을 할 생각에 눈앞이 캄캄했다. 그리고 실제로 해 보면서도 마음대로 되지 않아서 머리를 싸매고 있었는데, 어떤 학우분이 올려주신 질문을 참고한 것이 큰 도움이 되었다. 방법을 찾아서 인터넷을 참고하여 실습을 진행하니 생각보다 어렵지 않았다. 이번 주에는 과제도 밀리지 않고 해내서 뿌듯하다.