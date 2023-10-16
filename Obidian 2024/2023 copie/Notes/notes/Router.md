---
title: Router
tags: [Import-6cdc]
created: '2023-02-22T08:15:29.000Z'
modified: '2023-03-21T10:48:47.939Z'
---

```
Router#show running-config
Building configuration...

Current configuration : 1002 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname Router
!
boot-start-marker
boot-end-marker
!
enable secret 5 $1$iYOe$i62MKLMIWG1V/ccQBSc7x1
!
no aaa new-model
ip cef
!
!
!
!
ip auth-proxy max-nodata-conns 3
ip admission max-nodata-conns 3
!
vty-async
!
!
!
!
!
!
!
!
interface FastEthernet0/0
 ip address 192.168.0.11 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/1.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface FastEthernet0/1.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
!
interface FastEthernet0/1.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
!
no ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
!
!
!
!
control-plane
!
!
!
line con 0
line aux 0
line vty 0 4
 no login
 transport input telnet
!
scheduler allocate 20000 1000
end

```
