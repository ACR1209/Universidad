# Modelo OSI ISO
Inicialmente, el modelo OSI (*Open System Interconnection*) fue diseñado por la ISO (*International Standarizing Organization*) para proporcionar un marco sobre el cual crear una suite de protocolos se utilizara para desarrollar una red internacional que no dependiera de sistemas exclusivos. Proporciona una amplia lista de funciones y servicios que se pueden presenta en cada capa. Tiene 7 capas, véase [[OSI]]. 

## Capas
### Capa 1: Fisica
Vemos cosas como los niveles de voltaje, los conectores físicos, los tiempos, tasa de datos, ergo todo lo físico.

### Capa 2: Enlace de datos
Esta capa asegura que los datos estén formateados de la forma correcta, se encarga de la detección de errores y se asegura de que los datos se entreguen de manera confiable. En esta capa vive [[Ethernet]], tanto las direcciones MAC como los tramas Ethernet están en la capa de enlace de datos. 

### Capa 3:  Red
Tanto IPv4 como IPv6 están en esta capa, que se encarga de la conectividad y la selección de la mejor ruta. Todos los dispositivos conectados a la red necesita una dirección [[Quinto Semestre/Redes de Computadoras/Terminología Redes/IP|IP]] única.

### Capa 4: Transporte
Esta capa se encarga del transporte de segmentos de redes entre los dispositivos de red. En esta capa tenemos los siguientes protocolos:
- TCP (*Transmission Control Protocol*): Protocolo que envía de forma confiable los datos.
- UDP (*User Datagram Protocol*): Protocolo que no envía de forma confiable los datos.

### Capa 5: Sesión
Se encarga de establecer, gestionar y finalizar las sesiones entre dos host. Cuando navegas por un sitio web en Internet, probablemente no sea el único usuario del servidor web que aloja un sitio web. Este servidor necesita seguir cada "sesión" en este.

### Capa 6: Presentación
Se asegura de que la información sea legible para la capa de aplicación formateando y estructurando los datos. La mayoría de las computadoras usan la tabla ASCII para los caracteres. Si otra computadora utilizara otros caracteres como EBCDIC, entonces la capa de presentación necesita "reformatear" los datos para que ambas computadoras coincidan en los mismos caracteres.

### Capa 7: Aplicación
Tenemos aplicaciones como el correo electrónico, browsing, http, ftp y más. Para enviar datos a través de la red, siempre debemos pasar por todas las capas, una a una, sin saltarnos ninguna.