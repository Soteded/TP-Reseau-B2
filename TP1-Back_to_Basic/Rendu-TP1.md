# TP1 - Back to Basics

## I.Gather Informations

* Liste des cartes réseaux :
    ```
    [sote@localhost ~]$ ip a
        1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
            link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
            inet 127.0.0.1/8 scope host lo
                valid_lft forever preferred_lft forever
            inet6 ::1/128 scope host
                valid_lft forever preferred_lft forever
        2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
            link/ether 08:00:27:2e:1b:a3 brd ff:ff:ff:ff:ff:ff
            inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
                valid_lft 85836sec preferred_lft 85836sec
            inet6 fe80::f9ba:9cc:b82f:350e/64 scope link noprefixroute
                valid_lft forever preferred_lft forever
        3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
            link/ether 08:00:27:6b:9b:e4 brd ff:ff:ff:ff:ff:ff
            inet 192.168.140.2/24 brd 192.168.140.255 scope global noprefixroute enp0s8
                valid_lft forever preferred_lft forever
            inet6 fe80::a00:27ff:fe6b:9be4/64 scope link
                valid_lft forever preferred_lft forever
    ```

* Déterminer si les cartes réseau ont récupéré une IP en DHCP :
  * enp0s3 (à internet) : Oui comme le montre le fichier `internal-8c885912-ab77-4838-8846-6a7d444dcb84-enp0s3.lease` dans le dossier `/var/lib/NetworkManager/` avec la commande ci-suivant : ```[sote@localhost ~]$ sudo cat /var/lib/NetworkManager/internal-8c885912-ab77-4838-8846-6a7d444dcb84-enp0s3.lease
  *This is private data. Do not parse.*
    ADDRESS=10.0.2.15
    NETMASK=255.255.255.0
    ROUTER=10.0.2.2
    SERVER_ADDRESS=10.0.2.2
    NEXT_SERVER=10.0.2.4
    T1=43200
    T2=75600
    LIFETIME=86400
    DNS=10.33.10.20 10.33.10.2 8.8.8.8 8.8.4.4
    DOMAINNAME=auvence.co
    CLIENTID=010800272e1ba3```
  * enp0s8 (SSH) : L'IP de cette carte réseau est fixe car on peut constater qu'il n'y a pas de bail DHCP via : ```[sote@localhost ~]$ nmcli con show enp0s8 | grep "dhcp"
            ipv4.dhcp-client-id:                    --
            ipv4.dhcp-timeout:                      0 (default)
            ipv4.dhcp-send-hostname:                yes
            ipv4.dhcp-hostname:                     --
            ipv4.dhcp-fqdn:                         --
            ipv6.dhcp-duid:                         --
            ipv6.dhcp-send-hostname:                yes
            ipv6.dhcp-hostname:                     --```