---
title:  "컴퓨터시스템관리 11주차 실습일지"
excerpt: "메일 서버를 구축하는 실습을 했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-06-05T18:57:00
--- 
## 실습 과제  
![](https://salmon99.github.io/assets/images/11week/4-1.PNG)  
server-b에 메일 서버를 만드는 것 까진 성공했는데, 무슨 이유에선지 모르겠지만 이전에 server에 만들었던 메일 서버의 아이피가 갑자기 바뀌었다....  
![](https://salmon99.github.io/assets/images/11week/4-2.PNG)  
![](https://salmon99.github.io/assets/images/11week/5.PNG)  
DNS서버(네임서버): (serverb)192.168.117.131  
메일서버: (server)192.168.117.129(였었다)  
  
## 새로 배운 내용  
**Mail Server**  
- Email의 송수신에서 사용되는 프로토콜
  
**SMTP(Simple Mail Transfer Protocol)**  
- 클라이언트가 메일을 보내거나, 메일 서버끼리 메일을 주고 받을 때 사용한다.  
  
**POP3(Post Office Protocol)**  
- 메일 서버에 도착되어 있는 메일을 클라이언트로 가져올 때 사용한다. (서버에서 로컬 장치로 다운로드)  
  
**IMAP(Internet Mail Access Protocol)**  
- POP3와 유사함, 중앙 서버에서 동기화를 한다.  
- 모든 장치에서 동일한 이메일을 확인 가능하다.  
  
## 문제가 발생하거나 고민한 내용  
![](https://salmon99.github.io/assets/images/11week/1.PNG)  
실습 마지막에, client에서 evolution을 이용하여 메일을 확인하는 과정에서 메일 계정 연결이 안된다고 오류 메세지가 떴다. 구글링을 열심히 해보아도 원인을 알 수 없어 골머리를 싸맸다.  
![](https://salmon99.github.io/assets/images/11week/2.PNG)  
그리고 client에서 nslookup에 mail.cs.ac.kr 을 입력해보니 주소에 메일서버 주소인 192.168.117.129가 나오는 게 아니라 dns서버 주소인 192.168.117.131이 나왔다. 그래서 내가 설정을 뭔가 잘못했구나 싶어서 server-b에서 cs.ac.kr.db 파일의 주소를 192.168.117.129로 수정했더니 잘 연결이 되었다.  
![](https://salmon99.github.io/assets/images/11week/3.PNG)  
  
## 참고할 만한 내용  
* [WARNING: local host name is not qualified](https://www.digitalwhores.net/2015/07/21/warning-local-host-name-digitalwhores-is-not-qualified-see-cfreadme-who-am-i/)  
* [리눅스(linux) hostname 변경하는 방법](https://webinformation.tistory.com/40)  
  
## 회고  
생각보다 예상치 못한 문제가 너무 많이 발생해서, 고쳐 보려고 구글링을 열심히 했다. 그런데도 이상한 곳에서 돌발상황이 많이 생겨서 도저히 고칠 수가 없어서 무력감을 느꼈다... 갑자기 아이피가 바뀌다니 중간에 무엇을 잘못했는지 전혀 모르겠다. 메일이 보내지는 것은 신기했지만 마음대로 되는 것이 없어서 힘들었다.