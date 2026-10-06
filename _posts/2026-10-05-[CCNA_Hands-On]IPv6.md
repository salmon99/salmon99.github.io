---
published: true
title:  "[CCNA Hands-On] IPv6 Setup & Routing"
excerpt: "Cisco Packet Tracer로 Router의 IPv6 설정 및 라우팅을 실습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - IPv6
  - CCNA
  - Hands-On
last_modified_at: 2026-10-05T16:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-10-05
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** IPv6을 활용한 라우터 IP 주소 설정 및 타 네트워크로의 라우팅 구현
IPv6を活用したルーターIPアドレスの設定および他ネットワークへのルーティング実装

---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
```text
[ Network 1 : 2001:1::/64 ]                                   [ Network 2 : 2001:2::/64 ]
  [ R1 ] ── (Fa0/0) ───────────────── (Fa0/0) ── [ R2 ] ── (Fa0/1) ───────────────── (Fa0/0) ── [ R3 ]
  GUA:  2001:1::1/64                  GUA:  2001:1::2/64    GUA:  2001:2::1/64        GUA:  2001:2::2/64
  Link-Local: FE80::1                 Link-Local: FE80::2   Link-Local: FE80::1       Link-Local: FE80::2
```

- **발생 이슈(Issue):** 서로 다른 IPv6 네트워크 대역 간 통신을 위한 인터페이스 IP 주소(GUA/Link-Local) 할당 및 정적 라우팅(Static Route) 설정 필요
- **事象:** 異なるIPv6ネットワーク帯域間の通信を実現するため、インターフェースIPアドレス（GUA/Link-Local）の割り当ておよび静的ルーティング（Static Route）の設定が必要

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **분석 내용:** 
  - GUA(Global Unicast Address): 외부 및 타 네트워크와 통신하기 위한 공인/사설 개념의 라우팅 가능 주소(2001:...).
  - Link-Local Address: 동일 링크(L2 구간) 내 통신 및 라우팅 이웃 관계 형성을 위한 주소(FE80::/10).
  - R1과 R3는 직접 연결되지 않은 원격 네트워크 대역에 대해 Next-Hop IP 주소를 지정하는 정적 라우팅(ipv6 route) 설정 필요.
- **詳細:** 
  - GUA（Global Unicast Address）: 外部および他ネットワークと通信するためのルーティング可能なグローバルアドレス（2001:...）
  - Link-Local Address: 同一リンク（L2区間）内の通信およびルーティングのネイバー関係構築のためのアドレス（FE80::/10）
  - R1およびR3は、直接接続されていないリモートネットワーク帯域に対してNext-Hop IPアドレスを指定する静的ルーティング（ipv6 route）の設定必要

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド

```bash
# IPv6 Address Setup
R1(config)# ipv6 unicast-routing
R1(config)# int f0/0
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# ipv6 address 2001:1::1/64
R1(config-if)# no shutdown

R2(config)# ipv6 unicast-routing
R2(config)# int f0/0
R2(config-if)# ipv6 address fe80::2 link-local
R2(config-if)# ipv6 address 2001:1::2/64
R2(config-if)# no shutdown
R2(config)# int f0/1
R2(config-if)# ipv6 address fe80::1 link-local
R2(config-if)# ipv6 address 2001:2::1/64
R2(config-if)# no shutdown

R3(config)# ipv6 unicast-routing
R3(config)# int f0/0
R3(config-if)# ipv6 address fe80::2 link-local
R3(config-if)# ipv6 address 2001:2::2/64
R3(config-if)# no shutdown

# IPv6 Address Setup Check
R1# show ipv6 int f0/0
R2# ping ipv6 2001:1::1

# IPv6 Routing Setup
R1(config)# ipv6 route 2001:2::/64 2001:1::2
R1# show ipv6 route

R3(config)# ipv6 route 2001:1::/64 2001:2::1
R3# show ipv6 route

# IPv6 Routing Setup Check
R1# ping ipv6 2001:2::2
```