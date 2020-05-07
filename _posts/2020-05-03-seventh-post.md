---
title:  "컴퓨터시스템관리 7주차 실습일지"
excerpt: "shell 스크립트를 이용한 간단한 프로그래밍 실습을 했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-05-07T20:39:00
--- 
## 실습 과제  
shell 스크립트 중 현재 디렉터리에 존재하는 파일과 디렉터리의 개수를 세 주는 스크립트를 유용하다고 생각해 실행해 보았습니다.  
평소에 실습용으로 사용하는 리눅스 시스템은 항상 초기화를 하기 때문에 파일이나 디렉터리가 거의 없는 상태지만, 계속해서 사용하는 리눅스 시스템이라면 파일과 디렉터리가 아주 많을 것이기 때문에 간편하게 그것들의 개수를 알 수 있는 스크립트가 있으면 좋을 것이라고 생각했습니다.  
![](https://salmon99.github.io/assets/images/7week/2.PNG)  


## 새로 배운 내용  
**shell**  
사용자의 명령을 해석하여 Kernel에게 전달함.  
**shell script**  
명령어의 집합. 과정이 복잡해 하나라도 빠지면 문제가 생기거나, 매일 또는 주기적으로 해야하는 명령에 이용됨.  
**Bash(Bourne Agina SHell)**  
브라이언 폭스가 1989년 발표한 유닉스 shell. 우분투에서 기본으로 사용하는 shell이다.  
Alias(명령 단축 기능), History 기능, 연산 기능, 자동 이름 완성 기능 등 모두 Bash의 특징.  
**shell의 명령문 처리 방법**  
(프롬프트) 명령 [옵션...] [인자]  
ex) rm -rf /mydir  
**shell script에서의 환경 변수**  
- 미리 선언하지 않으며, 처음 변수에 값이 할당되면 자동으로 변수가 생성됨.  
- 변수에 넣는 모든 값은 문자열(string)으로 취급.  
- 변수 값을 사용하기 위해서는 변수명 앞에 $를 붙여서 사용. 변수에 값을 대입할 때는 $를 사용하지 않는다.  
- 대입연산자 '=' 좌우에는 공백이 없어야 함.  
- 파라미터 변수는 $0, $1, $2의 형태. 실행하는 명령의 각 부분을 변수로 지정함. 모든 인자는 $*으로 표현됨.  
  
(환경변수 설정) export 환경변수=값  
(환경변수 생성) export HI='hi'  
(환경변수 실행) echo $HI  
(환경변수 해제) unset HI  
  
**shell script에서의 조건문**  
- [ 조건 ]의 결과가 참 또는 거짓에 따라 동작하는 구조이다.  
- [ 조건 ] 안의 각 단어 사이에 공백이 있어야 함.  
- 조건문에서는 관계 연산자인 AND(-a/&&) 와  OR(-o/| |)를 사용한다.  
  
**shell script의 명령어**  
eval: 문자열을 명령어로 인식하고 실행함.  
export: 변수를 외부 변수로 선언함. 선언한 변수를 다른 프로그램에서도 사용 가능.  
set, $(command): 리눅스 명령을 결과로 사용하려면 '$(command)' 형식을 사용해야 한다. 결과를 파라미터로 사용할 때 set 사용함.  
shift: 파라미터 변수를 왼쪽으로 한 단계씩 이동시킨다.  

**shell 프로그래밍 디버깅**  
sh -n script.sh 문법 에러 검사, 실행 안함  
sh -v script.sh 명령어를 실행하기 전에 출력  
sh -x script.sh 명령어와 결과를 출력  
  
**cron과 at**  
cron: 주기적으로 반복되는 일을 자동으로 실행할 수 있도록 시스템 작업을 예약할 수 있음.  
cron과 관련된 데몬(서비스)은 crond, 관련 파일은 /etc/crontab  
/etc/crontab의 형식: 분 시 일 월 요일 사용자 실행명령 ex) 00 05 1 * * root cp -r /home /backup 매월 1일 새벽 5시 00분에 root가 /home 디렉터리를 /backup 디렉터리로 복사한다.  
at: 일회성 작업을 예약할 수 있음. ex) at 3:00am tomorrow 프롬포트에 예약 명령어 입력 후 <enter>, 완료되면 <ctrl>+<d>  
(취소) atrm 작업번호  

## 문제가 발생하거나 고민한 내용  
실습 도중에 backup.sh 파일이 실행되지 않아서 오류 메세지를 검색해 보았다.  
[] 사이에 반드시 [  ] 이런 식으로 띄어쓰기를 해야 하는 사소한 문제였지만, 똑같이 입력했는데도 실행되지 않는 것 같아서 고민을 많이 했다.  
![](https://salmon99.github.io/assets/images/7week/1.PNG)  
  
## 참고할 만한 내용  
* [shell 스크립트 실행 오류 해결](https://stackoverflow.com/questions/15849095/bash-shell-script-error-sh-missing)  
* [40 Simple Yet Effective Linux Shell Script Examples](https://www.ubuntupit.com/simple-yet-effective-linux-shell-script-examples/)
* [$@의 의미](https://stackoverflow.com/questions/9994295/what-does-mean-in-a-shell-script)  
* [리눅스 find 명령어 사용법](https://recipes4dev.tistory.com/156) 
  
## 회고  
평소에 c++ 혹은 c밖에 사용할 일이 없었는데, 새로운 문법의 shell 스크립트 프로그래밍을 해 본 것이 새로웠다. 마치 다른 프로그래밍 과목을 실습하는 느낌이었다. 다른 프로그래밍 과목은 실제 컴퓨터 시스템과 동떨어진 실습을 많이 하는데에 비해, 명령어를 이용하여 실제 리눅스 시스템을 조작할 수 있다는 점이 재밌었다. 