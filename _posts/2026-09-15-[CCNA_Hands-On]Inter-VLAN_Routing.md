---
published: true
title:  "[CCNA Hands-On] Inter-VLAN Routing"
excerpt: "Inter-VLAN Routing을 Router-On-A-Stick으로 구현한 실습 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - VLAN
  - Inter-VLAN_Routing
  - CCNA
  - Hands-On
last_modified_at: 2026-09-15T15:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-15
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** 라우터를 통한 Inter-VLAN Routing 구현 실습
トランクポートを経由したスイッチ間VLAN通信の実装

---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
```text
              [ Router (L3) ]
                     │
                     │ Fa0/0    (VLAN 1) : 192.168.1.254/24
                     │ Fa0/0.10 (VLAN 10): 192.168.10.254/24
                     │ Fa0/0.20 (VLAN 20): 192.168.20.254/24
                     │
                     │
                     │ Fa0/8 (Trunk Port)
              [ Switch (L2) ]
          ┌──────────┼──────────┐
    Fa0/1 │    Fa0/2 │    Fa0/3 │
 (VLAN 1) │ (VLAN 10)│ (VLAN 20)│
          │          │          │
        [PC1]      [PC2]      [PC3]

PC1: 192.168.1.1/24 (Default Gateway: 192.168.1.254)
PC2: 192.168.10.1/24 (Default Gateway: 192.168.10.254)
PC3: 192.168.20.1/24 (Default Gateway: 192.168.20.254)
```

- **발생 이슈(Issue):** 서로 다른 VLAN(PC1, PC2, PC3) 간 Ping 통신 실패
- **事象:** 異なるVLAN間(PC1, PC2, PC3)におけるPing通信不可

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **원인:** Router의 Fa0/0포트의 서브인터페이스 설정 누락.
- **原因:** ルーターのFa0/0ポートのサブインタフェース未設定のため。
- **분석 내용:** 
  - Router의 Fa0/0포트는 VLAN 1 트래픽만 처리 가능하며, VLAN 10/20 패킷을 수신할 서브인터페이스(Sub-interface) 및 802.1Q 캡슐화 설정이 누락됨.
- **詳細:** 
  - ルーターのFa0/0ポートはVLAN 1トラフィックのみ処理可能であり、VLAN 10/20パケットを受信するサブインタフェース及び802.1Qカプセル化が未設定。

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド
라우터 Fa0/0 포트에 서브인터페이스(Fa0/0.10, Fa0/0.20)를 생성하고 encapsulation dot1Q 적용.
ルーターのFa0/0ポートにサブインタフェース(Fa0/0.10, Fa0/0.20)を生成し、802.1Qカプセル化(dot1Q)を適用。

```bash
# Router Fa0/0 Port setup
Router(config)# int fa0/0
Router(config-if)# ip address 192.168.1.254 255.255.255.0
Router(config-if)# no shutdown

# Router Fa0/0 Port sub-interface setup
Router(config)# int fa0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.254 255.255.255.0
Router(config-subif)# no shutdown

Router(config)# int fa0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.254 255.255.255.0
Router(config-subif)# no shutdown
```