---
layout: post
title: OOP Comparison between C++ and Python
key: 20201115
tags:
  - Python
  - C++
  - OOP
---


1. Inheritance
2. Polymorphism
3. Encapsulation
4. Abstraction

## class definition


### C++

```c++
//class
class Points
{
public:
	//constructor
	Points(int x, int y){
		this->_x = x;
		this->_y = y;
	}

	//print function
	void print() const{
		std::cout<<this->_x<<" "<<this->_y<<std::endl;
	}
	//public data members
	string alias = "position of point";
private:
	//private data members
	int _x;
	int _y;
};
```
<!--more-->

* create instances:
```c++
//create temporary Points using constructor, implicitly call the copy
//constructor of Points to copy from that temporary into point1
Points point1 = Points(1,1,1);

//explicit constructor
Points point2(2,2,2);

//invoke default constructor, implicitly calling default constructor
Points point_default;

std::cout<<"default constructor"<<endl;

point_default.print();

//accessing private data member
std::cout<<point1.getX()<<" "<<point1.getY()<<std::endl;

//print function
point1.print();

//accessing public data member
std::cout<<point1.alias<<std::endl;
```

```
default constructor
0 0
1 1
1 1
position of point
```

1. `;` after class `{}`
2. `this` is pointer, not reference, accessing current object data member needs to use this form: `this->data_member`
3. declare an instance must predeclare it's class type, for instance, `SoftwareEngineer student1 = SoftwareEngineer()` is correct, while `student1 = SoftwareEngineer()` can only be used in Python.
4. private class members are accessible by the member functions of this class only while public members are accessible everywhere.


### Python

```python
# class
class SoftwareEngineer:
    # class attribute
    alias = 'SE'

    def __init__(self,name,age,level,salary):
        #instance attribute
        self.name = name
        self.age = age
        self.level = level
        self.salary = salary
```

```python
#create instance
student1 = SoftwareEngineer('Max',20,'Junior',5000)
#access instance attribute
print(student1.name,student1.alias,student1.salary)
#access class attribute
print(SoftwareEngineer.alias)
```

```
Max SE 5000
SE
```

1. create class
2. class attribute
3. instance attribute
4. create instance
5. instance vs class

## method and functions

### Python

#### instance method with input argument and return type

```python
class SoftwareEngineer:
	...
	# instance method
    def code(self):
        print(f"{self.name} is writing code...")
    
    def code_in_language(self,language):
        print(f"{self.name} is writing code in {language}...")
    
    def information(self):
        information = f"name = {self.name}, age = {self.age}, level = {self.level}"
        return information
    ...
```

```python
student1.code()
student1.code_in_language('pyhton')
print(student1.information())
```
```
Max is writing code...
Max is writing code in pyhton...
name = Max, age = 20, level = Junior
```

#### python special method

* `__eq__`

Comparison two instances without defining `__eq__` would result in false since two instances memory locations are not the same:

```python
student2 = SoftwareEngineer('Max',20,'Junior',5000)
print(student1 == student2) #comparing memory
```
```
False
```

* `__str__`

this method is called whenever object is converted to string

for instance:

```python
print(student2)
<__main__.SoftwareEngineer object at 0x106996070>
```
now adding `__str__` method to `SoftwareEngineer` class:

```python
...
def __str__(self):
        information = f"name = {self.name}, age = {self.age}, level = {self.level}"
        return information
...
```

```python
print(student2)
name = Max, age = 20, level = Junior
```

```python
class SoftwareEngineer:
	    # python default method
    def __str__(self):
        information = f"name = {self.name}, age = {self.age}, level = {self.level}"
        return information
    
    #python equal method
    def __eq__(self,other):
        return self.name == other.name and self.age == other.age
```

#### class method

```python
class SoftwareEngineer:
	...
    #class method
    def entry_salary2(age):
        if age < 10:
            return "without object <10"
        else:
            return "without object >=10"

	    #instance method
    def entry_salary1(self,age):
        if age < 25:
            return 5000
        elif age <30:
            return 7000
        return 9000
    
    #cannot access self attribute, decorator
    @staticmethod
    def entry_salary(age):
        if age < 25:
            return 5000
        elif age < 30:
            return 7000
        return 9000
    ...
```   

``` python
print(student2.entry_salary(30))
print(SoftwareEngineer.entry_salary(27))
print(SoftwareEngineer.entry_salary2(11))
```

```
9000
7000
without object >=10
```

Note that using both decorator and class method, accessing self attribute is not allowed since it is not tied to specific instance.
{:.warning}


How ever calling `entry_salary2` from instance is not allowed since it didn't pass object as input:

```python
print(student2.entry_salary2(11))
```

```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-79-76716bf772b6> in <module>
----> 1 print(student2.entry_salary2(11))

TypeError: entry_salary2() takes 1 positional argument but 2 were given
```

### C++  

#### Default constructor

```c++
class Points{
public:
	Points(int x=0, int y=0){
		this->x=x;
		this->y=y;
	}
	...
private:
	int x;
	int y;
}
```

```c++
//defaut constructor
Points point3 = Points();
point3.print();
```

```
0 0
```

#### constructor initializer list

```c++
class Points{
public:
	Points(int x=0, int y=0):x(x),y(y){}
	...
private:
	int x;
	int y;
}
```

* When do we use initializer list

1. for initialization of non-static const data members

```c++
class Points{
public:
	Points(int x,y):x(x),y(y){};
private:
	const int x;
	const int y;
}
```

* initializer list is a copy constructor, we don't need and cannot all the assignment operator which means we are avoiding one extra operation.
* initializer list initializes objects first, even if you do not explicitly initialise them there, the compiler will do for it. const object can only initialised, cannot be assigned


2. for initialization of reference members
3. for initialization of member objects which do not have default constructor
4. for initialization of base class members
5. when constructor's parameter name is same as data member


Reference: 
1. https://www.geeksforgeeks.org/when-do-we-use-initializer-list-in-c/
2. https://stackoverflow.com/questions/355258/why-must-const-members-be-initialized-in-the-constructor-initializer-rather-than



#### get and set

Public getters and setters for private variables: Member variables are suually declared private to prevent direct access. Instea, public getter and setter are defined to retrieve and modify the private member variable.

```c++
class Points{
    ...
//set function
    void setX(int x){
        this->_x = x;
    }
    //get function
    int getX() const{
        return this->_x;
    }
    //set function
    void setY(int y){
        this->_y = y;
    }
    //get function
    int getY() const{
        return this->_y;
    }
    //set function
    void setXY(int x, int y){
        this->_x = x;
        this->_y = y;
    }
    ...
}
```

#### object initialization with dynamic/static memory

```c++
    //object pointer
    Points *point3;
    point3 = new Points(); 
    point3->print();

    Points *point4 = new Points(4,4);
    point4->print();

    //segmentation fault 11 since object pointer will not implicitly call default constructor
    // Points *ptr_point;
    // std::cout<<"default pointer of object"<<std::endl;
    // ptr_point->print();
    // std::cout<<"default pointer of object"<<std::endl;


    //remove storage via delete
    delete point3;
    delete point4;

    //object reference
    Points &point5 = point2;
    point5.print();

    //object pointer points to already existed object
    Points *point6 = &point1;
    point6->print();

    //array of objects with static memory and default constructor
    Points ptsArray[2];
    //below is not working since above is already use default constructor for all elements
    // ptsArray[0] Points();
    ptsArray->print();
    ptsArray[1].print();
    (ptsArray+1)->print();


    //array of objects with static memory and customized constructor
    Points pts_array[3] = {Points(11,11),Points(21,21),Points(31,31)};

    pts_array[0].print();
    pts_array[1].print();
    pts_array[2].print();

    //array of object pointers with dynamical memory
    Points *pts_arrays = new Points[2];
    pts_arrays[0].print();
    pts_arrays[1] = Points(41,41);
    (pts_arrays+1)->print();

    //array of object pointers with dynamical memory using malloc, implicitly calling constructor
    Points * arr = (Points*)malloc(sizeof(Points)*2);
    //cannot calling constructor if object data members have const
    arr[0] = Points();
    arr[1] = Points(51,51);
    arr[0].print();
    arr[1].print();

    //array of object pointers with dynamical memory, this will defautly call constructor
    Points *ptr_points = new Points[3];
    ptr_points[1].print();
    ptr_points[0] = Points(51,51);
    ptr_points[0].print();


```  

### Inheritance

#### Inheritance in Python

* Base class

```python
class Employee:  #inherits,extend,override
    def __init__(self,name,age,salary):
        self.name = name
        self.age = age
        self.salary = salary
    
    def work(self):
        print(f"{self.name} is working...")
```

* child class

```python
class SoftwareEngineer(Employee):
    #extend
    def __init__(self,name,age,salary,level):
        super().__init__(name,age,salary)
        self.level = level
    #overide
    def work(self):
        print(f"{self.name} is coding...")
    
    def debug(self):
        print(f"{self.name} is debugging...")
```

```python
se = SoftwareEngineer('Max',25,5000,'Junior')
print(se.name,se.age)
se.work()
se.debug()
```

```
Max 25
Max is coding...
Max is debugging...
```

* child class

```python
class Designer(Employee):
    def drawing(self):
        print(f"{self.name} is drawing...")
    #override
    def work(self):
        print(f"{self.name} is designing...")
```

```python
d = Designer('Philipp',27,7000)
print(d.name,d.age)
d.work()
d.drawing()
```

```
Philipp 27
Philipp is designing...
Philipp is drawing...
```

#### Inheritance in Python

* Example

![img](https://raw.githubusercontent.com/hadleyhzy34/OOP-Comparison-between-C-and-Python/main/source/c%2B%2B_inheritance.png)  

##### Subclass header
```c++
/* Header for Moving 3D Points with int coords (MovablePoint.h) */
#ifndef MOVING_POINT_H
#define MOVING_POINT_H
 
#include "Points.h"   // Include header of the base class
 
class MovablePoint : public Points { // MovablePoint is a subclass of Point
private:
   int xSpeed, ySpeed;
 
public:
   MovablePoint(int x, int y, int xSpeed = 0, int ySpeed = 0);
   int getXSpeed() const;
   int getYSpeed() const;
   void setXSpeed(int xSpeed);
   void setYSpeed(int ySpeed);
   void move();
   void print() const;
};
 
#endif
```
##### Subclass/derived class implementation
```c++
#include "MovablePoints.h"   // Include header of the base class

//note that do not set default argument here, otherwise it could cause redefinition issue
MovablePoint::MovablePoint(int x, int y,int xSpeed,int ySpeed)
    :Points(x,y),xSpeed(xSpeed),ySpeed(ySpeed){}

int MovablePoint::getXSpeed() const{
    return xSpeed;
}

int MovablePoint::getYSpeed() const{
    return ySpeed;
}

void MovablePoint::setXSpeed(int xSpeed){
    this->xSpeed = xSpeed;
}

void MovablePoint::setYSpeed(int ySpeed){
    this->ySpeed = ySpeed;
}

void MovablePoint::print() const{
    std::cout<<"Movable";
    Points::print();
    std::cout<<" Speed="<<xSpeed<<" "<<ySpeed<<std::endl;
}

void MovablePoint::move(){
    Points::setX(Points::getX()+xSpeed);
    Points::setY(Points::getY()+ySpeed);
}
```

* When the subclass construct its instance, it must construct a superclass object, which it inherited.
* The subclass does not have direct access to superclass' private members x and y. To initialize these inherited members, the subclass constructors invokes the superclass constructor which is `public`, in the member initializer list.
* You need to use the member initializer list to invoke the superclass Point's constructor to initialize the superclass, before initializing the subclass. Object data member can only initialized via member initializer list.
* If you did not explicitly invoke the superclass' constructor, the compiler implicitly invoke the superclass' default constructor to construct a superclass object.
* To use the superclass members, use scope resolution operator in the form of `SuperclassName::memberName`. For example, Point::print(), Point::getX().
{:.warning}  

##### Test driver
```c++
/* Test Driver Program for MovablePoint (TestMovablePoint.cpp) */
#include <iostream>
#include "Points.h"
#include "MovablePoints.h"  // included "Point.h"
 
int main() {
   Points p1(4, 5);  // superclass
   p1.print();      // Point @ (4,5)
   std::cout << std::endl;
 
   MovablePoint mp1(11, 22); // subclass, default speed
   mp1.print();       // MovablePoint @ (11,22) Speed=(0,0)
   std::cout << std::endl;
   mp1.setXSpeed(8);
   mp1.move();
   mp1.print();       // MovablePoint @ (19,22) Speed=(8,0)
   std::cout << std::endl;
 
   MovablePoint mp2(11, 22, 33, 44);
   mp2.print();  // MovablePoint @ (11,22) Speed=(33,44)
   std::cout << std::endl;
   mp2.move();
   mp2.print();  // MovablePoint @ (44,66) Speed=(33,44)
   std::cout << std::endl;
}
```

Note that private data member in the superclass is not accessible in the subclass. For example, in the function `move()` of MovablePoint, you cannot reference `_x` of superclass `Points` directly.

```c++
void MovablePoint::move() {
   x += xSpeed;     // error: 'int Point::x' is private
//   Point::setX(Point::getX() + xSpeed);
   Point::setY(Point::getY() + ySpeed);
}
```
However, if we make `_x` protected instead of private, the subclass can access `_x` directly.

```c++
// Superclass Point
class Point {
protected:
   int x, y;
......
};   

// Subclass MovablePoint
class MovablePoint : public Point {
   ......
}
 
void MovablePoint::move() {
   x += xSpeed;
   y += ySpeed;
}
```  

### Polymorphism

#### Polymorphism in Python

```python
employees = [SoftwareEngineer("Max", 25, 6000, "Junior"),
             SoftwareEngineer("George", 25, 6000, "Junior"),
             Designer("Lisa", 25, 6000),
            ]
```

```python
def motivate_employees(employees):
    for employee in employees:
        employee.work()

motivate_employees(employees)
```

```
Max is coding...
George is coding...
Lisa is designing...
```

#### Polymorphism in C++

##### driver program

```c++
int main() {
    //object pointer
    Points *ptr1 = new MovablePoint(11,12,13,14);
    ptr1->print(); //run baseClass version->(virtual)->run subclass version
    delete ptr1;

    //using object reference
    MovablePoint mp(21,22,23,24);
    Points *ptr2 = &mp;
    ptr2->print(); //run baseclass version->(virtual)->run subclass

    //using object with explicit constructor
    Points p3 = MovablePoint(31,32,33,34); //upcast, create baseclass object using subclass constructor
    p3.print(); //run baseClass version->virtual->run subclass
}
```

Note that a subclass instance(mp) can be substituted for a superclass reference. Once substituted, only the superclass functions can be called, not the subclass' one.

```c++
// Point.h
class Points {
   ......
   virtual void print() const;
}
```

They keyword `virtual` determines which method is used if the method is invoked by a pointer. Without `virtual`, the program chooses the method based on the pointer type. With `virtual`, the program chooses the method based on the type of the object pointed to.

Take note that virtual functions work on object pointers/references, but not on regular objects.
{:.warning}

* Using keyword virtual on a superclass function makes the function virtual for the superclass, as well as ALL its subclasses.  
* If a virtual function is invoked using a pointer (or reference), the program uses the method defined for the object type instead of the pointer type. This is called `dynamic binding` or late binding, contrast to static binding during the compile time.  
* It is recommended that functions to be overridden in the subclass be declared virtual in the superclass.  
* Constructor can't be virtual, because it is not inherited. Subclass defines its own constructor, which invokes the superclass constructor to initialize the inherited data members.  
* Destructor should be declared virtual, if a class is to to be used as a superclass, so that the appropriate object destructor is invoked to free the dynamically allocated memory in the subclass, if any.  
* Friends can't be virtual, as friends are not class member and are not inherited.  
* If you override function in the subclass, the overridden function shall have the same parameter list as the superclass' version.


#### Upcasting VS Downcasting

Normally C++ does not allow you to assign an address of one type to pointer or reference of another type. For example:

```c++
int i=8;
double *ptr1 = &i; //error
double &ref = i;    //error
```

However, a pointer or reference of superclass can hold a subclass object without explicit type cast:

```c++
//using object reference
MovablePoint mp(21,22,23,24);
Points *ptr2 = &mp;
Points &ptr2 = mp;
```

The reverse option, converting a superclass reference or pointer to subclass, is called downcasting. Downcasting requires explicit type cast.

```c++
//downcast
Points p4();
MovablePoint *ptr3 = ptr1;
MovablePoint *ptr4 = &p4;
```

```c++
main1.cpp:23:19: error: cannot initialize a variable of type 'MovablePoint *' with an lvalue of
      type 'Points *'
    MovablePoint *ptr3 = ptr1;
                  ^      ~~~~
main1.cpp:24:19: error: cannot initialize a variable of type 'MovablePoint *' with an rvalue of
      type 'Points (*)()'
    MovablePoint *ptr4 = &p4;
```

Explicit downcast and `dynamic_cast`  

```c++
    //downcast implicitly and explicitly
    Points p4();
    // MovablePoint *ptr3 = ptr1;
    // MovablePoint *ptr4 = &p4;
    std::cout<<"test5: ";
    MovablePoint *ptr5 = (MovablePoint*)ptr1;
    ptr5->print();
    std::cout<<std::endl;

    //downcast using dynamic cast
    std::cout<<"test6";
    MovablePoint *ptr6 = dynamic_cast<MovablePoint*>(ptr1);
    std::cout<<"test6:"<<std::endl;
    ptr6->print();
    std::cout<<"test6"<<std::endl;
```

#### typeid

The operator typeid returns a reference to an object of class `type_info`. You can use `type_info` member function `name()` to get the type name. For example:

```c++
/* Test Driver Program for MovablePoint (TestMovablePoint.cpp) */
#include <iostream>
#include <typeinfo>
#include "Points.h"
#include "MovablePoints.h"  // included "Point.h"
 
int main() {
    //object pointer
    Points *ptr1 = new MovablePoint(11,12,13,14);
    std::cout<<typeid(*ptr1).name()<<std::endl;

    MovablePoint *ptr2 = dynamic_cast<MovablePoint*>(ptr1);
    std::cout<<typeid(*ptr2).name()<<std::endl;

    delete ptr1;

    Points p2;
    std::cout<<typeid(p2).name()<<std::endl;

    MovablePoint mp2(1,2,3,4);
    std::cout<<typeid(mp2).name()<<std::endl;
}
```

Note that the number in front of the name gives the length of the string.
{:.warning}



























