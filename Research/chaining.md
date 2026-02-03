_______
10-16-2023 | 04:46
Status: #Research 
Tags: #Cpp #CS-1310 #HashTable 

# [[chaining]] in C++
[[chaining]] handles [[Hash Table]] [[collision]]s by using a [[List]] for each [[bucket]], where each [[List]] may store multiple items that map to the same [[bucket]]. The insert operation first uses the item's [[key]] to determine the [[bucket]], and then inserts the item in that [[bucket]]'s [[List]]. Searching also first determines the [[bucket]], and then searches the [[bucket]]'s [[List]]. Likewise for removes. 

```cpp
HashInsert(hashTable, item) {
	if (HashSearch(hashTable, item->key) == NULL) {
		bucketList = hashTable[Hash(item->key)];
		node = Allocate new linked list node
		node->next = null;
		node->data = item;
		ListAppend(bucketList, node);
	}
}

HashRemove(hashTable, item) {
	bucketList = hashTable[Hash(item->key)];
	itemNode = ListSearch(bucketList, item->key);
	if (itemNode is not NULL) {
		ListRemove(bucketList, itemNode);
	}
}

HashSearch(hashTable, key) {
	bucketList = hashTable[Hash(key)];
	itemNode = ListSearch(bucketList, key);
	if (itemNode is not NULL)
		return itemNode->data;
	else
		return NULL;
}
```