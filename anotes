// SEGURIDAD BÁSICA   ---------------------------------
ENABLE
CONF T
USERNAME NEY SECRET upc123
enable secret upc321
line console 0
login local
exit
line vty 0 15
login local
exit
banner motd % *** Solo personal AUTORIZADO, accede al dispositivo*** %
service password-encryption
no ip domain-lookup
----------------------------------------------------------
CREAR VLANs: S1 - S6

VLAN 21
NAME ADMINISTRACION
VLAN 22
NAME VENTAS
VLAN 23
NAME LOGISTICA
VLAN 24
NAME FINANZAS
VLAN 25
NAME WIFI-CLIENTES
VLAN 26
NAME MARKETING
VLAN 27
NAME WIFI-EJECUTIVO
VLAN 28
NAME SERVIDORES
VLAN 99
NAME NATIVE

-> show vlan brief

----------------------------------------------------------
ASIGNAR VLANS A LOS PUERTOS
_______________
INTERFACE RANGE F0/1 - 24
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 21

INTERFACE RANGE F0/1 - 4
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 21
INTERFACE RANGE F0/5 - 24
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 22

INTERFACE RANGE F0/1 - 13
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 26
INTERFACE RANGE F0/14 - 24
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 28

INTERFACE RANGE F0/1 - 15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 24

INTERFACE RANGE F0/1 - 15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 23

INTERFACE RANGE F0/1 - 10
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 27
INTERFACE RANGE F0/11 - 23
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS VLAN 25

-------------------------------------------------------------

show vlan brief
-------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

CONFIGURAR TRUNKING: en cada SWM
___________________
interface range g1/0/1 - 7
switchport mode trunk
switchport trunk native vlan 99

interface g0/1
switchport mode trunk
switchport trunk native vlan 99
---------------------------------------------------------------------------------------------------

SVI  ASIGNAR IP A LOS SWITC   //QUEDAMOS
___S1
INTERFACE VLAN 99
IP ADDRESS 10.12.16.200 255.255.255.240
DESCRIPTION VLAN99 PREDETERMINADA
NO SHUTDOWN
IP DEFAULT-GATEWAY 10.12.16.193


ESTA ES PARA ELIMINAR IP DE CADA SWTICH
no interface vlan 15
no interface vlan 17
no interface vlan 18
___S2
SUSECCIVAMENTE

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
ROUTER

interface g0/1
no ip address
no shutdown
exit
interface g0/1.21
ENCAPSULATION DOT1Q 21
IP ADDRESS 10.12.16.1 255.255.255.224
interface g0/1.22
ENCAPSULATION DOT1Q 22
IP ADDRESS 10.12.16.33 255.255.255.224
interface g0/1.23
ENCAPSULATION DOT1Q 23
IP ADDRESS 10.12.16.65 255.255.255.224
interface g0/1.24
ENCAPSULATION DOT1Q 24
IP ADDRESS 10.12.16.97 255.255.255.224
interface g0/1.25
ENCAPSULATION DOT1Q 25
IP ADDRESS 10.12.16.129 255.255.255.240
interface g0/1.26
ENCAPSULATION DOT1Q 26
IP ADDRESS 10.12.16.145 255.255.255.240
interface g0/1.27
ENCAPSULATION DOT1Q 27
IP ADDRESS 10.12.16.161 255.255.255.240
interface g0/1.28
ENCAPSULATION DOT1Q 28
IP ADDRESS 10.12.16.177 255.255.255.240
interface g0/1.99
 encapsulation dot1q 99 native
 ip address 10.12.16.193 255.255.255.240
-------------------------------------------------------

EN MISMO ROUTER (es exclusivo para switch=) XD

interface g0/0
switchport mode trunk
switchport trunk native vlan 99

interface g0/1
switchport mode trunk
switchport trunk native vlan 99

-------------------------------------------------------

tips para tu proyecto:
SWM:
interface range g1/0/1
switchport trunk encapsulation dot1q 
switchport mode trunk
switchport trunk native vlan 99

interface range GigabitEthernet1/0/1
 switchport trunk native vlan 99
 switchport mode trunk

-------
interface Gig0/1
switchport mode trunk
switchport trunk native vlan 99
