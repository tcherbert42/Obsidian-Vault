_______
10-16-2023 | 03:59
Status: #Research 
Tags: #Cpp #CS-1310 


# [[Hash Table]]s in C++
A [[Hash Table]] is a data structure that stores unordered items by mapping (or [[hashing]]) each item to a location in an [[Array]] (or [[Vector]]). Ex: Given an [[Array]] with indices $0..9$ to store integers from $0..500$, the [[modulo]] (remainder) operator can be used to map $25$ to index $5$ (25 % 10 = 5), and $149$ to index $9$ (149 % 10 = 9). 

A [[Hash Table]]'s main advantage is that searching (or inserting / removing) an item may require only $O(1)$, in contrast to $O(N)$ for searching a [[List]] or to $0(log N)$ for binary search. 

- In a [[Hash Table]], an item's [[key]] is the value used to map to an index. For all items that might possibly be stored in the [[Hash Table]], every [[key]] is ideally unique, so that the [[Hash Table]]'s [[algorithm]]s can search for a specific item by that [[key]].
- Each [[Hash Table]] [[Array]] element is called a [[bucket]]. A [[hash function]] computes a [[bucket]] index from the item's [[key]]. 

### [[Hash Table]] operations
A common [[hash function]] uses the [[modulo]] operator %, which computes the integer remainder when dividing two numbers. Ex: For a $20$ element [[Hash Table]], a [[hash function]] of [[key]] % $20$ will map [[key]]s to [[bucket]] indices $0$ to $19$.

A [[Hash Table]]'s operations of insert, remove, and search each use the [[hash function]] to determine an item's [[bucket]]. Ex: Inserting $113$ first determines the [[bucket]] to be $133$ % $10 = 3$.

- For Ex: A [[modulo]] [[hash function]] for a $50$ entry [[Hash Table]] is: key % $50$
- Key % $1000$ maps to indices $0$ to $999$. 



