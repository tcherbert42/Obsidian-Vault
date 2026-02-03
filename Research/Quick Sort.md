_______
09-19-2023 | 3:56
Status: #Research #Cpp 


# [[Quick Sort]] in C++
- [[Quick Sort]] is a [[Sorting]] [[algorithm]] that repeatedly [[partition]]s the input into low and high parts (each part unsorted), and then recursively sorts each of those parts. To partition the input, [[Quick Sort]] chooses a [[Pivot]] to divide the data into low and high parts. 
- The [[Pivot]] can be any value within the [[Array]] being sorted, commonly the value of the middle array element. 
- Ex: For the [[List]] $(4, 34, 10, 25, 1)$, the middle element is located at index $2$ (the middle of indices $[0,4]$) and has a value of $10$. 

- Once the [[Pivot]] is chosen, the [[Quick Sort]] [[algorithm]] divides the array into two parts, referred to as the low [[partition]] and the high [[partition]]. 
- All values in the low [[partition]] are less than or equal to the [[Pivot]] value. All values in the high [[partition]] are greater than or equal to the [[Pivot]] value. The values in each [[partition]] are not necessarily sorted. 
- Ex: Partitioning $(4, 34, 10, 25, 1)$ with a [[Pivot]] value of $10$ results in a low [[partition]] of $(4, 1, 10)$ and a high [[partition]] of $(25, 34)$. Values equal to the [[Pivot]] may appear in either or both of the [[partition]]s

### Partitioning [[algorithm]]
- The [[Partitioning Algorithm]] uses two index variables lowIndex and highIndex, initialized to the left and right sides of the current elements being sorted. As long as the value at index lowIndex is less than the [[Pivot]] value, the [[algorithm]] increments lowIndex, because the element should remain in the low partition. 
- Likewise, as long as the value at index highIndex is greater than the [[Pivot]] value, the [[algorithm]] decrements highIndex, because the element should remain in the high [[partition]]. 
- Then, if lowIndex >= highIndex, all elements have been [[partition]]ed, and the [[Partitioning Algorithm]] returns highIndex, which is the index of the last element in the low [[partition]]. Otherwise, the elements at indices lowIndex and highIndex are swapped to move those elements to the correct [[partition]]s. The [[algorithm]] then increments lowIndex, decrements highIndex, and repeats. 

## [[Quick Sort]] [[runtime]]
- The [[Quick Sort]] [[algorithm]]s runtime is typically O$(N log N)$. [[Quick Sort]] has several [[partition]]ing levels, the first level dividing the input into 2 parts, the second part into 4 parts, the third into 8 parts, etc. At each level, the [[algorithm]] does at most $N$ comparisons moving the lowIndex and highIndex indices. If the [[Pivot]] yields two equal-sized parts, then there will be $log N$ levels, requiring the $N * log N$ comparisons. 

##### Worst case [[runtime]]
- For typical unsorted data, such equal [[partition]]ing occurs. However, [[partition]]ing may yield unequally sized parts in some cases. If the [[Pivot]] selected for [[partition]]ing is the smallest or largest element, one [[partition]] will have just 1 element, and the other [[partition]] will have all other elements. If this unequal [[partition]]ing happens at every level, there will be $N-1$ levels, yielding $N+N-1+N-2+...+2+1 = (N + 1)*(N/2)$, which is O$(N^2)$. So the worst case [[runtime]] for the [[Quick Sort]] [[algorithm]] is O$(N^2)$. Fortunately, this worst case [[runtime]] rarely occurs.  

```Cpp
Partition(numbers, lowIndex, highIndex) {
	//Pick a middle element as pivot
	midpoint = lowIndex + (highIndex - lowIndex) / 2;
	pivot = numbers[midpoint];

	bool done = false;
	while(!done) {
		while(numbers[lowIndex] < pivot) {
			lowIndex += 1;
		}
		while(pivot < numbers[highIndex]) {
			highIndex -= 1;
		}

		//If zero or one elements remain, then all numbers are
		//partitioned
		if(lowIndex >= highIndex) {
			done = true;
		}
		else {
			//Swap numbers[lowIndex] and numbers[highIndex]
			temp = numbers[lowIndex];
			numbers[lowIndex] = numbers[highIndex];
			numbers[highIndex] = temp;

			//Update lowIndex and highIndex
			lowIndex += 1;
			highIndex -= 1;
		}
	}
	return highIndex;
}
```