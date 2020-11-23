---

layout: single
title: 프로토콜에 따른 패킷의 헤더
categories: [네트워크]

---

 프로토콜에 따라 패킷의 헤더는 달라진다. 이에 대해 알아보자
 
 <h2>UDP 패킷 헤더</h2>
 <strong>UDP 패킷 헤더</strong>는 64비트로 16비트의 4가지 필드로 구성되어 있다.
 
- Source Port Number: 송신 포트 번호
- Destination Port Number: 수신 포트 번호
- UDP Length: 패킷의 길이
- UDP Checksum: 패킷 전체의 Checksum, 이 필드가 0일 경우 수신측은 체크섬을 계산하지 않는다. 