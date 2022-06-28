# Implementación de la lista doblemente enlazada
La implementación de una [[Lista enlazada#Lista doblemente enlazada|lista doblemente enlazada]] en lenguaje de programación Python se vería de la siguiente manera:

	class Node:
	    def __init__(self, data):
	        self.data = data
	        self.prev = None
	        self.next = None
	
	    def getData(self):
	        return self.data
	
	    def getNext(self):
	        return self.next
	
	    def getPrev(self):
	        return self.prev
	
	class DoublyLinkedList:
	    def __init__(self, data:int):
	        self.head = Node(data)
	        self.tail = self.head
	
	    def __init__(self, data:list):
	        self.head = Node(data[0])
	        self.tail = self.head
	        for i in data[1:]:
	            self.addNode(i)
	
	    def addNode(self, data):
	        newData = Node(data)
	        self.tail.next = newData
	        newData.prev = self.tail
	        self.tail = newData
	
	    def printList(self):
	        current = self.head
	        while current:
	            print(current.getData(), end="->")
	            current = current.getNext()