# Linked lists
In order to understand linked lists, you must at least be familiar with dynamic arrays in python. once you understand how dynamic arrys function, the purpose of linked lists will become more clear. If you are already familiar with dynamic arrays, then you may want to skip ahead to 
***
## Dynamic arrays
A dynamic array differs from a regular array in one specific aspect. Instead of needing to calculate or estimate how much memory would need to be allocated to hold a specific number of equally sized elements, auto-resizing is built in to this function of Python. Other than that, everything else remains the same. Elements can be added into the array or appended so long as they are contiguously (in a consecutive fashion) inserted, and are of the same character type.

Any and all elements that are appended to a dynamic arrary will yield a size. The potential amount of elements that can fit within an array is referred to as the capacity. If there is only one element, then that element will be considered to be both the first and last index

Example of a dynamic array: 
![dyn_array_img](https://miro.medium.com/max/418/1*tEU9_sDRCz-MkDA9NHyp0Q.png)

### Creating an array
In order to create a dynamic array in python 3.0 and above, you should at the very least create an empty list. Using the example image above, we can then fill in the first 4 "slots".
```python
a_list = []

a_list = ["D","e","a","r"]
```

### Return the length
If you need to return the length of this array for any reason, you can do so by using the `len()` method
```python
a_list = ["D","e","a","r"]

print(len(a_list))

>>> 4
```

### Access an element
If you need to access a specific element within the array, you would need to refer to the array's variable name and its specific index
```python
a_list = ["D","e","a","r"]

print(a_list[0])

>>> D
```

### Append and pop an element
If you need to add or delete an element at the end of the array, you may use the `append()` method to add, or the `pop()` methond to remove an element at a specified index from an array.

```python
# Adding/appending an item
a_list = ["D","e","a","r"]

print(a_list.append("y"))

>>> ['D','e','a','r','y']
```

```python
# removing/popping an item
a_list = ["D","e","a","r"]

print(a_list.pop(0))

>>> ['e','a','r']
```

### Big O notation analysis for dynamic arrays
"Big O" notation for those who do not yet know, is essentially shorthand for describing the performance of a program or function. Specifically how much time is taken to complete the program/function given a certain amount of input (n).

The best, most efficient performance classification of any "Big O" analysis would be O(1) or constant. Meaning no matter how much input data the program/function recieves, the time taken to finish executing remains the same.
* This is the case if you are only appending or popping from an array since all you are doing is adding/removing one new element. Not having any need to copy the current size of all the elements in an array, increase the capacity of the array, paste those same elements in the new array, and then add the or remove the desired element at any other index other than the last, or at the end.
![reassign_arr_img](https://media.geeksforgeeks.org/wp-content/uploads/darray.png)

The worst and most inefficient performance classification would be O(n!) or factorial. For the most part the areas that are to be covered such as: dynamic arrays, linked lists, sets, and binary search trees; will at worst fall under O(n), or linear performance.
***
## Linked list attribuites
A linked list is nothing more than a sequence of elements contaning data (a node), not in any specific order, which are connected together via links. These links would then be referred to as pointers since they would point the input data to which node should store it, whether it be the preceeding or following node.

It is important to remember since python does not have any built in libraries so the next best solution would be to implement this concept of linked lists as a Node class in order to better demonstrate it.

### Creating a linked list
It would be necessary to create two classes here. One to create and initiate the object `Node` and the other `Linked_List` to use the Node object by passing in values and point to the next nodes in this case.

```python
class Node:
    def __init__ (self, data=None):
        self.data = data
        self.next = None

class Linked_List():
    def __init__ (self):
        self.head = None

list_1 = Linked_List()
list_1.head = Node("Sunday")
node_2 = Node("Monday")
node_3 = Node("Tuesday")

# The first/head node is linked to the second node
list_1.head.next = node_2

# The second node is linked to the third and final node
node_2.next = node_3
```

Note: If the linking of one node to another still appears too complicated, think of it as a daisy-chain. Much like how the [Panasonic 3DO](https://en.wikipedia.org/wiki/3DO_Interactive_Multiplayer) game console worked with multiple players
 
![3do_controllers](https://i.imgur.com/FhszdQS.jpeg)

### Traversing a linked list
If you need to traverse a linked list, all that means is that you would need to iterate through each node of the list and return its results. It is for this reason you would need to at the very least print each data result in the nodes. To confirm you have reached the end of your list, you must also put in check to make sure there are no more more nodes with data to return. 

In order to demonstrate this concept, take the previous code example used above to create a linked list, but with a small addition to the `Linked_List` class which is shown here:
 
```python
# class Node [...]

class Linked_List():
    def __init__ (self):
        self.head = None

    def traverse_list(self):
        Node = self.head
        while Node is not None:
            print(Node.data)
            Node = Node.next

# Creation of linked lists and nodes [...]
```

### Insertion in a linked list
There are multiple ways you can insert nodes with data. We will cover 3 of them. Inserting at the beginning, the end, and in between two nodes.

Inserting a new node at the beginning is relatively straight forward since there is no need to traverse the entire linked list to do so. As a result, all you you would need to do is create a new node (as a parameter) and point to the head of `list_1`, ergo linking it.
```python
# class Linked_List [...]
    def insert_beg(self,data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
```

To insert in a node at the end of a linked list, you would need to traverse the list first, or iterate through it, and create the new node and point to the end or tail node of `list_1`, assuming there is already a linked list with dat to traverse.
```python
# class Linked_List [...]
    def insert_end(self,data):
        new_node = Node(data)

# A quick check to make sure if there is even a head or first node exits
        if self.head is None:
            self.head = new_node
            return

# While end.next returns true, end or self.head data originally, will be set equal to end.next
        end = self.head
        while(end.next):
            end = end.next

# Linking the end node to new_node via the .next pointer
        end.next = new_node
```
To insert in between two different nodes, you must first traverse the linked list (if there is one already) and essentially combine the linking techniques as demonstrated in the last 2 examples. You would have to change the pointer of the previous node to point to `new_node`. That is possible by passing in both the new node and the existing node after which the new node will be inserted. So we define an additional class which will change the `.next` pointer of the new node to the `.next` pointer of the node to be inserted. Then assign `new_node` to next pointer of the node to be inserted.
```python
# class Linked_List [...]
    def insert_mid(self,prev,data):
 
        # Quick check to see if the given if the previous node (prev) exists
        if prev is None:
            return "There is NO previous node"
        # Create the new_node to insert
        new_node = Node(new_data)
    
        # Point the new_node first in order to not lose any data 
        new_node.next = prev.next
    
        # Replace the prev.next (previous node and its pointer) with the new_node and its pointer value
        prev.next = new_node
```

Should you choose to remove a node that is no longer needed, you would have to first locate where the key of that node. If you are worried that you are unfamiliar with keys and values within the realm of python, dont worry. Here is a very brief summary of what they are.
***
### Keys and values
This topic will be reviewed more in depth in the following tutorial about sets. There are only 2 key features you need to know for the time being. 
* Lets say you have a big box of 33 tomatoes and 44 squash, and you organize it per food type in separately labled boxes. As long as you counted and labled everything properly, whenever you in a rush when you promised to bring something to the ward activity to eat, you no longer have to look for each individual food item, all you would have to look for is the label denoting what is inside each box

The same goes for keys and values for any given variable in python. For performance sake, locating the key (box label) first will save a great amount of time instead of have to iterate through each individual value to find what you want. Since any key will always have to have one or more values attached to it.
***
### Removing from a linked list
In reality, you are not really removing or deleting anything. You are simply taking advantage of the value of the node you want to "remove" and changing its pointer to point to the following node. Effectively taking the aforementioned node out of the loop and using the parameter `rem_key` to serve as a key in order to find the node you want to remove.
```python
# class Linked_List [...]
    # Initiate head
    def remove(self,rem_key):
        head = self.head

        # Check to see if head exist
        if (head is not None):
            if (head.data == rem_key):
                # Change the head.next pointer none
                self.head = head.next
                head = None
                return

        while (head is not None):
            if head.data == rem_key:
            break
            # Re-assign the previous node's pointer prev to the following node's next pointer
            prev = head
            head = head.next

        if (head == None):
            return

        prev.next = head.next
            head = None
```
***
## Performance and applications of linked lists
Performance for these methods are evaluated in "Big O" notation. We will be comparing "Big O" analysis of both dynamic arrays and linked lists. The following are ordered by efficiency in descending order:

**Method**    | **Dynamic Array**     | **Linked List**
----------------|-----------------------|----------------|
Accessing   | O(1)  | O(n)
Insert or remove at beginning| O(n)| O(1)
Insert or remove at end| O(1)| O(n)
Insert or remove in middle| ~ O(n)| ~ O(n)

**Accessing**

In order to access anything from a dynamic array, you simply would look up the value to return through a print statment for example, resulting in a constantly efficient function. Accessing a node's data in a linked list would take a certain amount of time that is directly proportional to the size of the input data `n`, making its efficiency dependent on the size of data.

**Insert or remove at the beginning**

If you wish to insert or remove an element of an array at the beginning, you append/pop the desired element and would then have to copy the rest of the elements over one "slot" in order to maintain the contiguous memory trait of dynamic arrays. Linked lists have no dependency on the input data size since you are only adding one new node with a pointer that points next to the old head of the list.

**Insert or remove at the end**

Inserting or removing at the end of an array functions much like a stack or queue. As in the most addition/removal of an element will always be found at the end of the array. Linked lists will take more time since you would have to traverse the entire list before you assign the tail node's pointer to a new tail node.

**Insert or remove in the middle**

The reason for the tilde `~` is because the exact classification of "Big O" analysis for these methods will not always yield the same result in terms of efficiency. Both data structures will depend entirely on the size of the input data divided by the index of wherever the new item will be inserted or removed. Since you would have to iterate through both a dynamic array or traverse a linked list to get to that point.