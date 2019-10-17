# TP3 - Routage Inter-VLAN + Mise en situation

## I - ROAS (Router On A Stick)

![Infrastructure n°1](images/infra1.PNG)

On configure les addresse IP sur chaque VPCs avec `ip 10.3.x0.x/24` (`x` à remplacer selon le tableau d'adressage ci-dessous).

| Machine | VLAN | IP `net1` | IP `net2` | IP `net3` | IP `netP` |
| ------: | :------: | :------: | :------: | :------: | :------: |
| PC1 | 10 | `10.3.10.1/24` | X | X | X |
| PC2 | 20 | X | `10.3.20.2/24` | X | X |
| PC3 | 30 | X | `10.3.20.3/24` | X | X |
| PC4 | 30 | X | X | `10.3.30.4/24` | X |
| P1 | 40 | X | X | X | `10.3.40.1/24` |
| R1 | X | `10.3.10.254/24` | `10.3.20.254/24` | `10.3.30.254/24` | `10.3.40.254/24` |

Pour configurer les différentes adresses IP sur `R1`, on se rend sur le mode configuration du routeur (`conf t`), on set l'interface que l'on va découper en `no shutdown`. Ensuite, on créée/configure chacune des sous-interfaces de l'interface préalablement choisie, ici e0/0, avec `int e0/0.10`, et on applique l'encapsulation `dot1q` pour le VLAN 10 (`encapsulation dot1q 10`) et finalement, on set l'adresse IP de l'interface avec la commande classico-classique : `ip address 10.3.10.254 255.255.255.0`.

Same shit pour les autres VLANs mais avec des adresse adaptées, hein !

## II - Cas Concret
