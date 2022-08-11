# Enrutamiento estático básico en Packet Tracer

El proceso de enrutamiento no es más que el proceso de escoger una ruta en la cual vamos a enviar los paquetes. El enrutamiento es necesario cuando se quiere entregar paquetes a una red que no esta directamente conectada con el emisor.

## Tipos de enrutamiento en Packet Tracer
### Configuración básica 
```
Router(config)# interface interfaz-serial
Router(config-if)# ip address ip-interfaz snm-interfaz
Router(config-if)# clock rate velocidad-reloj
Router(config-if)# no shutdown
```
### Configuración de rutas estáticas
#### Configurar una ruta estática recursiva
```
Router(config)# ip route ip-red-objetivo snm-red-objetivo ip-puerto-acceso
Router(config)# ip route 192.168.1.0 255.255.255.0 10.1.1.2
```
#### Configurar una ruta estática directamente conectada
```
Router(config)# ip route ip-red-objetivo snm-red-objetivo puerto-acceso
Router(config)# ip route 192.168.0.0 255.255.255.0 s0/0/0
```

## Ejemplo
Realizaremos la siguiente topología básica que nos permite entender los fundamentos básicos de enrutamiento: 

![[Pasted image 20220811100547.png]]

>[!INFO]- Configuración extra a tomar en cuenta en la topología
>Se debe agregar a los router (en este caso el 1941) el módulo HWIC-2T para poder utilizar los puertos serial, como se muestra en la imagen de abajo 
>
>![[Pasted image 20220811095040.png]]
>
>De igual forma, es necesario configurar los computadores con sus respectivos gateway, de la siguiente manera
>
>![[Pasted image 20220811111026.png]]


Empezaremos realizando la [[#Configuración básica|configuración básica]] de los router donde se conecta el cable serial DCE (es decir en aquellos donde encontramos el reloj), es decir le asignamos las ips a las salidas del router, de la siguiente manera:

## Router0 (R0)
```
Router>enable
Router#config t
Router(config)#hostname R0
R0(config)#int se0/0/0
R0(config-if)#ip add 10.1.1.1 255.255.255.252
R0(config-if)#clock rate 128000
R0(config-if)#no shut
%LINK-5-CHANGED: Interface Serial0/0/0, changed state to down
R0(config-if)#exit
R0(config)#int gig0/1
R0(config-if)#ip add 192.168.0.1 255.255.255.0
R0(config-if)#no shut
R0(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
```

## Router1 (R1) 
```
Router>enable
Router#config t
Router(config)#hostname R1
R1(config)#int se0/1/0
R1(config-if)#ip add 10.1.1.5 255.255.255.252
R1(config-if)#clock rate 128000
R1(config-if)#no shut
%LINK-5-CHANGED: Interface Serial0/1/0, changed state to down
R1(config-if)#exit
R1(config)#int se0/0/1
R1(config-if)#ip add 10.1.1.2 255.255.255.252
R1(config-if)#no shut
%LINK-5-CHANGED: Interface Serial0/0/1, changed state to up
R1(config-if)#exit
R1(config)#int gig0/1
R1(config-if)#ip add 192.168.1.1 255.255.255.0
R1(config-if)#no shut
R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
```

## Router2 (R2)
```
Router>enable
Router#config t
Router(config)#hostname R2
R2(config)#int gi0/1
R2(config-if)#ip add 192.168.2.1 255.255.255.0
R2(config-if)#no shut
R2(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
R2(config-if)#exit
R2(config)#int se0/1/1
R2(config-if)#ip add 10.1.1.6 255.255.255.252
R2(config-if)#no shut 
R2(config-if)#
%LINK-5-CHANGED: Interface Serial0/1/1, changed state to up
R2(config-if)#exit
R2(config)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial0/1/1, changed state to up
```

A partir de este punto nos encargaremos de realizar el enrutamiento como tal, donde básicamente le estamos diciendo a los paquetes a donde ir, se puede entender como las señales de tránsito que se encuentran en las autopistas que indican a donde se debe ir para llegar a un destino. 

![[Pasted image 20220811105142.png]]

Ahora configuremos estas "señales de tránsito" en packet tracer:

## R0
```
R0(config)#ip route 192.168.1.0 255.255.255.0 se0/0/0
%Default route without gateway, if not a point-to-point interface, may impact performance
R0(config)#ip route 10.1.1.4 255.255.255.252 se0/0/0
%Default route without gateway, if not a point-to-point interface, may impact performance
R0(config)#ip route 192.168.2.0 255.255.255.0 se0/0/0
%Default route without gateway, if not a point-to-point interface, may impact performance
```
## R1
```
R1(config)#ip route 192.168.0.0 255.255.255.0 se0/0/1
%Default route without gateway, if not a point-to-point interface, may impact performance
R1(config)#ip route 192.168.2.0 255.255.255.0 se0/1/0
%Default route without gateway, if not a point-to-point interface, may impact performance
```
## R2
```
R2(config)#ip route 0.0.0.0 0.0.0.0 se0/1/1
%Default route without gateway, if not a point-to-point interface, may impact performance
```

>[!INFO] Configuración de R2
>En el R2 se utilizó el gateway of last resort para redirigir cualquier paquete que se tenga que enviar desde este router R2, a la linea se0/1/1

> [!MISSING]- ¿Cuándo se utiliza una configuración de ruta estática recursiva?
> 
>Aún no tengo claro la razón por la cual se utilizaría una configuración de ruta estática recursiva sobre una ruta estática directamente conectada, a mi parecer esta distinción es arbitraria

De esta forma ya se tiene la capacidad de realizar ping entre todos los computadores de todas las redes, como se puede comprobar: 

![[Pasted image 20220811111350.png]]

Este es el ejemplo más básico de enrutamiento estático que demuestra las virtudes de este, de igual forma se puede comprobar la configuración y la conectividad en el [archivo de Packet Tracer](https://drive.google.com/file/d/1AUVCAkDeLnEhjGviBeF66aoGCY9SdSqn/view?usp=sharing)

