___________
09-18-2023 | 09:54
Status: #school #Research 
Tags: #CS-1310 #Cpp 

# Segmentation Fault
- Will probably see [[Segmentation Fault]] in Program2, it means:
pointer that is NULL and don't realize

```Cpp
//Example linkedlist constructor and node's from start of class
class linkedlist
{
	private:
	struct node
	{
		int value;
		node* next;
	}
	node* head;
	node* tail; //add tail if neccessary
	int length;

	public:
	linkedlist() // Constructor 
	{
		head = NULL;
		length = 0; 
	}
	~linkedlist() //think about "What has been dynamically allocated?"
	{
		node* curr = head;
		node* prev = NULL;
		while(curr)
		{
			prev = curr;
			curr = curr->next;
			delete prev; 
		}
	}

	void append(int val)
	{
		node* newNode = new node; 
		newNode->value = val;
		newNode->next = NULL;

		//node* curr = head;    <- if doing without tail
		//while(curr->next)
		//{
			//curr = curr->next;
		//}
		//curr->next = newNode; 

		if(!head) //equivalent to head == NULL
		{
			head = newNode; 
			tail = newNode;
			return;
		}
		else:
		{
			tail->next = newNode;
			tail = newNode;  
		}
	}
}
```

```Cpp
Object* obj = NULL;
obj->attr;
```
