
Se va a realizar la siguiente topología para poder demostrar la utilización de OSPF:

![[Pasted image 20220823074209.png]]

Para iniciar, configuramos las ip de los puertos de los routers y de las PCs:
## Router0 (R0)
```
Router>enable
Router#config t
Router(config)#hostname R0
R0(config)#int gig0/1
R0(config-if)#ip add 192.168.0.1 255.255.255.0
R0(config-if)#no shut
R0(config-if)#exit
R0(config)#int se0/0/0
R0(config-if)#ip add 10.10.1.1 255.255.255.252
R0(config-if)#no shut
R0(config-if)#exit
R0(config)#do wr
```
## Router1 (R1)
```
Router>enable
Router#config t
Router(config)#hostname R1
R1(config)#int gig0/1
R1(config-if)#ip add 192.168.1.1 255.255.255.0
R1(config-if)#no shut
R1(config-if)#exit
R1(config)#int se0/0/0
R1(config-if)#ip add 10.10.1.2 255.255.255.252
R1(config-if)#no shut
R1(config-if)#exit
R1(config)#int se0/0/1
R1(config-if)#ip add 10.10.1.5 255.255.255.252
R1(config-if)#no shut
R1(config-if)#exit
R1(config)#do wr
```
## Router2 (R2)
```
Router>enable
Router#config t
Router(config)#hostname R2
R2(config)#int se0/0/0
R2(config-if)#ip add 10.10.1.6 255.255.255.252
R2(config-if)#no shut
R2(config-if)#exit
R2(config)#int gig0/1
R2(config-if)#ip add 192.168.2.1 255.255.255.0
R2(config-if)#no shut
R2(config-if)#exit
R2(config)#do wr
```

Ahora procederemos a configurar OSPF en los routers respectivos:

>[!INFO]+ Comandos para configurar OSPF
>_router_ _ospf PROCESS_ID_ - Activa OSPF en el router 
>_network IP_ADDRESS  WILCARD_MASK  AREA_ - Agrega una red que se va a compartir, la wildcard mask es básicamente restar el valor que se tiene en la máscara de subred a 255.
## R0
```
R0(config)#router ospf 1
R0(config-router)#network 10.10.1.0 0.0.0.3 area 0
R0(config-router)#network 192.168.0.0 0.0.0.255 area 0
```
## R1
```
R1(config)#router ospf 1
R1(config-router)#network 10.10.1.0 0.0.0.3 area 0
R1(config-router)#network 192.168.1.0 0.0.0.255 area 0
R1(config-router)#network 10.10.1.4 0.0.0.3 area 1
```
## R2
```
R2(config)#router ospf 2
R2(config-router)#network 10.10.1.4 0.0.0.3 area 1
R2(config-router)#network 192.168.2.0 0.0.0.255 area 1
```

>[!INFO]+ 
> Notar que la id del proceso no tiene que ser necesariamente la misma en todos los routers, pero el area si debe serlo (o al menos con los router que sean vecinos)

De esta manera ya tenemos la posibilidad de realizar ping entre todas las redes presentes en la topología:

![[Pasted image 20220823080613.png]]

Y entre routers:

![[Pasted image 20220823081150.png]]