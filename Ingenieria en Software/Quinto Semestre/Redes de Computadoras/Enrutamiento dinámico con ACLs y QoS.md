# Enrutamiento dinámico con ACLs y QoS

## Preparación de la red

### Subneteo

### Topología
Se va a realizar la topología propuesta utilizando las redes obtenidas luego de subnetear para los hosts solicitados

![[Pasted image 20220828151730.png]]

## Configuración de los dispositivos

Se empezará configurando los routers respectivos de forma que se obtenga los DHCP solicitados así como el protocolo de enrutamiento OSPF en cada uno

### Router0 (RT-0)
```
Router>enable
Router#configure terminal
Router(config)#hostname RT-0
RT-0(config)#banner motd 'NO INGRESAR'
RT-0(config)#enable secret enable
RT-0(config)#service password-encryption
RT-0(config)#line console 0
RT-0(config-line)#password console
RT-0(config-line)#login
RT-0(config-line)#exit
RT-0(config)#line vty 0 15
RT-0(config-line)#password vty
RT-0(config-line)#login
RT-0(config-line)#exit
RT-0(config)#line aux 0
RT-0(config-line)#password aux
RT-0(config-line)#login
RT-0(config-line)#exit
RT-0(config)#interface Gig0/1
RT-0(config-if)#no shutdown

RT-0(config-if)#interface Gig0/1.30
RT-0(config-subif)#encapsulation dot1q 30
RT-0(config-subif)#ip add 172.20.8.1 255.255.252.0
RT-0(config-subif)#exit
RT-0(config)#interface Gig0/1.40
RT-0(config-subif)#encapsulation dot1q 40
RT-0(config-subif)#ip add 172.20.12.1 255.255.254.0
RT-0(config-subif)#exit
RT-0(config)#do wr

RT-0(config)#ip dhcp pool ADMIN
RT-0(dhcp-config)#network 172.20.12.0 255.255.254.0
RT-0(dhcp-config)#default-router 172.20.12.1
RT-0(dhcp-config)#exit
RT-0(config)#ip dhcp excluded-address 172.20.12.1 172.20.8.1
RT-0(config)#ip dhcp pool ESTUDIANTES
RT-0(dhcp-config)#network 172.20.8.0 255.255.252.0
RT-0(dhcp-config)#default-router 172.20.8.1
RT-0(dhcp-config)#exit

RT-0(config)#router ospf 1
RT-0(config-router)#router-id 3.3.3.3
RT-0(config-router)#network 172.20.12.0 0.0.1.255 area 0
RT-0(config-router)#network 172.20.8.0 0.0.3.255 area 0
RT-0(config-router)#network 172.20.14.72 0.0.0.3 area 0
RT-0(config-router)#network 172.20.14.84 0.0.0.3 area 0

RT-0(config)#int se0/0/0
RT-0(config-if)#ip add 172.20.14.74 255.255.255.252
RT-0(config-if)#no shut
RT-0(config-if)#exit
RT-0(config)#int se0/0/1
RT-0(config-if)#ip add 172.20.14.85 255.255.255.252
RT-0(config-if)#no shut


```
### Router1 (RT-1)
```
Router>enable
Router#configure terminal

Router(config)#hostname RT-1
RT-1(config)#banner motd 'NO INGRESAR'
RT-1(config)#enable secret enable
RT-1(config)#service password-encryption
RT-1(config)#line console 0
RT-1(config-line)#password console
RT-1(config-line)#login
RT-1(config-line)#exit
RT-1(config)#line vty 0 15
RT-1(config-line)#password vty
RT-1(config-line)#login
RT-1(config-line)#exit
RT-1(config)#line aux 0
RT-1(config-line)#password aux
RT-1(config-line)#login
RT-1(config-line)#exit
RT-1(config)#interface se0/0/0
RT-1(config-if)#ip add 172.20.14.78 255.255.255.252
RT-1(config-if)#no shut

RT-1(config-if)#exit
RT-1(config)#interface gig0/1
RT-1(config-if)#ip add 172.20.14.65 255.255.255.252
RT-1(config-if)#no shut

RT-1(config-if)#exit
RT-1(config)#interface se0/0/1
RT-1(config-if)#ip add 172.20.14.81 255.255.255.252
RT-1(config-if)#no shut

RT-1(config-if)#exit
RT-1(config)#router ospf 1
RT-1(config-router)#router-id 4.4.4.4
RT-1(config-router)#network 172.20.14.80 0.0.0.3 area 0
RT-1(config-router)#network 172.20.14.76 0.0.0.3 area 0
RT-1(config-router)#network 172.20.14.64 0.0.0.3 area 0
RT-1(config-router)#do wr
```
### Router2 (RT-2)
```
Router>enable
Router#configure terminal
Router(config)#hostname RT-2
RT-2(config)#banner motd 'NO INGRESAR'
RT-2(config)#enable secret enable
RT-2(config)#service password-encryption
RT-2(config)#line console 0
RT-2(config-line)#password console
RT-2(config-line)#login
RT-2(config-line)#exit
RT-2(config)#line vty 0 15
RT-2(config-line)#password vty
RT-2(config-line)#login
RT-2(config-line)#exit
RT-2(config)#line aux 0
RT-2(config-line)#password aux
RT-2(config-line)#login
RT-2(config-line)#exit
RT-2(config)#interface se0/0/0
RT-2(config-if)#ip add 172.20.14.82 255.255.255.252
RT-2(config-if)#no shut
RT-2(config-if)#exit
RT-2(config)#interface se0/1/0
RT-2(config-if)#ip add 172.20.14.89 255.255.255.252
RT-2(config-if)#no shut
RT-2(config-if)#exit
RT-2(config)#interface se0/0/1
RT-2(config-if)#ip add 172.20.14.86 255.255.255.252
RT-2(config-if)#no shut
RT-2(config-if)#exit
RT-2(config)#router ospf 1
RT-2(config-router)#network 172.20.14.84 0.0.0.3 area 0
RT-2(config-router)#network 172.20.14.80 0.0.0.3 area 0
RT-2(config-router)#network 172.20.14.88 0.0.0.3 area 0
RT-2(config-router)#router-id 5.5.5.5
RT-2(config-router)#do wr
```
### Router3 (RT-3)
```
Router(config)#hostname RT-3
RT-3(config)#banner motd 'NO INGRESAR'
RT-3(config)#enable secret enable
RT-3(config)#service password-encryption
RT-3(config)#line console 0
RT-3(config-line)#password console
RT-3(config-line)#login
RT-3(config-line)#exit
RT-3(config)#line vty 0 15
RT-3(config-line)#password vty
RT-3(config-line)#login
RT-3(config-line)#exit
RT-3(config)#line aux 0
RT-3(config-line)#password aux
RT-3(config-line)#login
RT-3(config-line)#exit
RT-3(config)#interface se0/0/0
RT-3(config-if)#ip add 172.20.14.70 255.255.255.252
RT-3(config-if)#no shut
RT-3(config-if)#exit
RT-3(config)#interface se0/1/0
RT-3(config-if)#ip add 172.20.14.77 255.255.255.252
RT-3(config-if)#no shut
RT-3(config-if)#exit
RT-3(config)#interface se0/1/1
RT-3(config-if)#ip add 172.20.14.73 255.255.255.252
RT-3(config-if)#no shut
RT-3(config-if)#exit
RT-3(config)#router ospf 1
RT-3(config-router)#network 172.20.14.68 0.0.0.3 area 0
RT-3(config-router)#network 172.20.14.72 0.0.0.3 area 0
RT-3(config-router)#network 172.20.14.76 0.0.0.3 area 0
RT-4(config-router)#router-id 1.1.1.1
RT-3(config-router)#do wr
```
### Router4 (RT-4)
```
Router>enable
Router#configure terminal
Router(config)#hostname RT-4
RT-4(config)#banner motd 'NO INGRESAR'
RT-4(config)#enable secret enable
RT-4(config)#service password-encryption
RT-4(config)#line console 0
RT-4(config-line)#password console
RT-4(config-line)#login
RT-4(config-line)#exit
RT-4(config)#line vty 0 15
RT-4(config-line)#password vty
RT-4(config-line)#login
RT-4(config-line)#exit
RT-4(config)#line aux 0
RT-4(config-line)#password aux
RT-4(config-line)#login
RT-4(config-line)#exit
RT-4(config)#interface Gig0/1
RT-4(config-if)#no shutdown
RT-4(config-if)#interface Gig0/1.10
RT-4(config-subif)#encapsulation dot1q 10
RT-4(config-subif)#ip add 172.20.4.1 255.255.252.0
RT-4(config-subif)#exit
RT-4(config)#interface Gig0/1.20
RT-4(config-subif)#encapsulation dot1q 20
RT-4(config-subif)#ip add 172.20.0.1 255.255.252.0
RT-4(config-subif)#exit
RT-4(config)#do wr

RT-4(config)#ip dhcp pool DCCO
RT-4(dhcp-config)#network 172.20.4.0 255.255.252.0
RT-4(dhcp-config)#default-router 172.20.4.1
RT-4(dhcp-config)#exit
RT-4(config)#ip dhcp excluded-address 172.20.4.1
RT-4(config)#ip dhcp pool DOCENTES
RT-4(dhcp-config)#network 172.20.0.0 255.255.252.0
RT-4(dhcp-config)#default-router 172.20.0.1
RT-4(dhcp-config)#exit
RT-4(config)#ip dhcp excluded-address 172.20.0.1
RT-4(config)#do wr


RT-4(config)#int se0/0/0
RT-4(config-if)#ip add 172.20.14.69 255.255.255.252
RT-4(config-if)# no shut
RT-4(config-if)#exit
RT-4(config)#router ospf 1
RT-4(config-router)#network 172.20.4.0 0.0.3.255 area 0
RT-4(config-router)#network 172.20.0.0 0.0.3.255 area 0
RT-4(config-router)#network 172.20.14.68 0.0.0.3 area 0
RT-4(config-router)#router-id 1.1.1.1
```
### Router5 (RT-5)
```
Router>enable
Router#configure terminal
Router(config)#hostname RT-5
RT-5(config)#banner motd 'NO INGRESAR'
RT-5(config)#enable secret enable
RT-5(config)#service password-encryption
RT-5(config)#line console 0
RT-5(config-line)#password console
RT-5(config-line)#login
RT-5(config-line)#exit
RT-5(config)#line vty 0 15
RT-5(config-line)#password vty
RT-5(config-line)#login
RT-5(config-line)#exit
RT-5(config)#line aux 0
RT-5(config-line)#password aux
RT-5(config-line)#login
RT-5(config-line)#exit
RT-5(config)#interface Gig0/1
RT-5(config-if)#ip add 172.20.14.1 255.255.255.192
RT-5(config-if)#no shutdown
RT-5(config-if)#exit
RT-5(config)#do wr

RT-5(config)#ip dhcp pool LAN1
RT-5(dhcp-config)#network 172.20.14.0 255.255.255.192
RT-5(dhcp-config)#default-router 172.20.14.1
RT-5(dhcp-config)#exit
RT-5(config)#ip dhcp excluded-address 172.20.14.1
RT-5(config)#do wr

RT-5(config)#int se0/0/0
RT-5(config-if)#ip add 172.20.14.90 255.255.255.252
RT-5(config-if)#no shut
RT-5(config-if)#exit
RT-5(config)#router ospf 1
RT-5(config-router)#network 172.20.14.88 0.0.0.3 area 0
RT-5(config-router)#router-id 6.6.6.6pp
RT-5(config-router)#network 172.20.14.0 0.0.0.63 area 0
RT-5(config-router)#exit
RT-5(config)#do wr

```

De igual forma configuramos los switchs realizando las vlans

### Switch0 (SW-0)
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname SW-0
SW-0(config)#banner motd 'NO INGRESAR'
SW-0(config)#enable secret enable
SW-0(config)#service password-encryption
SW-0(config)#line console 0
SW-0(config-line)#password console
SW-0(config-line)#login
SW-0(config-line)#exit
SW-0(config)#line vty 0 15
SW-0(config-line)#password vty
SW-0(config-line)#login
SW-0(config-line)#exit
SW-0(config)#vlan 10
SW-0(config-vlan)#name DCCO
SW-0(config-vlan)#exit
SW-0(config)#vlan 20
SW-0(config-vlan)#name DOCENTES
SW-0(config-vlan)#exit
SW-0(config)#vlan 30
SW-0(config-vlan)#name ADMIN
SW-0(config-vlan)#exit
SW-0(config)#vlan 40
SW-0(config-vlan)#name ESTUDIANTES
SW-0(config-vlan)#exit
SW-0(config)#interface range fa0/1-10
SW-0(config-if-range)#switchport mode access
SW-0(config-if-range)#switchport access vlan 10
SW-0(config-if-range)#exit
SW-0(config)#interface range fa0/11-20
SW-0(config-if-range)#switchport mode access
SW-0(config-if-range)#switchport access vlan 20
SW-0(config-if-range)#exit
SW-0(config)#interface range gig0/1
SW-0(config-if-range)#switchport mode trunk
SW-0(config-if-range)#exit
SW-0(config)#int vlan 30
SW-0(config-if)#ip address 172.20.12.20 255.255.254.0
SW-0(config-if)#no shutdown
SW-0(config-if)#exit
SW-0(config)#ip domain-name test.com
SW-0(config)#crypto key generate rsa general-keys modulus 2048
SW-0(config)#username andres secret H400
SW-0(config)#line vty 0 15
SW-0(config-line)#transport input ssh
SW-0(config-line)#login local
SW-0(config-line)#no password vty
SW-0(config-line)#exit
SW-0(config)#do wr
```

### Switch1 (SW-1)
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname SW-1
SW-1(config)#banner motd 'NO INGRESAR'
SW-1(config)#enable secret enable
SW-1(config)#service password-encryption
SW-1(config)#line console 0
SW-1(config-line)#password console
SW-1(config-line)#login
SW-1(config-line)#exit
SW-1(config)#line vty 0 15
SW-1(config-line)#password vty
SW-1(config-line)#login
SW-1(config-line)#exit
SW-1(config)#vlan 10
SW-1(config-vlan)#name DCCO
SW-1(config-vlan)#exit
SW-1(config)#vlan 20
SW-1(config-vlan)#name DOCENTES
SW-1(config-vlan)#exit
SW-1(config)#vlan 30
SW-1(config-vlan)#name ADMIN
SW-1(config-vlan)#exit
SW-1(config)#vlan 40
SW-1(config-vlan)#name ESTUDIANTES
SW-1(config-vlan)#exit
SW-1(config)#interface range fa0/1-10
SW-1(config-if-range)#switchport mode access
SW-1(config-if-range)#switchport access vlan 30
SW-1(config-if-range)#exit
SW-1(config)#interface range fa0/11-20
SW-1(config-if-range)#switchport mode access
SW-1(config-if-range)#switchport access vlan 40
SW-1(config-if-range)#exit
SW-1(config)#interface range gig0/1
SW-1(config-if-range)#switchport mode trunk
SW-1(config-if-range)#exit
SW-1(config)#int vlan 30
SW-1(config-if)#ip address 172.20.12.21 255.255.254.0
SW-1(config-if)#no shutdown
SW-1(config-if)#exit
SW-1(config)#ip domain-name test.com
SW-1(config)#crypto key generate rsa general-keys modulus 2048
SW-1(config)#username andres secret H400
SW-1(config)#line vty 0 15
SW-1(config-line)#transport input ssh
SW-1(config-line)#login local
SW-1(config-line)#no password vty
SW-1(config-line)#exit
SW-1(config)#do wr

```

### Switch2 (SW-2)
```
Switch>enable
Switch#configure terminal
Switch(config)#hostname SW-2
SW-2(config)#banner motd 'NO INGRESAR'
SW-2(config)#enable secret enable
SW-2(config)#service password-encryption
SW-2(config)#line console 0
SW-2(config-line)#password console
SW-2(config-line)#login
SW-2(config-line)#exit
SW-2(config)#line vty 0 15
SW-2(config-line)#password vty
SW-2(config-line)#login
SW-2(config-line)#exit
SW-2(config)#vlan 10
SW-2(config-vlan)#name DCCO
SW-2(config-vlan)#exit
SW-2(config)#vlan 20
SW-2(config-vlan)#name DOCENTES
SW-2(config-vlan)#exit
SW-2(config)#vlan 30
SW-2(config-vlan)#name ADMIN
SW-2(config-vlan)#exit
SW-2(config)#vlan 40
SW-2(config-vlan)#name ESTUDIANTES
SW-2(config-vlan)#exit
SW-2(config)#interface range gig0/1
SW-2(config-if-range)#switchport mode trunk
SW-2(config-if-range)#exit
SW-2(config)#int vlan 30
SW-2(config-if)#ip address 172.20.12.22 255.255.254.0
SW-2(config-if)#no shutdown
SW-2(config-if)#exit
SW-2(config)#ip domain-name test.com
SW-2(config)#crypto key generate rsa general-keys modulus 2048
SW-2(config)#username andres secret H400
SW-2(config)#line vty 0 15
SW-2(config-line)#transport input ssh
SW-2(config-line)#login local
SW-2(config-line)#no password vty
SW-2(config-line)#exit
SW-2(config)#do wr

```

Ahora se configurará las ACL en los routers RT-0 y RT-1 de tal forma que el RT-0 no permita realizar ping a la VLAN 30 desde cualquier red y que el RT-1 no permita conectarse al servidor web desde la LAN

### RT-0
```
RT-0(config)#ip access-list extended blockPingAny
RT-0(config-ext-nacl)#deny icmp any 172.20.12.0 0.0.1.255 echo 
RT-0(config-ext-nacl)#permit ip any any
RT-0(config-ext-nacl)#exit
RT-0(config)#int se0/0/1
RT-0(config-if)#ip access-group blockPingAny in
RT-0(config-if)#exit
RT-0(config)#int se0/0/0
RT-0(config-if)#ip access-group blockPingAny in
RT-0(config-if)#exit
RT-0(config)#int gig0/1.40
RT-0(config-subif)#ip access-group blockPingAny in
RT-0(config-subif)#exit
RT-0(config)#do wr
```

### RT-1
```
RT-1(config)#ip access-list extended test
RT-1(config-ext-nacl)#deny tcp 172.20.14.0 0.0.0.63 172.20.14.67 0.0.0.3 eq www
RT-1(config-ext-nacl)#permit ip any any
RT-1(config-ext-nacl)#exit
RT-1(config)#int se0/0/1
RT-1(config-if)#ip access-group test in
RT-1(config-if)#exit
RT-1(config)#int se0/0/0
RT-1(config-if)#ip access-group test in
RT-1(config-if)#exit
RT-1(config)#int gig0/1
RT-1(config-if)#ip access-group test in
RT-1(config-if)#exit
```