[TOC]
# Operator Overloading

Operator overloading is a special type of function overloading.
[Review](https://hackmd.io/kQ9sGMhPRW2Gk-KQAuEixA?view#function-overloading)

Operator overloading enables users to use existing operators to manipulate objects of their class. An operator is overloaded if it can perform multiple operations.

For example, the operator ‘*’ can be used to multiply two values of int, float, double, long long…, and it can also be used to declare a pointer or dereference a pointer.

```C++
#include <iostream>
using namespace std;
int main(){
    int a;
    cin>>a;
    int* pa = &a;
    cout << *pa**pa << endl;
    return 0;
}
```

```C++
class A
{

};

int main()
{
      A   a1,a2,a3;

      a3= a1 + a2;

      return 0;
}
```
In the example above, we have 3 variables “a1”, “a2” and “a3” of type “class A”. Here we are trying to add two objects “a1” and “a2”, which are of user-defined type i.e. of type “class A” using the “+” operator. This is not allowed, because the addition operator “+” is predefined to operate only on built-in data types. But here, “class A” is a user-defined type, so the compiler generates an error. This is where the concept of “Operator overloading” comes in. 

[*reference*](https://www.geeksforgeeks.org/operator-overloading-c/)


Basically, there are 

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


```C++
#include <iomanip>
#include <iostream>
using namespace std;

class TwoDVector{
private:
    float x, y;
public:
    TwoDVector(double x=0, double y=0){
        this -> x = x;
        this -> y = y;
    }
    void print(void);
    TwoDVector operator+(const TwoDVector &);
    friend float operator*(const TwoDVector &, const TwoDVector &);
    friend TwoDVector operator*(const TwoDVector &, double);
    friend TwoDVector operator*(double, const TwoDVector &);
};

void TwoDVector::print(void){
    // setprecision(20);
    cout<<"("<<setprecision(20)<<x<<","<<setprecision(20)<<y<<")"<<endl;
}

TwoDVector TwoDVector::operator+(const TwoDVector & v1){
    TwoDVector v;
    v.x = this -> x + v1.x;
    v.y = this -> y + v1.y;
    return v;
}

TwoDVector operator*(const TwoDVector & v1, double a){
    TwoDVector v;
    v.x = v1.x * a;
    v.y = v1.y * a;
    return v;
}

TwoDVector operator*(double a, const TwoDVector & v1){
    TwoDVector v;
    v.x = v1.x * a;
    v.y = v1.y * a;
    return v;
}

float operator*(const TwoDVector & v1, const TwoDVector & v2){
    return v1.x * v2.x + v1.y * v2.y;
}

int main(){
    double t=0.000000000123456, t2=0.0000000001234567;
    TwoDVector v1(t,t2), v2(3,4), v3;
    v3 = v1 + v2;
    v3.print();
    cout << v1 * v2 << endl;
    v3 = 2 * v1;
    v3.print();
    return 0;
}
```

Below is one kind of wrong code


```C++
#include <iomanip>
#include <iostream>
using namespace std;

class TwoDVector{
private:
    float x, y;
public:
    TwoDVector(double x=0, double y=0){
        this -> x = x;
        this -> y = y;
    }
    void print(void);
    // TwoDVector operator+(const TwoDVector &);
    TwoDVector operator+(const TwoDVector &, const TwoDVector &);
    friend float operator*(const TwoDVector &, const TwoDVector &);
    friend TwoDVector operator*(const TwoDVector &, double);
    friend TwoDVector operator*(double, const TwoDVector &);
};

void TwoDVector::print(void){
    // setprecision(20);
    cout<<"("<<setprecision(20)<<x<<","<<setprecision(20)<<y<<")"<<endl;
}

// TwoDVector TwoDVector::operator+(const TwoDVector & v1){
//     TwoDVector v;
//     v.x = this -> x + v1.x;
//     v.y = this -> y + v1.y;
//     return v;
// }

TwoDVector TwoDVector::operator+(const TwoDVector &v1, const TwoDVector &v2){
    TwoDVector v;
    v.x = v1.x +v2.x;
    v.y = v1.y +v2.y;
    return v;
}

TwoDVector operator*(const TwoDVector & v1, double a){
    TwoDVector v;
    v.x = v1.x * a;
    v.y = v1.y * a;
    return v;
}

TwoDVector operator*(double a, const TwoDVector & v1){
    TwoDVector v;
    v.x = v1.x * a;
    v.y = v1.y * a;
    return v;
}

float operator*(const TwoDVector & v1, const TwoDVector & v2){
    return v1.x * v2.x + v1.y * v2.y;
}


int main(){
    double t=0.000000000123456, t2=0.0000000001234567;
    TwoDVector v1(t,t2), v2(3,4), v3;
    v3 = v1 + v2;
    v3.print();
    cout << v1 * v2 << endl;
    v3 = 2 * v1;
    v3.print();
    return 0;
}
```

Basically every operator can be overloaded except for some.

Operators that can be overloaded
![](https://i.imgur.com/1CfGm7v.png)

Operators that can not be overloaded
![](https://i.imgur.com/N0js4hg.png)

[ You don't have to remmeber that though. ]

When building operator overloading with binary operators, we have to ensure that we create two overloading functions if needed.

```C++
//for example
TwoDVector v1;
TwoDVector v2 = v1 * 2;
TwoDVector v3 = 2 * v1;
//may be error if we only create one side
//i.e. operator*(const TwoDVector &, float) but not reverse
```

```C++
#include <iostream>
using namespace std;
class TwoDVector{
private:
    float x, y;
public:
    TwoDVector(float x=0, float y=0) {
        this->x=x;
        this->y=y;
    }
    void print(void);
    friend TwoDVector operator++(TwoDVector &);
    friend TwoDVector operator++(TwoDVector &, int);
};

void TwoDVector::print(void) {
    cout<<"("<<x<<","<<y<<")"<<endl;
}

TwoDVector operator++(TwoDVector & v1) {
    //PLZ complete it
}

TwoDVector operator++(TwoDVector & v1, int) {
    //PLZ complete it
}
int main() {
    TwoDVector v1(1,2), v2;
    v2=++v1;
    v1.print();
    v2.print();
    v2=v1++;
    v1.print();
    v2.print();
    return 0;
}

```


The assign operator ('=') can be used to create bit-by-bit copy without explicit overloading declaration.

If a class containing pointers as members, like we mentioned last chapter, we have to clearly define its behavior to avoid having the same pointer in tow or more objects. Which will cause error because destroy one obeject will destory the pointers in other objects.


<**review**>

```C++
#include<iostream>
using namespace std;

class Numbers{
private:
    float *fptr; // points to a float array
    int num; // size of the array
public:
    Numbers(int x); // regular constructor
    // Numbers(const Numbers &); // copy constructor
    ~Numbers(){ // desctructor
        delete [] fptr;
        cout << "destroy the array!"<<endl;
    } 
    // const Numbers & operator = (const Numbers &);
    void getNumbers();
    void getSize();
};


Numbers::Numbers(int x = 10){
    num = x;
    fptr = new float[num]; // Allocates memory dynamically
    if(!fptr) {
        cout << "Memory allocation error!";
        exit(1);
    }
    for(int i = 0; i < num; i++) // Initializes array
        fptr[i] = 0;
}

// Please write a copy constrctor to avoid delete the pointer data


// const Numbers & Numbers::operator =(const Numbers & f){
//     if(&f!=this){ //Frees memory allocated by constructor
//         delete [] fptr;
//         num = f.num;
//         fptr = new float[num];
//         if(!fptr){
//             cout<<" Memory allocation error.";
//             exit(1);
//         }
//         for(int i=0; i<num; i++)
//             fptr[i]=f.fptr[i];
//     }
//     return *this;
// }

void Numbers::getNumbers(){
    for(int i = 0; i < num; i++){
        cout << *(fptr + i) << " ";
    }
    cout << endl;
}

void Numbers::getSize(){
    cout << num << endl;
}

void test(Numbers N){
    return;
}

int main(){
    Numbers a(6), b;
    b = a;
    test(a);
    a.getNumbers();
    a.getSize();
    // b.getNumbers();
}
```


We can overload the stream insertion (<<) and
stream extraction (>>) operators in order
to perform user defined I/O operations. 

The istream and ostream classes are used when overloading the << and >> operators. (cin is an instance(object) of the istream class and is connected to the standard input device, most commonly a keyboard. cout is an instance of the ostream class and is connected to the standard output device, most commonly a display screen.)

```C++
#include <iostream>
using namespace std;
class TwoDVector{
private:
    float x, y;
public:
    TwoDVector(float x=0, float y=0){
        this->x=x;
        this->y=y;
    }
    friend ostream & operator<<(ostream &, const TwoDVector &);
    friend istream & operator>>(istream &, TwoDVector &);
};

ostream & operator<<(ostream & os, const TwoDVector & v){
    os << "(" << v.x << "," << v.y << ")";
    return os;
}

istream & operator>>(istream & is, TwoDVector & v){
    is>>v.x;
    is>>v.y;
    return is;
}


int main(){
    TwoDVector v1;
    cin>>v1;
    cout<<v1;
    return 0;
}
```
