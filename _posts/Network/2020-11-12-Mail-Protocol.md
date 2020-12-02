---
type: posts
title: 메일 프로토콜과 구성요소에 대해 알아보자
categories: [네트워크]

---

메일 프로토콜과 구성요소에 대해 알아보자.

<h2>메일 프로토콜</h2>

<strong>SMTP</strong> : Simple Mail Transfer Protocol 클라이언트에서 메일을 보내거나 메일 서버끼리 메일을 주고 받을 떄 사용하는 프로토콜

<strong>POP3, IMAP3</strong> : 메일 서버에 있는 메일을 클라이언트로 가져오는 프로토콜

보낼 때는 SMTP 받을 때는 POP3, IMAP3

<strong>차이점</strong>
POP3의 경우 클라이언트가 서버의 메일을 가져오게 되면 서버의 메일은 삭제된다. IMAP3의 경우 클라이언트가 가져간다 하더라도 서버의 메일은 유지된다. 서버가 메일을 감당하기 힘들 경우 POP3를 사용하게 되면 서버의 비용이 준다는 장점이 있다. 요즘은 보통 IMAP을 사용합니다.

구성 요소

MTA, MUA, MDA, MRA, 메일 큐

<strong>MUA</strong>: Mail User Agnet 자신이 속한 메일 서버에 전송해 줍니다. 메일을 다운로드하거나 MTA로 업로드. SMTP에 의해 접속하며 인증과정 필요.

ex) Thunderbird, Outlook, Evolution

<strong>MTA</strong>: Mail Transfer Agent. 다른 MTA나 메일 사용자에게 메일을 보내거나 받는 역할을 해줍니다.(RELAY 과정) 또한, 바이러스 및 스팸 메일과 같은 필터링 기능이 있다. 25포트를 사용하는 SMTP에 의해 이뤄진다.  

ex) sendmail,Qmail,Postfix

<strong>MDA</strong>: Mail Delivery Agent 메일 서버간 메일을 송신해줍니다. MTA한테 메일을 받아 사용자의 메일서버에 저장 및 운반하는 역할. 메일 서버의 메일을 MUA가 읽어 로컬 PC에 다운로드 시 IMAP POP3

ex) Dovecot, Courier, Cyrus

<strong>메일 큐</strong>: 전송량이 많아 메일이 전송되지 않을 경우 메일이 보내지지 않는 경우가 많았다고 한다. 그래서 메일 큐를 생성해 메일을 보내지 못할 경우 큐에 저장을 해놓고 전송이 가능할 때 메일을 보내주는 개념이다. 


<!--

dns mx(mailexchanger) 추가
nslookup에서 지정한 도메인을 쳤을 경우 ip가 정확하면 성공.

dns 설정을 자신이 설정한 ip로 설정해줘야합니다.
sendmail-cf , dovecot 다운로드 
이툴을 이용해서 할껀가봐
/sendmail.cf
85 localhost를 자신이 설정한 mail 도메인으로
264 수정 루프백 아이피 제거

/etc/mail/access에 지정한 도메인 추가

restart 하고 makemap hash를 통해 재생성

/etc/dovecot/conf.d/10-mail.conf
25,116 : 주석제거
121 : group mail 추가

10-auth.conf
10: no로 plaintext_auth를 가능하게

10-ssl.conf
8 :ssl yes

user 추가

sendmail, dovecot  재시작


thunderbird 설치 후 자신에게 메일 보내보기

thunderbird 설정 포트 110,25 서버 호스트 생성해준것으로, ssl은 사용하지 않고 인증은 평문패스워드와 커버로스 -->