_______
10-16-2023 | 04:45
Status: #Research 
Tags: #Cpp #CS-1310 #HashTable

# [[collision]]s 
A [[collision]] occurs when an item being inserted into a [[Hash Table]] maps to the same [[bucket]] as an existing item in the [[Hash Table]]. Ex: For a [[hash function]] of key % $10$, $55$ would be inserted in [[bucket]] $55$ % $10$ = $5$; later inserting $75$ would yield a [[collision]] because $75$ % $10$ is also $5$. 

Various techniques are used to handle [[collision]]s during insertions, such as [[chaining]] or [[open addressing]]. 
- [[chaining]] is a [[collision]] resolution technique where each [[bucket]] has a list of items (so bucket 5's list would become 55, 75). 
- [[open addressing]] is a [[collision]] resolution technique where [[collision]]s are resolved by looking for an empty [[bucket]] elsewhere in the table (so 75 might be stored in bucket 6). 