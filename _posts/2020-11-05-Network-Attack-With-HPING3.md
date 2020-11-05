---
layout: single
title: DDoS 공격 - hping3
categories: 정보보안
---

<font color= '#ffcc66' >LAND Attack</font>

Land Attack이란 source ip(송신자의 ip)와 destination ip(수신자의 ip)를 같게 만들어 공격하는 방법이다. IP Spoofing을 이용한 공격이다. 

<font color= '#ffcc66' >IP Spoofing</font>
IP Spoofing이란 자신의 ip를 변조해 자신이 만든 패킷을 다른 컴퓨터가 만든 패킷처럼 만드는 것이다. 

hping3 -a [변조할 ip] [수신자의 ip] \-\-icmp \-\-flood 

\-\-flood : 좀 더 패킷을 빠르게 보내기 위해 사용하는 옵션

Ping of Death



