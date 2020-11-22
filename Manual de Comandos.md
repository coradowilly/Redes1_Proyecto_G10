
# MANUAL DE COMANDOS PRACTICA 4

## Topologia 1

> ----------------------------ESW-----------------------------

`config t `

`int range f#/# - # `

`switchport mode trunk `

`no shutdown`

`end`

`sh int trunk `

> ----------------------------VLAN----------------------------

`conf t`

`vlan <numero>`

`name <nombre>`

`end`

`sh vlan-sw`

> ----------------------------Router Interfaz----------------------------


`conf t`

`inf f0/0`

`no shutdown`

`end`

> ----------------------------Routing Estatico----------------------------

`conf t`

`ip address 8.8.8.1 255.255.0.0`

`ip ROUTE 192.168.15.0 255.255.255.0 8.8.8.2`

`exit`
## Topologia 2

- ### **EIGRP**

>----------------------------Router----------------------------

`conf t`

`router eigrp 10`

`network 10.10.0.0 0.0.0.255`

`network 20.10.0.0 0.0.0.255`

`network 192.168.15.0 0.0.0.255`

`end`


- ### **VRRP**

>------------------------Router----------------------------

`conf t`

`vrrp 10`

`vrrp 10 ip 192.168.15.3`

`vrrp 10 priority 120`

`vrrp 10 preempt`

`end`


- ### **INTERFACES**

>------------------------ESW----------------------------

`conf t`
`int range f1/0 - 3`
`no shut`
`end`


- ### **VLAN**

>------------------------EWS2----------------------------

`conf t`

`VLAN 70`

`name INVITADOS`

`end`

`wr`

