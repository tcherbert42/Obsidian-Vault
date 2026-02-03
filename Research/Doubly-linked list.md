________
10-02-2023 | 05:35
Status: #school 
Tags: #CS-1310 #Cpp 


# [[Doubly-linked list]] in C++ 
A [[Doubly-linked list]] is a data structure for implementing a list ADT, where each node has data, a [[Pointer]] to the next node, and a [[Pointer]] to the previous node. The list structure typically points to the first node and the last node. The [[Doubly-linked list]] usually includes a head and tail node. 

A [[Doubly-linked list]] is similar to a [[Singly-linked list]], but instead of using a single pointer to the next node in the list, each node has a [[Pointer]] to the next and previous nodes. Such a list is called "[[Doubly-Linked]]" because each node has two [[Pointer]]s, or "links". A [[Doubly-linked list]] is a type of [[positional list]]: A list where elements contain [[Pointer]]s to the next and/or previous elements in the list.

### [[Append]]ing a node to a [[Doubly-linked list]]
Given a new node, the [[Append]] operation for a [[Doubly-linked list]] inserts the new node after the [[List]]s tail node. The [[Append]] [[algorithm]] behavior differs if the [[List]] is empty versus not empty:

- Append to empty list: If the [[List]]s head [[Pointer]] is [[null]] (empty), the [[algorithm]] points the [[List]]'s head and tail [[Pointer]]s to the new node. 
- Append to non-empty list: If the [[List]]s head [[Pointer]] is not [[null]] (not empty), the [[algorithm]] points the tail node's next [[Pointer]] to the new node, points the new node's previous [[Pointer]] to the [[List]]s tail node, and points the [[List]]s tail [[Pointer]] to the new node. 

```cpp
ListAppend(list, newNode) {
	if (list->head == null) { // List empty
		list->head = newNode;
		list->tail = newNode;
	}
	else {
		list->tail->next = newNode;
		newNode->prev = list->tail;
		list->tail newNode;
	}
}
```

### [[Prepend]]ing a node to a [[Doubly-linked list]] 
Given a new node, the [[Prepend]] operation of a [[Doubly-linked list]] inserts the new node before the [[List]]s head node and points the head [[Pointer]] to the new node. 
- Prepend to empty list: If the [[List]]'s head [[Pointer]] is [[null]] (empty), the [[algorithm]] points the [[List]]'s head and tail [[Pointer]]s to the new node. 
- Prepend to non-empty list: If the [[List]]'s head [[Pointer]] is not [[null]] (not empty), the [[algorithm]] points the new node's next [[Pointer]] to the [[List]]'s head node, points the [[List]] head node's previous [[Pointer]] to the new node, and then points the [[List]]'s head [[Pointer]] to the new node. 

```cpp
ListPrepend(list, newNode) {
	if (list->head == null) { // List empty
		list->head = newNode;
		list->tail = newNode;
	}
	else {
		newNode->next = list->head;
		list->head->prev = newNode;
		list->head = newNode; 
	}
}
```

### [[Doubly-linked list]]: Insert


### [[Doubly-linked list]]: Remove 


## [[Linked List]]: Traversal


# Sorting [[Linked List]]s in C++