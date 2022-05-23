# Topología de redes

Hace referencia a la forma en la que se conectan las computadoras para formar redes e intercambiar datos entre si. Esto puede resumirse como las maneras que se coloca el cableado para conectar las computadores y formar redes con estas. Los tipos de redes son: 

- ### Topología punto a punto (P2P)
	Es aquella a la que se conecta un dispositivo una a uno, es decir una red compuesta de dos dispositivos que se comunican entre si. Generalmente se hace en un línea dedicada.
	
- ### Topología de anillo
	Es aquella en la cual los computadores estan conectados los unos a los otros formando un circuito (en forma de anillo). Esto presenta el problema que si una de las conexiones de uno de los computadores falla los datos dejan de transferirse y comunicación se corta. Esta red se puede entender como se ve en la imagén en la parte inferior. 
		
	![[Pasted image 20220516195219.png|400]]
- ### Topología de árbol
	Es una de las topologías más simples. Es donde se encuentran nodos y estos se interconectan entre si en forma de un árbol, con una punta y una base. Este cuenta con un Backbone o conexión troncal que permite la comunicación con facilidad, si una de las "hojas" se cae no interrumpe el intercambio de información entre el resto de la red. Esta se presenta como en la imagen que se encuentra en la parte inferior.

	![[Pasted image 20220516195718.png|450]]
- ### Topología de bus
	Se basa en un cable o conexión troncal que lleva la información y los computadores se ramifican de este ( Se conocen como nodos). Su desventaja es que los datos se reparten secuencialmente hacia los nodos de red y depende de la integridad del cable central ya que si este se daña las conexiones se hacen imposibles. Esta se presenta como en la imagen que se encuentra en la parte inferior.
	
	![[Pasted image 20220516200021.png|500]]
- ### Topología de estrella
	Esta distribución consiste en un nodo central conocido como **Host** el cual envia los datos al resto de nodos que conforman la red. Esta es ampliamente usada en la actualidad debido a su simpleza y utilidad. Depende claramente del Host ya que si este se cae la red falla pero si los nodos fallan no afectan a la red. Esta se presenta como en la imagen que se encuentra en la parte inferior.
	
	![[Pasted image 20220516200407.png|400]]
- ### Topología de malla
	En esta se interconectan todas las computadoras entre si, de esta forma la información se puede transferir desde varios caminos y si uno de los nodos cae no afecta a la red. El problema es que se necesita más cable. Esta se presenta como en la imagen que se encuentra en la parte inferior. 
	
	![[Pasted image 20220516200943.png|400]]
- ### Topología híbrida
	Esta es una combinación de dos o más topologías de redes, esta nos permite adaptar la red a la necesidades del cliente. Esta nos permite adaptar y cambiar a conveniencia de las topologias utilizadas. Un ejemplo de esto se puede ver en la imagen inferior que combina la topolgía de anillo y de árbol.
	![[Pasted image 20220516201229.png|400]]
### Referencias
Beal, V. (2021). What Is Network Topology?. Recuperado de: https://www.webopedia.com/reference/network-topology/

TutorialPoint (2018). Computer Network Topologies. Recuperado de: https://www.tutorialspoint.com/data_communication_computer_network/computer_network_topologies.htm