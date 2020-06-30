## STACKS AND QUEUES

### STACK

A _**stack**_ is a data structure that consists of Nodes. Each Node references the next Node in the stack, but does not reference its previous. LIFO

`top` - This is the top of the stack;  
`push` - Nodes or items that are put into the stack are pushed O(1):

    def push(self, val):
        new_node = Node(val)
        new_node.next = self.top
        self.top = new_node

`pop` - Nodes or items that are removed from the stack are popped. When you attempt to pop an empty stack an exception will be raised O(1):

    def pop(self):
        if not self.is_empty():
            tmp = self.top
            self.top = self.top.next
            tmp.next = None
            return tmp.val
        return False / raise Exception

`peek` - When you peek you will view the value of the top Node in the stack. When you attempt to peek an empty stack an exception will be raised O(1):

    def peek(self):
        if not self.is_empty():
            return self.top.val
        return False / raise Exception

`isEmpty` - returns true when stack is empty otherwise returns false O(1):

    def is_empty(self):
        return self.top == None

### QUEUE

A _**queue**_ is a data structure that consists of Nodes. Each Node references the next Node in the queue, but does not reference its previous. FIFO

`front` - This is the front/first Node of the queue;
`rear` - This is the rear/last Node of the queue;
`enqueue` - Nodes or items that are added to the queue O(1):

    def enqueue(self, val):
        new_node = Node(val)
        self.rear.next = new_node
        self.rear = new_node

`dequeue` - Nodes or items that are removed from the queue. If called when the queue is empty an exception will be raised O(1):

    def dequeue(self):
        if not self.is_empty:
            tmp = self.front
            self.front = self.front.next
            tmp.next = None
            return tmp.val
        return False / raise Exception

`peek` - When you peek you will view the value of the front Node in the queue. If called when the queue is empty an exception will be raised O(1):

    def peek(self):
        if not self.is_empty():
            return self.front.val
        return False / raise Exception

`is_empty` - returns true when queue is empty otherwise returns false O(1):

    def is_empty(self):
        return self.front == None

## INTRO TO DATA SCIENCE

_**Data Science**_ is basically trying to make sense of data by identifying patterns, applying algorithms to extract information and predict future actions that are suitable for a specific situation.

Data --> Data Analytics --> Data Visualization --> Information

When the machine tries to identify patterns in data after rigorous training and testing and there upon gives us desired results - this is _**Machine Learning**_. Whenever there is situation when the machine needs to make decisions on its own where judgment is involved, it is called _**Artificial Intelligence**_.

[Go back](./README.md)
