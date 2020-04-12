---
title:  "컴퓨터시스템관리 3주차 실습일지"
excerpt: "리눅스 시스템을 관리하는 명령어를 배웠다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-04-12T23:27:00
---
1) 생성한 계정 및 그룹 정보 캡처  
/etc/passwd 와 /etc/group 파일 정보 활용  
![](https://salmon99.github.io/assets/images/4week/1.png)  
groupadd 명령어를 이용하여 developer, web, db, office 그룹을 만들었습니다.
![](https://salmon99.github.io/assets/images/4week/2.png)  
그리고 adduser 명령어를 이용하여 w-user을 만들었고, 기본 그룹을 web으로 만들었습니다.  
위와 같은 방법으로 d-user와 o-user도 만들었습니다.  
![](https://salmon99.github.io/assets/images/4week/3.png)  
/etc/passwd 끝자락을 확인해 보면 w-user, d-user, o-user가 추가되었습니다.  
![](https://salmon99.github.io/assets/images/4week/4.png)  
/etc/group 끝자락을 확인해 보면 developser, web, db, office가 추가되어 있고, developer 그룹에 w-user, d-user이 추가되어 있는 것을 확인할 수 있습니다.  
  
2) /home/info 폴더의 소유권 및 허가권 정보 캡처  
ls 명령어 활용  
![](https://salmon99.github.io/assets/images/4week/5.png)  
/home/info 폴더의 소유권 및 허가권을 변경하기 전 모습입니다.  
![](https://salmon99.github.io/assets/images/4week/6.png)  
chgrp와 chmod 명령어를 이용하여 info 폴더의 그룹과 허가권을 변경했습니다.  
  
3) info.sh 실행 결과 캡처  
sh info.sh  
![](https://salmon99.github.io/assets/images/4week/8.png)  
info.sh 파일을 vi편집기로 열어 위와 같은 내용을 작성했습니다.  
![](https://salmon99.github.io/assets/images/4week/7.png)  
info.sh 파일을 실행한 화면입니다.  
  
4) info.sh 파일의 소유권 및 허가권 정보 캡처  
ls 명령어 활용  
![](https://salmon99.github.io/assets/images/4week/9.png)  
info 파일의 소유권 및 허가권을 바꿨습니다.  
그룹을 chgrp developer을 이용하여 w-user과 d-user이 들어가 있는 그룹으로 바꾸었고, chmod 764를 이용하여 그룹의 경우 읽고 쓸 수 있으며 그 외의 사람들은 읽기만 할 수 있도록 바꾸었습니다. 
![](https://salmon99.github.io/assets/images/4week/10.png)  
  
## 새로 배운 내용  
**압축 묶기와 풀기**  
컴퓨터를 사용하면서 windows로 압축 묶기와 풀기는 다른 프로그램(알집과 같은)이 있어야 가능하다고 생각했는데 리눅스에서 간단하게 명령어로 파일들을 묶거나 압축하고 풀 수 있다는 것을 알았다.  
  
**사용자 계정 생성과 관리**  
root 계정으로 간단하게 사용자를 만들어 관리할 수 있다는 것을 배웠다. 실습실에서 실습할 때 나는 계정을 만든 기억이 없지만 실습실을 관리하는 분들이 만들었겠다는 생각이 들었다. 
그 이외에 여러가지 계정을 관리하는 방법도 배워서, 언젠가 컴공과 조교를 해보고 싶다는 생각이 든다.  
  
**apt-get과 dpkg의 차이**
apt-get과 dpkg는 단순히 다른 종류의 명령어라고만 생각했고, 어떤 일을 하는 지는 잘 몰랐는데 수업을 들으면서 확실히 알게 됐다. 둘 다 패키지 설치 프로그램이지만 dpkg의 경우에는 의존성 문제로 설치되지 않을 수 있고, apt-get은 의존성 문제를 파악해서 자동으로 함께 설치해주기 때문에 훨씬 편리하다는 것을 알게 되었다.
  
**root계정의 비밀번호를 잊어버린 경우 해결방법**
GRUB 부트로더를 이용하여 패스워드를 설정할 수 있다는 것을 배웠다. 과정이 조금 복잡해서 완전히 기억하지는 못했지만, 다시 연습해 보면서 언젠가 비밀번호를 잊어버리는 상황이 생긴다면 활용해 봐야겠다.
  
## 문제가 발생하거나 고민한 내용  
과제를 하면서 교수님께서 공지사항에 sh info.sh 로 파일을 실행하라고 되어 있었는데 이상하게 파일을 실행할 수 없다는 메세지만 나왔다. 파일 허가권도 변경했는데 왜 안되는 지 알 수 없었다...   
  
## 참고할 만한 내용  
인터넷에 검색해 보았지만 해결하지 못했다.
  
## 회고    
교수님이 처음에 조교가 되었다고 생각하고 수업을 들으라고 해서 흥미있었다. 실제로 사용하는 사용자들의 정보를 관리하는 것도 해보고 싶다는 생각이 들었다. 그런데 실습을 하는 데에 시간이 오래 걸려서 과제를 자꾸 지각제출하게 된다. 다음부턴 미리 열심히 실습하고 제출하도록 해야겠다... 