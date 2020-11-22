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

- Calculo Ruta STP

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

|Vlan| IP VIRTUAL |
|----|----|
|1|192.168.101.10/24|
|2|192.168.20.10/24|
|3|192.168.30.20/24|
|4|192.168.40.20/24|


- TOPOLOGIA 2

### **VLAN**

|Subred|VLAN| IP VIRTUAL |
|----|----|---|
|f0/0.1|60|192.168.60.254|
|f0/0.2|70|192.168.70.254|
|f0/1.1|60|192.168.61.254|
|f0/1.2|70|192.168.71.254|
|f1/0.1|60|192.168.62.254|
|f1/0.2|70|192.168.72.254|

### **HSRP**

|Interfaz|Modo| IP VIRTUAL |
|----|----|---|
|f0/0|Espera|192.168.0.254|
|f0/1|Activo|192.168.1.254|
|f1/0|Espera|192.168.2.254|


---
---
# Topologia.
> La topologia para la solucion del  problema es la siguiente:

TOPOLOGIA 1

![Topologia](/Images/T1.png)

TOPOLOGIA 2

![Topologia](/Images/Topologia2.jpeg)

---
**Dispositivos a Configurar**
Topologia 1
- 1 Cloud
- 3 Router
- 2 Etherneth Switch
- 4 Switch
- 4 Maquina Virtual con SO TinyLinux 

Topologia 2
- 1 Cloud
- 1 Router
- 3 Etherneth Switch
- 2 Switch
- 2 Maquina Virtual con SO TinyLinux 
- 1 VPC
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

El rango de las interfaces dependera de cuales estan conectados al ESW.

> Paso 2: Crear VLAN's en ESW


Las vlans se configuran con los siguientes comandos:

`conf t`

`vlan <numero>`

`name <nombre>`

`end`

Para observar las vlans se utiliza el siguiete comando:

`sh vlan-sw`

Para configurar la VTP en modo servidor o cliente utilizamos los siguientes comandos:

`conf t`

`vtp domain <nombre> `

`vtp password <password> `

`vtp mode server|client`

`end`

Para configurar el port-channel se utilizan los siguientes comandos:

`conf t`

`int range f#/# - # `

`channel-group <numero> mode on`

`end`

Configuracion ESW Topologia 1

EWS1
![esw](/Images/EWS1-T1.png)

EWS2
![esw](/Images/EWS2-T1.png)

PORT-CHANNEL
![esw](/Images/EWS2-CH-T1.png)

Configuracion ESW Topologia 2

EWS1
![esw](/Images/esw1.jpg)

EWS2
![esw](/Images/esw2.jpg)
![esw](/Images/ews22.jpg)


EWS3
![esw](/Images/esw3.jpg)

> Paso 3: Configurar los puertos de los switch.

Se necesita configurar los tipos de los puertos de los switch, esto dependera de cuales estan conectados a los ESW y cuales estan conectados a los host dependiendo a que vlan pertenecen


GNS3 nos permite configurar desde un panel estos puertos.

`Click derecho -> Configure `

TOPOLOGIA 1

Switch 1
![sw](/Images/SWITCH1-T1.png)
Switch 2
![sw](/Images/SWITCH2-T1.png)
Switch 3
![sw](/Images/SWITCH3-T1.png)
Switch 4
![sw](/Images/SWITCH4-T1.png)

TOPOLOGIA 2

Switch 1
![sw](/Images/sw1.jpeg)
Switch 2
![sw](/Images/sw2.jpeg)


> Paso 4: Configuracion del Router 

Para configurar las subinterfaces en el router primero se habilita la interfaz conectada y despues se crean la subinterfaces:

`conf t`

`inf f#/# | int f#/#.#`

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



---
---
# Calculo de ruta STP.

Se utilizo el siguiente comando para ver y observar que interfaces estan conectadas o no son necesarias.

` sh spanning-tree blockedports`

TOPOLOGIA 1
ESW1
![pq](/Images/ESW1-SPT-T1.png)

ESW2
![pq](/Images/ESW2-SPT-T1.png)

CON STP
![pq](/Images/SPT-T1.png)


---
---
# Captura de Parquetes.

Para verificar que los host se estan enviando y recibiendo los paquetes de informacion se procedera a verificar la captura de paquetes:

Primero se realiza un ping a cualquiera de los demas host con:

`ping <ip> -t`

Posterior se coloca sobre una conexcion y se inica la captura de paquetes:

`Click derecho -> Start Capture`

Se abrira la aplicacion Wireshark y se pude observar que los paquetes se estan enviando y recibiendo correctamente:

TOPOLOGIA 1
![pq](/Images/cap1.jpg)

---
