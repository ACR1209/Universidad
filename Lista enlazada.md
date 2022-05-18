# Lista enlazada
Es una colección lineal de datos donde su orden no esta dispuesto por su posición física en la memoria, sino que un elemento contiene la posición del siguiente elemento. Esta compuesta por un conjunto de **nodos**. De su manera más simples un nodo consta de sus datos y de una referencia posteriormente (la cual apunta al siguiente nodo).  Esta estructura permite la facil inserción de valores en cualquier parte de la iteración de la lista.

## Tipos de lista enlazada
### Lista simplemente enlazada
Es la lista enlazada más sencilla que es la ya descrita donde se tiene un nodo con el dato y la dirección del siguiente nodo. Esto se puede entender con el diagrama ubicado en la parte inferior.

![[Pasted image 20220517163927.png]]

**Veáse la [[Implementación de la lista simplemente enlazada]]**

### Lista doblemente enlazada
Es la simplemente enlazada pero esta presenta un nodo con las caracteristicas de datos y la referencia al nodo anterior y siguiente. Esto se puede entender con el diagrama ubicado en la parte inferior.

![[Pasted image 20220517164441.png]]

**Veáse la [[Implementación de la lista doblemente enlazada]]**

### Lista enlazada circular
Es una lista simplemente enlazada pero donde el último nodo redirecciona al inicio de la lista enlazada. Esto se puede entender con el diagrama ubicado en la parte inferior.

![[Pasted image 20220517164451.png]]

**Veáse la [[Implementación de la lista enlazada circular]]**
