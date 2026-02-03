#python 
# A string is a sequence of characters
ex: CSC1200 is a sequence of 7 characters

```Python
course = 'CSC1200' #( range is 0,6 )
	course[1] = 'S'
	course[4] = '2'
	course[-1] = will go backwards, so '0'
	course[-4] = '1'
```

#### Strings are immutable, which means they can't be changed.
- Suppose we have a string, word='quiat'and we realized that we really want character 3 to be 'e' (so that the word is 'quiet').
	- its tempting to think that we can use .word[3] to change a to e
	however it results in syntax

#### Searching a string
- Searching a squence for a particular item is a common thing to do
- For  example, we might want to see if a string contains a particular letter of sequence of letters. 
- Two built-in functions that come in handy when dealing with characters are [ord] and [chr]

#### String Traversal
- We often need to process a string character by character. Moving sequentially through the string one character at a time is called a traversal. 
- Example: print the characters of a string backwards
(while loop version)
```Python
def print_backwards( string ):
	curr_index = len(string) - 1
	while curr_index >= 0:
		print(string[curr_index], end='')
			curr_index -= 1
	print()

print_backwards('backwards')
print_backwards('yo banana boy')
```
#### Output: 
			sdrawkcab
			yob ananab oy 
(for loop version)
```Python
def print_backwards( string ):
	for 
```
Output:
			()

#### String Methods
- A method is a function that belongs to a partiular type or object, and we must use dot notation to access the method
- Some useful string methods include:
-upper - returns the string converted to all uppercase
-lower - returns the string converted to all lowercase
-isupper / islower - to check if a string is upper or lowercase (returns True or False)
-isdigit - returns True if all characters are numeric
-isalpha - returns True if all characters are alphabetic
-find 

Example:
```Python
word='quIT'
uc = word.upper()
uc
'QUIT'
lc = word.lower()
lc
'quit'
```

#### The in Operator
- The word [in] is a Boolean operator. For strings, it returns True if the first string is a substring of the second. 
1. A 

#### Relational Operators for Strings
- Several relational operators can be used with strings.
1. to check for equality: ==
2. To check if a string comes alphabetically before another: <
3. To check if a string comes alphabetically after another: >
- Note that ordering of characters is based on ASCII
```Python
fruit = 'apple'
fruit == 'apple'
True
fruit != 'banana'
True
```


