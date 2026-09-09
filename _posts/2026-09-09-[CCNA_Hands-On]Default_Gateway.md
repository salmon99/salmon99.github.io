---
published: true
title:  "[CCNA Hands-On] Default Gateway"
excerpt: "CCNA 합격 후 Cisco Packet Tracer로 Hands-On을 하며 복습한 기록입니다."

categories:
  - CCNA
  - Hands-On
tags:
  - DefaultGateway
  - CCNA
  - Hands-On
last_modified_at: 2026-09-09T15:00:00
--- 

# [CCNA Hands-On] Default Gateway

> **Notice:** 본 포스트는 일본어 실무 표현 연습을 위해 한국어와 일본어로 동일한 내용을 작성하였습니다.
※ 本記事は、実務表現の練習を兼ねて、韓国語と日本語で同じ内容を記載しています。

- **Date:** 2026-09-09
- **Environment:** Cisco Packet Tracer / Udemy(【超絶入門】CCNA対策 Packet Tracerで学ぶ ハンズオン講座)
- **Goal:** Default Gateway 설정
デフォルトゲートウェイ設定

---

### 1. 토폴로지＆발생 이슈(Topology & Issue)
### 1. 構成および発生事象
- **토폴로지(Topology) / 構成図**
[PC1 (10.10.10.1/24)] --- [R1] --- [PC2 (192.168.1.1/24)]
<br>
- **발생 이슈(Issue):** PC1 / PC2 상호 Ping 통신 실패(`Request timed out.`)
- **事象:** PC1 / PC2 相互Ping通信不可(`Request timed out.`)

---

### 2. 원인 분석 (Root Cause)
### 2. 原因分析
- **원인:** PC1, PC2의 IP 설정 중 Default Gateway 주소가 누락됨.
- **原因:** PC1, PC2のIP設定の中でデフォルトゲートウェイのIPアドレス設定漏れ
- **분석 내용:** 같은 서브넷 내 통신은 가능하나, 외부 네트워크로 나가는 출입구(Gateway) 경로를 찾지 못함.
- **詳細:** 同じサブネットの中では通信可能、外部ネットワークに通じるゲートウェイ経路未設定

---

### 3. 해결 방법 & 커맨드 (Solution & Commands)
### 3. 対応内容およびコマンド
원인 해결을 위해 PC1, PC2의 IP Configuration 설정 수정.
事象解消のため、PC1/PC2のIP Configuration設定修正

```bash
# PC1 IP Configuration
Default Gateway: 10.10.10.254
# PC2 IP Configuration
Default Gateway: 192.168.1.254
```