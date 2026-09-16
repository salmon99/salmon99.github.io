---
published: true
title:  "[CCNA Hands-On] Standard ACL"
excerpt: "Cisco Packet Tracer로 Standard ACL를 실습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - StandardACL
  - CCNA
  - Hands-On
last_modified_at: 2026-09-16T17:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-16
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** 특정 네트워크의 접근을 제어하는 Standard ACL 구현
特定ネットワークのアクセスを制御する標準ACLの実装

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

- **발생 이슈(Issue):** 192.168.1.0/24 네트워크의 Server1 접근 제한 필요
- **事象:** 192.168.1.0/24ネットワークからServer1へのアクセス制限が必要

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **분석 내용:** 
  - Standard ACL (1~99): 출발지(Source) IP 주소만 검사 가능함.
  - 목적지 서버로 가는 라우터 포트(Gi0/1)의 Outbound 방향에 Standard ACL을 적용하여 192.168.1.0/24 트래픽을 차단함.
  - ACL의 암묵적 차단(Implicit Deny)으로 인한 다른 트래픽의 차단 방지를 위해 permit any 구문 추가.
- **詳細:** 
  - 標準ACL(1~99):送信元のIPアドレスのみ検査可能。
  - 通信先向けのルーターポート(Gi0/1)のアウトバウンドに標準ACLを適用し、192.168.1.0/24トラフィックを遮断。
  - ACLの暗黙の廃棄(Implicit Deny)による他トラフィックの遮断を防ぐため、permit anyを追加。

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド
라우터 포트(Gi0/1)의 Outbound 방향에 Standard ACL을 적용.
ルーターのポート(Gi0/1)のアウトバウンドに標準ACLを適用。

```bash
# Create Standard ACL
Router(config)# access-list 1 deny 192.168.1.0 0.0.0.255
Router(config)# access-list 1 permit any

# Router Gi0/1 Port setup
Router(config)# int gi0/1
Router(config-if)# ip access-group 1 out

# Setup check
Router# show access-lists
Router# show running-config
```