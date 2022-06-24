# Particionamiento
Es el proceso de tener la [[Base de datos|base de datos]] y separarla para usar en localizaciones remotas, esto se hace para ahorrar recursos que de otra forma se malgastarían tratando de acoplar la base de datos en todas las localizaciones. Así bien, existen 2 tipos de particiones: 
- **Partición vertical**: Definir que tablas y/o que partes se van a tener en las localizaciones remotas. Esto es homologo a realizar una [[Vista|vista]].
- **Partición horizontal:** consiste en poner diferentes filas en diferentes tablas. Se diseña antes de implementarse.
	- Campo clave (No necesariamente una [[Primary Key]]): se selecciona la separación basado en un atributo determinado.
	- Rango: es seleccionar columnas basadas en cantidades de un rango a otro.
	- Tabla Hash: hacer una función que nos permita transformar los datos en una salida determinada para ver si esta cumple con una condición.
	- Lista: da una lista de valores de atributos a los cuales se quiere particionar.