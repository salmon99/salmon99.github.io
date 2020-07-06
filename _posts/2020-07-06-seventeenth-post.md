---
title:  "Windows 10에서 파이썬 3.8.0 이상에 kivy 설치하기"
excerpt: ""

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-06-30T16:15:00
--- 
* [Windows에 키비 설치](https://kivy.org/doc/stable/installation/installation-windows.html)  
파이썬 최신 버전(3.8.*)을 설치하고, kivy 홈페이지에서 메뉴얼을 따라하면 설치되지 않는 문제에 부딪혔다.  
* [파이썬 3.8.0에 키비 설치 문제](https://github.com/kivy/kivy/issues/6563)  
위 링크에서 해결책을 얻었다.  
>>We are not likely to release a 1.11.1 version for 3.8 to pypi. However, you can install kivy master using  
>>pip install kivy[base] kivy_examples --pre --extra-index-url https://kivy.org/downloads/simple/.  
명령 프롬프트에 위의 명령어를 입력하면 정상적으로 kivy가 작동된다.  
  
* [탁구 게임 튜토리얼](https://kivy.org/doc/stable/tutorials/pong.html)  
아래의 사진은 kivy 홈페이지에 있는 예제를 실행한 모습이다.    
![](https://salmon99.github.io/assets/images/17/example.PNG)  