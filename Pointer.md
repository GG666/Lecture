[TOC]
# Pointer
## Whats' Pointers

Pointer is a variable that store the data which is the address of another variable.

```C++
#include <cstdio>
int main(){
    int *p, a;
    p = &a;
    printf("%p\n", &a);
    printf("%p\n", p);
}
```

Actually in the program above, the thing left to '=' is the address value, as a result we can seem the above program as we assign the value right to the '=' to the address.

```C++
#include <cstdio>
int main(){
    int *p, a=0;
    p = &a;
    //use pointer to make a++
    *p=*p+1;
    *p++;
    printf("%d\n", a);
    printf("%p\n",&a);
    printf("%p\n",p);
}
```

When using pointer to do the operations, remember it must be with the '*' sign. Pointers with the star sign must be regarded as one. And also the substitute(替身) of the variable which the pointer points.

## The size of pointer type variable

As we already know, different types use As we already know, different types take different sizes of spaces.
##### Review

```
1bytes = 8bits

int       => 4 bytes

bool      => 1 bytes
char      => 1 bytes
float     => 4 bytes
double    => 8 bytes
long long => 8 bytes
pointer   => ???
```

**Question**
1. What is the range of integer can we count by our hands when using binary expression.
2. What is the size of pointer in a 32-bit operating system? [hint] A 32-bit operating system use 32-bit memory address.
3. How about 64-bit?

<練習>
Using the **sizeof()** function to check the size of pointer in your environment. And check the sizes of the variables that pointers point to with '*'.

## The type conversion in pointers

Because of pointers store the memory addresses. Intuitively, we can use one pointer for every address in the memory. However, the compiler needs to know how much the size it has to deal with. Therefore the type is necessary. To change the type of a pointer points to , we have to declare the pointer as a **void** type variable.

```C++
#include<iostream>

using namespace std;

int main()
{
    int i=77,*pi;
    float f=0.22,*pf;
    void *ptr;
    ptr=&f;
    printf("Current *ptr = %f\n",*(float *)ptr);
    ptr=&i;
    printf("Current *ptr = %d\n",*(int *)ptr);
}
```

Try to debug the following code.

```C++
#include<iostream>

using namespace std;

int main()
{
    int i=77,*pi;
    float f=0.22,*pf;
    void *ptr;
    ptr=&f;
    printf("Current *ptr = %f\n",ptr);
    *ptr=&i;
    ptr=ptr+5; //make i=i+5
    printf("Current *ptr = %d\n",ptr);
}
```

## Pointer and the char string

Memory is a one-dimension space, one address store one byte. So what will happen if we do some operations to pointers?

```C++
#include<iostream>

using namespace std;

int main()
{
    char c='a',*pc=&c;
    for(int i=0;i<10;pc++,i++)
        printf("%p\n",pc);
}
```

To travel through an string with a pointer, we must initailize the pointer(makes the pointer point to the start of the string)

<練習>
Try to fix the following code to make it go through the char string
```C++
#include<iostream>

using namespace std;

int main()
{
    char arr[10]="123456789";
    char *pc;
    int i;
    pc=&arr[0];
    for(i=0;i<8;i++)
        cout<<*pc+i<<endl;
}

```

<練習>

Pointer only went through the even number in the array.


## Static memory allocation
**Static memory allocation** is an allocation technique which allocates a fixed amount of memory during compile time and the operating system internally uses a data structure known as Stack to manage this.

In Static Memory Allocation the memory for your data is allocated when the program starts. The size is fixed when the program is created. It applies to global variables, file scope variables, and variables qualified with static defined inside functions. This memory allocation is fixed and cannot be changed, i.e. increased or decreased after allocation. So, exact memory requirements must be known in advance.

### Deletion of static allocated memory
Deletion of memory allocated to a program is as important as allocation otherwise it results in memory leakage. Statically allocated memory is automatically released on the basis of scope, i.e., as soon as the scope of the variable is over, memory allocated get freed.

### Static Variables
As the name suggests, the value of static variables persists until the end of the program. A variable can be declared static using the keyword static like
```C++
static int x;
static float y;
```
#### Internal static variables
**Internal static variables** are those which are declared inside a function. The scope of static variables extend up to the end of the function in which they are defined. Therefore, internal static variables are similar to auto variables, except that they remain in existence(alive) throughout the remainder of the program.For example, it can be used to count the number of calls made to a function

```C++
void stat(void);

int main()
{
   int i;
   for(i=1; i<=3 ; i++)
      stat();
   return 0;
}
void stat(void) 
{
   static int x = 0;
   x = x+1;
   printf("x = %d\n", x); 
}
```


**[Key features]**
1. Allocation is done before program execution
2. It uses the data structure called stack for implementing static allocation
3. Less efficient with space
4. Variables get allocated permanently
5. There is no memory reusability

## Dynamic memory allocation

All the variables that we declare in our program take some memory to store.
Moreover, all of them are distributed by compiler in the compile-time. The way to store the data are called static memory allocation.

In contrast to static memory allocation, there is a way for the programs to ask the CPU for memory in run-time, this is what we called "dynamic memory allocation".

malloc is defined in the header file stdlib.h, the return value of it is the begin address(first address). It's recommended to use the "sizeof(type)" function to give it the size you need.

```C++
int *a;
a=(int *) malloc(sizeof(int)*5);
//int a[5];

char *s;
s=(char *)malloc(sizeof(char)*10);
//s[10]

```

Before we go into the practice, there is a very important thing that we must remember : **release of the memory**.

When using static memory allocation, the memory will be released after the program ends. But the memory that we get in run-time has to be recycled manually. 

```C++
free(variable_name);
```

We must keep in mind that the malloc and the free functions must come in pairs. Once we use the malloc function, we must write the free function, too.
The memory in our CPU is not infinity resources. If we keep using malloc without free, the speed of our system will be more and more slow.

If the CPU can't give us the resources that we asked for, the return value of malloc will be NULL. As a result, when we use the dynamic memory allocation, we must check whether we get the memory or not.

<練習> Please write a program that the users can input the array size and allocate the array memory dynamically.

<練習>
```C++
#include<stdio.h>
#include<stdlib.h>
int main(){
    int *pNum;
    int res = 0,i,n;
    printf("Inputs the number of variables: \n");
    scanf("%d",&n);
    pNum = (int *) malloc ( sizeof (int) * n);
    for(int i=0;i<n;i++){
        //printf("PLZ input the %2d numbers.\n",i+1);
        scanf("%d",pNum+i);
        res+=*(pNum+i);
    }
    printf("%d\n", res);
    free(pNum);
    return 0;
}

```

Like the program above, we can consider that the memory we get with malloc is an one-dimension array.

**[Question1]** What problem(s) is/are in the program above?

:::spoiler Ans
The problem is that we didn't check whether we get the memory we need.
:::


**[Question2]** But how to fix the problem?

[hint1] To think what are the differences between the success cases and the failure cases.
[hint2] Use if-else to handle it.


So there is the general syntax with the function malloc

:::spoiler 
```C++
if((variable_num=(type *)malloc(sizeof(type)*size))==NULL){
    printf("Error! Memory space isn't enough!");
    exit(0);
}
```
:::

<練習> Please modify the code above(modify the malloc function) to make it more stable.

**[Bonus]**
Stack memory is allocated during compilation time execution. This is known as static memory allocation.

Heap memory is allocated at run-time compilation. This is know as dynamic memory allocation.
![](https://i.imgur.com/YVEH4kW.jpg)


[Bonus練習] Please write(modify) a program that the user can keep input the number of numbers to calculate the sum.