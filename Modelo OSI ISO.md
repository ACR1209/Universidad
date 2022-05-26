# Modelo OSI ISO
Inicialmente, el modelo OSI (*Open System Interconnection*) fue diseñado por la ISO (*International Standarizing Organization*) para proporcionar un marco sobre el cual crear una suite de protocolos se utilizara para desarrollar una red internacional que no dependiera de sistemas exclusivos. Proporciona una amplia lista de funciones y servicios que se pueden presenta en cada capa. Tiene 7 capas, véase [[OSI]]. 

## Capas
### Capa 1: Fisica
Vemos cosas como los niveles de voltaje, los conectores físicos, los tiempos, tasa de datos, ergo todo lo físico.

### Capa 2: Enlace de datos
Esta capa asegura que los datos estén formateados de la forma correcta, se encarga de la detección de errores y se asegura de que los datos se entreguen de manera confiable. En esta capa vive [[Ethernet]], tanto las direcciones MAC como los tramas Ethernet están en la capa de enlace de datos. 

### Capa 3:  Red
Tanto IPv4 como IPv6 están en esta capa, que se encarga de la conectividad y la selección de la mejor ruta. Todos los dispositivos conectados a la red necesita una dirección [[Terminología Redes/IP|IP]] única.

### Capa 4: Transporte
Esta capa se encarga del transporte de segmentos de redes entre los dispositivos de red. En esta capa tenemos los siguientes protocolos:
- TCP (*Transmission Control Protocol*): Protocolo que envía de forma confiable los datos.
- UDP (*User Datagram Protocol*): Protocolo que no envía de forma confiable los datos.

### Capa 5: Sesión
### Capa 6: Presentación
### Capa 7: Aplicación