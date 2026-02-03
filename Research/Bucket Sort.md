______
09-20-2023 | 07:10
Status: #Research 
Tags: #Cpp 

# [[Bucket Sort]] in C++
- [[Bucket Sort]] is a numerical [[Sorting]] [[algorithm]] that distributes numbers into [[bucket]]s, sorts each [[bucket]] with an additional [[Sorting]] [[algorithm]], and then [[concatenate]]s [[bucket]]s together to build the sorted result. A [[bucket]] is a [[Container]] for numerical values in a specific range. 
- Ex: All numbers in the range $0$ to $49$ may be stored in a bucket representing this range. [[Bucket Sort]] is designed for [[Array]]s with non-negative numbers. 

##### [[Bucket Sort]] terminology
- The term "[[Bucket Sort]]" is sometimes used to refer to a category of [[Sorting]] [[algorithm]]s, instead of a specific [[Sorting]] [[algorithm]]. 
- When used as a categorical term, [[Bucket Sort]] refers to a [[Sorting]] [[algorithm]] that places numbers into [[bucket]]s based on some common attribute, and then combines [[bucket]] contents to produce a sorted [[Array]]. 

### [[Bucket Sort]] [[algorithm]] & [[runtime]]
- [[Bucket Sort]] first creates a [[List]] of [[bucket]]s, each representing a range of numerical values. Collectively, the [[bucket]]s represent the range from $0$ to the maximum value in the [[Array]]. For $N$ [[bucket]]s and a maximum value of $M$, each [[bucket]] represents $\frac{M+1}{N}$ values. 
- Ex: For $10$ [[bucket]]s and a maximum value of $49$, each [[bucket]] represents a range of $\frac{49+1}{10} = 5$ values; the first [[bucket]] will hold values ranging from $0$ to $4$, the second [[bucket]] $5$ to $9$, and so on. Each [[Array]] element is placed in the appropriate [[bucket]]. The [[bucket]] index is calculated as $[number*\frac{N}{M+1}]$. Then, each [[bucket]] is sorted with an additional [[Sorting]] [[algorithm]]. Lastly, all [[bucket]]s are [[concatenate]]d together in order, and copied to the original [[Array]]. 

```Cpp
BucketSort(numbers, numbersSize, bucketCount) {
	if(numbersSize < 1)
		return;

	buckets = Create list of bucketCount buckets
	
	//Find the maximum value
	maxValue = numbers[0];
	for(int i = 1; i < numbersSize; i++) {
		if(numbers[i] > maxValue)
			maxValue = numbers[i];
	}

	//Put each number in a bucket
	for each (number in numbers) {
		index = floor(number * bucketCount / (maxValue + 1));
		Append number to buckets[index]
	}

	//Sort each bucket
	for each (bucket in buckets)
		Sort(bucket)

	//Combine all buckets back into numbers list
	result = Concatenate all buckets together
	Copy result to numbers
}
```