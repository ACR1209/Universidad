# Base de datos distribuida
Esta es, una base de datos construida sobre una red de computadores. La información que estructura la base de datos esta almacenada en diferentes sitios en la red, y los diferentes sistemas de información que las utilizan accedan datos en distintas posiciones geográficas.

## Características
- Los datos deben estar físicamente en más de un ordenador, es decir, los datos se encuentran almacenados en distintas sedes.
- Las sedes deben estar interconectadas mediante una red de computadoras (cada sede será un nodo de la red). Para realizar el diseño no se tendrá en cuenta la topología, tipo y rendimiento de la red, aunque estas propiedades tengan relevancia en el buen funcionamiento del sistema.
- Los datos han de estar lógicamente integrados en una única estructura o esquema lógico global común.
- Los usuarios han de tener acceso (recuperación y actualización) a los datos pertenecientes a la BDD, ya residan éstos en la misma sede (acceso local) o en otra sede (acceso remoto).
- Cada nodo o emplazamiento facilita un entorno para la ejecución de transacciones tanto locales como globales.
- En una única operación, tanto de consulta como de actualización, se puede acceder a datos que se encuentran en más de una sede sin que el usuario sepa la distribución de los mismos en las distintas sedes. Es decir, que la distribución de la información sea transparente para el usuario.

## Tipos
- **Distribuciones homogéneas:** 
	En las bases de datos distribuidas homogéneas todos los sitios tienen idénticamente el mismo software de sistema gestor de base de datos, y son conscientes de que los demás sitios y acuerdan cooperar en el procesamiento de las solicitudes de los usuarios. En estos sistemas estos sitios renuncian a la parte de su autonomía.
	
- **Distribuciones heterogéneas:** 
	Las bases de datos distribuidas heterogéneas son sitios diferentes que pueden utilizar diferentes esquemas y diferente software de gestión de bases de datos, a diferencia en estas no son conscientes de la existencia de los demás sitios y esto nos causa que haya facilidades limitadas para la cooperación en el procesamiento de las transacciones de información en la base de datos.