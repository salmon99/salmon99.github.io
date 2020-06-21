---
title:  "컴퓨터시스템관리 14주차 실습일지"
excerpt: "FTP 서버를 구현하고 파일을 업로드, 다운로드하는 실습을 했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-06-21T20:09:00
driveId: 1BmzvQxuWQjW7Kfuwr12v2DfG9aXhqmcQ/preview
--- 
## 실습 과제  
{% include googleDrivePlayer.html id=page.driveId %}  
Server에 vsftpd를 설치하고 윈도우 터미널을 이용해 파일을 업로드하고 다운로드 하는 실습을 했다.  
![](https://salmon99.github.io/assets/images/14week/2.PNG)  
컴퓨터의 다운로드 폴더에 파일이 다운로드 된 것을 확인할 수 있다.  
아래에는 보안 설정을 한 실습을 캡쳐했다.  
  
![](https://salmon99.github.io/assets/images/14week/3.PNG)  
**chroot_local_user=YES**  
chroot() 기능은 자신의 홈디렉토리를 루트디렉토리로 인식하도록 하는 기능으로, 사용자의 홈디렉토리의 상위디렉토리로 벗어나지 못하도록 하는 설정이다. 사용자가 루트 디렉토리나 다른 곳으로 쉽게 이동하면 보안에 문제가 생길 수 있다고 생각해서 이 기능을 사용하도록 설정했다.  
  
![](https://salmon99.github.io/assets/images/14week/4.PNG)  
![](https://salmon99.github.io/assets/images/14week/5.PNG)  
**anon_upload_enable=NO**  
**anon_mkdir_write_enable=NO**  
익명 사용자에게는 다운로드 권한만 주고, 파일 업로드나 디렉토리 생성 권한을 주는 것은 보안에 위협이 될 수 있다고 생각해서 두 권한을 사용하지 못하도록 설정했다.  
  
## 새로 배운 내용  
**파일 전송 프로토콜(File Transfer Protocol, FTP)**  
- 서버와 클라이언트 사이의 파일 전송을 하기 위한 프로토콜.  
- 1971년 Abhay Bhushan이  FTP에 대한 사양을 작성했다.  
  
**FTP의 연결 종류**  
- 명령 연결: 제어 포트인 서버의 21번 포트로 사용자 인증을 하고, 명령을 위한 연결을 생성한다. 21번 포트를 통해 클라이언트에서 지시하는 명령어를 전달한다.  
- 데이터 전송용 연결: 파일 전송시 새로운 연결을 생성하여 데이터를 전송한다.  
- 능동 모드(Active mode): 서버가 자신의 데이터 포트인 20번 포트에서부터 클라이언트가 지정된 지점으로의 데이터 연결을 생성한다. 클라이언트가 방화벽, NAT 등을 사용할 경우 잘 작동하지 않을 수 있다. (이때 수동 모드를 사용해야 함)  
- 수동 모드(Passive mode): 클라이언트가 서버가 지정한 서버 포트로 연결할 수 있게 설정한다.  
  
**파일 송수신 모드**  
- text mode: 문서 파일 전송시 사용.  
- binary mode: 그림 파일 전송시 사용.
  
## 문제가 발생하거나 고민한 내용  
![](https://salmon99.github.io/assets/images/14week/1.PNG)  
실습 도중에 vsftpd 데몬이 masked 되었다면서 실행되지 않는 오류가 있었다. 원인은 알아내지 못했지만, 간단하게 unmask 명령어를 이용하여 서비스를 삭제하고 다시 실행했더니 해결되었다.  
그리고 vsftpd를 이용하여 파일을 다운로드 하려고 할 때 계속 550 에러가 떠서, 처음 실습을 할 때에는 apt install, wget 등을 이용했지만 이후에 원인을 알았다. 아마도 설정 파일을 수정할 때 빼먹은 부분이 있었던 것 같다.  
  
## 참고할 만한 내용  
* [masked service 해결법](https://askubuntu.com/questions/1017311/what-is-a-masked-service)  
* [FTP 550: Permission Denied](https://uiandwe.tistory.com/1055)  
* [애플리케이션 보안-VSFTP 설정 파일  vsftpd.conf](https://yjshin.tistory.com/entry/%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EB%B3%B4%EC%95%88-VSFTP-%EC%84%A4%EC%A0%95-%ED%8C%8C%EC%9D%BC-vsftpdconf)  

## 회고  
ftp는 컴퓨터를 오랫동안 써 왔지만 꽤나 생소한 단어였다. 그런데 http 또한 ftp와 비슷한 프로토콜의 한 종류라고 하니까 어느정도 이해가 되는 것 같았다. 온라인 저장소를 만드는 것은 굉장히 많은 비용과 복잡한 방법이 필요할 것이라고 생각했지만, 생각보다 간단하게 원격 접속을 하며 파일을 업로드하거나 다운로드 할 수 있다는 것이 놀라웠다. 언젠가 다른 사람에게 파일을 공유할 일이 있다면 ftp를 이용하여 파일을 공유해 줄 수 있도록 실제로 해 보고 싶다.  