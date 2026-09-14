---
published: true
title:  "[CCNA Hands-On] VLAN"
excerpt: "Cisco Packet Tracer로 Hands-On을 하며 VLAN에 대해 복습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - VLAN
  - CCNA
  - Hands-On
last_modified_at: 2026-09-14T15:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-14
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** Trunk 포트를 통한 스위치 간 VLAN 통신 실습
トランクポートを経由したスイッチ間VLAN通信の実装

---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
                  [ Fa0/8 ]
 [ SW1 ] ========================== [ SW2 ]
    |                                  |
    +-- Fa0/1: PC1 (VLAN 1)            +-- Fa0/1: PC4 (VLAN 1)
    +-- Fa0/2: PC2 (VLAN 10)           +-- Fa0/2: PC5 (VLAN 10)
    +-- Fa0/3: PC3 (VLAN 20)           +-- Fa0/3: PC6 (VLAN 20)

- **발생 이슈(Issue):** PC2 / PC5 ＆ PC3 / PC6 같은 VLAN간 Ping 통신 실패
- **事象:** PC2 / PC5 および PC3 / PC6 の同一VLAN間におけるPing通信不可

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **원인:** SW1, SW2의 Fa0/8 포트가 Trunk 모드로 설정되지 않음.
- **原因:** SW1およびSW2のFa0/8ポートがトランクモード(Trunk Mode)に未設定のため。
- **분석 내용:** 
  - SW1과 SW2의 Fa0/8 포트를 IEEE 802.1Q 태깅을 지원하는 **Trunk Mode**로 변경하여 복수 VLAN의 프레임이 통과할 수 있도록 설정 필요.
- **詳細:** 
  - 事象解消のため、SW1とSW2のFa0/8ポートをIEEE 802.1Qカプセル化に対応する**トランクモード(Trunk Mode)**に変更し、タグ付きフレームを通過させる必要あり。

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド
초기 VLAN 설정 진행.
원인 해결을 위해 SW1, SW2의 Fa0/8 포트를 Trunk 모드로 변경.
初級VLAN設定の実施。
事象解消のため、初期VLAN設定の実施およびSW1/SW2のFa0/8ポートをトランクモードに変更。

```bash
# SW1, SW2 VLAN setup
# Create VLAN 10, 20 
Switch(config)# vlan 10
Switch(config)# vlan 20

# Access port setup
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 1

Switch(config)# interface FastEthernet 0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

Switch(config)# interface FastEthernet 0/3
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20

# Trunk port setup
Switch(config)# int f0/8
Switch(config-if)# switchport mode trunk
```