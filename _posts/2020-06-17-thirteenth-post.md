---
title:  "컴퓨터시스템관리 13주차 실습일지"
excerpt: "웹 서버를 구현하고, 웹 사이트를 구축하고 클라우드 서비스를 설치했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-06-17T18:52:00
--- 
## 실습 과제  
![](https://salmon99.github.io/assets/images/13week/2.PNG)  
![](https://salmon99.github.io/assets/images/13week/3.PNG)  
![](https://salmon99.github.io/assets/images/13week/4.PNG)  
wordpress 웹사이트에 접속한 화면이다.  
![](https://salmon99.github.io/assets/images/13week/5.PNG)  
database를 이용해서 사용자 계정을 만들었다.  
![](https://salmon99.github.io/assets/images/13week/6.PNG)  
![](https://salmon99.github.io/assets/images/13week/7.PNG)  
클라우드 서비스에 햄스터 사진을 올렸다.  
웹 사이트는 wordpress를 이용하고, 클라우드 서비스는 owncloud를 이용했다.  
  
## 새로 배운 내용  
**웹 서버(Web Server)**  
- 웹 브라우저와 같은 클라이언트로부터 HTTP 요청을 받아들이고, HTML 문서와 같은 웹 페이지를 반환하는 컴퓨터 프로그램.  
- 위와 같은 기능을 제공하는 컴퓨터 프로그램을 실행하는 컴퓨터.  
  
**클라우드 서비스(Cloud Service)**  
- 인프라 서비스: Dropbox  
- 개발 플랫폼 제공 서비스: AWS, Azure  
- 소프트웨어 서비스: Google Drive, One Drive  
  
**클라우드 컴퓨팅(Cloud Computing)**  
- 클라우드(인터넷)을 통해 가상화된 컴퓨터의 시스템 리소스를 요구하는 즉시 제공하는 것.  
  
**설치형 클라우드 서비스**  
- pydio, owncloud, nextcloud  
- 웹서버 위에서 PHP와 DBMS를 이용하여 가동한다.  
- 서버의 저장공간에 파일을 저장하고, 클라우드로 제공한다.  
  
## 문제가 발생하거나 고민한 내용  
며칠 전부터 가상머신을 실행시키려고 하면 오류(This virtual machine appears to be in use.)가 떠서 고민을 했는데, 인터넷에 검색해보니 특정 폴더를 삭제하면 된다고 해서 쉽게 해결했다.  
![](https://salmon99.github.io/assets/images/13week/1.PNG)  
server(b)에는 GUI 환경이 설치되어 있지 않아서 nm-connection-editor 명령어를 사용할 수 없었다. 그래서 고정 IP를 설정하는 데에 애를 먹었는데, 교수님이 제시해주신 글과 인터넷 서핑을 통해서 해결할 수 있었다.  
그리고 고정 IP를 설정하는 과정에서 Invalid YAML … did not find expected key 이런 에러가 발생했는데, 들여쓰기(?)를 잘못한 것 같았다. 인터넷에 서핑해서 형식을 조금 고치니 해결되었다.  
  
## 참고할 만한 내용  
* [This virtual machine appears to be in use.문제](https://jootc.com/p/20180411807)  
* [우분투에서 고정 아이피 설정하기](https://www.lesstif.com/lpt/ubuntu-18-lts-ip-static-ip-config-61899302.html)  
* [서브넷 마스크란?](https://limkydev.tistory.com/166)  
* [우분투에서 워드프레스 설치하기](https://jimnong.tistory.com/746)  
  
## 회고  
이번 실습은, 수업을 들으면서 할 때에는 전혀 어려움이 없었지만, GUI 환경이 아닌 server(b)에서 똑같은 실습을 하려니 수업에서 한 것과 방법이 많이 달라서 혼란을 겪었다. 처음에는 계속 설정이 잘 안돼서 시행착오를 겪으며 초기화를 여러번 했지만, 포기하지 않고 웹서핑과 수업을 참고하며 과제를 해결하려고 노력했다. 하는 과정은 힘들고 시간도 오래 걸렸지만 원하는 결과가 나와서 만족스러웠다. 그리고 웹서버를 직접 설치해보는 경험도 생각과는 다르게 간단한 편에 속해서 신기하고 재밌었다. 