________
09-27-2023 | 09:50
Status: #school 
Tags: #CS-1310 #Cpp 

##### What have we covered??
- Sorting
- Lists/Stacks/Queues
- Searching
- Templates
- Encapsulation 
- Big O Notation (multiple choice)
- Recursion 

## Sorting Algorithms
- Bubble Sort - * worst case O$(N^2)$ best O$(N)$
- Selection Sort - * worst case O$(N^2)$ best O$(N^2)$ because still does linear search 
- Insertion Sort - * worst case O$(N^2)$  best O$(N)$
- Quick Sort - worst: O$(N^2)$, best O$(N log N)$
- Merge Sort - worst: O$(N log N)$, best O$(N log N)$ 
Average for Bubbe, Selection, Insert is O$(N^2)$
Average for Quick and Merge is O$(N log N)$
### Format
- Multiple Choice
- Short Answer
- Steps of a process
- Handwritten Code 

#### Write it Out
Ex: Selection Sort
- Find next smallest # 
- move to front 

# Selection Sort
- Given a list of numbers (5, 4, 6, 1, 3, 2)
- Find One (smallest value) (1, 4, 6, 5, 3, 2)
- Move to front
- Find next smallest value (1, 2, 6, 5, 3, 4)
- Move to front 

## Quick Sort vs Merge Sort (both recursive)
Quick
1. Rearrange
2. Recurse
Merge
1. Recurse
2. Rearrange
Find pivot value, middle value (0 + max Index / 2 = pivot)
Split in half
small values left and large values right

# Templates
```cpp
void func(int x)
{...}

void func(char x)
{...}

void func(string x)
{...}

//Instead use a Template!
template<typename T>
void func(T x)
{...}

//then, in main
int main()
{
	int y = 5;
	func(y);
}

//Can also be used for Objects
template<typename T, U>
class Container
{
	T attribute;
	U other;
	void func(T);
}

int main()
{
	Container<int> cont;
}
```

# Stacks and Queues
Stack - add to the top, remove from the top FIFO
- add xyz to a stack, and remove them in reverse (zyx)
Queue - add to one side, remove from the other LIFO
- add xyz to queue, remove x then y then z in the same order 

##### Static and Dynamic Stacks and Queues
- Array is static, cannot change size 
- Linked List is Dynamic 