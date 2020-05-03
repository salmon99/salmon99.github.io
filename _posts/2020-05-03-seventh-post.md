---
title:  "컴퓨터시스템관리 7주차 실습일지"
excerpt: ""

categories:
  - ComputerSystemManagement
tags:
  - ComputerSystemManagement
last_modified_at: 2020-05-02T18:43:00
--- 
## 새로 배운 내용  
**RAID6, RAID1+0, RAID1+6**  

  
**LVM(Logical Volum Manage)**  

  
**쿼터(Quota)를 이용한 사용자별 공간 할당**  

  
## 문제가 발생하거나 고민한 내용  
RAID1(결함 허용 시스템)에 결함을 만든 후 복구하는 실습에서 교수님의 화면과 똑같이 나오지 않아서 당황했다.  
![](https://salmon99.github.io/assets/images/6week/1.png)  
![](https://salmon99.github.io/assets/images/6week/2.png)  
그러나 내가 작성했던 명령어들을 자세히 살펴보니 명령어에 오타가 있었다는 것을 알았다.  
sudo mdadm /dev/md0 --add /dev/sdb1  
sudo mdadm /dev/md1 --add /dev/sdb2  
이라고 작성해야 하는 것을  
sudo mdadm /dev/md0 --add /dev/sdb1  
sudo mdadm /dev/md0 --add /dev/sdb2  
으로 md0에 두개의 디스크를 추가해버린 것이었다.  
강의로는 디스크를 추가하는 방법만 알고 제거하는 방법은 알 수가 없었기 때문에 검색을 했더니 제거하는 옵션인 -r을 찾을 수 있었다.  
![](https://salmon99.github.io/assets/images/6week/3.png)  
그래서 md0에 추가했던 sdb2 디스크를 제거하고 다시 md1에 sdb2를 추가했더니 해결되었다.  
![](https://salmon99.github.io/assets/images/6week/4.png) 
  
## 참고할 만한 내용  
* [[리눅스] RAID ( 명령어 : mdadm )](https://dgblog.tistory.com/141)
  
## 회고  
이번 실습에는 가상머신에서 하드디스크의 파티션을 생성하고 포맷하는 과정을 아주 많이 반복했다. 처음에는 낯설기만 하고 어려운 과정이었지만 여러번 반복하니 어느정도 순서와 방법을 외울 수 있게 되었다. 또한 결함이 허용되는 RAID1에 우분투를 설치하고 고의로 하드디스크 하나를 없앤 후 복구하는 실습도 해 보았는데, 실제로 사용자가 응급모드 등을 이용하여 설정하지 않아도 정상적으로 작동되는 모습이 신기했다. 데이터의 안전을 생각한다면 RAID1 혹은 결함을 허용하는 시스템을 사용하는 게 좋겠다는 생각이 든다.