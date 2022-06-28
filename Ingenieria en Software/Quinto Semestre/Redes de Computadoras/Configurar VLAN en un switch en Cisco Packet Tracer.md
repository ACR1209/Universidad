# Configurar VLAN en un switch en Cisco Packet Tracer

Después de haber realizado la [[Configuración inicial de un switch en Cisco Packet Tracer]] vamos a configurar las [[VLAN]] de la siguiente manera. Empezamos creando las VLAN en este caso se va a realizar esta topología de red:

![[Pasted image 20220627203016.png]]

Creamos las 2 VLAN usando *name* para darles nombres personalizados:

```
	SW-1#configure terminal
	SW-1(config)#vlan 10
	SW-1(config-vlan)#name SALES
	SW-1(config-vlan)#exit
	SW-1(config)#vlan 20
	SW-1(config-vlan)#name IT
	SW-1(config-vlan)#exit
	SW-1(config)#
```

Asignamos puertos de acceso a las VLAN a las cuales se van a conectar:

```
	SW-1#config t
	SW-1(config)#interface FastEthernet0/1
	SW-1(config-if)#switchport mode access
	SW-1(config-if)#switchport access vlan 10
	SW-1(config-if)#exit
	SW-1(config)#
	//Se hace esto con todos los puertos a los que se les quiera asignar a una VLAN
```

>[!INFO]
> Se puede evitar realizar la configuración por puerto y en lugar hacer la configuración en un rango de puertos, de la siguiente manera:
> ```
> 	SW-1(config)#interface range FastEthernet0/1-2
> 	SW-1(config-if-range)#switchport mode access
> 	SW-1(config-if-range)#switchport access vlan 10
> 	SW-1(config-if-range)#exit
> 	SW-1(config)#interface range FastEthernet0/3-4
> 	SW-1(config-if-range)#switchport mode access
> 	SW-1(config-if-range)#switchport access vlan 20
> 	SW-1(config-if-range)#exit
> 	SW-1(config)#
> ```
> 

Se asigna el puerto troncal para poder tener comunicación entre las diferentes VLAN:

```
	SW-1(config)#interface FastEthernet0/5
	SW-1(config-if)#switchport mode trunk
```


A partir de aquí se configuran las IP de las PC para que se conecten a sus respectivas VLAN (Luego de guardar la configuración):

| PC | Dirección IP | Máscara de subred | Default Gateway |
| - | - | - | - |
| 1 | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| 2 | 192.168.1.20 | 255.255.255.0 | 192.168.1.1 |
| 3 | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |
| 4 | 192.168.2.20 | 255.255.255.0 | 192.168.2.1 |

![[Pasted image 20220627205144.png]]

Para poder tener comunicación entre VLAN debemos de configurar el Router de la siguiente manera:

```
	Router>enable
	Router#configure terminal
	Router(config)#interface FastEthernet0/0
	Router(config-if)#no shutdown
	
	Router(config-if)#
	%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
	
	Router(config-if)#interface FastEthernet0/0.10
	Router(config-subif)#
	%LINK-5-CHANGED: Interface FastEthernet0/0.10, changed state to up
	
	Router(config-subif)#enc
	Router(config-subif)#encapsulation dot1q 10
	Router(config-subif)#ip add 192.168.1.1 255.255.255.0
	Router(config-subif)#interface FastEthernet0/0.20
	Router(config-subif)#
	%LINK-5-CHANGED: Interface FastEthernet0/0.20, changed state to up
	
	Router(config-subif)#encapsulation dot1q 20
	Router(config-subif)#ip add 192.168.2.1 255.255.255.0
	Router(config-subif)#exit
	Router(config)#exit
	Router#copy running-config startup-config
	Router#exit
```

Al hacer esto podremos hacer comunicaciones inter-VLAN en inter-Host en cada VLAN.