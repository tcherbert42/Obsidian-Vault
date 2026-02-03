_______
09-19-2023 | 3:56
Status: #Research #Cpp 

# [[Insertion Sort]] in C++
- [[Insertion Sort]] is a [[Sorting]] [[algorithm]] that treats the input as two parts, a sorted part, and an unsorted part, and repeatedly inserts the next value from the unsorted part into the correct location in the sorted part. 

### [[runtime]] for [[Insertion Sort ]]
- [[Insertion Sort]]'s typical [[runtime]] is O$(N^2)$. If a [[List]] has N elements, the outer loop executes $N - 1$ times. For each outer loop execution, the inner loop may need to examine all elements in the sorted part. Thus, the inner loop executes on average $\frac{N}{2}$ times. So the total number of comparisons is proportional to $(N-1) * (\frac{N}{2})$, or O$(N^2)$. Other [[Sorting]] [[algorithm]]s involve more complex [[algorithm]]s but faster execution. 

```Cpp
for(int i = 1; i < numbersSize; i++)
{
	int j = i;
	//Insert numbers[i] into sorted part, stopping once numbers[i] in
	//correct position
	while (j > 0 && numbers[j - 1])
	{
		//Swap numbers[j] and numbers[j - 1]
		temp = numbers[j];
		numbers[j] = numbers[j - 1];
		numbers[j - 1] = temp;
		j--;
	}
}
```

### Explained 
- The index variable $i$ denotes the starting position of the current element in the unsorted part. Initially, the first element (i.e. element at index $0$) is assumed to be sorted, so the outer loop initializes $i$ to $1$. The inner while loop inserts the current element into the sorted part by repeatedly swapping the current element with the elements in the sorted part that are larger. Once a smaller or equal element is found in the sorted part, the current element has been inserted in the correct location and the while loop terminates. 