---
title:  "컴퓨터시스템관리 12주차 실습일지"
excerpt: "데이터베이스 서버를 구현하고 관련 파일을 생성하는 실습을 했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-06-06T16:58:00
--- 
## 실습 과제  
![](https://salmon99.github.io/assets/images/12week/2.PNG)  
![](https://salmon99.github.io/assets/images/12week/3.PNG)  
![](https://salmon99.github.io/assets/images/12week/4.PNG)  
![](https://salmon99.github.io/assets/images/12week/5.PNG)  
데이터베이스: market_db  
테이블: product_t, shop_t  
  
## 새로 배운 내용  
**DB(DataBase)**  
- 테이블을 저장하는 저장 공간 또는 테이블의 집합.
  
**DBMS(DataBase Management System)**  
- 데이터의 효율적인 관리(추가,삭제,검색,수정 등)를 위한 프로그램이다.  
- ex) Oracle, MS-SQL,MySQL,MariaDB 등  
  
**RDBMS(Relational DBMS)**  
- 테이블과의 관계성을 기반으로 둔 DBMS의 한 종류.  
- 사용자에게 행과 열을 집합으로 구성된 테이블의 묶음 형식으로 데이터를 제공한다.  
- 테이블 형식의 데이터를 조작할 수 있는 관계 연산자를 제공한다.  
  
**SQL(Structured Query Language)**  
- 데이터베이스를 조작하거나 접근할 수 있는 표준 언어.  
- 모든 DBMS에서 지원하고, 대소문자를 구분하지 않는다.(주로 명령어는 대문자로 작성한다.)   
  
**Oracle Database**  
- 1979년 발표된 미국 오라클(Oracle)사의 관계형 데이터베이스 관리 시스템(RDBMS).  
- 신뢰성이 담보되어야 하는 기업 등에서 활용된다.  
  
**MariaDB**  
- 2009년 발표된 오픈소스의 관계형 데이터베이스 관리 시스템(RDBMS).  
- MySQL과 동일한 소스 코드를 기반으로 한다.  
  
## 문제가 발생하거나 고민한 내용  
![](https://salmon99.github.io/assets/images/12week/1.PNG)  
실습을 하던 도중, 테이블에 데이터를 추가하는 과정에서 오류가 나길래 오류 메세지를 검색해 보았다.  
알고보니 데이터의 중복이 발생해서 오류가 났던 것으로, 테이블을 확인해보니 데이터가 한개 들어가 있었다. 원인은 잘 모르겠지만 나머지 4개만 추가하는 것으로 해결했다.  
  
## 참고할 만한 내용  
* [INSERT 시 Duplicate entry 에러가 발생한다면?](https://ojava.tistory.com/148)
  
## 회고  
지난 학기에 데이터베이스 수업을 들었었다. 교수님께서 다른 학교에서는 데이터베이스 수업을 하면서 실습을 한다고 하는데, 우리 학교에서는 이론만 먼저 배운다는 걸 듣고 내심 조금 실망했었다. 배운 내용 자체는 별로 어렵지 않았지만 실제로 어떻게 쓰이는 지 실감이 전혀 나지 않았던 기억이 있다. 그런데 이번에 이렇게 데이터베이스 수업에서 배웠던 명령어들을 실습할 수 있어서 반갑고 재밌었다. 이론으로만 배웠던 명령어들이 실제로 데이터베이스를 만드는 데 쓰인다는 걸 느껴서 좋았다.  