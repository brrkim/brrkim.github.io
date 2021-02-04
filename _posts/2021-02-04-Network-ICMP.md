---
title: "파이프라인과 벡터처리"
date: 2020-12-27 12:07:28 -0400
marp: true
categories: computerstructure pipeline vector
---

# 4. 네트워크

## 4.1 IP주소와 라우팅

### 4.1.3 ICMP

- 정의

  - ICMP(Internet Control Message Protocol)
  - 인터넷 제어 메세지 프로토콜
    - IP 통신은 목적지에 패킷을 정상적으로 전달하는 방법은 있지만 에러 발생시 처리 불가
    - ICMP는 IP 통신의 에러 상황을 출발지에 전달 & 메시지 제어 역할
    - ICMP는 IPv4 패킷으로 캡슐화되어서 전달
  - Protocol ID = 1 <-- IP Header에 1로 표시
    - Ping & Traceroute 명령어를 사용
- 기능
  - IP 패킷에 포함
  - Type 8 & 0 (Echo Request & Echo Reply) --> 정보용
    - 네트워크 문제 진단 시 사용 (ping)
    - 목적지 도달 여부, RTT(Round Trip delay time), hop count
    - TTL 값에 따라 OS 종류도 알 수 있음. 일반적으로 Windows계열 128, Linux 계열 64
  - Type 9 & 10 (라우터 광고 & 라우터 정보 요청) --> 정보용
    - 자신이 라우터임을 응답 & 네트워크 진입 시 라우터 정보 요청
  - Type 3 & 5 (Destination Unreachable & Redirect) --> 오류 보고용
    - 라우터가 IP 패킷을 라우팅 하지 못하는 경우 발생
      - 0 = net unreachable
      - 1 = host unreachable
      - 2 = protocol unreachable
      - 3 = port unreachable
      - 4 = fragment unreachable
      - 5 = source route failed
    - Type 5 Redirect: 로컬 네트워크에 2개 이상의 경로가 있을 때 더 좋은 경로 알려줌 --> 이쪽 게이트웨이가 더 좋음을 알려줌 (그러나 대부분 비정상으로 셋팅 확인 필요)
  - Type 11 & 12 (Time Exceeded & Parameter Problem) --> 오류 보고용
    - 시간초과, TTL 값이 0 이 되면 출발지에 응답
    - 11의 코드
      - 0 = TTL Exceeded <-- 목적지 잘못 쓰거나, 라우터 경로에 문제가 있거나, 그쪽 라우터에서 처리를 못하거나, ...
      - 1 = Fragment Reassembly Time Exceeded <-- 바이트를 쪼개서 보냈는데 나머지 를 못받을 경우 그 사이에 발생.
        - MTU(IP패킷 전송 가능한 최대 크기)를 넘어갈 때 발생
    - 12의 코드
      - IP 옵션을 잘못 사용해서 라우터에서 폐기

