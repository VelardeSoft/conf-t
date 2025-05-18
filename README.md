# 📘 Apuntes de Configuración de Red (Emergencia)

Este archivo contiene comandos esenciales para configurar switches y routers Cisco. Útil para configuraciones de VLANs, seguridad, SVI, trunking, y subinterfaces en proyectos de redes.

---

## 🔐 Seguridad Básica

```bash
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
```

---

## 🧱 Crear VLANs (S1 - S6)

```bash
vlan 21
name ADMINISTRACION

vlan 22
name VENTAS

vlan 23
name LOGISTICA

vlan 24
name FINANZAS

vlan 25
name WIFI-CLIENTES

vlan 26
name MARKETING

vlan 27
name WIFI-EJECUTIVO

vlan 28
name SERVIDORES

vlan 99
name NATIVE
```

📄 **Verificación:**

```bash
show vlan brief
```

---

## 🧷 Asignar VLANs a Puertos

```bash
interface range f0/1 - 24
switchport mode access
switchport access vlan 21

interface range f0/1 - 4
switchport mode access
switchport access vlan 21

interface range f0/5 - 24
switchport mode access
switchport access vlan 22

interface range f0/1 - 13
switchport mode access
switchport access vlan 26

interface range f0/14 - 24
switchport mode access
switchport access vlan 28

interface range f0/1 - 15
switchport mode access
switchport access vlan 24

interface range f0/1 - 15
switchport mode access
switchport access vlan 23

interface range f0/1 - 10
switchport mode access
switchport access vlan 27

interface range f0/11 - 23
switchport mode access
switchport access vlan 25
```

📄 **Verificación:**

```bash
show vlan brief
```

---

## 🔀 Configurar Trunking en SWM

```bash
interface range g1/0/1 - 7
switchport mode trunk
switchport trunk native vlan 99

interface g0/1
switchport mode trunk
switchport trunk native vlan 99
```

---

## 🌐 SVI - Asignar IP a los Switches

### 🖥️ S1

```bash
interface vlan 99
ip address 10.12.16.200 255.255.255.240
description VLAN99 PREDETERMINADA
no shutdown

ip default-gateway 10.12.16.193
```

### ❌ Eliminar VLANs Innecesarias

```bash
no interface vlan 15
no interface vlan 17
no interface vlan 18
```

📌 Repetir configuración en S2, S3... (según sea necesario)

---

## 🚦 Configuración de Subinterfaces en el Router

```bash
interface g0/1
no ip address
no shutdown
exit

interface g0/1.21
encapsulation dot1q 21
ip address 10.12.16.1 255.255.255.224

interface g0/1.22
encapsulation dot1q 22
ip address 10.12.16.33 255.255.255.224

interface g0/1.23
encapsulation dot1q 23
ip address 10.12.16.65 255.255.255.224

interface g0/1.24
encapsulation dot1q 24
ip address 10.12.16.97 255.255.255.224

interface g0/1.25
encapsulation dot1q 25
ip address 10.12.16.129 255.255.255.240

interface g0/1.26
encapsulation dot1q 26
ip address 10.12.16.145 255.255.255.240

interface g0/1.27
encapsulation dot1q 27
ip address 10.12.16.161 255.255.255.240

interface g0/1.28
encapsulation dot1q 28
ip address 10.12.16.177 255.255.255.240

interface g0/1.99
encapsulation dot1q 99 native
ip address 10.12.16.193 255.255.255.240
```

---

## 🚧 Router Exclusivo para Switches

```bash
interface g0/0
switchport mode trunk
switchport trunk native vlan 99

interface g0/1
switchport mode trunk
switchport trunk native vlan 99
```

---

## 💡 Tips para el Proyecto

```bash
# SWM - Switch de administración o distribución

interface range g1/0/1
switchport trunk encapsulation dot1q 
switchport mode trunk
switchport trunk native vlan 99

interface range GigabitEthernet1/0/1
switchport trunk native vlan 99
switchport mode trunk

interface Gig0/1
switchport mode trunk
switchport trunk native vlan 99
```

---

## ✅ Notas Finales

- Siempre usar `show vlan brief` para verificar asignaciones en switch,s
- Asegúrate de que los enlaces troncales tengan configurada correctamente la `native vlan`.
- La `VLAN 99` sirve como VLAN nativa para gestión.
