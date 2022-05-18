# Implementación de la lista enlazada circular
La implementación de una [[Lista enlazada#Lista enlazada circular|lista enlazada circular]] en lenguaje de programación Python se vería de la siguiente manera:

	class Node:
	    def __init__(self, data):
	        self.data = data
	        self.next = None
	
	    def getData(self):
	        return self.data
	
	    def getNext(self):
	        return self.next
	
	    def getPrev(self):
	        return self.prev
	
	class RoundLinkedList:
	
	    def __init__(self, data: int):
	        self.head = Node(data)
	        self.tail = self.head
	        self.head.next = self.tail
	
	  
	
	    def __init__(self, data: list):
	        self.head = Node(data[0])
	        self.tail = self.head
	        self.head.next = self.tail
	        for i in data[1:]:
	            self.addNode(i)
	
	    def addNode(self, data):
	        newData = Node(data)
	        self.tail.next = newData
	        self.tail = newData
	        self.tail.next = self.head
	  
	    def printList(self):
	        current = self.head
	        while current.next != self.head:
	            print(current.getData(), end='->')
	            current = current.getNext()
	        print(current.getData())