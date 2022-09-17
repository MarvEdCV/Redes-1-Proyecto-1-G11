# Redes-1-Proyecto-1-G11

---
### Universidad de San Carlos de Guatemala
### Facultad de Ingeniería 
### Laboratorio Redes de Computadoras 1 N
### Segundo Semestre 2022
### Grupo 11
### Tutor: Jhonnatan Orantes 
---

| Estudiante | Carné | 
| ------ | ------ |
| Sara Paulina Medrano Cojulún | 201908053 |
| Marvin Eduardo Catalán Véliz | 201905554 |
| Julio José Orellana Ruíz | 201908120 |

---
# Creación de una VPN

### Pasos

- Se creó una VM en GCP con SO Ubuntu.
- Se actualizaron paquetes sudo apt-get update
- Se instaló Open VPN con el siguiente script

```bash
curl -O **[https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh](https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh)** chmod +x openvpn-install.sh
```

- Se configura la VPN con las ip´s publicas y privadas de la VM y todo lo demás se deja por default.
- Se crean los clientes (en nuestro caso sin contraseña y se descarga cada uno de los archivos que se generan)
- Cada cliente descarga OpenVPN connect para poder ejecutar el archivo que se generó desde el server.

![](/Img/vp1.png)

![](/Img/vp2.png)

---

### Detalles de VLAN

| VLAN | #VLAN | Dirección de red | Gateway |
| -------| -------| -------|  -------|
| RRHH | 10 | 192.168.111.0/24 | 192.168.111.1 |
| Informatica | 20 | 192.168.112.0/24 | 192.168.112.1 |
| Contabilidad | 30 | 192.168.113.0/24 | 192.168.113.1 |
| Ventas | 40 | 192.168.114.0/24 | 192.168.114.1 |

## Configuración de Topologia
Uno de los primeros pasos a realizar será el cargar la Imagen del swith a utilizar en el Emulador GNS3.

Debe realizarse los siguientes pasos:

#### Paso 1
Primero debe descargarse la imagen de Ethernetswith o Switch de capa 3 que se encuentra en el siguiente enlace:
```
https://drive.google.com/file/d/10810USuKu7M6s-_u6cIxek-6czPIt7XH/view
```

#### Paso 2
Luego abrimos el emulador GNS3 y en todos los servicios en llamado "Browse all device", y luego se preciona en "New Template".

![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/General_1.png)

#### Paso 3
Se abrira la ventana de Preferencias, acá buscaremos del lado izquierdo de la ventana el menú "Dynamips" u daremos click en el sub-menu "IOS routers".

Acá apareceran los Routes o Switchs capa 3 que se tengan configurados. Luego buscaremos el botón "Nuevo" o "New" y daremos click cn el boton para agregar un nuevo Router.

![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/General_2.png)


#### Paso 4
Se abrira una ventana, en la cual pedira que escoja la ruta de la Imagen que desea cargar. Para ello presionara el botón "Browse...".

Esto le abrira una ventana en la cual podrá buscar la imagen en su computadora y seleccionarla.
Al seleccionar la imagen se cargara la ruta en la pantalla y tendrá que presionar el boton "Siguiente" o "Next".

![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/General_3.png)

#### Paso 5
Luego se abrirar una pantalla en la cual le pedirá que ingrese en el campo "Name" o "Nombre" el nombre del Switch que esta cargando (esto queda a su discrecion).
Adicional la pantalla le solicita que seleccione la Plataforma del Router que desea cargar, para este proyecto se utilizo la Plataforma "C3725"

Seleccionar la opción "This is an EtherSwitch router".

Por último presione "Siguiente" en la parte inferior derecha de la pantalla a todas las pestañas posteriores y al finalizar se le apacara el boton "finish".

![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/General_4.png)

#### Paso 6
Último paso, acá debera comprobar que el router se encuentra configurado en su simulador, en la parte izquierda deberá aparecerle el logo del nuevo dispositivo.

![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/General_5.png)

---

## Topología 1

![topo1](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_0.jpg)

### Distribución de direcciones IP correspondientes a cada departamento de la empresa

| VPCS | IP | Mascara de subred | Gateway | Comando |
| ------ |------ |------ |------ | ------ |
| RRHH_1 | 192.168.111.10 | 255.255.255.0 | 192.168.111.1 | ip 192.168.111.10 255.255.255.0 192.168.111.1 |
| Conta_1 | 192.168.113.10 | 255.255.255.0 | 192.168.113.1 | ip 192.168.113.10 255.255.255.0 192.168.113.1 |
| RRHH_2 | 192.168.111.20 | 255.255.255.0 | 192.168.111.1 | ip 192.168.111.20 255.255.255.0 192.168.111.1 |
| Conta_2 | 192.168.113.20 | 255.255.255.0 | 192.168.113.1 | ip 192.168.113.20 255.255.255.0 192.168.113.1 |
| Ventas_1 | 192.168.114.10 | 255.255.255.0 | 192.168.114.1 | ip 192.168.114.10 255.255.255.0 192.168.114.1 |
| Informatica_1 | 192.168.112.10 | 255.255.255.0 | 192.168.112.1 | ip 192.168.112.10 255.255.255.0 192.168.112.1 |


### Comandos 
RHHH_1
```
ip 192.168.111.10 255.255.255.0 192.168.111.1
sh ip
save
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_1.jpg)

Conta_1
```
ip 192.168.113.10 255.255.255.0 192.168.113.1
sh ip
save
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_2.jpg)


RRHH_2
```
ip 192.168.111.20 255.255.255.0 192.168.111.1
sh ip
save
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_3.jpg)


Conta_2
```
ip 192.168.113.20 255.255.255.0 192.168.113.1
sh ip
save
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_4.jpg)


Ventas_1
```
ip 192.168.114.10 255.255.255.0 192.168.114.1
sh ip
save
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_5.jpg)


Informatica_1
```
ip 192.168.112.10 255.255.255.0 192.168.112.1
sh ip
save
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_6.jpg)

### ESW1
```
conf t
vtp domain GRUPO11
vtp password grupo11
vtp mode client
exit
sh vtp st
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_7.jpg)


Configurando modo truncal
```
conf t
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_8.jpg)


### ESW2
```
conf t
vtp domain GRUPO11
vtp password grupo11
vtp mode client
exit
sh vtp st
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_9.jpg)


Configurando modo truncal
```
conf t
int f1/3
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_10.jpg)

Configurando modo acceso
```
conf t
int f1/4
switchport mode access
switchport access vlan 10
exit
int f1/0
switchport mode access
switchport access vlan 30
exit
int f1/1
switchport mode access
switchport access vlan 10
exit
exit
sh vlan-sw
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_11.jpg)

### ESW3

```
conf t
vtp domain GRUPO11
vtp password grupo11
vtp mode client
exit
sh vtp st
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_12.jpg)

Configurando modo truncal
```
conf t
int f1/4
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
int f1/5
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit
exit
write
sh int tr
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_13.jpg)

Configurando modo acceso
```
conf t
int f1/0
switchport mode access
switchport access vlan 30
exit

int f1/2
switchport mode access
switchport access vlan 40
exit

int f1/1
switchport mode access
switchport access vlan 20
exit
exit
sh vlan-sw
```
![elementos](https://github.com/MarvEdCV/Redes-1-Proyecto-1-G11/blob/main/Img/T1_14.jpg)

---
# Topología 3

![](/Img/Topo.png)

| --- | --- | --- | --- | --- |

## Configuración clientes

### ESW8

Configuración vtp

```bash
conf t
vtp domain Grupo11
vtp password Grupo11
vtp version 2
vtp mode client
exit
sh vtp st
```

![](/Img/TP3_0.png)

Configuración modo troncal

```bash
conf t
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```

![](/Img/TP3_1.png)

Configuración modo de acceso

```bash
conf t
int f1/0
switchport mode access
switchport access vlan 40
exit
exit
sh vlan-sw
```

### ESW9

Configuración vtp

```bash
conf t
vtp domain Grupo11
vtp password Grupo11
vtp version 2
vtp mode client
exit
sh vtp st
```

Configuración modo troncal

```bash
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr
```

Configuración modo de acceso

```bash
conf t
int f1/3
switchport mode access
switchport access vlan 30
exit
exit
sh vlan-sw
```

### ESW10

Configuración vtp

```bash
conf t
vtp domain Grupo11
vtp password Grupo11
vtp version 2
vtp mode client
exit
sh vtp st
```

Configuración modo troncal

```bash
conf t
int f1/0
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr

```

Configuración modo de acceso

```bash
conf t
int f1/1
switchport mode access
switchport access vlan 10
exit
exit
sh vlan-sw
```

### ESW11

Configuración vtp

```bash
conf t
vtp domain Grupo11
vtp password Grupo11
vtp version 2
vtp mode client
exit
sh vtp st
```

Configuración modo troncal

```bash
conf t
int f1/1
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

int f1/2
switchport mode trunk
switchport trunk allowed vlan 1,10,20,30,40,1002-1005
exit

exit
write
sh int tr

```

Configuración modo de acceso

```bash
conf t
int f1/0
switchport mode access
switchport access vlan 20
exit
exit
sh vlan-sw
```

## **Configuración de conexión con Topología 2**

![](/Img/config_tpl2.png)
---

