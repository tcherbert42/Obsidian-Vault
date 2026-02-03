____
09-19-2023 | 3:56
Status: #Research #Cpp 

# [[Selection Sort]] in C++
- [[Selection Sort]] is a [[Sorting]] [[algorithm]] that treats the input as two parts, a sorted part and an unsorted part, and repeatedly selects the proper next value to move from the unsorted part to the end of the sorted part. 

### [[runtime]] for [[Selection Sort]]
- [[Selection Sort]] may require a large number of comparisons. The [[Selection Sort]] [[algorithm]] [[runtime]] is O$(N^2)$. If a list has $N$ elements, the outer loop executes $N - 1$ times. For each of those $N - 1$ outer loop executions, the inner loop executes an average of $\frac{N}{2}$ times.
- So the total number of comparisons is proportional to $(N - 1) * \frac{N}{2}$ or O$(N^2)$. Other [[Sorting]] [[algorithm]]s involve more complex [[algorithm]]s but have faster execution times. 

```Cpp
for(int i = 0; i < numbersSize - 1; i++)
{
	//Find index of smallest remaining element
	indexSmallest = i;
	for(int j = i + 1; j < numbersSize; j++)
	{
		if(numbers[j] < numbers[indexSmallest])
		{
			indexSmallest = j;
		}
	}

	//Swap numbers[i] and add numbers[indexSmallest]
	temp = numbers[i];
	numbers[i] = numbers[indexSmallest];
	numbers[indexSmallest] = temp;
}
```

### Explained
- The index variable $i$ denotes the dividing point. Elements to the left of $i$ are sorted, and elements including and to the right of $i$ are unsorted. All elements in the unsorted part are searched to find the index of the element with the smallest value. The variable indexSmallest stores the index of the smallest element in the unsorted part. Once the element with the smallest value is found, that element is swapped with the element at location $i$. Then, the index $i$ is advanced one place to the right, and the process repeats. 
- The term "selection" comes from the fact that for each iteration of the outer loop, a value is selected for position $i$. 