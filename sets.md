# Python sets
Put simply, A set is a variable that can store multiple types data in a single variable. Within a set you can store data that is unordered *and* unindexed. As a result, any set will have the following 3 defining characteristics:
* No indexing or slicing of elements are allowed
* Individual elements are immutable, or cannot be modified
* No elements can be duplicated

Using sets check for associated data of a user for instance can be highly advantageous since it is significantly faster than linearly iterating through arrays or linked lists due the use of hash tables. Its basic functionalities can be compared to a Venn digagram.
![venn_digram](https://files.realpython.com/media/t.8b7abb515ae8.png)
***
## Hash Tables
Very briefly, this data structure works on the principle that multiple values are present at the same "index" position, the value is then appended to that position and form a mini linked list. 

![set implementation](https://media.geeksforgeeks.org/wp-content/uploads/HashTable-300x278.png)

### Hash function
The only way how these hash tables can be created is from a hash function. It converts a large amount of data mapped to a variable to a smaller more maneagable value, such as a single integer. This mapped integer is then used as an index in a hash table. In simple terms, a hash function maps a big number or string to a smaller value that can be used as index in hash table

A simple and common hash function that demonstrates this principle by using the modulus of the capacity of an array or list
* So for example if you have a list with a capacity of 10 and want to store some data at some index. You can save on time and performance by getting that hashed value by finding the modulo of that number
```python
mod = 77 % 10
print(mod)

>>> 7
```
***
## Set methods and functions
We will go over different ways to take advantage of the characteristics of a Python set. These methods are:
1. Creating a set
2. Accessing a set of values
3. Adding and removing items from a set
4. Union and Intersection of sets
5. Difference of sets

### Creating a set
You may begin by initiating an empty set by using the keyword `set()` or by setting a variable equal to some value(s) contained in curly braces `{}`
```python
set_1 = set()

set_2 = {["Some", "Random", "Values"]}
```

### Accessing a set
Because the data/values within a set are immutable, you *cannot* access individal values. Only the set as a whole if you were to print it out. The most practical way of seeing individual values of a set would be to iterate through them using a for loop.
```python
set_2 = set(["Some", "Random", "Values"])

# Keep in mind you can also use the range() method to print out a specific quantity of values
for i in set_2:
    print(i)

>>> Some
    Random
    Values
```

### Adding and removing from a set
Adding values are straight forward. You would use the `add()` method to add values at the end of the set much like a typical array or stack.
```python
set_2 = set(["Some", "Random", "Values"])
set_2.add("Bop it")
print(set_2)

>>> {'Values', 'Bop it', 'Some', 'Random'}
```

For removing an element, it is recommended you use the `remove()` method over `pop()` or `discard()`. Mainly because `pop()` removes an element at random, since there are no indices to speak of in a set, and `discard()` will not raise an exception (not run properly) if the specified element does not exist.
```python
set_2 = set(["Some", "Random", "Values"])
set_2.remove("Some")
print(set_2)

>>> {'Random', 'Values'}
```

### Union and intersection of sets
Just like in mathematics, the union of 2 different sets will yield a new set and containing any and all *distinct* elemenents from both sets. You would use the `|` symbol in between the variable names of the sets to produce the union.
```python
set_1 = set(["Other", "Random", "Words"])

set_2 = set(["Some", "Random", "Values"])

set_union = set_1 | set_2
print(set_union)

>>> {'Some', 'Values', 'Words', 'Random', 'Other'}
```

The intersection of 2 different sets will yield a new set and containing any and all *common* elemenents from both sets. You would use the `&` symbol in between the variable names of the sets to produce the intersection.
```python
set_1 = set(["Other", "Random", "Words"])

set_2 = set(["Some", "Random", "Values"])

set_inter = set_1 & set_2
print(set_inter)

>>> {'Random'}
```
### Difference of sets
The difference of sets will result in a new set containing the elements of the first set minus any common elements found in the second set. You would use the `-` symbol in between the variable names of the sets to get the difference.
```python
set_1 = set(["Other", "Random", "Words"])

set_2 = set(["Some", "Random", "Values"])

set_diff = set_1 - set_2
print(set_diff)

>>> {'Words', 'Other'}
```
***
## Performance and applications of sets
Performance will be evaluated in "Big O" notation. We will be comparing "Big O" analysis of each method followed by a short explaination of each analysis.
**Method**  | **Efficiency**
------------|--------------
Accessing   | O(1) or O(n)
Adding or removing  | O(1)
Union or intersection   | O(1)
Difference  | O(n)

**Accessing**

Depending on what you have your program set to do, accessing a set in python may be constant, O(1), if you want any random element from the set. O(n) if you want to see every item in the set as shown in the example above.

**Adding or removing**

Since all elements are already accounted for in a set, the specified element you would want to add or remove would take the same amount of time every time.

**Union or intersection and difference**
Since the union or intersection of a set of values is already a concept that exists in mathematics, finding the amount of common elements and either including or excluding them is nothing more than a math equation that compiles within the program. Which will always result in constant efficiency O(1)

### Applications
Database organization is among the most common uses for a set, or a funciton containing a set. Should you have the need to organize a database of employess or present the overall collection of data you have quickly. Inddividual employees or employers can be found easily entering their names into a set and printing the results since there can be no duplicates. Or if there is a large group of people who are all equally qualified to take an assignment, you may want to access a set containing those people at random to simulate "drawing straws".
![db_example](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fgatelogsystems.com%2Fwp-content%2Fuploads%2F2018%2F04%2Fdatabase-development.png&f=1&nofb=1)