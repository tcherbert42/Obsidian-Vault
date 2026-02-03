____
09-19-2023 | 3:56
Status: #Research #Cpp 

# [[Bubble Sort]] in C++
- [[Bubble Sort]] is a [[Sorting]] algorithm that Iterates through a [[List]], comparing and swapping adjacent element if the second element is less than the first element.
- [[Bubble Sort]] uses [[Nested Loops]]. Given a list with N elements, the outer i-loop iterates N - 1 times. Each iteration moves the $i^{th}$ largest element into sorted position. The inner j-loop iterates through all adjacent pairs, comparing and swapping adjacent elements as needed, except for the last i pairs that are already in the correct position. 
- Because of the [[Nested Loops]], [[Bubble Sort]] has a [[runtime]] of O$(N^2)$. [[Bubble Sort]] is often considered impractical for real-world use because many faster [[Sorting]] algorithms exist. 

```Cpp
BubbleSort(numbers, numbersSize)
{
	for(int i = 0; i < numbersSize - 1; i++)
	{
		for(int j = 0; j < numbersSize - i - 1; i++) 
		{
			if(numbers[j] > numbers[j + 1])
			{
				temp = numbers[j];
				numbers[j] = numbers[j + 1];
				numbers[j + 1] = temp;
			}
		}
	}
}
```