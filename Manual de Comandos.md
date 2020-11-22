
# MANUAL DE COMANDOS PRACTICA 4

## Topologia 1

> # VTP & VLAN

----------- ESW1 -----------

`conf t `

`int range f1/0 - 9`

`switchport mode trunk`

`no shu`

`exit `

`vtp domain T1Grupo10`

`vtp password T1Grupo10`

`vtp mode server `

`vlan 20 `

`name RED1`

`exit`

`vlan 30`

`name RED2`

`exit`

`vlan 40 `

`name RED3`

`exit`

`vlan 50 `

`name RED4`

`exit`

`write`

----------- ESW2 -----------

`conf t `

`int range f1/0 - 9`

`switchport mode trunk`

`no shu`

`exit `

`vtp domain T1Grupo10`

`vtp password T1Grupo10`

`vtp mode client`

`exit`

`write`

> # Portchannel 
------------ ESW1 ---------

`conf t `

`int range f1/1 - 4`

`channel-group 1 mode on`

`end`

------------ ESW2 ---------

`conf t `

`int range f1/1 - 4`

`channel-group 1 mode on`

`end`

## Topologia 2

