________
02-06-2025 | 06:06
Status: #school 
Tags: #DesignOfAlgorithms

### Analysis of Algorithms
[[time efficiency]] (also called [[Time Complexity ( Big O-Notation )]]) 
- Running time/How fast an algorithm runs
[[space efficiency]] 
- Memory Space
- How many memory units are required by the algorithm, in addition to input & output space. 
- Also called [[space complexity]]
- Less important then time because we have so much space at our disposal. We can always add hard drives. We can't add time to a day. 

# Analysis Framework
- Input Size
- Basic Operation
- Running time formula
- Order of growth
- Best-case, average-case, & worst-case efficiency

##### Measuring An Input's Size
We measure an algorithm's efficiency as a function of a parameter, n, indicating the algorithm's input size. 
- Problems dealing with sorting, searching, finding smallest, etc. 
	$n$ = size of list (number of elements or nodes)
- Problems dealing with matrices
	$n$ = order of matrix
- Problems such as checking if a number is prime
	$n$ = number's magnitude
	(number of bits in the n's binary representation)

###### Finding the Number of Bits in $n$'s binary representation
The formula for finding the number of bits in $n$'s binary representation is: 
$$\begin{equation} b = \lfloor log_2n \rfloor + 1 \end{equation}$$

- $log_2n$ means the logarithm in base 2 of $n$. The  presence of a fractional part means $n$ is between powers of two. 

==Example: $log_2 49 = 5.615$ and so $49$ is between powers of two== 

- $\lfloor x \rfloor$ is the floor of $x$, which is the integer part of $x$. 

==Example: $\lfloor 5.322 \rfloor = 5$ (exponent of the highest power of two in the binary representation of 49)

- $+1$ takes the exponent to the next higher power of two. Think of this step as accounting for the $2^0$th place of your binary number, which then gives you its total number of bits. 

==Example: $5 + 1 = 6$ (so the number of bits in the binary representation $49$ is $6$)
- The binary number for $49$ is 110001, which is $6$ bits. 

==Example: What is the number of bits in the binary representation of $39,485,888$?==
b = $\lfloor log_2 39485888 \rfloor + 1$
b = $\lfloor 25.237 \rfloor + 1$
b = $25 + 1$
b = $26$ 

# Measuring Running Time
**Option 1:** We could measure running time based on ==number of seconds== but the drawback is that this would widely **vary based on the user's computer**.
**Option 2:** We could ==count the number of times each operation is executed.== However, this would be **difficult & usually unnecessary**.
**Option 3:** We could compute the ==basic operation== - this is the ==number of times the most important operation== of the algorithm occurs. **The basic operation is the operation contributing the most to the total running time**. 

### It is usually the most time-consuming operation in the algorithm's innermost loop. 
==Example:== for sorting algorithms it would be the **comparison**. 
==Another Example:== in math operations, the most time-consuming operation is **division**, then **multiplication**, and then **addition and subtraction**. 

# Analysis of Time Efficiency 
Count the number of times the algorithm's basic operation is executed on inputs of size n. 
**Running Time Formula:** $T(n) \approx c_{op}C(n)$ 
- $T(n)$ is the estimated **running time** of a program based on input size $n$.
- $c_{op}$ is the **execution time** of an algorithm's basic operation on a particular computer. 
- $C(n)$ is the **number of times the basic operation** needs to be executed for this algorithm. 

### Running Time Formula for Sequential Search
- The **Basic Operation** is comparison: $A[i] \neq K$ 
- Comparison will happen $n$ times so: $C(n)=n$ 
- Running time will be the execution time of the comparison times $n$. So, $T(n) = c_{op}*n$ 

==Example:== The sequential search algorithm basic operation runs in linear time. Therefore, $C(n) = n$. How much longer will the algorithm run if we **triple** its input size?
==Answer:== $3n$ 

==Another Example:== A given algorithm's runtime is $C(n) = log_2(n)$. How much will the function's value change if we **quadruple** its input size? 
==Answer:== $log_2 4n = log_2 4 + log_2 n = 2 + log_2 n$ 

# Overall Efficiency 
An algorithm's efficiency is determined by the part with a higher order of growth (its least efficient part). 
==Example:== If the basic operation of an algorithm happens $n^3 + 5n$ times, then the algorithm's efficiency is determined by $n^3$, since it has the highest order of growth. 

