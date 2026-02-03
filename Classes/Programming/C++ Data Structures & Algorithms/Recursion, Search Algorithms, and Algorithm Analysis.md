_____
08-23-2023 | 09:54
Status: #school #Research 
Tags: #CS-1310 #Cpp

### Recursion 
- Recursive algorithms solve problems by breaking them down into a series of smaller sub-problems, finding solutions to those sub-problems, and combining the solutions. 
- They do this by using recursive functions.

2 + 2 or (1 + 1)+(1 + 1) simplest version

##### Recursion
-  A base case is how we prevent infinite recursion. It returns a value without making any more recursive calls, and is how we know the recursion is DONE. 

##### Recursion
Basically, a recursive function has two cases:

- A base case, where the problem can be immediately solved 


```C++
int fib(int);

const int SIZE = 300;
int main()
{
	
}

int fib(int n)
{
    //if (n <= 0)
    //  return 0;                         // Base Case
    if (n == 1 || n == 2)
        return 1;                         // Base Case
    else
        return fib(n - 1) + fib(n - 2);   // Recursive
}
//1 1 2 3 5 8 13

```

```C++
void function (int num)   // can also be int
{
    if(num > 0) //recursive case
    {
        for (int x = 0; x<num; x++)
            cout << '*';
        cout << endl;
        function(num-1);
    }
                         // if int function return would go here ( return 0;)
}

if {
	return 0;
}
else {        //Recursive Case
    return function(num-1) + num;
}
//f(10) 10+f(9) (10 + 45)
//f(9) 9+36
//f(8) 8+28
//f(7) 7+21
//f(6) 6+15
//f(5) 5+10
//f(4) 4+6
//f(3) 6
//f(2) 3
//f(1) 1
//f(0) 0
```