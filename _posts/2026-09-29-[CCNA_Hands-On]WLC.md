---
published: true
title:  "[CCNA Hands-On] WLC(Wireless LAN Controller) & LAP"
excerpt: "Cisco Packet Tracer로 WLC를 이용한 무선 AP 중앙 집중 관리 및 WLC 기초 설정을 실습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - WLC
  - Wireless
  - CCNA
  - Hands-On
last_modified_at: 2026-09-29T16:00:00
--- 

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-29
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** WLC(Wireless LAN Controller)를 활용한 복수 LAP(Lightweight AP)의 중앙 집중 관리 및 무선 LAN(WLAN) 환경 구축
WLC(Wireless LAN Controller)を活用した複数LAP(Lightweight AP)の一元管理および無線LAN（WLAN）環境の構築


---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
```text
[ Wireless Clients ]
 ├── Tablet PC0 ──┐ (Wi-Fi)
 ├── Tablet PC1 ──┼───────────── [ LAP0 / LAP1 / LAP2 ]
 └── Tablet PC2 ──┘                   (Gig0)
                                         │
                               (Fa0/1, Fa0/2, Fa0/3)
                                         │
  [ Server0 ] ──── (Fa0) ───── (Fa0/4) [ Switch ] (Fa0/5) ─── (Gig1) [ WLC-2504 ] (Gig2) ─── (Fa0) [ Laptop0 ]
 (DHCP Server)                                                             (Wireless Controller)              (Admin PC)
```

- **발생 이슈(Issue):** 기업 내 다수의 무선 AP를 개별 설정하지 않고, WLC를 통해 중앙에서 일괄 제어 및 WLAN 배포 필요
- **事象:** 企業内の多数の無線APを個別に設定せず、WLCを介して中央から一括制御およびWLANの配布が必要

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **분석 내용:** 
  - LAP(Lightweight Access Point): 자체적인 설정 기능이 최소화된 AP로, WLC와 CAPWAP 터널을 형성하여 중앙(WLC)의 제어를 받음.
  - WLC(Wireless LAN Controller): 관리용 PC(Laptop0)에서 WLC Management 포트에 입력한 IP주소에 웹(HTTPS)으로 접속하여 무선 정책(SSID, 보안 인증 방식(WPA+WPA2), VLAN 매핑 등)을 설정하고 AP Group에 지정하면, 그룹 내의 모든 LAP로 일괄 적용됨.
  - TabletPC 등 무선 기기에 SSID와 비밀번호를 입력하면 네트워크 접속 가능.
- **詳細:** 
  - LAP(Lightweight Access Point): 自体的な設定機能が最小化されたAPであり、WLCとCAPWAPトンネルを形成して中央(WLC)の制御を受ける。
  - WLC(Wireless LAN Controller): 管理用PC(Laptop0)からWLCのManagementポートに記入したIPアドレスのウェブページ(HTTPS)へ接続し、無線ポリシー（SSID、セキュリティ認証方式(WPA+WPA2)、VLANマッピング等）を設定してAP Groupに指定することで、グループ内のすべてのLAPへ一括適用される。
  - タブレットPC等の無線機器にSSIDとパスワードを入力することでネットワークアクセス可能となる。

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド

```text
1. [Initial Setup] / [初期設定]
   - WLC Management Port Setup / WLC Managementポートの設定
     - IPv4 Address: 10.10.10.5
     - Subnet Mask: 255.255.255.0
     - Default Gateway: 10.10.10.1
   - Server0 Fa0 Port Setup / Server0 Fa0ポートの設定
     - IPv4 Address: 10.10.10.2
     - Subnet Mask: 255.255.255.0
   - Server0 DHCP Service Setup / Server0 DHCPサービスの設定
     - Default Gateway: 10.10.10.1
     - Start IP Address: 10.10.10.100
     - Subnet Mask: 255.255.255.0
     - Maximum Number of Users: 100
     - WLC Address: 10.10.10.5
   - LAP 전원 연결 및 DHCP IP 자동 할당 확인
     LAPの電源投入およびDHCPによるIPアドレス自動割当の確認
   - Laptop0 Setup (Admin PC) / Laptop0の設定 (管理用PC)
     - IP Address: 10.10.10.10
     - Subnet Mask: 255.255.255.0
     - Default Gateway: 10.10.10.1
     - 설정 후 웹 브라우저에서 WLC(10.10.10.5) 접속 확인
       設定後、ウェブブラウザよりWLC（10.10.10.5）への接続を確認

2. [WLC Setup & WLANs Creation] / [WLC初期設定およびWLAN作成]
   - Admin Account Creation / 管理者アカウントの作成
   - WLC Initial Setup / WLC初期パラメータ設定
     - Management IP Address: 10.10.10.5
     - Subnet Mask: 255.255.255.0
     - Default Gateway: 10.10.10.1
     - Network Name: OFFICE
     - Security: WPA2 Personal
     - Passphrase: 1234567890
   - 설정 완료 후 Laptop0에서 https://10.10.10.5 접속 및 Admin 로그인
     設定完了後、Laptop0から https://10.10.10.5 へアクセスしAdminでログイン
   - WLC GUI -> WLANs 탭 진입 -> OFFICE 설정 수정
     WLC GUI -> WLANsタブへ遷移 -> OFFICE設定の編集
   - SSID(예: Office) 지정 및 Layer 2 Security(WPA+WPA2) 설정
     SSID（例：Office）の指定およびLayer 2 Security（WPA+WPA2）の設定

3. [AP Groups Creation & Setup] / [AP Groupの作成および設定]
   - Add Group 클릭 후 생성
     「Add Group」をクリックして作成
     - AP Group Name: OFFICE
     - Description: OfficeAP
   - WLANs 탭 -> Add New(WLAN SSID=Office) -> Add
     WLANsタブ -> Add New（WLAN SSID=Office） -> Add
   - APs 탭 -> LAP 전체 선택 -> Add APs
     APsタブ -> 対象LAPをすべて選択 -> Add APs

4. [Tablet PC Connection Setup] / [タブレットPCの接続設定]
   - Tablet PC의 Wireless0 Port에 SSID(Office), WPA2-PSK Pass Phrase(1234567890) 설정 후 네트워크 연결 및 통신 검증
     タブレットPCのWireless0ポートにSSID（Office）、WPA2-PSK Pass Phrase（1234567890）を設定し、ネットワーク接続および通信検証を実施
```