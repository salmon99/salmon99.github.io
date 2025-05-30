---
title:  "[PXE 부팅] USB 없이 네트워크로 Ubuntu 설치하기"
excerpt: "Tiny PXE Server를 사용하여 네트워크 부팅으로 Ubuntu 설치하는 가이드"

categories:
  - PXE
tags:
  - PXE
  - Ubuntu
  - Linux
  - NetworkBooting
  - TinyPXEServer
last_modified_at: 2025-05-31T03:12:00
--- 

귀여운 나만의 미니PC가 생겼다.

원래는 홈서버를 돌릴 용도로 새걸 장만하려고 했는데 어쩌다보니 공짜로 생겨서… 이 친구를 잘 써먹어보려고 했다.

![KakaoTalk_20250531_013410243.jpg](https://salmon99.github.io/assets/images/20250531/KakaoTalk_20250531_013410243.jpg)

모델명은 에이서 레보 빌드 M1-601-Revo20 (eMMC 32GB) 이다.

지금은 단종된… 좀 오래된 모델이고, 램은 원래는 2GB지만 8GB로 교체했다.

저장공간은 하드디스크가 아니라 eMMC(embedded Multi Media Card)라는데, 용량이 32GB라서 불만스럽지만… 교체가 어려울 것 같아서 일단은 내버려뒀다.

그래서 이 친구를 어떻게 하려고 했냐면,

1. 기본으로 설치된 윈도우를 밀고 우분투 설치하기
2. 개인용 웹서버로 이런저런 테스트하는 데에 써보기

아무래도 윈도우는 서버로 쓰기에 불편하기도 하고, 굳이 gui가 필요하지 않기도 하고…

이중공유기라 포트포워딩도 번거로울 것 같아서 추후 Cloudflare 터널을 활용하여 웹서버로 써보는 게 제일 적당할 것 같았다.

아무튼, 가장 먼저 우분투를 설치하려고 시도했다.

그런데 usb를 우분투 부팅용으로 구웠는데도 도무지 부팅 디스크로 인식을 못하는 것이다…

usb에 문제가 있나 싶어서 원래 사용하던 컴퓨터에서도 시도해봤는데 잘 됐다.(ㅠㅠ)

결론은 미니PC라서 BIOS가 간소화 버전이 아닌가… 추측을 할 뿐이었다…

BIOS를 업데이트 하면 되려나? 싶어서 ACER 홈페이지에서 모델명 검색도 했으나 업데이트 제공도 안 했다…

우분투를 설치하려는 시도부터 막히나 싶어서 막막했는데, 네트워크를 통해 OS를 설치하는 방법이 있다고 해서 시도해봤고, 성공한 김에 후기 겸 가이드도 올린다.

# USB 없이 네트워크로 우분투 설치하기 - PXE 부팅

PXE(Preboot eXecution Environment) 부팅이란 네트워크에서 부팅 이미지를 가져와 운영체제를 부팅하는 방법이다.

이게 어떤 원리로 동작하는지 이해하는 데 도움이 된 포스트를 함께 남긴다.

[PXE 부팅으로 Ubuntu 22.04 설치하기 [1편]](https://tech-recipe.tistory.com/28)

여기에 적힌 것처럼 직접 DHCP 서버나 PXE 서버를 구축해서 하지는 않고, TINY PXE Server라고 훨씬 간편하게 PXE 부팅을 할 수 있도록 도와주는 프로그램을 사용했다.

## PXE 부팅을 위한 준비물

- 인터넷 연결이 가능한 미니 PC (혹은 usb 없이 PXE 부팅으로 OS를 설치하고 싶은 컴퓨터)
- 위 컴퓨터에 연결할 여분의 모니터와 키보드
- 위 컴퓨터와 같은 네트워크(유선)에 연결된 컴퓨터(Windows)
    - 같은 공유기에서 랜선으로 각각 연결해주면 된다.
- [TINY PXE Server](https://github.com/erwan2212/tinypxeserver) (Github에서 다운 가능하다.)
- [netboot.xyz-부트로더](https://netboot.xyz/downloads) (Legacy 부팅을 한다면 netboot.xyz.kpxe 파일을 받고, UEFI 부팅을 한다면 netboot.xyz.efi 파일을 받으면 된다. 이 가이드에서는 Legacy 방식으로 부팅하였다.)
- (선택사항)Putty 등 SSH 접속 가능한 툴
    - Ubuntu를 설치하고 나면 SSH로 접속 가능하다. 그러면 바로 모니터와 키보드를 치워버릴 수 있다.

자, 일단은 미니 PC에 모니터와 키보드를 연결한 상태고, 미니PC와 같은 네트워크에 유선으로 연결되어 있는 다른 컴퓨터가 준비된 상황이라고 가정하고 가이드를 시작하겠다.

## 1. Tiny PXE Server 세팅

우선 미니 PC가 아닌 다른 컴퓨터에 Tiny PXE Server를 다운받고 압축을 풀면 아래와 같은 파일들이 보인다.

여기서 pxesrv.zip도 압축을 풀어준다. (이미지에선 이미 압축을 푼 상태이다.)

![image.png](https://salmon99.github.io/assets/images/20250531/image.png)

압축을 푼 pxesrv 폴더에 들어가면 아래와 같은 파일들이 있는데, 여기서 pxesrv.exe를 관리자 권한으로 실행해준다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%201.png)

Tiny PXE Server를 처음 실행하면 아래와 같은 화면이 뜬다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%202.png)

우리는 여기서 빨간 박스 친 부분만 확인하면 된다.

간단히 개념을 설명하자면, DHCP 서버란 같은 네트워크에 연결된 장치에게 IP 주소를 할당해주는 서버이다.

PXE 서버는 DHCP 서버의 역할도 하면서, 부팅 이미지도 클라이언트에게 제공해주는 것이다.

그런데, 우리는 이미 공유기를 사용하고 있기 때문에 공유기가 이미 DHCP 서버의 역할을 하고 있다.

이때 충돌을 방지하기 위해서 ProxyDhcp 설정을 체크해준다.

그리고, Option 54는 지금 우리가 사용하고 있는 (미니 PC가 아닌)다른 컴퓨터의 내부 IP가 들어가야 한다.

자동으로 셋팅을 해주는 것 같지만, cmd창에서 ipconfig로 동일한 IP주소인지 확인해보자.

![image.png](https://salmon99.github.io/assets/images/20250531/3681e3f6-72c9-4e26-9d7a-aa3fedc46f96.png)

Option 54와 동일하게 192.168.0.2이 나오는 걸 확인했다.

다음으로 Boot file은 [netboot.xyz](http://netboot.xyz) 홈페이지에서 netboot.xyz.kpxe 파일을 다운받아 넣어주면 된다.

[https://netboot.xyz/downloads](https://netboot.xyz/downloads)

ProxyDhcp도 체크했고, 부트 파일도 다운받아서 넣었으면 아래와 같은 화면이 된다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%203.png)

여기서 오른쪽 위의 Online 버튼을 누르면 아래와 같이 서버가 동작하는 상태가 된다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%204.png)

이제 PXE 부팅을 위한 다른 컴퓨터에서의 설정은 다 끝났다.

## 2. 미니 PC BIOS 설정 변경 및 부팅

미니 PC가 네트워크 부팅이 가능하도록 설정을 변경해야지 부팅이 가능하다.

일단, 미니 PC의 전원을 키고 BIOS 옵션 페이지로 들어가는 버튼을 연타해준다.

(내 미니 PC의 경우는 Del 키를 연타했다.)

![image.png](https://salmon99.github.io/assets/images/20250531/image%205.png)

그러면 이런 화면으로 들어가게 되는데,

여기서 다른 페이지를 잘 살펴보면서 설정을 변경해줘야 한다.

Network Boot 옵션을 Enable로 하고,

Boot Mode를 Legacy로 설정하고,

Boot priority order를 Network Boot-IPv4가 맨 위로 가도록 해줘야 한다.

BIOS 종류마다 메뉴 모양이나 조작 방식이 달라서 자세히 설명하기는 어렵지만 잘 찾아서 할 수 있을 것이다. ^^;;

설정을 완료하고 저장을 반드시 한 후, 재부팅을 해준다.

그러면 이런 화면이 뜨면서 다른 컴퓨터의 Tiny PXE Server 화면에도 로그가 쭉 올라온다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%206.png)

그리고 이 화면이 보인다면 PXE로 부팅하기가 이미 성공한 것이다!

![image.png](https://salmon99.github.io/assets/images/20250531/image%207.png)

## 3. 네트워크 부팅 메뉴에서 Ubuntu 선택 및 설치

아까 등장했던 화면에서 Linux Network Installs 항목을 키보드로 조작해서 선택해준다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%208.png)

그러면 아래처럼 Linux 종류가 뜨는데, 나는 아래로 쭉 내려서 Ubuntu를 선택했다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%209.png)

![image.png](https://salmon99.github.io/assets/images/20250531/image%2010.png)

여기서 원하는 Ubuntu 버전을 선택해주면 된다. 난 22.04 LTS를 선택했다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%2011.png)

그 다음에는 Install를 선택하면 다운로드를 하며 순조롭게 진행이 된다.

![image.png](https://salmon99.github.io/assets/images/20250531/image%2012.png)

이렇게 Ubuntu 설치 화면이 뜨면 다른 곳에서 설치하는 것과 동일하게 진행하면 된다!

![image.png](https://salmon99.github.io/assets/images/20250531/64109065-5cab-4150-9f74-cc6d1fe33a46.png)

## 4. 후기

USB 없이 Ubuntu 설치하기… 등의 여러 키워드로 검색해도 듀얼부팅이 가능한 정도만 나와서 고민을 많이 했는데, PXE를 통해 네트워크로 설치하니 깔끔하게 윈도우를 지우고 Ubuntu를 설치할 수 있었다.

나와 비슷하게 고민하는 사람이 있을까 싶어 이 가이드를 남긴다.