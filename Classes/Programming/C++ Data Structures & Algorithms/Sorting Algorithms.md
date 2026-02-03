__________
09-13-2023 | 09:54
Status: #school #Research 
Tags: #CS-1310 #Cpp

## Sorting
- Sorting algorithms are used to arrange data in some order.
- Typically numeric or alphabetic, and can be ascending or descending
- This chapter covers different strategies for getting the data into the order we want it.

# Bubble Sort 
- [[Bubble Sort]] is a simple sorting [[algorithm]] the steps through that steps through the list and compares each pair of adjacent data (puts them in a bubble), and swaps them if necessary.
- It's like linear search, but it swaps data if its out of order. 

### Bubble Sort
- Best and Worst case efficiency: 
- Best: The list is already sorted! You only have to pass through the [[Array]] one time and compare each [[Array]] element once, so there would be n comparisons where n is the number of elements. 
- Worst: The list is sorted in the opposite order, which is the maximum number of operations, $n^2$

##### Bubble Sort
[[Big O Notation]] of [[Bubble Sort]]:
Best case:                     O(n)
Average case:              O($n^2$)
Worst case:                  O($n^2$)
Space Complexity:     O(1)

- This is not a very practical sorting method, but it is very illustrative for thinking about the sorting process. 

```C++
```
# Selection Sort
- [[Selection Sort]] repeatedly searches the remaining unsorted data, finds the smallest data, and moves it to the correct position. 
- Places data correctly one at a time

### Selection Sort
[[Big O Notation]] of [[Selection Sort]]:
Best case:                       O($n^2$) 
Average case:                 O($n^2$)
Worst case:                     O($n^2$)
Space Complexity:        O(1)

- [[Selection Sort]] typically does fewer swaps than [[Bubble Sort]], but it has to search the list for every iteration. 

```C++
//assume first # is smallest
//
void selection(int[] arr, int size)
{
	int temp;
	int min = 0;
	for(int j = 0; j < size; j++)
	{	
		min = j;
		for(int i = j; i < size; i++)
		{
			if(arr[i] < arr[min])
				min = i;
		}
		temp = arr[j];
		arr[j] = arr[min];
		arr[min] = temp;
	}
}
```

# Insertion Sort
- [[Insertion Sort]] builds the final [[Array]] one element at a time by stepping through each item and placing it in its correct position. 
- It repeatedly inserts a new element into the sorted results. 
- (best and worst case are the same as the previous two)

### Insertion Sort
[[Big O Notation]] of [[Insertion Sort]]:
Best case:                       O(n)
Average Case:                O($n^2$)
Worst Case:                    O($n^2$)
Space Complexity:        O(1)

- Although the efficiency class for average case is the same, [[Insertion Sort]] typically does fewer comparisons. 

```C++
//Grab key from front of unsorted partition 
//Compare key to left neighbor (K < L swap, move key one space left)
//If K !< L,  key inserted successfully
//move on to next key

//             sorted       unsorted
void selection(int[] arr, int size)
{
	//i will hold the subscript of the unsorted array
	for(int i = 1; i < size; i++)
	{
		// since we assume 0 is already sorted, start at index 1 (unsorted)
		int key = arr[i]; //select the item to be sorted
		int j = i-1; //j is the element to the furthest right of the key
		while(j >= 0 && arr[j] > arr[key])
		{
			arr[j+1] = arr[j]; //move elements to the right
			j = j-1; //decrement j
		}
		arr[j+1] = key; //place item in final sorted position
	}
}
```
# Quick Sort
- [[Quick Sort]] repeatedly partitions the [[Array]] into smaller and larger sections around a [[Pivot]] value such that everything left of the pivot is smaller, and everything to the right is larger. We then do [[Quick Sort]] on each half. 
- Because we are subdividing the [[Array]], this is typically done [[Recursively]]

### Quick Sort
[[Big O Notation]] of [[Quick Sort]]:
Best Case:                      O(n log n)
Average Case:               O(n log n)
Worst case:                    O($n^2$)
Space Complexity:       O(log n)

- Its faster, but this is where we start sacrificing space/[[Conceptual Complexity]] for speed. 

```C++
```
# [[Merge Sort]]  
