# Configuration du switch client #3 :

```
conf t
vlan 10
name admins-vlan
exit
vlan 20
name guests-vlan
exit
vlan 30
name infra-vlan
exit
interface Ethernet 0/0
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30
exit
interface Ethernet 1/0
switchport mode access
switchport access vlan 10
exit
interface Ethernet 1/1
switchport mode access
switchport access vlan 20
exit
interface Ethernet 1/2
switchport mode access
switchport access vlan 20
exit
exit
wr
```

Ce qui donne la conf ci-suivante :

```
client-sw3#show run
Building configuration...

Current configuration : 1711 bytes
!
version 15.1
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname client-sw3
!
boot-start-marker
boot-end-marker
!
!
logging discriminator EXCESS severity drops 6 msg-body drops EXCESSCOLL
logging buffered 50000
logging console discriminator EXCESS
!
no aaa new-model
no ip icmp rate-limit unreachable
!
ip cef
!
!
no ip domain-lookup
no ipv6 cef
ipv6 multicast rpf use-bgp
spanning-tree mode pvst
spanning-tree extend system-id
!
!
vlan internal allocation policy ascending
!
ip tcp synwait-time 5
!
!
interface Ethernet0/0
    switchport trunk encapsulation dot1q
    switchport trunk allowed vlan 10,20,30
    switchport mode trunk
    duplex auto
!
interface Ethernet0/1
    duplex auto
!
interface Ethernet0/2
    duplex auto
!
interface Ethernet0/3
    duplex auto
!
interface Ethernet1/0
    switchport access vlan 10
    switchport mode access
    duplex auto
!
interface Ethernet1/1
    switchport access vlan 20
    switchport mode access
    duplex auto
!
interface Ethernet1/2
    switchport access vlan 20
    switchport mode access
    duplex auto
!
interface Ethernet1/3
    duplex auto
!
interface Ethernet2/0
    duplex auto
!
interface Ethernet2/1
    duplex auto
!
interface Ethernet2/2
    duplex auto
!
interface Ethernet2/3
    duplex auto
!
interface Ethernet3/0
    duplex auto
!
interface Ethernet3/1
    duplex auto
!
interface Ethernet3/2
    duplex auto
!
interface Ethernet3/3
    duplex auto
!
interface Vlan1
    no ip address
    shutdown
!
!
!
no ip http server
!
!
!
!
control-plane
!
!
line con 0
    exec-timeout 0 0
    privilege level 15
    logging synchronous
line aux 0
    exec-timeout 0 0
    privilege level 15
    logging synchronous
line vty 0 4
    login
!
end

```