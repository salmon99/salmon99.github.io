---
title:  "컴퓨터시스템관리 5주차 실습일지"
excerpt: "리눅스 시스템에 하드디스크를 추가 장착하고 관리하는 법을 배웠다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-04-26T18:49:00
---
![](https://salmon99.github.io/assets/images/5week/project.png)  
Server(B)에 RAID1 레벨의 RAID를 설치했다. 1기가의 하드디스크 두개를 이용하였다.  
RAID1은 다른 레벨에 비해서 공간 효율성이 낮지만, 신뢰성이 높기 때문에 나는 RAID1을 선택하였다. 만약 내가 학교의 실습 서버를 관리하는 조교라면 무엇보다도 학생들이 실습하는 환경의 데이터를 보존하고, 오류가 생긴다면 복구할 수 있는 환경이 중요할 것이라고 생각했다.
  
## 새로 배운 내용  
**SATA와 SCSI의 차이점**  
다른 수업을 들을 때 컴퓨터 부품 중 SATA라는 이름을 가진 것이 있었다. 그 당시에는 정확하게 어떤 역할을 하는지 몰랐는데 이번 기회에 알게 되었다.  
SATA: 하드디스크 또는 광학 드라이브와 데이터 전송을 주요 목적으로 만든 단자.  
SCSI: 컴퓨터에 주변기기를 연결할 때 직렬 방식으로 연결하기 위한 표준.  
SATA는 속도가 빠르지만 연결할 수 있는 길이가 짧고, SCSI는 상대적으로 속도가 느리지만 케이블 길이가 길기 때문에 멀리 있는 곳까지 정보를 전송할 수 있다.
  
**여러 개의 하드디스크를 하나의 하드디스크처럼 사용하는 RAID**  
여러 개의 하드디스크로 RAID를 이용하면 비용, 신뢰성, 성능 조절을 할 수 있다. RAID는 여러가지 레벨이 있는데, 주로 사용하는 레벨은 Linear RAID, RAID0, RAID1, RAID5, RAID6, RAID1+0 등이 있다.  
Linear RAID: 2개 이상의 하드디스크 이용, 첫번째 디스크부터 순차적으로 데이터를 저장해서 공간 효율성이 100%로 비용이 저렴하다.  
RAID0: 2개 이상의 하드디스크 이용, 모든 디스크에 동시에 데이터를 나누어서 저장해서 속도가 빠르다. 공간 효율성이 100%로 비용이 저렴하다.  
RAID1: 2개 이상의 하드디스크 이용, 하나의 데이터를 두 개의 하드 디스크에 각각 동일하게 저장한다. Linear RAID, RAID0에 비해 비용이 2배로 효율이 낮다. 하지만 한개의 하드디스크에 오류가 생겼을 때 복구가 가능해 신뢰성이 높다. 
RAID5: 3개 이상의 하드디스크 이용, 패리티 정보를 사용해 1개 디스크의 결함을 복구할 수 있어 신뢰성이 높으며, RAID1에 비해 공간 효율이 좋다.  
RAID6: 4개 이상의 하드디스크 이용, 중복 패리티 정보를 이용해 2개 디스크의 결함도 복구할 수 있어 신뢰성이 높다.  
  
## 문제가 발생하거나 고민한 내용  
포맷에 대해 단순히 컴퓨터 하드디스크를 초기화 하는 것이라고 생각했는데, 수업 중 디스크를 포맷해줘야 한다는 표현을 듣고 포맷의 정확한 뜻을 검색해 보았다. 포맷이란 디스크에 데이터를 기록할 수 있도록 준비하는 작업을 말한다. 아무런 작업을 하지 않은 디스크에는 곧바로 데이터를 기록할 수 없으며, 파일 시스템이라고 하는 데이터의 기록 체계를 설정해 주어야 디스크에 정보를 기록할 수 있다는 것을 알았다.  
  
## 참고할 만한 내용  
* [PC 초기화를 위한 필수 상식 - 디스크 포맷(Disk formatting)](https://it.donga.com/8634/)
  
## 회고  
수업시간에 raid 레벨에 대해 이론을 들을 때, 내용은 이해했지만 실제로 사용해 볼 일이 없을 것 같아 아쉬웠는데 직접 여러가지의 경우를 실습해 볼 수 있어서 좋았다. 