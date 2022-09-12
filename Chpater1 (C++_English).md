[TOC]
# C++

## cin manipulator and cout manipulator

### cout.width() and setw

Both cout.width() and setw() can help we control the output sizes.
Rememeber that setw() is in iomanip header.

<問題> Observe the program below and modified it to check how is the two functions work.(To see the range of the two functions could influence the program)

```C++
int a = 10;
cout.width(10);
cout<<a<<endl;
cout<<a<<endl;
cout<<setw(10)<<a<<endl;
```

### Alignment 

The default output of cout is align to the right. If we want to change it, we have to use the 

```C++
cout<<setiosflags(ios::left);
cout<<setw(10)<<a;
```

<練習> Observe and modify the code above like last question.

### cout.fill(char) and setfill()
Change the fill char from space to the char you set.
<練習> Write code and test the two functions.
```C++
cout.fill('*');
```

### setprecision

```C++
    double d = 0.0000017121219;
    cout<<d<<endl;
    cout<<setprecision(20);
    cout<<d<<endl;
    cout<<d<<endl;
    cout<<setiosflags(ios::fixed);
    cout<<d<<endl;
    cout<<d<<endl;
```

---

### getline(cin, s)

Keep reading the input until encounter the '\n' character. The max_char_nums indicates the maximum numbers of characters it can handle. If it encounter the '\n' character, it will stop reading, and remove the '\n' character in the buffer.

### cin.get()

Get a character.
char c = cin.get();

```C++
int main(){
    string c;
    string s;
    getline(cin, s);
    cout<<s<<endl;
    c = cin.get();
    cout<<c<<endl;
}
```

---


## inline

Put "inline" before the function will suggest compiler to unfold the function code just like macro. But when the compiler may ignore the inline if
1. function is too big
2. the function could call itself(recuresive)
3. the compiler does not support inline

In contrast to macro, inline functions have 2 advantages

1. inline function has type checking
2. inline function has type conversion

```C++

inline int add(int a, int b){
    return a+b;
}

```

## function overloading

C++ allows the same name to be used for two or more different functions, which is called function overloading. The compiler will decide which function should be called with the following cases.

1. Those functions have different numbers of parameters.

```C++
    void fun1(int);
    void fun1(int, int);
    void fun1(int, int, int);
```

2. Those fucntions have at least a different type of data parameter.

```C++
    void fun2(int, char)
    void fun2(float, char)
```

3. Those parameters of the functions be in a different order

```C++
    void fun3(char, int, float)
    void fun3(int, char, float)
```

In a function call, the C++ compiler checks the function name as well as the arguments on each call to determine which function to use.

Return type is not used for distinguish functions in C/C++.

```C++
int fun(int, int)
float fun(int, int) // Error
```

## default arguments

C++ allow to give default arguments. A function can has both default arguments and non-default arguments. The default arguments must always be right of non-default arguments.

```C++
void fun(int a = 5, int b = 10);
void fun2(int a, int b = 55)

```

## ambiguity

Sometimes the errors will raise during function call.

```C++
int fun(float a);
int fun(double b);

int main(){
    int x=10;
    fun(x); // Invalid because x can be converted to float or double
}

```


## reference

A reference is an implicit pointer that is automatically dereferenced. A reference also act as a alternative name of a variable.

The value of reference must be assigned when declared it.
```C++
    int a = 1;
    int &ra = a;
    cout << a << endl;
    cout << ra << endl;
    ra = 8;
    cout << a << endl;
```

### The difference between pointer and reference

1. Pointer requires an extra space to store the memory address that is points to.
2. Reference must be initialized when declared.
    1. Reference can not be change to another variable
    2. Reference can not be a NULL reference
    3. Reference can not point to another reference
    4. We can not create an array of reference
4. Pointer needs to be dereferenced to get the value it point to

### passing reference to a function

We can pass reference to a function. The benefit of it is that when pass by value, we need an copy of the variable which will cause both time and memory space. Also, the more pointers in the code, the more hard to read the code. 

```C++
void swap(int a, int b){
    int temp;
    temp = a;
    a = b;
    b = temp;
}

void swap2(int* a, int* b){
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

void swap3(int &a, int &b){
    int temp;
    temp = a;
    a = b;
    b = temp;
}
int main(){
    int a = 1, b = 2;
    cout << a << ' ' << b << endl;
    swap(a,b); // output: 2 1
    cout << a << ' ' << b << endl;
    swap2(&a, &b); // output: 1 2
    cout << a << ' ' << b << endl;
    swap3(a,b); // output: 2 1
    cout << a << ' ' << b << endl;
    return 0;
}
```

## new and delete

C++ support new and delete to help dynamic allocation. The word "new" will return NULL when error occurs in memory allocation.

```C++
int * a = new int (10);
if(a == NULL){
    cout<<"Error\n";
    exit(1);
}
*a = 7;
cout << *a;
delete a;
```

### Memory leak

Like malloc function, we must use new and delete carefully, or we will encounter memory leak.

```C++
float *ptr = new float; //Allocates first block
*ptr = 7.9; //Accesses first block
ptr = new float; //Allocates second block
*ptr = 5.1; //Accesses second block
```
![](https://i.imgur.com/JsXOXxc.png)

```C++
pointer_var = new data_type[size];
detete []pointer_var;
```


```C++
#include <iostream>
#include <iomanip>
using namespace std;
int main(){
    int *ptr, n = 50;
    ptr = new int[n]; //Allocates an array dynamically
    if(!ptr) {
        cout<<"Memory allocation error!";
        exit(1);
    }
    for(int i=0; i<n; i++){
        ptr[i] = i; //Initializes the array
        cout << setw(3) << ptr[i];
    }
    delete []ptr; //Deletes the array from the heap
    return 0;
}
```

```C++
#include <iostream>
#include <iomanip>
using namespace std;
void memError() {
    cout<<"Memory allocation error!";
    exit(1);
}
int main() {
    int rows, columns, i, j;
    int **p2d; //Declares a pointer to pointer
    cout<<"Enter a number of rows => ";
    cin>>rows;
    cout<<"\nEnter a number of columns => ";
    cin>>columns;
    p2d=new int*[rows];
    if(!p2d) //Checks for an allocation error
        memError();
    for(i=0; i<rows; i++) {
        p2d[i] = new int [columns]; //Sets up the columns
    if(!p2d[i]) //Checks for an allocation error
        memError();
    }
    cout<<"\n***MULTIPLICATION TABLE***"<<endl;
    for(i=0; i<rows; i++) {
        for(j=0; j<columns; j++) {
            p2d[i][j]=(i+1)*(j+1); //Initializes the array
            cout<<setw(5)<<p2d[i][j]; //Displays its values
        }
        cout<<endl;
    }
    for(i=0; i<rows; i++)
        delete [] p2d[i]; //Deletes the columns
    delete [] p2d; //Deletes the rows
    return 0;
}
```
