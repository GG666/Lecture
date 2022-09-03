# Class

[TOC]

## A Class

A class is like a struct, it does not have a entity. It just like some blueprints or templates(just like other data types). We have to declare a class variable to create an entity. To put it shortly,  Class is a concept while objects are instances of a class.

```C++

class class_name{
    public:
        public_data_members
        public_member_functions
    private:
        private_data_members
        private_member_functions
};
```

- The naming convention of class is the same as other variables. In practice, we usually put first letter in uppercase.
- The braces({}) indicates the range of the class. (The contents are in {})
- Data members are the variables in class, also called member variables or attributes.
- Member functions are the functions that declared in class. Also called method or behavior.
- Public and private. Public members can be accessed from outside the class. Private members can only be accessed from the member function of the class.
- A class entity has it own data members, but all the class entities share a same member functions.

Similiar to struct, we can use the '.' operator to access the member of the class.

The only difference of class and struct in C++ is that struct-related functions are all public functions.

```C++
#include <iostream>

using namespace std;

class CRectangle{
    int width, height;
    public:
    // constructors and destructors
    CRectangle();
    CRectangle(int, int);
    ~CRectangle();
    
    // methods
    int area(){
        return width * height;
    }
};
CRectangle::CRectangle(){
    width=1;
    height=1;
}
CRectangle::CRectangle(int w, int h){
    width=w;
    height=h;
}

int main()
{
    CRectangle a;
    CRectangle b(8,7);
    // cout<<a.width<<" "<<a.height<<endl;
    cout<<a.area()<<endl;
    cout<<b.area()<<endl;

    return 0;
}

```
<練習>Read the code above and test it to understand the basic of class.

### class member

#### Member variables
Also called data members. Data members can be viewed as the  attributes or properties of an object.

#### Member functions
Member functions also called as behaviors or methods.

### Public and Private member

Private: Private member can only access by the member function of the class.

Public: can be accessed by members of its class as well as members of any other class and non-member functions, including main function.

```C++
#include<iostream>
using namespace std;


class Jet {
private:
    float acc, vel;
    float getTime();
public:
    void setValues(float x, float y){
        acc=x;
        vel=y; //Sets the acceleration and velocity
    }
    float getDisplacement() {//Returns the displacement of the jet
        return (vel*getTime());
    }
};
float Jet::getTime() { 
    return vel/acc;
}
int main(){
    Jet J;
    cout<<J.getTime()<<endl;
}

```


### new and delete

```C++
int main() {
    Jet plane1; //Instantiates plane1
    Jet *plane2;
    plane2=new Jet(); //Instantiates plane2
    plane1.setValues(40, 65);
    plane2->setValues(30,20);
    delete plane2;
    // plane2 is manually destroyed
    return 0;
    // plane1 is automatically destroyed
}
```

### constructor and destructor

#### constructor
Constructor is the function with the same name of the class. Constructor will be invoked automatically when a class instance is initialized.
We often use it to initialize data members.

```C++
class Jet{
public:
    Jet(){
        ...
    }
}
```

1. Constructor has no return type
2. It can have parmeters.
3. It has the same name as the class.
4. Constructor function is automatically called when the class object is declared.
5. It should be public so the outside function can call it.
6. A class can have many constructors.(function overloaded)

#### destructor

1. Function with the same name as the class but preceded with a tilde character.
2. Will be invoked when an object is destroyed.

```C++
~Jet(){
    ...
}
```


```C++
#include <iostream>
using namespace std;
class test{
private:
    int value;
public:
    test() { value=10; }
    int getValue1(void){
        return value;
    }
    int& getValue2(void){
        return value;
    }
    void showValue(void) {
        cout<<"Value: "<<value<<endl;
    }
};

int main(){
    test t;
    int v1;
    t.showValue(); //10
    v1=t.getValue1();
    v1++;
    t.showValue(); //10
    int & v2=t.getValue2();
    v2++;
    t.showValue(); //11
    return 0;
}
```

< problem >


```C++
#include <iostream>
using namespace std;
int bcount=0;
class Box {
private:
    float side1, side2, side3;
public:
    Box(float s1, float s2, float s3){
        side1=s1; side2=s2; side3=s3;
        bcount++;
        cout<<"BOX Generated!"<<endl;
     }
    ~Box(){ 
        bcount--;
        cout<<"\t\tBox destroyed!\n";
    }
    float getVolume(){
        return side1 * side2 * side3;
    }
};

float addBoxes(Box b1, Box b2){
    cout<<"\t\tAdding boxes:\n";
    cout<<"\t\t"<<bcount<<" boxes built so far.\n";
    return b1.getVolume()+b2.getVolume();
}
int main(){
    Box a(1,2,3),b(2,3,4);
    cout<<bcount<<" boxes built so far.\n";
    cout<<"\t\tTotal volume = "<<addBoxes(a, b)<<endl;
    cout<<bcount<<" boxes built so far.\n";
    return 0;
}
```

Consider a class whose constructor allocates memory dynamically. When the object's copy is destroyed, the destructor will free memory allocated for the original object, which will destroy the original object.
![](https://i.imgur.com/V7xjXZr.png)

```C++
#include<iostream>
using namespace std;

class Foo {
    int * bar; 
public:
    Foo() {
        bar=new int(3);
    }
    ~Foo() {
        delete bar;
    }
};

Foo f;
void func(Foo x){
    return;
}
int main(){
    func(f);
    return 0;
}
```

#### copy constructor

The copy constructor will be automatically called when 
1. An object is passed to a function
2. An object is used to initialize another object in a declaration statement
3. An object is returned from a function(depends on compiler implements)

Copy constructor has only one parameter, the reference to the object to be copied.

```C++
class name(const class_name & object_name){
    // body of copied constructor
}
```

```C++
#include <iostream>
using namespace std;
class Test{
// private:
    int x, y;
public:
    Test(int a, int b){
        x=a;
        y=b;
        cout<<"\tCall Normal Constructor"<<endl;
    }
    Test(const Test &p){
        x=p.x;
        y=p.y;
        cout<<"\tCall Copy Constructor"<<endl;
    }
    ~Test(){
        cout<<"\tCall Destructor, Destroy " << x << ' ' << y <<endl;
    }
    void setX(int a){
        x=a;
    }
    void setY(int b){
        y=b;
    }
    void showXY(){
        cout<<"X = "<<x<<" Y = "<<y<<endl;
    }
};
Test center(Test T){ //and returns the object
    T.setX(512);
    T.setY(512);
    return T;
}
int main(){
    Test p1(10, 20); //Calls regular constructor
    p1.showXY();
    Test p2 = p1; //Calls the copy constructor
    p2.showXY();
    p2 = center(p1); //Calls the copy constructor twice
    p2.showXY();
    p1.showXY(); // like normal function, it would no change p1 value
    return 0;
}
```

- The sum of calls of normal constructors and copy constructors are equal to the number of calls of destructors.

- If a class doesn't have an explicit copy constructor, the compiler will create default copy constructor, the default copy constructor will simply make an identical (bit-by-bit) copy of the object.

![](https://i.imgur.com/H1k1lB5.png)


### Friend class and friend function

#### friend funciton

Have to be declared in the class preceded by the keyword "friend".

```C++
#include <iostream>
using namespace std;
class Count{
    friend void setX(Count &c, int val){
        c.x=val;
    }
public:
    Count(){
        x=0;
    }
    void print(){
        cout << x << endl; 
    }
private:
    int x;
};
int main(){
    Count counter; // create Count object
    cout << "counter.x : ";
    counter.print();
    setX(counter, 8);
    cout << "counter.x after call to setX: ";
    counter.print();
}
```

#### friend class

A class can be a friend of other classes. All the member functions in the friend class can access the private members of its friend.

#### friendship relation

There are many points of friend relations that are like human friendship.
- It is not reverse, if A say it has B as its friend, does not mean that B regard A as its friend. 
- It is not transitive. If A is a friend of B and B is a friend of C, doesn't means that A is a friend of C.

#### "this" pointer

The this pointer stores the address of an object. In C++, We usually ignore it and let the compiler deal with it implicitly. The programmar can use the pointer explicitly as well.

```C++
#include <iostream>
using namespace std;
class Pixel{
    int x, y;
public:
    Pixel(){
        cout<<"-> Pixel created!"<<endl;
        x=0;
        y=0;
    }
    ~Pixel(){
        cout<<"-> Pixel destroyed!"<<endl;
    }
    // void setCoord(int x1, int y1){
    //     x=x1;
    //     y=y1;
    // }
    void setCoord(int x, int y){
        this->x=x;
        this->y=y;
    }
    void getCoord(){
        cout<<"Pixel's coordinates:"<<endl;
        cout<<"X="<<x<<" Y="<<y<<endl;
 }
    Pixel move_10(){
        this->x = this->x + 10;
        this->y = this->y + 10;
        return *this;
    }
};

int main(){
    Pixel p1, p2;
    int x1, y1;
    cout<<"Enter X and Y coordinates =>";
    cin>>x1>>y1;
    p1.setCoord(x1,y1);
    p1.getCoord();
    p2 = p1.move_10();
    p2.getCoord();
    p1.getCoord();
}

```

### static members

Static members belong to the class itself. No matter how many objects have been created, the program creates only one copy of each static member. All the objects of a class share the same copy of a static member. All the static members exist in memory before any object is initialized.

```C++
#include <iostream>
using namespace std;
class Node{
public:
    static int count;
    int num;
    Node(){
        num=1;
        count++;
    }
    ~Node(){
        count--;
    }
    void print(void);
    void add(void)
        num++;
    }
};
void Node::print(){
    cout<<"count= "<<count<<" num= "<<num<<endl;
}
//Allocates memory for static data members
int Node::count=0;

int main(){
    cout<<"\ncount= "<<Node::count<<endl;
    //cout<<"\nnum= "<<Node::num<<endl; //ERROR
    Node *n1, *n2, *n3;
    n1=new Node();
    n2=new Node();
    n3=new Node();
    n1->add();
    n1->print();
    n2->print();
    n3->print();
    cout<<"\ncount "<<Node::count<<endl;
    delete n1;
    cout<<"\ncount "<<Node::count<<endl;
    return 0;
}
```
#### static member function

A static member function is not attached to
any object. And an object is not needed when calling static member functions.

```C++
#include <iostream>
using namespace std;
class Node {
private:
    static int count;
public:
    int num;
    Node(){
        num=1;
        count++; 
    }
    ~Node(){
        count--;
    }
    void print(void);
    void add(void){
        num++;
    }
    static int getCount(void) {
        return count; 
    }
};
void Node::print(){
    cout<<"count= "<<count<<" num= "<<num<<endl;
}
//Allocates memory for static data members
int Node::count=0;
int main(){
    cout<<"\ncount= "<<Node::getCount()<<endl;
    Node *n1, *n2, *n3;
    n1=new Node();
    n2=new Node();
    n3=new Node();
    n1->add();
    n1->print();
    n2->print();
    n3->print();
    cout<<"\ncount "<<Node::getCount()<<endl;
    delete n1;
    cout<<"\ncount "<<Node::getCount()<<endl;
    return 0;
}
```

#### const member function

```C++
// Example: of Constant member function
 
#include<iostream>
using namespace std;
 
class Demo{
    int x;
    public:
        void set_data(int a){
            x=a;
        }
        int get_data() const {
            ++x;                 // Error while attempting to modify the data member
            return x;
        }
  
};
 
 
int main(){
    Demo d;
    d.set_data(10);
    cout<<endl<<d.get_data();
    return 0;
}
```

