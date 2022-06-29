# Configuración inicial de un switch en Cisco Packet Tracer

## Tipos de terminales
*default*: es la que viene por defecto en el switch.
*enable*: en esta se puede realizar las configuraciones

## Proceso de configuración
Empezamos colocándole el nombre al switch, utilizando los siguientes comandos:

```
	Switch>enable
	Switch#configure terminal
	Switch(config)#hostname SW-1
	SW-1(config)#
	SW-1#
```

Colocamos una contraseña y un secret en la consola, con los siguientes comandos:

```
	SW-1#configure terminal
	SW-1(config)#line console 0
	SW-1(config-line)#password password
	SW-1(config-line)#login
	SW-1(config-line)#exit
	SW-1(config)#enable secret password
```

Colocamos una contraseña de igual manera a las líneas VTY:

```
	SW-1(config)#line vty 0 15
	SW-1(config-line)#password password
	SW-1(config-line)#login
	SW-1(config-line)#exit
```

Encriptamos las contraseñas puestas:

```
	SW-1(config)#service password-encryption
```

Configuramos el MOTD:

```
	SW-1(config)#banner motd 'NO INGRESAR'
```

Guardamos la configuración realizada:

```
	SW-1#copy running-config startup-config 
	Destination filename [startup-config]? 
	Building configuration...
	[OK]
	SW-1#
```

Al reiniciar el switch tendremos que:

```
	NO INGRESAR
	
	User Access Verification
	
	Password: 
	SW-1>enable
	Password: 
	SW-1# config t
	SW-1(config)#
```
