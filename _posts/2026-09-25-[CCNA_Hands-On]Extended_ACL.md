---
published: true
title:  "[CCNA Hands-On] Extended ACL"
excerpt: "Cisco Packet Tracer로 Extended ACL를 실습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - ExtendedACL
  - CCNA
  - Hands-On
last_modified_at: 2026-09-25T15:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-25
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** 출발지, 목적지의 IP주소와 포트를 제어하는 Extended ACL 구현
送信元・送信先のIPアドレスとポートを制御する詳細ACL実装

---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
```text
[ LAN A : 192.168.1.0/24 ]
  ├── PC1 (.1)
  ├── PC2 (.2) ─── [ Switch ] ─── Gi0/0 (.254)
  └── PC3 (.3)                      │
                               [ Router ]
                                ├── Gi0/1 (.254) ─── [ S1 : 192.168.2.1/24 ]
                                └── Gi0/2 (.254) ─── [ S2 : 192.168.3.1/24 ]
```

- **발생 이슈(Issue):** PC1(192.168.1.1/24)의 Server1 HTTP 접근 허용, Ping 제한 필요
- **事象:** PC1(192.168.1.1/24)からServer1へのHTTPアクセス許可し、Ping制限が必要

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **분석 내용:** 
  - Extended ACL (100~199): 출발지(Source), 목적지(Destination) IP 주소, 포트 검사 가능.
  - 출발지와 가장 가까운 라우터 포트(Gi0/0)의 Inbound 방향에 Extended ACL을 적용하여 PC1(192.168.1.1/24)의 Server1(192.168.2.1/24)로 향하는 HTTP(TCP) 트래픽을 허용하고 Ping(ICMP) 트래픽을 차단함.
  - 암묵적 차단(Implicit Deny)으로 인한 타 트래픽 차단을 방지
- **詳細:** 
  - 詳細ACL(100~199):送信元・送信先のIPアドレス・ポート検査可能
  - 送信元に最も近いルーターポート(Gi0/0)のインバウンドに詳細ACLを適用し、PC1(192.168.1.1/24)からServer1(192.168.2.1/24)へのHTTP(TCP)トラフィックを許可し、Ping(ICMP)トラフィックを遮断
  - ACLの暗黙の廃棄（Implicit Deny）による他トラフィックの全遮断を防止

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド
라우터 포트(Gi0/0)의 Inbound 방향에 Extended ACL을 적용.
ルーターのポート(Gi0/0)のインバウンドに詳細ACLを適用

```bash
# Create Extended ACL
Router(config)# access-list 100 permit tcp host 192.168.1.1 host 192.168.2.1 eq www
Router(config)# access-list 100 deny icmp host 192.168.1.1 host 192.168.2.1 echo
Router(config)# access-list 100 permit ip any any

# Router Gi0/0 Port setup
Router(config)# int gi0/0
Router(config-if)# ip access-group 100 in

# Setup check
Router# show access-lists 100
Router# show running-config
```