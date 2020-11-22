
# MANUAL DE COMANDOS Proyecto Final

## Topologia 1

> VTP & VLAN

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

>  Portchannel 

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

----------- EWS2  -------------------

`conf t`

`interface range f1/0 - 2`

`switchport mode trunk`

`no shutdown`

`end`

`write`


--- configurando dominio ----

`conf t`

`vtp domain T2GRUPO10`

`vtp password T2GRUPO10`

`vtp mode server`

`end`

`write`

`sh vtp status`

---configurando vlan ---------

`conf t`

`vlan 510`

`name RED5`

`end`

`write`

`conf t`

`vlan 610`

`name RED6`

`end`

`write`

`sh vlan-sw`



----------- EWS1 ----------------

`conf t`

`interface range f1/0 - 2`

`switchport mode trunk`

`no shutdown`

`end`

`write`



`conf t`

`vtp domain T2GRUPO10`

`vtp password T2GRUPO10`

`vtp mode client`

`end`

`write`

`sh vtp status`



-----------EWS3-------------------------

`conf t`

`interface range f1/0 - 2`

`switchport mode trunk`

`no shutdown`

`end`

`write`


`conf t`

`vtp domain T2GRUPO10`

`vtp password T2GRUPO10`

`vtp mode client`

`end`

`write`

`sh vtp status`

---------------- HSRP ----------------

ACTIVO

`configure terminal`

`interface F#/# `

`standby # ip "ip-virtual"`

`standby # priority #`

`standby # preempt`

`exit`

STAND BY

`configure terminal`

`interface f#/# `

`standby # ip "ip-virtual"`

`standby # priority # `

`exit`

> ASIGNAR IP VIRTUAL A LAS VLAN 

`conf t`

`int f#/#.#`

`encapsulation dot1q #`

`ip address <gateway> <mask>`

`exit`