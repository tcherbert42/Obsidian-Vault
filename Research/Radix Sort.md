______
09-20-2023 | 07:10
Status: #Research 
Tags: #Cpp 

# [[Radix Sort]] in C++
- [[Radix Sort]] is a [[Sorting]] [[algorithm]] designed specifically for integers. The [[algorithm]] makes use of a concept called [[bucket]]s and is a type of [[Bucket Sort]].
- Any [[Array]] of integer values can be subdivided into [[bucket]]s by using the integer values' digits. A [[bucket]] is a collection of integer values that all share a particular digit value. Ex: Values $57, 97, 77,$ and $17$ all have a $7$ as the $1's$ digit, and would all be placed into [[bucket]] $7$ when subdividing by the $1's$ digit. 

### [[Radix Sort]] [[algorithm]] 
- [[Radix Sort]] is a [[Sorting]] [[algorithm]] specifically or an [[Array]] of integers: The [[algorithm]] processes one digit at a time starting with the least significant digit and ending with the most significant. Two steps are needed for each digit.
- First, all [[Array]] elements are placed into [[bucket]]s based on the current digit's value. Then, the [[Array]] is rebuilt by removing all elements from [[bucket]]s, in order from lowest [[bucket]] to highest. 

```Cpp
RadixSort(array, arraySize) {
	buckets = create array of 10 buckets

	//Find the max length, in number of digits
	maxDigits = RadixGetMaxLength(array, arraySize);

	//Start wit the least significant digit
	pow10 = 1;
	for(digitIndex = 0; digitIndex < maxDigits; digitIndex++) {
		for(int i = 0; i < arraySize; i++) {
			bucketIndex = abs(array[i] / pow10) % 10;
			Append array[i] to buckets[bucketIndex]
		}
		arrayIndex = 0;
		for(int i = 0; i < arraySize; i++) {
			for(int j = 0; j < buckets[i]->size(); j++)
				array[arrayIndex++] = buckets[i][j];
		}
		pow10 = 10 * pow10;
		Clear all buckets
	}
}
```

### RadixGetMaxLength and RadixGetLength functions

```Cpp
//Returns the maximum length, in number of digits, out of all elements in the array
RadixGetMaxLength(array, arraySize) {
	maxDigits = 0;
	for(int i = 0; i < arraySize; i++) {
		digitCount = RadixgetLength(array[i]);
		if(digitCount > maxDigits)
		maxDigits = digitCount; 
	}
	return maxDigits; 
}

//Returns the length, in number of digits, of value
RadixGetLength(value) {
	if(value == 0)
		return 1;

	digits = 0;
	while(value != 0) {
		digits = digits + 1; 
		value = value / 10;
	}
	return digits; 
}
```