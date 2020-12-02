---

title: GNS3 Firewall 실습
category: 네트워크

---

GNS3에서 방화벽 Transparent 모드를 실습해 보자. 

<h2>Transparent 모드</h2>

- 방화벽을 2계층에서 동작 시킨다.
- 외부에서 봤을 때 홉수가 달라지지 않아 존재를 파악하기 힘들다. -> 보안적으로 뛰어나다?!
- 기존 장비들의 IP 주소를 변경시킬 필요가 없다.
- 동일한 서브넷 상에서 이동하는 패킷을 검사하고 필터링할 수 있다.
- 2계층 트래픽 검사하고 원하지 않는 트래픽 필터링 가능
- 관리용 IP가 필요하다
- 동적 라우팅 프로토콜을 지원하지 않으며, 수신한 패킷의 목적지 주소가 방화벽의 MAC 주소 테이블에 이씅면 해당 패킷을 전송하고, 존재하지 않을시 ARP를 수행해 MAC를 참조한다.
- 컨텍스트?!
  이용할시 별개의 네트워크 주소 사용, 동일한 서브넷 이용시 라우터에서 추가 설정 필요, 두 개 이상의 컨텍스에서 하나의 인터페이스 사용 불가. 

<h2>실습</h2>

### 1. <strong>네트워크 전개</strong>
![Network Structure](/img/gns3TPFirewall/firewall_tp_network.png)
### 2. Firewall 설정

```
FW1(config)# firewall transparent
FW1(config)# int bvi 1
FW1(config)# ip add 10.1.12.10 255.255.255.0
FW1(config)# int gi0/0
FW1(config)# bridge-group 1
FW1(config)# nameif inside
FW1(config)# no sh
FW1(config)# int gi0/1
FW1(config)# bridge-group 1
FW1(config)# nameif outside
FW1(config)# no sh
FW1(config)# show bridge-group
```

![fwimg1](/img/gns3TPFirewall/firewall_tp_fw1.png)

```
FW1(config)# show int ip brief
```

![fwimg2](/img/gns3TPFirewall/firewall_tp_fw2.png)

```
FW1(config)# access-list INSIDE-INBOUND permit ip any any
FW1(config)# access-list INSIDE-INBOUND in interface inside
FW1(config)# access-group INSIDE-INBOUND in interface inside
FW1(config)# access-list OUTSIDE-INBOUND permit ospf host 10.1.12.2 any
FW1(config)# access-group OUTSIDE-INBOUND in interface outside
FW1(config)# access-list OUTSIDE-INBOUND permit icmp host 10.1.12.2 host 10.1.12.1
# 이렇게 하면 핑이 갑니다.
# 이게 뭘까..
object network INSIDE-NETWORK
subnet 10.1.12.0 255.255.255.0
nat (inside,outside) dynamic 1.1.1.1
# 10.1.12.0 대역을 1.1.1.1로 변환하는 것. 아펭서는 10.1.12.1 밖에 없으니 1.1.1.1로 다 변환을 하더라도 무리가 없겠죠?
```
	
### 3. 라우터 설정

```
R1(config)# router ospf 1
R1(config)# network 10.1.12.1 0.0.0.0 area 0
R1(config)# network 10.1.1.1 0.0.0.0 area 0

R2(config)# ip route 0.0.0.0 0.0.0.0 1.1.23.3
R2(config)# router ospf 1
R2(config)# net 10.1.2.2 0.0.0.0 area 0
R2(config)# net 10.1.12.2 0.0.0.0 area 0
R2(config)# default-information originate

R3(config)# ip route 1.1.1.0 255.255.255.0 1.1.23.2 
# NAT를 하기 위함이래...
R3(config)# line vty 0 4
R3(config)# password cisco
R3(config)# login
# R1에서 telnet으로 R3에 접속하면 R1의 아이피가 1.1.1.1로 바뀌어 오겠지?	
```
	
### 4. 결과 확인

```
FW1(cofig)# show xlate
```
![fwimg3](/img/gns3TPFirewall/firewall_tp_fw3.png)

### 5. 추가 과제

<strong>ARP Spoofing</strong> 막아보기!

```
FW1(config)# clear configure object
```
	
기존 정보 삭제
```
FW1(config)# arp inside 10.1.12.1 [mac address]
FW1(config)# arp outside 10.1.12.2 [mac address]
```

 MAC Address는 라우터에서 show interface를 통해 확인할 수 있습니다. 

 ex) ```R1(config)# do show interface int fa0/0```
 ```
 R2(config)# int fa0/0 mac-address 1234.5678.0000
 ```
 R2의 MAC 주소를 수정한 후 R1에서 핑을 날릴 경우 R1의 ARP 테이블이 변경되는 것을 알 수 있습니다. 
 ```
 R1(config)# do ping 10.1.12.2
 R1(config)# show arp
 ```
 ![fwimg4](/img/gns3TPFirewall/firewall_tp_fw3.png)
 ```
 FW1(config)arp-inspection inside enable
 FW1(config)arp-inspection outside enable no-flood
 ```
 
 
 ```
 R1# clear arp-cache
 R1# show arp
 ```
 show arp로 기존에 지정된 1234.5678.0000이 없어질 때까지 `clear arp-cache` 명령어를 반복해주자. 한번에 잘 안된다.
```
R1# ping 10.1.12.2
```
ping이 막힌 것을 볼 수 있다. 지정된 MAC 주소와 현재 R2의 MAC 주소가 달라서 기존에 전송되던 핑이 전송이 되지 않는다.
전 포스트에서 ARP Spoofing에 대해 