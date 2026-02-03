#school #CS-1300 

```c++
while(input < 0 || input > 24) {
	cin.clear(); //input validation
	cin.ignore(255, '\n');
	cout << "Invalid Input";
	cin >> input;
}
```
