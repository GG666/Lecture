[TOC]

# Inheritance



```C++
#include <iostream>

using namespace std;

class Animal {
    int weight;
    public:
    void eat(){
        cout<<"eating..."<<endl;
    }
    void sleep(){
        cout<<"sleeping..."<<endl;
    }
};

class Dog : public Animal {
    public:
    void bark(){
        cout<<"Woof! Woof!"<<endl;
    }
};

class Cat : public Animal {
    public:
    void meow(){
        cout<<"Meow~ "<<endl;
    }
};

int main()
{
    Cat c;
    Dog d;
    d.bark();
    d.eat();
    d.sleep();
    c.meow();
    c.eat();
    c.sleep();
}
```

From the code above, we first saw the inheritance in C++. Inheritance allows others classes to inherit the member variables and member functions of a super class(Base class). The derived class inherits the features from the base class and can have additional features of its own.

<**Question**> What is(are) the benefit(s) of inheritance?

:::spoiler Answer
Inheritance can help us reduce the duplicate codes. Which will also increase the implement speed for programmars.
:::



### Protected members

In addition to public and private, there is a another keyword "protected". The access modifier "protected" is like "private". Like private members, protected members are inaccessible outside of the class. However, protected member can be accessed by derived class and friend classes/functions.

```C++
// C++ program to demonstrate protected members

#include <iostream>
#include <string>
using namespace std;

// base class
class Animal {

   private:
    string color;

   protected:
    string type;

   public:
    void eat() {
        cout << "I can eat!" << endl;
    }

    void sleep() {
        cout << "I can sleep!" << endl;
    }

    void setColor(string clr) {
        color = clr;
    }

    string getColor() {
        return color;
    }
};

// derived class
class Dog : public Animal {

   public:
    void setType(string tp) {
        type = tp;
    }

    void displayInfo(string c) {
        cout << "I am a " << type << endl;
        cout << "My color is " << c << endl;
    }

    void bark() {
        cout << "I can bark! Woof woof!!" << endl;
    }
    
    void setColor(string clr) {
          // Error: member "Animal::color" is inaccessible
          color = clr; 
    }
};

int main() {
    // Create object of the Dog class
    Dog dog1;

    // Calling members of the base class
    dog1.eat();
    dog1.sleep();
    dog1.setColor("black");

    // Calling member of the derived class
    dog1.bark();
    dog1.setType("mammal");

    // Using getColor() of dog1 as argument
    // getColor() returns string data
    dog1.displayInfo(dog1.getColor());
    //dog1.color="White";
    return 0;
}
```

## C++ Public, Protected and Private Inheritance

- public inheritance : public members of the base class become public in the derived class, and the protected members of the base class remain protected in the derived class.
- public and protected members of the base class become protected in the derived class.
- public and protected members of the base class become private in the derived class.
- private members of the base class are inaccessible to the derived class.

```C++
#include <iostream>
using namespace std;

class Base {
  private:
    int pvt = 1;

  protected:
    int prot = 2;

  public:
    int pub = 3;

    // function to access private member
    int getPVT() {
      return pvt;
    }
};

class PublicDerived : public Base {
  public:
    // function to access protected member from Base
    int getProt() {
      return prot;
    }
};

class ProtectedDerived : protected Base {
  public:
    // function to access protected member from Base
    int getProt() {
      return prot;
    }

    // function to access public member from Base
    int getPub() {
      return pub;
    }
    
    int getPVT_protected() {
        return getPVT();
    }
};


class PrivateDerived : private Base {
  public:
    // function to access protected member from Base
    int getProt() {
      return prot;
    }

    // function to access private member
    int getPub() {
      return pub;
    }
    
    int getPVT_protected() {
        return getPVT();
    }
};

int main() {
    PublicDerived object1;
    cout << "Public inheritance access Private = " << object1.getPVT() << endl;
    cout << "Public inheritance access Protected = " << object1.getProt() << endl;
    cout << "Public inheritance access Public = " << object1.pub << endl;
    
    ProtectedDerived object2;
    cout << "Protected inheritance access Private = " << object2.getPVT_protected() << endl;
    cout << "Protected inheritance access Protected = " << object2.getProt() << endl;
    cout << "Protected inheritance access Public = " << object2.getPub() << endl;
    
    PrivateDerived object3;
    cout << "Private inheritance access Private = " << object3.getPVT_protected() << endl;
    cout << "Private inheritance access Protected = " << object3.getProt() << endl;
    cout << "Private inheritance access Public = " << object3.getPub() << endl;
  
  return 0;
}
```



### Constructor Inheritance

```C++
// CPP program to demonstrate Default constructors
#include <iostream>
using namespace std;

class A {
public:
    // User defined constructor
    A() {
        cout << "A Constructor" << endl;
    }
 
    // uninitialized
    int size;
};
 
class B : public A {
    // compiler defines default constructor of B, and
    // inserts stub to call A constructor
 
    // compiler won't initialize any data of A
};
 
class C : public A {
public:
    C()
    {
        // User defined default constructor of C
        // Compiler inserts stub to call A's constructor
        cout << "C Constructor" << endl;
 
        // compiler won't initialize any data of A
    }
};
 
class D {
public:
    D()
    {
        // User defined default constructor of D
        // a - constructor to be called, compiler inserts
        // stub to call A constructor
        cout << "D Constructor" << endl;
 
        // compiler won't initialize any data of 'a'
    }
 
private:
    A a;
};
 
// Driver Code
int main(){
    B b;
    C c;
    D d;
    return 0;
}
```
[Ref](https://www.geeksforgeeks.org/default-constructors-in-cpp/)



### Multilevel inheritance

```C++
#include <iostream>  
using namespace std;  

class Animal {
    public:
    void eat() {
        cout<<"Eating..."<<endl;
    }
};

class Dog: public Animal {
    public:
    void bark(){
        cout<<"Barking..."<<endl;
    }
};   

class BabyDog: public Dog{
    public:
    void weep() {
        cout<<"Weeping...";
    }
};

int main(void) {
    BabyDog d1;
    d1.eat();
    d1.bark();
    d1.weep();
    return 0;
}
```

[Reference](https://www.1ju.org/cplusplus/cpp-inheritance)
