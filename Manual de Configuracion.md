# MANUAL DE CONFIGURACION PRACTICA 4
---
![](/Images/Logo.png)
## Laboratorio Redes de Computadoras 1
### Segundo Semestre 2020
---

| Carnet | Nombre |
| ------ | ------ |
|201602412|William Adolfo Corado Cabrera |
| 201602517 | Marvin Saul Guzman Garcia |
|201603016|Miamin Eliel Barrios Arrivillaga|



> 06/11/2020
---
---
## INDICE

- Definicion de las redes.

- Configuracion de la topologia de red.

- Calculos de Sub Interfaces

- Captura de Paquetes.

---
---
## Software que se Utilizada (GNS3)
>GNS3 es un simulador gráfico de red lanzado en 2008, que te permite diseñar topologías de red complejas y poner en marcha simulaciones sobre ellos, ​​​ permitiendo la combinación de dispositivos tanto reales como virtuales.

![GNS3](/Images/gns3.png)

---
---
# Definicion de las redes.

>Redes utilizadas dentro de la topologia:

- VPN

| Interna | Externa | CLIENTE1 | CLIENTE2 |
|---------|---------|-----------|---------|
|10.128.0.2|35.226.224.98|10.8.0.4|10.8.0.3|


- TOPOLOGIA 1

![Topologia](/Images/rede1.jpg)

- TOPOLOGIA 2

|Aparato| IP VIRTUAL |
|----|----|
|EWS2|192.168.15.3|
|R3|192.168.15.1|
|R4|192.168.15.2|
|VM|192.168.15.10|
|VM|192.168.15.15|


---
---
# Topologia.
> La topologia para la solucion del  problema es la siguiente:

TOPOLOGIA 1

![Topologia](/Images/Topologia1.jpeg)

TOPOLOGIA 2

![Topologia](/Images/Topologia2.jpeg)

---
**Dispositivos a Configurar**
Topologia 1
- 1 Cloud
- 1 Router
- 1 Etherneth Switch
- 2 Switch
- 4 Maquina Virtual con SO TinyLinux 

Topologia 2
- 1 Cloud
- 3 Router
- 1 Etherneth Switch
- 2 Switch
- 2 Maquina Virtual con SO TinyLinux 
---
---

# Configuracion de la topologia de red.

Se presentaran los comandos utilizados para configurar cada parte de la topologia asi como capturas de pantalla como prueba de la elaboracion en GNS3

---
## **Ethernets Switch**

> Paso 1: Configurar todas las interfaces de los ESW.

`config t `

`int range f#/# - # `

`switchport mode trunk `

`no shutdown`

`end`

Para visualizar la configuracion se utiliza el comando:

`sh int trunk `

ESW1

![esw](/Images/esw1.jpg)


El rango de las interfaces dependera de cuales estan conectados al ESW.


> Paso 2: Crear VLAN's en ESW

Para esta topologia se utilizaran 3 vlans:

|Vlan| Nombre |
|----|----|
|20| PROFESORES|
|50| ESTUDIANTES|
|70| INVITADOS|

Las vlans se configuran con los siguientes comandos:

`conf t`

`vlan <numero>`

`name <nombre>`

`end`

Para observar las vlans se utiliza el siguiete comando:

`sh vlan-sw`

![esw](/Images/esw13.jpg)


> Paso 3: Configurar los puertos de Switch1 y Switch2.

Se necesita configurar los tipos de los puertos de los switch, esto dependera de cuales estan conectados a los ESW y cuales estan conectados a los host dependiendo a que vlan pertenecen


GNS3 nos permite configurar desde un panel estos puertos.

`Click derecho -> Configure `

Ejemplo

Switch 1

![sw](/Images/sw1.jpeg)



> Paso 4: Configurar una red a cada subinterfaz del router 

Para configurar las subinterfaces en el router primero se habilita la interfaz conectada:

`conf t`

`inf f0/0`

`no shutdown`

`end`

![r](/Images/r1.jpg)

>Paso 5: Enrutamiento Estatico

Para el enrutamiento se utilziaron los siguientes comandos

Topologia 1

`conf t`

`ip address 8.8.8.1 255.255.0.0`

`ip ROUTE 192.168.15.0 255.255.255.0 8.8.8.2`

`exit`

Topologia 2

`conf t`

`ip address 8.8.8.2 255.255.0.0`

`ip ROUTE 192.168.15.0 255.255.255.0 8.8.8.1`

`exit`

Ejemplo
![r](/Images/enrut.jpg)

>Paso 6: Configuracion Clouds

Para configurar las nubes que se conectaran entre ambas se hace lo siguiente:

`Click derecho->Configuracion`

Topologia 1
![r](/Images/cloud1.jpeg)

Topologia 2
![r](/Images/cloud2.jpeg)



>Paso 7: Realizar ping

Ahora se debera de realizar los diversos pings entre los host para verificar la conexion:

`ping <ip>`

![pn](/Images/ping13.jpeg)

![pn](/Images/ping24.jpeg)

![pn](/Images/ping31.jpeg)




---
---
# Calculo de SubInterfaces.

Se utilizo la herramienta de Excel para poder calcular todas las subinterfaces de las topologias.

![pq](/Images/calc.jpg)

---
---
# Captura de Parquetes.

Para verificar que los host se estan enviando y recibiendo los paquetes de informacion se procedera a verificar la captura de paquetes:

Primero se realiza un ping a cualquiera de los demas host con:

`ping <ip> -t`

Posterior se coloca sobre una conexcion y se inica la captura de paquetes:

`Click derecho -> Start Capture`

Se abrira la aplicacion Wireshark y se pude observar que los paquetes se estan enviando y recibiendo correctamente:

![pq](/Images/cap.jpg)

---
