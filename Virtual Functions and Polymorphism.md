# Virtual Functions and Polymorphism

Polymorphism means "Having many forms".

*A real-life example of polymorphism is a person who at the same time can have different characteristics. A man at the same time is a father, a husband, and an employee. So the same person exhibits different behavior in different situations.*  
<[***Reference***](https://www.geeksforgeeks.org/cpp-polymorphism/)>

There are two types of polymorphism.
- Compile time polymorphism : Complie time polymorphism is archieved by function overloading and operator overloading.
- Run time polymorphism : Run time polymorphism is archieved by function overriding.

### Binding

Binding is converting identifiers to addresses. (For variables and functions)



## Compile Time Polymorphism


```C++
#include <iostream>
using namespace std;


int add(int a, int b){
    return a+b;
}
 
double add(double a, double b){
    return a+b;
}

int main(){
    cout<<add(1,2)<<endl;
    cout<<add(1.3,4.2)<<endl;
    return 0;
}
```

The above code is function overloading. Which is also the example of compile time polymorphism.
[To see more info...](https://hackmd.io/kQ9sGMhPRW2Gk-KQAuEixA?view#function-overloading)


```C++
#include <iostream>
using namespace std;

class TwoDVector{
private:
    float x, y;
public:
    TwoDVector(float x=0, float y=0){
        this -> x = x;
        this -> y = y;
    }
    void print(void);
    friend TwoDVector operator+ (const TwoDVector &, const TwoDVector &);
    friend float operator* (const TwoDVector &, const TwoDVector &);
    friend TwoDVector operator* (const TwoDVector &, float);
    friend TwoDVector operator* (float, const TwoDVector &);
};

void TwoDVector::print(void){
    cout<<"("<<x<<","<<y<<")"<<endl;
}

TwoDVector operator+(const TwoDVector & v1, const TwoDVector & v2){
    TwoDVector v;
    v.x = v1.x + v2.x;
    v.y = v1.y + v2.y;
    return v;
}

TwoDVector operator*(const TwoDVector & v1, float a){
    TwoDVector v;
    v.x = v1.x * a;
    v.y = v1.y * a;
    return v;
}

TwoDVector operator*(float a, const TwoDVector & v1){
    TwoDVector v;
    v.x = v1.x * a;
    v.y = v1.y * a;
    return v;
}

float operator*(const TwoDVector & v1, const TwoDVector & v2){
    return v1.x * v2.x + v1.y * v2.y;
}


int main(){
    TwoDVector v1(1,2), v2(3,4), v3;
    v3 = v1 + v2;
    v3.print();
    cout << v1 * v2 << endl;
    v3 = 2 * v1;
    v3.print();
    return 0;
}
```

The above code is the operator overloading, which is also compile time polymorphism.

[To see more info...](https://hackmd.io/TxtqRWOMRK6U1w80oy9x7w)

### Static binding (Early binding)

Perform in compile time. The compiler reserves a space in memory for all user defined functions and keep track of the addresses of memory locations it allocated to. 

Compiler will replaces the call(identifier) with a machine language instruction that tells the mainframe to leap to the address of the function. (except for inline function)

In the case of inline functions, the name of the functions is substituted with the actual code of the functions (not its address)

## Run Time Polymorphism

#### Dynamic binding(Late binding)


Compiler adds code that identifies the kind of object at runtime then matches the call with the right function definition.

Function calls are resolved at run time. Function pointer is used to implement dynamic binding

##### Function pointer


```C++
#include <iostream>
using namespace std;

void func1(int x) {
    cout << "Call func1 " << x << endl;
}
void func2(int x) {
    cout << "Call func2 " << x << endl;
}
void func3(int x) {
    cout << "Call func3 " << x << endl;
}

int main(){
    int a;
    cin>>a;
    if (a==0)
        func1(a);
    else if (a==1)
        func2(a);
    else if (a==3)
        func3(a);
}
```

```C++
#include <iostream>
using namespace std;

void func1(int x) {
    cout << "Call func1 " << x << endl;
}
void func2(int x) {
    cout << "Call func2 " << x << endl;
}
void func3(int x) {
    cout << "Call func3 " << x << endl;
}

int main() {
    void (*fptr[3])(int) = {func1, func2, func3};
    int a;
    cin>>a;
    if (a >= 0 && a < 3)
        (*fptr[a])(a);
}
```

## Keyword Virtual 

We can add the keyword virtual infront of the class member functions. This keyword will tell the compiler to implement the compiler to use late binding. 

When a class contains virtual tables, every objects of the class will contains a "virtual table" and the virtual table pointer. (Array of function pointers)

```C++
#include <iostream>
using namespace std;

class Shape {
   protected:
      int width, height;

   public:
      Shape( int a = 0, int b = 0){
         width = a;
         height = b;
      }
      /*virtual*/ int area() {
         cout << "Parent class area :" << width * height << endl;
         return width * height;
      }
};
class Rectangle: public Shape {
   public:
      Rectangle( int a = 0, int b = 0):Shape(a, b) { }

      int area () {
         cout << "Rectangle class area :" << width * height << endl;
         return (width * height);
      }
};

class Triangle: public Shape {
   public:
      Triangle( int a = 0, int b = 0):Shape(a, b) { }

      int area () {
         cout << "Triangle class area :" << (width * height)/2 << endl;
         return (width * height / 2);
      }
};

// Main function for the program
int main() {
   Shape *shape;
   Rectangle rec(10,7);
   Triangle  tri(10,5);

    rec.area();
    tri.area();

   // store the address of Rectangle
   shape = &rec;

   // call rectangle area.
   shape->area();

   // store the address of Triangle
   shape = &tri;

   // call triangle area.
   shape->area();

   return 0;
}
```


```C++
#include <iostream>
using namespace std;
class Player {
public:
    virtual void attack(void) { cout<<"The player punches."<<endl;}
};

class Warrior : public Player {
public:
    void attack(void) /*override*/ { cout<<"The warrior slashes with a sword."<<endl;}
};

class Magician : public Player {
public:
    void attack(void) /*override*/ { cout<<"The magician attacks with a staff."<<endl;}
};

class Clerk : public Player {
public:
    void attack(void) /*override*/ { cout<<"The clerk attacks with a staff."<<endl;}
};

class Thief : public Player {
public:
    void attack(void) /*override*/ { cout<<"The thief stabs with a dagger."<<endl;}
};

int main(){
    Player p;
    Warrior w;
    Magician m;
    Clerk c;
    Thief t;
    p.attack();
    w.attack();
    m.attack();
    c.attack();
    t.attack();
    
    Player *players[5];
    players[0] = &p;
    players[1] = &w;
    players[2] = &m;
    players[3] = &c;
    players[4] = &t;
    for(int i=0;i<5;i++)
        players[i]->attack();
};
```





[References]
[1](https://medium.com/theskyisblue/c-%E4%B8%AD%E9%97%9C%E6%96%BC-virtual-%E7%9A%84%E5%85%A9%E4%B8%89%E4%BA%8B-1b4e2a2dc373#:~:text=%E5%9C%A8%20C%2B%2B%20%E4%B8%AD%EF%BC%8Cdynamic%20binding%20%E4%B8%BB%E8%A6%81%E5%8F%AF%E4%BB%A5%E9%80%8F%E9%81%8E%20virtual%20%E4%BE%86%E9%81%94%E6%88%90%E3%80%82,%E5%9C%A8%20static%20binding%20%E4%B8%AD%EF%BC%8C%E7%94%B1%E6%96%BC%E5%91%BC%E5%8F%AB%E5%87%BD%E5%BC%8F%E7%9A%84%E6%89%80%E6%9C%89%E8%B3%87%E8%A8%8A%E9%83%BD%E5%B7%B2%E7%B6%93%E6%8F%90%E5%89%8D%E5%85%88%E7%9F%A5%E9%81%93%E4%BA%86%EF%BC%8C%E6%89%80%E4%BB%A5%E5%9C%A8%E7%A8%8B%E5%BC%8F%E7%9C%9F%E6%AD%A3%E5%9F%B7%E8%A1%8C%E8%B5%B7%E4%BE%86%E6%9C%83%E6%AF%94%E8%BC%83%E5%BF%AB%E4%B8%80%E4%BA%9B%EF%BC%9B%E5%8F%8D%E4%B9%8B%EF%BC%8Cdynamic%20binding%20%E7%9A%84%E5%A5%BD%E8%99%95%E5%9C%A8%E6%96%BC%E5%9C%A8%20run-time%20%E6%89%8D%E6%B1%BA%E5%AE%9A%EF%BC%8C%E5%9B%A0%E6%AD%A4%E5%8F%AF%E4%BB%A5%E6%9B%B4%E5%BD%88%E6%80%A7%E5%9C%B0%E5%91%BC%E5%8F%AB%E5%87%BD%E5%BC%8F%E3%80%82)
[2](https://blog.csdn.net/fanyun_01/article/details/79122136)
[3](https://www.tutorialspoint.com/cplusplus/cpp_polymorphism.htm#:~:text=The%20word%20polymorphism%20means%20having%20many%20forms.%20Typically%2C,the%20type%20of%20object%20that%20invokes%20the%20function.)
[4] My teacher's lectures