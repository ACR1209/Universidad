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

>[!NOTE]
>Se debe agregar a los router (en este caso el 1941) el módulo HWIC-2T para poder utilizar los puertos serial, como se muestra en la imagen de abajo 
>
>![[Pasted image 20220811095040.png]]