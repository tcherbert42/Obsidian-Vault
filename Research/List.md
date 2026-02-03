____
10-02-2023 | 3:56
Status: #Research #Cpp 

# [[List]]s in C++
- A [[List]] is a common ADT (Abstract [[Data Type]]) for holding ordered data, having operations like append a data item, remove a data item, search whether a data item exists, and print the list. 
- Ex: For a given list item, after "Append 7", "Append 9", and "Append 5", then "Print" will print (7, 9, 5) in that order, and "Search 8" would indicate item not found. 
- Lists commonly holds kinds of data like [[integers]], [[Strings]], or even entire objects. 

### Common [[List]] operations:
![[ListOperaions.png]]

# [[List data structure]]
A common approach for implementing a [[Linked List]] is using two data structures.
- [[List data structure]]: A list data structure is a data structure containing the list's head and tail, and may also include additional information, such as the list's size
- [[List node data structure]]: The list node data structure maintains the data for each list element, including the element's data and pointers to the other list element

A [[List data structure]] is not required to implement a [[Linked List]], but offers a convenient way to store the [[List]]s head and tail. When using a list data structure, functions that operate on a list can use a single parameter for the list's data structure to manage the list
A [[Linked List]] can also be implement without using a [[List data structure]], which minimally requires using separate list node [[Pointer]] variables to keep track of the list's head. 