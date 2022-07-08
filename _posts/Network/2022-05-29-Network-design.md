---
layout: single
title: 네트워크 디자인
categories: Network
published : false
---  

## 네트워크 디자인

## Hierarchical 3 Layer
- Core Layer
- Distributiion Layer
- Access Layer

## OSI 7 Layer(ISO 표준 모델)
- Application
- Presentation
- Session
- Transport
- Network
- Data link
- Physical

## TCP/IP Model(미 국방부)
 - Application(HTTP, Telnet, FTP)   : 패킷
 - Transport(TCP,UDP) : DST Port 부여
 - Network(IPv4, IPv6) : Protocol Number 부여
 - Datalink(PPP, Ethernet)   : 네트워크 내부에서 동작, frame, Type Number 부여
 - Physical                  : 세그먼트 내부에서 동작
 각 계층별로 헤더를 부여한다. 패킷의 경우 2,3,4 계층의 헤더가 부여된 형태, 4계층의 데이터전송 단위.

Novel, Apple, DEC 등 10가지 정도의 프로토콜이 있다.
너무 많으니까 관리자 입장에서는 하나의 프로토콜을 이용하길 원한다.
OSI, TCP/IP의 2가지 프로토콜만 남았다.
TCP/IP 모델만 살아남아 사용을 하고 있다. OSI의 경우에는 상용화가 늦어서 TCP/IP 4계층 모델만 살아남게 되었다.

## 라우터와 스위치
 - 라우터 
        3계층(IP)를 가지고 매칭
        3계층에서는 라우팅
        2계층에서는 frame Rewrite
        1계층에서는 증폭

 - 스위치
        2계층(MAC)을 가지고 매칭
        2계층에서는 스위칭
        1계층에서는 증폭
        FCS 필드를 보고 패킷이 깨진거 확인

## Subnet Mask
 네트워크와 Host 주소를 나누는 역할.
 해당 주소의 경계 표시 0 ~ 255.255.255.255의 한정적인 주소 범위를 해결하기 위해 서브넷을 나눠 할당해 사용한다. 이도 부족해서 IPv6가 등장하게 되었다. 
 네트워크 주소를 이용해 라우팅 테이블을 설정한다.
 
## 패킷의 이동
 컴퓨터(APP)에서 가게 되면 장비별로 증폭 및 헤더 부착을 하고 전송

 WEB 서버 기준

 Client to Server : Request(Get, POST)

 Server to Client : Response(200,300,400,500)

## IP설계
 1. Subnet Mask 결정
 2. 중복되지 않은 IP 할당
 
## TCP/UDP 
 TCP: MSS(Max Segment Size) 단위로 자른다.-> 세그먼트 단위로 자른다. 네트워크 공유 가능. 어느 장비에서 보낸 패킷인지 확인 가능
 패킷 단위가 커도 쓸 수 있다.  
 - Sequence #에 맞춰서 조립 가능.
 - DST/SRC port가 존재

 UDP: 세그먼트 단위로 자르지 않는다.
 네트워크 독점한다. 자르지 않을 작은 크기의 패킷이라면 사용하는게 좋다.
 - Sequence #가 없다.
 - DST/SRC port가 존재

 ## TCP Packet
  - 2계층에서 TYPE #
  - 3계층에서 Protocol #
  - 4계층에서 DST/SRC port
  - Sequence #가 있으면 TCP 없으면 UDP 등의 프로토콜
  - Code Bit
    1. SYN 
    2. ACK : 받았다는 표시
    1. FIN : 통신 종료
    1. RST : 비정상적 종료
    1. PSH : 푸시 비트, 주로 클라이언트의 통신이 끝났을 때 사용
    1. URG : urgent 비트, 중요 데이터의 위치를 표시
  - Control Bit
    1. Error Control : Ack - #
    2. Flow Control : Window Size(RWND, CWND)
        - CWND : 통신이 원할하지 않을 때 보내는 비트 추가 조사 필요. 큰 문제가 있을 경우는 1로 내려가고 작은 문제 3-Ack 등 이 경우에는 cwnd가 1/2로 내려감
    3-Ack를 통해 특정 패킷이 깨진것을 확인 가능
## UDP
 - TYPE #
 - Protocol #
 - DST/SRC port
 - Length
 - Checksum
 데이터 사이즈 적고 가까운 거리에 client server가 있는경우

 SYN-ACK 3-way Handshake 과정에서 사용. 
 Connection Oriented(TCP/PPP)
 3-way Handshake 안할 경우 Connection less Protocol(UDP/IP/Ethernet)
 마칠 경우 4-way HandShake 사용