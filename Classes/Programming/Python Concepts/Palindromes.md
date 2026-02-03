#python 
#### Reversing a number in python

```Python
num = 1234
remain = num % 10
print(remain)
```
##### Prints the first number in the sequence

```Python
#input number
num = 1234
# reversed number
reversed_num = 0

while(num>0):
remain = num % 10
reversed_num = reversed_num * 10 + remain
num = num // 10

print(reversed_num)
```
##### Reverses the number(num)
