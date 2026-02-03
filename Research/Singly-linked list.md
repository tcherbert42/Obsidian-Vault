________
10-02-2023 | 05:35
Status: #school 
Tags: #CS-1310 #Cpp 

# [[Singly-linked list]] in C++
- A [[Singly-linked list]] is a data structure for implementing a list ADT, where each node has data and a [[Pointer]] to the next node. The list structure typically has [[Pointer]]s to the list's first node and last node.
- A [[Singly-linked list]] is a type of [[positional list]]: A list where elements contain [[Pointer]]s to the next and/or previous elements in the list. 

### Appending a node to a [[Singly-linked list]]
Given a new node, the [[Append]] operation for a [[Singly-linked list]] inserts the new node after the [[List]]s tail node. Ex: ListAppend(numsList, node 45) [[Append]]s node 45 to numsList. The notation "node 45" represents a [[Pointer]] to a node with a data value of 45. 

The [[Append]] algorithm behavior differs if the list is empty versus not empty:
- Append to empty list: If the [[List]]s head [[Pointer]] is [[null]] (empty), the [[algorithm]] points the list's head and tail [[Pointer]]s to the new node. 
- Append to non-empty list: If the [[List]]s head [[Pointer]] is not [[null]] (not empty), the [[algorithm]] points the tail node's next [[Pointer]] and the list's tail [[Pointer]] to the new node. 

```cpp
ListAppend(list, newNode) {
	if(list->head == null) { // List empty
		list->head = newNode;
		list->tail = newNode;
	}
	else{
		list->tail->next = newNode;
		list->tail = newNode;
	}
}
```

### [[Prepend]]ing a node to a [[Singly-linked list]] 
Given a new node, the [[Prepend]] operation for a [[Singly-linked list]] inserts the new node before the list's head node. The [[Prepend]] [[algorithm]] behavior differs if the list is empty versus not empty:
- Prepend to an empty list: If the [[List]]s head [[Pointer]] is [[null]] (empty), the [[algorithm]] points the list's head and tail [[Pointer]]s to the new node. 
- Prepend to non-empty list: If the [[List]]s head [[Pointer]] is not [[null]] (not empty), the [[algorithm]] points the new node's next [[Pointer]] to the head node, and then points the list's head [[Pointer]] to the new node. 

```cpp
ListPrepend(list, newNode) {
	if(list->head == null) { // List empty
		list->head = newNode;
		list->tail = newNode;
	}
	else{
		newNode->next = list->head;
		list->head = newNode; 
	}
}
```

## [[Singly-linked list]]s: Insert
Given a new node, the [[insertAfter]] operation for a [[Singly-linked list]] inserts the new node after a provided existing list node. curNode is a [[Pointer]] to an existing list node, but can be [[null]] when inserting into an empty [[List]]. 

The [[insertAfter]] [[algorithm]] considers three insertion scenarios:
- Insert as list's first node: If the list's head pointer is null, the [[algorithm]] points the list's head and tail [[Pointer]]s to the new node. 
- Insert after list's tail node: If the list's head pointer is not null (list not empty) and curNode points to the list's tail node, the [[algorithm]] points the tail node's next [[Pointer]] and the list's tail [[Pointer]] to the new node. 
- Insert in middle of list: If the list's head pointer is not null (list not empty) and curNode does not point to the list's tail node, the [[algorithm]] points the new node's next [[Pointer]] to curNode's next node, and then points curNode's next [[Pointer]] to the new node. 

```cpp
ListInsertAfter(list, curNode, newNode) {
	if(list->head == null) { // List Empty
		list->head = newNode;
		list->tail = newNode;
	}
	else if (curNode = list->tail) { // Insert after tail
		list->tail->next = newNode;
		list->tail = newNode;
	}
	else{
		newNode->next = curNode->next;
		curNode->next = newNode; 
	}
}
```

### [[Singly-linked list]]s: Remove
Given a specified existing node in a [[Singly-linked list]], the [[removeAfter]] operation removes the node after the specified [[List]] node. The existing node must be specified because each node in a [[Singly-linked list]] only maintains a [[Pointer]] to the next node.
The existing node is specified with the curNode parameter. If curNode is [[null]], [[removeAfter]] removes the [[List]]s first node. Otherwise, the [[algorithm]] removes the node after curNode. 

- Remove list's head node (special case): If curNode is [[null]] the [[algorithm]] points sucNode to the head node's next node, and points the list's head [[Pointer]] to sucNode. 
	- If sucNode is [[null]], the only list node was removed, so the list's tail [[Pointer]] is pointed to [[null]] (indicating the list is now empty)
- Remove node after curNode: If curNode's next [[Pointer]] is not a [[null]] (a node after curNode exists), the [[algorithm]] points sucNode to the node after curNode's next node. 
	- Then curNode's next [[Pointer]] is pointed to sucNode. If sucNode is [[null]], the [[List]]s tail node was removed, so the [[algorithm]] points the list's tail [[Pointer]] to curNode (the new tail node)

```cpp
ListRemoveAfter(list, curNode) {
	// Special case, remove head 
	if (curNode == null && list->head != null) {
		sucNode = list->head->next;
		list->head = sucNode;

		if (sucNode == null) // Removed last item
			list->tail = null;
	}
	else if (curNode->next != null) {
		sucNode = curNode->next->next;
		curNode->next = sucNode;

		if (sucNode == null) { // Removed tail
			list->tail = curNode; 
		}
	}
}
```

# [[Linked List]] search in C++
Given a key, a [[search algorithm]] returns the first node whose data matches that key, or returns [[null]] if a matching node was not found. A simple [[Linked List]] [[search algorithm]] checks the current node (initially, the list's head node), returning that node if a math, else pointing the current node to the next node and repeating. 
If the [[Pointer]] to the current node is [[null]], the [[algorithm]] returns [[null]] (matching node was not found). 

```cpp
ListSearch(list, key) {
	curNode = list->head; 
	while (curNode != null) {
		if (curNode->data == key) {
			return curNode;
		}
		curNode = curNode->next;
	}
	return null; 
}

```

### Forwards traversal
Forward traversal through a [[Linked List]] can be implemented using a [[recursive]] function that takes a node as an argument. If non-[[null]], the node is visited first. Then a [[recursive]] call is made on the node's next [[Pointer]], to traverse the remainder of the [[List]]

The ListTraverse function takes a list as an argument, and searches the entire list by calling ListTraverseRecursive on the [[List]]'s head. 
```cpp
ListTraverse(list) {
	ListTraverseRecursive(list->head)
}

ListTraverseRecursive(node) {
	if (node != null) {
		Visit node; 
		ListTraverseRecursive(node->next);
	}
}
```

### Searching
A [[recursive]] [[Linked List]] search is implemented similar to forward traversal. Each call examines 1 node. If the node is [[null]], then [[null]] is returned. Otherwise, the node's data is compared to the search key. 
If a match occurs, the node is returned, otherwise the remainder of the [[List]] is searched [[Recursively]]

```cpp
ListSearch(list, key) {
	return ListSearchRecursive(key, list->head);
}

ListSearchRecursive(key, node) {
	if (node != null) {
		if(node->data == key) {
			return node;
		}
		return ListSearchRecursive(key, node->next)
	}
	return null; 
}
```
