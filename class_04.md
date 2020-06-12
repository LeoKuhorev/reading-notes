## LINKED LISTS

_**Linked List**_- A data structure that contains nodes that links/points to the next node in the list.

**_Singly_** - Singly refers to the number of references the node has. A Singly linked list means that there is only one reference, and the reference points to the Next node in a linked list.

**_Doubly_** - Doubly refers to there being two (double) references within the node. A Doubly linked list means that there is a reference to both the Next and Previous node

**_Node_** - Nodes are the individual items/links that live in a linked list. Each node contains the data for each link.

**_Next_** - Each node contains a property called Next. This property contains the reference to the next node.
Head - The Head is a reference type of type Node to the first node in a linked list.

**_Current_** - The Current reference is a reference type of type Node that is currently being looked at. This node is traditionally used when traversing through a full linked list. When traversing, you typically reset the current to the head to guarantee you are starting from the beginning of the linked list.

The fundamental difference between _arrays_ and _linked lists_ is that arrays are static data structures, while linked lists are dynamic data structures (A static data structure needs all of its resources to be allocated when the structure is created)

<img src="./assets/ll_memory.jpeg" style="width:80%">

## Complexities

| Data Structure     | Access | Search | Insertion | Deletion |
| ------------------ | ------ | ------ | --------- | -------- |
| Array              | Θ(1)   | Θ(n)   | Θ(n)      | Θ(n)     |
| Singly-Linked List | Θ(n)   | Θ(n)   | Θ(1)      | Θ(1)     |
| Doubly-Linked List | Θ(n)   | Θ(n)   | Θ(1)      | Θ(1)     |

[Go back](./README.md)
