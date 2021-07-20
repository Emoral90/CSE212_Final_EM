# Python binary search trees
Much like how the name implies, this data structure is designed like a tree. Meaning there is a root, and can have as many branches as you need there to be. It is important to remember that binary search tree, or BSTs for short, parent nodes can have at most 2 child nodes, or none if that branch ends there. If balanced and implemented correctly, the algorithmic efficiency of this data structure can reach O(log n) rates. This efficiency classification will be explained more in detail towards the end of this document. For now, let's look at the attributes of a BST.

* This data structure is non-linear
* The first node is the root node, from which all other nodes spawn
* Every other node will have one parent node
* Each node can continue having child nodes if it so pleases the developer.

![upsidedown_tree](https://miro.medium.com/max/1000/1*ZwFiymjH10cG4aZCKqDBQA.png)
***
## BST functions
Since there is no built in library of BST methods in Python 3.0+ we will have to develop our own class to create nodes and pass values into them. Keep in mind many of these will include recursive functions. These functions would include:

1. Creating a root
2. Inserting
3. Traversing in order (from left side to root to right side)
4. Finding the height and size
5. Finding a specific node
6. Deleting a node

### Creating a root
In order to get things started quickly, we will be initiating a `Node` class with a few example node values to link to each other, similar to linked lists.
```python
class Node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

    # Create objects with the class of Node
    node_root = Node(3)
    node_1 = Node(4)
    node_2 = Node(5)

    # Connect the child nodes, node_1  and node_2, with the root node
    node_root.left = node_1
    node_root.right = node_2
```

### Inserting in a BST
Because of the principle of binary search, we only need to check whether whether the input `data` is more or less than the current node's data. If it is greater, it gets inserted to the right, otherwise it gets inserted to the left

![binary_search_algorithm](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.codesdope.com%2Fstaticroot%2Fimages%2Falgorithm%2Fbinary5.png&f=1&nofb=1)
```python
def insert(node,data):
    # Check to see if node does not have any data left
    if node is None:
        node = Node(data)

    # The next two elif statements will recursively put in data and link the pointer to the new node
    elif data < node.data:
        node.left = insert(node.left,data)
        node.left.parent = node

    elif data > node.data:
        node.right = insert(node.right,data)
        node.right.parent = node
    return node
```

### In order traversal
When traversing a BST "in order" it will always mean with respect to the root node. In this case you will start with the first node on the left subtree with respect to the root, go through the node, and end with the last node stored in the BST. All of the node's data will be appended to a list in order to view the results.
```python
def traverse(node):
    # Check to see if node does not have any data left
    if node is None: 
        return []

    # If there is data in a node, you are to return all the node's data in a list while going through the left, root, and right subtree in order
    return(traverse(node.left) + 
           [node.data] + 
           travers(node.right))
```

### Finding the height and size
The height of a BST may also be referred to as the *depth* or the longest continuous path from the root node. Finding the size on the on the other hand is simply a calculation of how many nodes there are. Starting from the largest node in the left subtree and working your way to the right subtree.
```python
def height(node):
    # Check to see if node does not have any data left
    if node is None:
        return 0

    # Only return the maximum amount of nodes, and not their data found in either the left or right subtree
    return 1 + max(tree_height(node.left), tree_height(node.right)
```

### Finding a specific node
Finding a desired node and its value follows much of the same logic as before. That is it will recursively find it will find a node with the input data you give it dividing the BST in half for each check (if statement).
```python
def find(node,data):
    # Check to see if node does not have any data left
    if node is None:
        return None

    # The small chance your input data is the node you choose to begin on
    if data == node.data:
        return node
    elif data < node.data:
        return find(node.left,data)
    elif data > node.data:
        return find(node.right,data)
```

### Deleting a node
You must first recursively find the node you want to delete with a base case `if root is None` and through the `elif` statements. Once you find the node, it is best to set the right pointer of the root node to something temporary since the root will be set to `None`
```python
def delete(root, key):
    # The recursive search for the one, true node
    if root is None:
        return root
    elif key < root.key:
        root.left = delete(root.left, key)
    elif key > root.key:
        root.right = delete(root.right, key)
 
    # Only when you have found the node to be deleted, may you continue forward here
    else:
         if root.left is None:
            temp = root.right
            root = None
            return temp
        elif root.right is None:
            temp = root.left
            root = None
            return temp 
    return root
```
***
## Performance and applications of BSTs
Thanks to the nature of a typical binary search algorithm, the all functions shown here would almost always fall under the "Big O" classification of O(log n). Because if the desired result is not in one half of the stored values, it immediately discards that half and continues searching in the indicated half of values through a series of higher or lower checks. Effectively cutting our searchable values in half through each iteration, or recusive function in this case. It is especially useful when the value to be found is not near the beginning or end. In mathematical terms, the original input data `n` size divided in half over and over again. Where searchable values = n/2, n/4, n/8, n/16...

Possible applications may include but is not limited to:
* BSTs are used for indexing and multi-level indexing for large databases
* They are also helpful to implement various searching algorithms (i.e. Binary and Merge sorting)
