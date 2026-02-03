___________
09-18-2023 | 09:54
Status: #school #Research 
Tags: #CS-1310 #Cpp


# Overview
- [[List]]s, [[Stack]]s, and [[Queue]]s are all data structures. 
- Data structures are abstract tools for keeping track of data. These abstractions are reflected in how the code is written. 
- We've already covered one of them! ([[Array]]s)

##### Overview
- A [[List]] is like an [[Array]], we have a linear sequence of data.
- A [[Stack]] is like a physical stack (pancakes!) where we can only work with what's on top ([[FILO]])
- A [[Queue]] is like standing in line at the store ([[FIFO]])

# List
- A [[List]] is an ordered sequence of data.
- There are multiple implementations of [[List]]s, such as a [[Linked List]] or an [[Arraylist]] (VideoGameLibrary in Program 1 is basically an [[Arraylist]])
- Most of what we'll be covering are different variations of [[Linked List]]s

### Linked List
- A [[Linked List]] is a collection of nodes.
- These nodes have a value and a [[Pointer]] to another node. (this pointer is typically called next, since its the next node in the [[List]])
- The [[Linked List]] only has to keep track of the first one, called the head (first node). (sometimes the last one too, called tail)

```cpp
class linkedlist
{
	private:
	struct node
	{
		int value;
		node* next;
	}
	node* head;

	public:
	void print()
	{
		for(node* curr = head; curr != NULL; curr = curr->next) //same                                                           as while loop

		node* curr = head; //current(curr) or ptr is generally used
		while(curr != NULL) //should end when next == NULL/nullptr 
		//can also do curr != NULL, or even while(curr)
		{
			curr = curr->next; //or *(curr).next
			
		}
	}
}
```

##### Linked List
- [[Linked List]]s are slow to access particular elements because it must traverse the previous nodes to get there. This is [[Linear Time]] O(n) (like [[Linear Search]]). An [[Array]] can access an element in [[Constant Time]] O(1) with an index.
- However, insertions and deletions can be done in [[Constant Time]] O(1) using [[Linked List]]s. [[Array]]s are linear.

##### Linked List
- [[Linked List]]s can be implemented as:
	- [[Singly-Linked]]
	- [[Doubly-Linked]]
	- [[Circular-Linked]]
	- [[Doubly-Circular-Linked]]
- Sometimes you'll see [[Quadruply-Linked]] for multi-dimensional data. 

### Singly-Linked List
- A node in a [[Singly-Linked]] List only points to one other node (so it only has one [[Pointer]]).
- The list has a [[Pointer]] to the first node (the head), and sometimes the last node (the tail).

# Singly-linked List
Typical [[Member Functions]]:
isEmpty() checks if the list is empty
getLength() returns the size of the list
append(x) inserts x at the end of the list
insertAfter(x,w) inserts x after w (value or position)
remove(x) removes x from the list
search(x) searches for x in the list 
print() prints the whole list in order 

### Doubly-Linked List
- A [[Doubly-Linked]] List is almost exactly the same as a [[Singly-Linked]] list. 
- A [[Singly-Linked]] node has a value and one [[Pointer]].
- A [[Doubly-Linked]] node has a value and two [[Pointer]]s, one to the next node and one to the previous node (typically next and prev).

### Circular-Linked List
- A [[Circular-Linked]] [[List]] doesn't have a tail node. The "last" node points to the head node. 
- There are no nodes whose next [[Pointer]] is null.

# Standard Template Libraries
- C++ [[Standard-Template-Libraries]] (stl) are [[Class]] templates that are build into C++ for common/useful data structures and algorithms. 
- These libraries are grouped into [[Container]]s, [[Iterator]]s, and Algorithms. 

## STL 
- [[Container]]s are objects that store and organize data. 
(The data structures we're learning in this chapter are containers.)
- This means C++ has libraries for all of them

### STL
- Some containers in the Standard Template Library:
- [[Array]] (not the same as the arrays we've been using)
- [[Deque]]
- [[Forward-List]] (forward_list)
- [[List]]
- [[Vector]]
- [[Set]] & [[Multiset]]
- [[Map]] & [[Multimap]]

##### STL
- [[Adapter Container]]s aren't really [[Container]]s, but manipulate some other [[Container]] for a specific use. (but as far as we're concerned they're basically [[Container]]s)
- These are things like [[Stack]]s and [[Queue]]s, we'll see why we get into their implementations

##### STL
- [[Iterator]]s are used to iterate across items in a [[Container]]. They behave like [[Pointer]]s to an object.
- Think of them like another approach to a [[For Loop]], where we keep track of the object at the current location, instead of accessing it through its index. 

##### STL
- Algorithms (in the algorithm library) are function templates that perform various common algorithms.
- These include simple ones like swap, min, and max to more complex like [[Sorting]]

# Stack
- A [[stack]] is a data structure that limits access to data based on how the data is arranged. 
- It's a physical metaphor (stack of plates, pancakes, cards, etc) that means we can only access data on top of the stack. 

### Stack
- [[Stack]]s are a last-in-first-out ([[LIFO]]) data structure. 
- Typical Functions are:
push(): add data on top of stack
pop(): returns and removes the data on top of the stack
peek(): return the data on top without removing it 

## Stack
Applications include:
undo/redo buttons
Backtracking 
Call Stack

# [[Call Stack]]
```Cpp
//LIFO call stack, so main() bottom of stack, then average(), then sum at the top of stack. 
int sum() //top of stack (current function executing)
{...}

int average() //middle
{..sum();...}

int main() //bottom
{...average();...}

//Once a function is complete and RETURNS, it is pop()'d from the call stack
```

# Stack
- [[Stack]]s can be implemented using [[Array]]s or [[Linked List]]s 
- [[Array]]s are referred to as static [[stack]]s (they have a fixed size)
- [[Linked List]]s are referred to as [[dynamic stack]]s (no fixed size, we can just add another node on top)

# [[Queue]]
- [[Queue]]s, like [[stack]]s, limit access to data in a [[Container]]
- Think of these more like standing/waiting in line (grocery store, boarding an airplane)
- Order of actions is still important, but a different order than [[stack]]s

### Queue
[[Queue]]s are a first-in-first-out ([[FIFO]]) data structure. 
Typical functions are:
- Enqueue(): add data to the end of the [[Queue]]
- Dequeue(): return and remove data from the front of the [[Queue]]
- Peek(): return the front item of the [[Queue]] 