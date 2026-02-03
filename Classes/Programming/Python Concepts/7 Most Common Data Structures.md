# Data Structures
Data Structures = ways to structure your data
#python 


## [[Array]]s = A container object that holds a fixed number of values of a single type. 

ex:
```java
int[] myNum = {10, 20, 30, 40};          //4
float[] myMoney = {3.50, 2.23, 1.00};    //3
String[] cars = {"Ford", "Chevy"};       //2
int[] arrayOfArrays = {array,            //3 (fixed number of values of a single type)
					   array2,
					   array3};
```

#### When dealing with Arrays: 
- The name of the Array
- The size of the array
- The elements within the array (will show you the type, ex: str, int, float)
- The index for that array (the value assigned to each element)

#### Operations
- Traversing = Traverse the array, which is accessing every single element within the array. 
for example: if you wanted to add them all up and get a single integer, or even print out all the elements in the array.
- Search = You can search by the index or by the element 
- Update = If you need to replace an element

#### Uses 
- Used in other Data Structures like array lists, heaps, hash tables, and matrices 
- You can also use arrays for sorting algorithms like bubble sort, quit sort, insertion short



## [Linked List] :
### A Linked List is a linear data structure where each element is a sperate object

ex:
```java
// Import the LinkedList class
import java.util.LinkedList;

public class MyClass {
	public static void main(String[] args) {
		LinkedList<String> cars
			= new LinkedList<String>();
		cars.add("Volvo"):
		cars.add("BMW");
		cars.add("Ford");
		cars.add("Mazda")
		System.out.printIn(cars);
	}
}
```

#### When dealing with Linked Lists:
- Nodes = each Node made up of a value as well as the pointer
	- typically known as {key} for value, and {next} for pointer
	- beginning of a linked list is called a head, which points to the first value in the linked list
	- end of the list is called the tail, which is the same, except null is the pointer 
(Singly Linked List)

#### Types of Linked Lists:
- Singly Linked List = Traversal from forward -> backwards
- Doubly Linked List = Traversal forwards and backward, but each node has a prev (previous). The same as next, but points to predecessor node instead of next (successor).  
- Circular Linked List = When the tail node points to the head, and the head node points to the tail.

#### Operations
Search = a squential seach, or linear search, going fowards/backwards looking for the first element with a {key} of your choice. 
You can freely insert/delete into a linked list, anywhere in the beginning, middle, or end of it. 

#### Uses
- Alt-tab = Enables you to circle through (circular linked list) whatever tabs you have opened.
- Simple table management for Compiler design



# [Stacks] :
### A Stack is a linear data structure which follows a particular order in which the operations are performed. The order may be LIFO(Last In First Out) or FILO(First In Last Out).

ex:
```Java
Stack<String> stack = new Stack<String>();

stack.push("1");

String topElement = stack.pop();
```

Think about it like a stack of plates; When your stacking them, the last plate that you stack is the first plate you grab. 

#### Operations
- Push = Inserting something to the top of the stack 
- Pop = Deleting and returning something at the top of the stack
- Peek = Returning what is at the top of the stack w/o deleting it
- You can also check if it is empty, or if it is full 
#### Uses
- Shunning Yards Algorithm = It is for parsing and evaluating mathematical expressions (expressione evaluation)
- You can also use it to implement function calls in recursive programming



# [Queue] :
### A Queue is a linear structure which follows a particular order in which the operations are performed. The order is First In First Out (FIFO).

ex:
```java
// Java program to add elememts to a Queue
import java.util.*;
public class SubScribePlease {
	public static void main(String args[])
	{
		Queue<String> thumbsUp
			= new PriorityQueue<>();
		pq.add("Subscribe");
		pq.add("To");
		pq.add("Channel");

		System.out.printIn(thumbsUp);
	}
}
```

Think about entering a video game. When the server is full, you are placed in a First In First Out Queue.

#### Operations
- inQueue = Inserting an element to the end of the queue
- deQueue = Deleting an element from the beginning of the queue

#### Uses
- Queues are used to manage the threads in multithreading 
- Implement queue systems like Priority Queues 
