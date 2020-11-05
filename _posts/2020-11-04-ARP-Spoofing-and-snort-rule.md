---
layout: single
title: ARP Spoofing - dnsniff
categories: 정보보안
---

ARP Spoofing

dnsniff

VMWARE 등의 가상 장비를 사용해서 
arp -a : 현재 MAC 테이블 확인

route -n  : 게이트웨이 주소 확인

arpspoof -i [인터페이스 이름] [target ip] [gateway ip]

VMware를 사용해 실습할 경우 각 OS의 네트워크 인터페이스가 다를 수가 있다. kali는 eth0인데 서버는 ens33이라던지. 이 경우 /etc/default/grub 파일을 수정해 주면 된다.(centOS 기준)
GRUB_CMDLINE_LINUX
/swap []net.ifnames=0] rhgb quite

\# grub2-mkconfig -o /boot/grub2grub.cfg

cd /etc/sysconfig/network-scripts

mv ifcfg-ens33 ifcfg-eth0

vi ifcfg-eth0

그 후 재부팅 후 네트워크를 확인하면 이름이 변경된 것을 알 수 있다.
