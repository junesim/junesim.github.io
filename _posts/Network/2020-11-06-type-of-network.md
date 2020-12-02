---

layout: single
title: 네트워크 통신 방식의 종류
categories: 네트워크

---
&nbsp;&nbsp;통신방식들에 대해 알아보자.

&nbsp;&nbsp;통신 방식을 나누는 방법엔 다양한 방법이 있다. 크게 <strong>연결형(Connection)</strong>과 <strong>비연결형(Connectionless)</strong>으로 나눌 수 있다. 
<h2>연결형(Connection)</h2>
&nbsp;&nbsp;데이터 송신을 시작하기 전에 호스트 간의 회선을 논리적으로 연결한 후 통신을 시작한다. 연결의 확립과 끊기 과정이 필요하지만 신뢰성이 높다. 데이터의 순서가 중요할 경우 적합하다. 전화를 생각하면 이해가 편할듯 하다. 대표적인 프로토콜로는 <strong>TCP</strong>가 해당된다. 
<h2>비연결형(Connectionless)</h2>
&nbsp;&nbsp;비연결형의 경우 연결의 확립과 끊기 처리가 없다. 송신자는 수신자가 확인되지 않아도 데이터의 전송이 가능하다. 신뢰성이 높지는 않지만 프로토콜이 간단해 비용이 작다는 장점이 있다. <strong>데이터그램</strong>이라는 전송 단위로 전송된다. 대표적으로 <strong>UDP</strong>가 해당된다.
<h2>유니캐스트</h2>
&nbsp;&nbsp;1대1 통신을 의미한다. 전화를 생각하면 편리하다. <strong>IPv4/IPv6</strong> 둘 다 지원하는 방식이다.
<h2>브로드캐스트</h2>
&nbsp;&nbsp;1대의 호스트에서 연결된 모든 호스트에게 정보를 발신한다. 브로드캐스트가 통신할 수 있는 범위를 브로드캐스트 도메인이라고 한다. 멀티캐스트를 사용해 구현할 수 있다. <strong>IPv4</strong>에서만 지원하는 방식이다. 
<h2>멀티캐스트</h2>
&nbsp;&nbsp;브로드캐스트와 여러 개의 호스트와 통신을 하지만 <strong>특정 그룹</strong>으로 한정한다. 네트워크 장비가 이 기능을 제공해야만 사용이 가능하다. <strong>IPv4/IPv6</strong> 모두 지원한다. 
<h2>애니캐스트</h2>
&nbsp;&nbsp;멀티캐스트와 같이 특정 그룹의 호스트를 향해 정보를 발신하지만 여러 호스트 중 네트워크상에 최적의 조건을 가지고 있는 호스트를 선별하고 이후 통신이 진행된다. <strong>IPv6</strong>에서 지원된다. 