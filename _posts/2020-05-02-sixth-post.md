---
title:  "컴퓨터시스템관리 6주차 실습일지"
excerpt: "RAID1+0을 구성하고 LVM을 사용해 보았으며, 사용자별 공간 할당 실습을 했다."

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-05-02T18:43:00
--- 
## 새로 배운 내용  
**RAID6, RAID1+0, RAID1+6**  
RAID6: RAID5의 개선판. 2개의 패리티 비트를 사용하여 최소 4개 이상의 하드디스크가 필요하다. RAID5보다 성능과 공간효율은 낮지만 데이터의 신뢰도가 높아진다.  
RAID1+0: RAID1로 구성한 데이터를 다시 RAID0으로 구성한 것. 미러링 기능이 있는 RAID1과 속도가 빠른 RAID0의 장점을 결합하여 데이터의 신뢰성과 성능을 동시에 확보할 수 있다.  
RAID1+6: RAID1로 구성한 데이터를 다시 RAID6로 구성한 것. RAID1의 미러링 기능과 RAID6의 중복 패리티를 이용하여 아주 중요한 데이터를 보관하는 경우에 사용한다.
  
**LVM(Logical Volum Manage)**  
LVM은 논리적 볼륨을 효율적이고 유연하게 관리하기 위한 커널의 한 부분이자 프로그램이다. 물리적으로 2개로 나눠진 장치를 논리적 볼륨으로 통합하여 3개의 공간으로 파티션을 나누는 등의 기능이 있다.
  
**쿼터(Quota)를 이용한 사용자별 공간 할당**  
쿼터(명령어: quota)를 이용하여 리눅스 서버에서 사용자 별로 공간을 할당할 수 있다. soft는 사용자가 사용할 수 있는 공간의 크기를 말하고(0이면 제한 없음) hard는 반드시 지켜야 하는 공간의 크기를 말한다. soft에서 지정한 이상의 파일을 저장하면 일정 기간동안(grace)만 저장되고, 그 이후엔 사라진다. inodes는 저장할 수 있는 파일의 개수를 말한다.
  
## 문제가 발생하거나 고민한 내용  
RAID1(결함 허용 시스템)에 결함을 만든 후 복구하는 실습에서 교수님의 화면과 똑같이 나오지 않아서 당황했다.  
![](https://salmon99.github.io/assets/images/6week/1.PNG)  
![](https://salmon99.github.io/assets/images/6week/2.PNG)  
그러나 내가 작성했던 명령어들을 자세히 살펴보니 명령어에 오타가 있었다는 것을 알았다.  
sudo mdadm /dev/md0 --add /dev/sdb1  
sudo mdadm /dev/md1 --add /dev/sdb2  
이라고 작성해야 하는 것을  
sudo mdadm /dev/md0 --add /dev/sdb1  
sudo mdadm /dev/md0 --add /dev/sdb2  
으로 md0에 두개의 디스크를 추가해버린 것이었다.  
강의로는 디스크를 추가하는 방법만 알고 제거하는 방법은 알 수가 없었기 때문에 검색을 했더니 제거하는 옵션인 -r을 찾을 수 있었다.  
![](https://salmon99.github.io/assets/images/6week/3.PNG)  
그래서 md0에 추가했던 sdb2 디스크를 제거하고 다시 md1에 sdb2를 추가했더니 해결되었다.  
![](https://salmon99.github.io/assets/images/6week/4.PNG) 
  
## 참고할 만한 내용  
* [[리눅스] RAID ( 명령어 : mdadm )](https://dgblog.tistory.com/141)
  
## 회고  
이번 실습에는 가상머신에서 하드디스크의 파티션을 생성하고 포맷하는 과정을 아주 많이 반복했다. 처음에는 낯설기만 하고 어려운 과정이었지만 여러번 반복하니 어느정도 순서와 방법을 외울 수 있게 되었다. 또한 결함이 허용되는 RAID1에 우분투를 설치하고 고의로 하드디스크 하나를 없앤 후 복구하는 실습도 해 보았는데, 실제로 사용자가 응급모드 등을 이용하여 설정하지 않아도 정상적으로 작동되는 모습이 신기했다. 데이터의 안전을 생각한다면 RAID1 혹은 결함을 허용하는 시스템을 사용하는 게 좋겠다는 생각이 든다.