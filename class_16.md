## Trees

### Terminology

- _**Node**_ - A node is the individual item/data that makes up the data structure
- _**Root**_ - The root is the first/top Node in the tree
- _**Left Child**_ - The node that is positioned to the left of a root or node
- _**Right Child**_ - The node that is positioned to the right of a root or node
- _**Edge**_ - The edge in a tree is the link between a parent and child node
- _**Leaf**_ - A leaf is a node that does not contain any children
- _**Height**_ - The height of a tree is determined by the number of edges from the root to the bottommost node
  ![Tree](./assets/tree.png)

### Traversals

- Depth First

  - Pre-order: root >> left >> right

        ALGORITHM preOrder(root)
        // INPUT <-- root node
        // OUTPUT <-- pre-order output of tree node's values

            OUTPUT <-- root.value

            if root.left is not Null
                preOrder(root.left)

            if root.right is not NULL
                preOrder(root.right)

  - In-order: left >> root >> right


        ALGORITHM inOrder(root)
        // INPUT <-- root node
        // OUTPUT <-- in-order output of tree node's values

            if root.left is not NULL
                inOrder(root.left)

            OUTPUT <-- root.value

            if root.right is not NULL
                inOrder(root.right)

- Post-order: left >> right >> root

        ALGORITHM postOrder(root)
        // INPUT <-- root node
        // OUTPUT <-- post-order output of tree node's values

            if root.left is not NULL
                postOrder(root.left)

            if root.right is not NULL
                postOrder(root.right)

            OUTPUT <-- root.value

- Breadth First

        ALGORITHM breadthFirst(root)
        // INPUT  <-- root node
        // OUTPUT <-- front node of queue to console

        Queue breadth <-- new Queue()
        breadth.enqueue(root)

        while breadth.peek()
            node front = breadth.dequeue()
            OUTPUT <-- front.value

            if front.left is not NULL
            breadth.enqueue(front.left)

            if front.right is not NULL
            breadth.enqueue(front.right)

[Go back](./README.md)
