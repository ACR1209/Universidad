# Configuración de InterVLAN con routers y servidores web-DNS


Empezamos subneteando y realizando las conexiones pertinentes en la topología de red, así como asignando las IPs a las computadoras, routers y servidores que forman parte de la red.

![[Pasted image 20220725201944.png]]

Configuramos los Switch y el Router respectivamente:

### SW-1
```
enable
configure terminal
hostname SW-1
banner motd 'NO INGRESAR'
enable secret cisco
service password-encryption
line console 0
password DCCO
login
exit
line vty 0 15
password G401
login
exit
vlan 10
name ADMIN
exit
vlan 20
name NAME2
exit
vlan 30
name NAME3
exit
vlan 40
name NAME4
exit
vlan 50
name NAME5
exit
vlan 60
name NAME6
exit
vlan 70
name NAME7
exit
interface range fa0/1-10
switchport mode access
switchport access vlan 10
exit
interface range fa0/11-20
switchport mode access
switchport access vlan 20
exit
int vlan 10
ip address 172.20.128.10 255.255.224.0
no shutdown
exit
ip domain-name test.com
crypto key generate rsa general-keys modulus 2048
username ismael secret andres
line vty 0 15
transport input all
login local
no password G401
exit
do wr

```
### SW-2
```
enable
configure terminal
hostname SW-2
banner motd 'NO INGRESAR'
enable secret cisco
service password-encryption
line console 0
password DCCO
login
exit
line vty 0 15
password G401
login
exit
vlan 10
name ADMIN
exit
vlan 20
name NAME2
exit
vlan 30
name NAME3
exit
vlan 40
name NAME4
exit
vlan 50
name NAME5
exit
vlan 60
name NAME6
exit
vlan 70
name NAME7
exit
interface range fa0/1-10
switchport mode access
switchport access vlan 30
exit
interface range fa0/11-20
switchport mode access
switchport access vlan 40
exit
int vlan 10
ip address 172.20.128.11 255.255.224.0
no shutdown
exit
ip domain-name test.com
crypto key generate rsa general-keys modulus 2048
username ismael secret andres
line vty 0 15
transport input all
login local
no password G401
exit
do wr

```
### SW-3
```
enable
configure terminal
hostname SW-3
banner motd 'NO INGRESAR'
enable secret cisco
service password-encryption
line console 0
password DCCO
login
exit
line vty 0 15
password G401
login
exit
vlan 10
name ADMIN
exit
vlan 20
name NAME2
exit
vlan 30
name NAME3
exit
vlan 40
name NAME4
exit
vlan 50
name NAME5
exit
vlan 60
name NAME6
exit
vlan 70
name NAME7
exit
interface range fa0/1-7
switchport mode access
switchport access vlan 70
exit
interface range fa0/8-15
switchport mode access
switchport access vlan 50
exit
interface range fa0/16-23
switchport mode access
switchport access vlan 60
exit
int vlan 10
ip address 172.20.128.12 255.255.224.0
no shutdown
exit
ip domain-name test.com
crypto key generate rsa general-keys modulus 2048
username ismael secret andres
line vty 0 15
transport input all
login local
no password G401
exit
do wr

```
### SW-4
```
enable
configure terminal
hostname SW-4
banner motd 'NO INGRESAR'
enable secret cisco
service password-encryption
line console 0
password DCCO
login
exit
line vty 0 15
password G401
login
exit
vlan 10
name ADMIN
exit
vlan 20
name NAME2
exit
vlan 30
name NAME3
exit
vlan 40
name NAME4
exit
vlan 50
name NAME5
exit
vlan 60
name NAME6
exit
vlan 70
name NAME7
exit
interface range fa0/21-23
switchport mode trunk
exit
interface range gi0/1
switchport mode trunk
exit
int vlan 10
ip address 172.20.128.13 255.255.224.0
no shutdown
exit
ip domain-name test.com
crypto key generate rsa general-keys modulus 2048
username ismael secret andres
line vty 0 15
transport input all
login local
no password G401
exit
do wr

```
### RT-1
```
enable
configure terminal
hostname RT-1
banner motd 'NO INGRESAR'
enable secret cisco
service password-encryption
line console 0
password DCCO
login
exit
line vty 0 15
password G401
login
exit
line aux 0
password santiago
login
exit
interface Gig0/1
no shutdown
interface Gig0/1.10
encapsulation dot1q 10
ip add 172.20.128.1 255.255.224.0
exit
interface Gig0/1.20
encapsulation dot1q 20
ip add 172.20.0.1 255.255.192.0
exit
interface Gig0/1.30
encapsulation dot1q 30
ip add 172.20.194.129 255.255.255.192
exit
interface Gig0/1.40
encapsulation dot1q 40
ip add 172.20.64.1 255.255.192.0
exit
interface Gig0/1.50
encapsulation dot1q 50
ip add 172.20.194.1 255.255.255.128
exit
interface Gig0/1.60
encapsulation dot1q 60
ip add 172.20.192.1 255.255.254.0
exit
interface Gig0/1.70
encapsulation dot1q 70
ip add 172.20.160.1 255.255.224.0
exit
do wr

```

De esta manera ya poseemos comunicación entre las VLAN debido al routing proporcionado por  el router-on-a-stick
