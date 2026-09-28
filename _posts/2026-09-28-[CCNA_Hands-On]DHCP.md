---
published: true
title:  "[CCNA Hands-On] DHCP"
excerpt: "Cisco Packet Tracer로 Router을 이용한 DHCP 설정을 실습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - DHCP
  - CCNA
  - Hands-On
last_modified_at: 2026-09-28T16:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-28
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** 라우터를 이용해 동일 네트워크상의 단말에 자동으로 IP주소를 할당해주는 DHCP 프로토콜 구현
ルーターを活用し、同一ネットワーク内の端末へ自動的にIPアドレスを割り当てるDHCPプロトコルの実装

---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
```text
[ LAN A : 192.168.1.0/24 ]                                      [ WAN/Point-to-Point : 10.10.10.0/24 ]
  ├── PC0 (Fa0) ─── Fa0/2 ┐
  └── PC1 (Fa0) ─── Fa0/3 ┴─ [ Switch ] ─ Fa0/1 ─── Fa0/1(.1) [ R1 ] Fa0/0(.1) ──── Fa0/0(.2) [ R2 ]
```

- **발생 이슈(Issue):** LAN A 대역의 PC0, PC1에 IP 주소, 기본 게이트웨이, DNS 자동 할당(DHCP) 필요
- **事象:** LAN A 帯域のPC0、PC1へIPアドレス、デフォルトゲートウェイ、DNSの自動割当（DHCP）が必要

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **분석 내용:** 
  - 별도의 DHCP 서버 없이 라우터(R1)의 DHCP 서버 기능을 활용하여 네트워크 설정 배포.
  - DHCP Pool을 생성하여 네트워크 대역, Default Gateway, DNS 서버 정보를 정의.
  - 게이트웨이 등 고정 IP로 사용되는 주소는 IP 충돌 방지를 위해 DHCP 할당 범위에서 사전 제외 필요.
- **詳細:** 
  - 専用のDHCPサーバーを配置せず、ルーター（R1）のDHCPサーバー機能を活用してネットワーク設定を配布
  - DHCP Poolを作成し、ネットワーク帯域、デフォルトゲートウェイ、DNSサーバー情報を定義
  - ゲートウェイなど固定IPとして使用されるアドレスは、IP衝突防止のためDHCP割当範囲から事前に除外が必要

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド
라우터(R1)에서 DHCP 서버 기능 설정 진행
ルーター（R1）にてDHCPサーバー機能の設定を実施

```bash
# Create DHCP Pool & DHCP Setup
Router(config)# ip dhcp pool DHCPPOOL
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8

# Excluded Address Setup
Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.149

# Setup Check
Router# show ip dhcp binding
Router# show running-config
```