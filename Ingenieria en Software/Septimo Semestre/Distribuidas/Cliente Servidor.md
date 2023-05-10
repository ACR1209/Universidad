Es un modelo de desarrollo de sistema donde las transacciones se dividen en procesos que cooperan entre si. 

![[Pasted image 20230510173911.png]]

## Características
- Los elementos son cliente, servidor y comunicaciones
- El cliente: presenta interface, captura datos, valida genera consultas e informes
- El servidor: devuelve resultados, maneja interbloqueos, recuperación a fallas, integridad, etc.
- El proceso cliente solicita al proceso servidor la ejecución de alguna acción.
- Los procesos pueden o no estar en una máquina física. 
- La respuesta ante una solicitud solo está a cargo del servidor de base de datos y no el cliente
- En el cliente solo se conoce la interface para comunicación con el servidor.

## Ventajas
- Aumento de la productividad.
- Menores costos de operación.
- Mejora el rendimiento de red.

## Desventajas
- Falta de control centralizado.
- Falta de seguridad.
- Sobrecarga en el cliente.




