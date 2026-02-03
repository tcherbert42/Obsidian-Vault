______
09-20-2023 | 06:05
Status: #Research 
Tags: #Cpp 


# [[Merge Sort]] in C++
- [[Merge Sort]] is a [[Sorting]] [[algorithm]] that divides a [[List]] into two halves, recursively sorts each half, and then merges the sorted halves to produce a sorted [[List]]. 
- The recursive [[partition]]ing continues until a [[List]] of 1 element is reached, as a [[List]] of 1 element is already sorted.

### [[Merge Sort]] [[partition]]ing 
- The [[Merge Sort]] [[algorithm]] uses three index variables to keep track of the elements to sort for each recursive function call. 
- The index variable $i$ is the index of the first element in the list, and the index variable $k$ is the index of the last element. The index variable $j$ is used to divide the list into two halves. Elements from $i$ to $j$ are in the left half, and elements from $j+1$ to $k$ are in the right half. 

### [[Merge Sort]] [[algorithm]]
- [[Merge Sort]] merges the two sorted [[partition]]s into a single [[List]] by repeatedly selecting the smallest element from either the left or right partition and adding that element to a temporary merged [[List]]. 
- Once fully merged, the elements in the temporary merged [[List]] are copied back to the original list

### [[Merge Sort]] [[runtime]]
- The [[Merge Sort]] [[algorithm]]'s [[runtime]] is O$(N log N)$. [[Merge Sort]] divides the input in half until a [[List]] of $1$ element is reached, which requires $log N$ [[partition]]ing levels. At each level, the [[algorithm]] does about $N$ comparisons selecting and copying elements from the left and right [[partition]]s, yielding $N * log N$ comparisons. 
- [[Merge Sort]] requires O$(N)$ additional memory elements for the temporary [[Array]] of merged elements. For the final merge operation, the temporary list has the same number of elements as the input. Some [[Sorting]] [[algorithm]]s sort the [[List]] elements in place and require no additional memory, but are more complex to write and understand.
- To allocate the temporary [[Array]], the 'Merge()' function dynamically allocated the [[Array]]. mergedNumbers is a pointer variable that points to the dynamically allocated [[Array]], and 'new int[mergedSize]' allocates the [[Array]] with 'mergedSize' elements. 
- Alternatively, instead of allocating the array within the 'Merge()' function, a temporary [[Array]] with the same size as the [[Array]] being sorted can be passed as an argument. 

```Cpp
Merge(numbers, leftFirst, leftLast, rightLast) {
	//Create a temporary array mergedNumbers
	//Initialize position variables
	while(leftPos <= leftLast && rightPos <= rightLast) {
		if(numbers[leftPos] <= numbers[rightPos]) {
			mergedNumbers[mergePos] = numbers[leftPos];
			++leftPos;
		}
		else {
			mergedNubers[mergePos] = numbers[rightPos];
			++rightPos;
		}
		++mergePos;
	}
	//If left partition not empty, add remaining elements
	while(leftPos <= leftLast) {
	mergedNumbers[mergePos] = numbers[leftPos];
	++leftPos;
	++mergePos;
	}
	//If right partition not empty, add remaining elements
	while(rightPos <= rightLast) {
	mergedNumbers[mergePos] = numbers[rightPos];
	++rightPos;
	++mergePos;
	}
	//Copy mergedNumbers back to numbers
	for(mergePos = 0; mergePos < mergedSize; ++mergePos) {
		numbers[leftFirst + mergePos] = mergedNumbers[mergePos];
	}
}
```



