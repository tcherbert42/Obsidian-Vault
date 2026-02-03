---

---
___________
08-21-2023 | 09:54
Status: #school #Research 
Tags: #CS-1310 #Cpp

#### Classes & Structs
Classes and Structs are pretty similar
- They both bundle related variables/data
- The syntax of classes expands on syntax of structs
- An object is an instance of a class the same way a variable can be an instance of a struct. 

#### Classes 
(They're basically structs that also have functions)
A class has:
- Attributes: variables that describe a class's properties
- Member Functions: functions that describe a class's behavior 

```C++
#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle 
{
	private:
		double width;
		double length;
	public:
		void setWidth(double);
		void setLength(double);
		double getWidth() const;
		double getLength() const;
		double getArea() const;
};

#endif
```

#### Encapsulation
The kind of word that shows up on exams! (hint hint)
- It's when we bundle data together (into a capsule)
- It also lets us hide and restrict access to data (yes, this is important)

```C++
struct rectangle
{
	int length;
	int width;
};

int main()
{
	Rectangle rect1;
cout << rect1.getArea();

	int length, int width; //does the same thing as above
cout << length x width;    //
}
```

#### Reusability
- Software is never written by just one person. Every program you've written has used objects (cin, cout, etc)
- Classes are great because they allow for modularity in your code, which forms the basis for Object-Oriented Programming (OOP).

### Namespaces 
