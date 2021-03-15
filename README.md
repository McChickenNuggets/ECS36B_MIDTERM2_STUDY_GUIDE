# ECS 36B MIDTERM 2 STUDY GUIDE

## 1. If a data member is declared as private, protected or public in a base class, discuss how it can or cannot be accessed in a public member function of a derived class.

```c++
class Base{
public:
	int  m_public;  // can be accessed by anybody
protected:
	int  m_protected;  // can be accessed by Base members, friends, and derived classes
private:
	int  m_private;  // can only be accessed by Base members and friends (but not derived classes)
};

class  Derived: public  Base{
public:
	Derived(){
	m_public  =  1;  // allowed: can access public base members from derived class
	m_protected  =  2;  // allowed: can access protected base members from derived class
	m_private  =  3;  // not allowed: can not access private base members from derived class
	}
};

int  main(){
Base base;
base.m_public  =  1;  // allowed: can access public members from outside class
base.m_protected  =  2;  // not allowed: can not access protected members from outside class
base.m_private  =  3;  // not allowed: can not access private members from outside class
}
```
- Private inheritance makes all public and protected members of the base class private in the derived class

## 2. Discuss the difference between overloading and overriding a member function in a derived class.

|overloading | overriding |
|---|---|
|2 or more functions can have the same name, but different parameters.| Occurs when a function of the base class is given a new definition in a derived class|
|Functions cannot be overloaded if they differ in return type| Virtual function: function in the base class that is declared using the keyword **virtual** |
|Class has more than one method with the same name, but arguments are different.|It only works when objects are passed by pointer or references|

## 3. Give an example of a situation where it is necessary to define a virtual destructor.
Destructor can be virtual
- can be used to delete derived object through base class pointer 
- "when trying to delete a derived object through a base class pointer, and the base class has a non-virtual destructor, the results are undefined” C++ standards
- Release derived before releasing base
```c++
#include<iostream>
using namespace std;
class A
{
  public:
    A(int i) : val(i) { cout << "A::A called" << endl; }
    int val;
    virtual void print(void)
    { cout << "Value printed using A::print: " << val << endl; }
    virtual ~A(void) { cout << "A::~A called" << endl; }
};

class B : public A
{
  public:
    B(int i) : A(i) { cout << "B::B called" << endl; }
    int x;
    virtual void print(void)
    { cout << "Value printed using B::print: " << val << endl; }
    virtual ~B(void) { cout << "B::~B called" << endl; }
};

int main()
{
  A *pa = new B(3);
  pa->print();
  delete pa;
}

```
## 4. What is the feature that makes a base class an abstract class?
- A class that has one or more pure virtual functions is called an abstract class
- It is not possible to create an instance of an abstract class
- The role of an abstract class is to specify an interface. No implementation is provided.
- Using the abstract class: inherit the interface only

## 5. When designing a class hierarchy involving classes A and B, what are the two questions that must be asked to determine whether class B should be derived from class A?
- Is a B a kind of A?
- Can a B do everything that an A can do?

## 6. What does the following code do?
```c++
void drawSquares(Shape **p, int size){
	Square *sp;
	for ( int i = 0; i < size; i++ ){
	sp = dynamic_cast<Square*>(p[i]);
	if ( sp )
		sp->draw();
	}
}
```
-  implement a function that takes an array of pointers to Shapes as an argument and draws Squares only
- Obtain type information during run time 
## 7. Explain why a factory member function should be a static member function.
- It provides more intuitive names
- Static factory methods can access the private members of that particular class
- Static factory methods are not required to create new objects when every time it is invoked
## 8. Write a function template sort that takes two references to generic objects and switches them if the first argument is larger than the second. It is only assumed that operator<(), operator=()and a default constructor are defined for the objects considered.
```c++
template< typename T >
void sort( T &v1, T &v2 )
{
	if(v2<v1){
		T temp = v1;
		v1 = v2;
		v2 = temp;
	}
}
```
## 9. Write a program that reads integers from input until an end-of-file is found, and then prints all the integers read on output in reverse order, with one integer per line.
```c++
#include<iostream>
using namespace std;
int main(void){
        int *arr = new int[10000];
        int i=0;

        do{
                cin>>arr[i];
                i++;
        }while(cin);

        for(int j = i-2;j>=0;j--){
                cout<<arr[j]<<" "<<endl;
        }
        cout<<endl;

}                  
```
## 10. Write a program that reads integers from input until an end-of-file is found, and then prints the sum of all integers on output.
```c++
#include<iostream>
using namespace std;
int main(void){
        int *arr = new int[10000];
        int i=0;

        do{
                cin>>arr[i];
                i++;
        }while(cin);

        int sum=0;
        for(int j = i-2;j>=0;j--){
                sum+=arr[j];
        }
        cout<<sum<<endl;
}                
```
