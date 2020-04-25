# Configuration du routeur :

```
conf t
int f0/0
no shut
ip nat outside
ip address dhcp
exit
int f2/0
no shut
exit
int f2/0.30
encapsulation dot1q 30
ip address 10.5.30.254 255.255.255.0
ip nat inside
exit
int f1/0
no shut
ip nat inside
exit
int f1/0.10
encapsulation dot1q 10
ip address 10.5.10.254 255.255.255.0
ip nat inside
exit
int f1/0.20
encapsulation dot1q 20
ip address 10.5.20.254 255.255.255.0
ip nat inside
exit
access-list 1 permit any
ip nat inside source list 1 interface fastEthernet 0/0 overload
exit
wr
```

Ce qui donne la configuration :

```
R1#show run
Building configuration...

Current configuration : 1594 bytes
!
upgrade fpd auto
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
boot-start-marker
boot-end-marker
!
logging message-counter syslog
!
no aaa new-model
ip source-route
no ip icmp rate-limit unreachable
ip cef
!
!
no ip domain lookup
no ipv6 cef
!
multilink bundle-name authenticated
!
!
archive
 log config
  hidekeys
!
!
ip tcp synwait-time 5
!
!
interface FastEthernet0/0
    ip address dhcp
    ip nat outside
    ip virtual-reassembly
    duplex half
!
interface FastEthernet1/0
    no ip address
    ip nat inside
    ip virtual-reassembly
    duplex half
!
interface FastEthernet1/0.10
    encapsulation dot1Q 10
    ip address 10.5.10.254 255.255.255.0
    ip nat inside
    ip virtual-reassembly
!
interface FastEthernet1/0.20
    encapsulation dot1Q 20
    ip address 10.5.20.254 255.255.255.0
    ip nat inside
    ip virtual-reassembly
!
interface FastEthernet2/0
    no ip address
    duplex half
!
interface FastEthernet2/0.30
    encapsulation dot1Q 30
    ip address 10.5.30.254 255.255.255.0
    ip nat inside
    ip virtual-reassembly
!
ip forward-protocol nd
no ip http server
no ip http secure-server
!
!
ip nat inside source list 1 interface FastEthernet0/0 overload
!
access-list 1 permit any
no cdp log mismatch duplex
!
!
control-plane
!
!
gatekeeper
 shutdown
!
!
line con 0
    exec-timeout 0 0
    privilege level 15
    logging synchronous
    stopbits 1
line aux 0
    exec-timeout 0 0
    privilege level 15
    logging synchronous
    stopbits 1
line vty 0 4
    login
!
end

```