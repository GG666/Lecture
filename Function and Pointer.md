# Function and Pointer

Each function is essentially a small program, with its own 
declarations, statements and name.

```C++
#include <stdio.h>
double average(double a, double b){
    return (a + b) / 2;
}
int main(){
    double x, y, z;
    printf("Enter three numbers: ");
    scanf("%lf%lf%lf", &x, &y, &z);
    printf("Average of %g and %g: %g\n", x, y, average(x, y));
    printf("Average of %g and %g: %g\n", y, z, average(y, z));
    printf("Average of %g and %g: %g\n", x, z, average(x, z));
    return 0;
}

```

## Advantages of functions
1. A program can be divided into small pieces that are easier to understand and modify
2. We can avoid duplicating code that’s used more than once
3. A function that was originally part of one program can be reused in other programs



## A General Function 
Below is the standard function

```C++
Return_type function_name(parameter type1 parameter name1, parameter type2 parameter name2, ......){
    //function body
        // Declartions...
        // Statements...
        return value;
} 
```

### function call

When we want to use the funciton, we must call the function with the **arguments** it need.

A function call consists of a function name followed by a list of arguments, enclosed in parentheses.

Call of a non-void function produces a value that can be stored in a variable, tested, printed, or used in some other way

```C++
avg = average(x, y);
if (average(x, y) > 0){
    printf("Positive\n");
}

```

The value returned by a non-void function can be discarded like below
```C++
average(x, y);
```




```C
average(5.1, 8.9);
average(a/5,b/3);
printf("Average: %g\n", average(x, y));
...
```

<練習> Please write a function that can help calculate the average score in the calss. Your program have to make user input the number of subjects first, then the numbers of students in the class, follow by their grades. The function should return the average of certain subject.

<練習> Please write a program to print Hello World


<Bonus> Discard the return value may seems strange but sometimes its useful.

```C++
int test=printf("hello world!\n");
printf("%d\n",test);
```
```C++
//example
//p is parameter
return_type function_name(p1_type , p2_type )
```
    
### Function prototype (Function declaration)

C does not require function definition but the function declaration preceded the function call.

A function declaration provides the compiler with a brief glimpse at a function whose full definition will appear later.

    
---
### Pass-by-value
When a function has been called, the value of each argument is assigned to the corresponding parameter.
    
Therefore, when we change the value of the parameter. It does not effect the original variable(cause we only change the copy of the variable).

Look at the function below, since n is a copy of the original exponent, we can modify the function safely:

```C++
#include <iostream>

using namespace std;

int power(int x, int n){
 int temp = x;
 x=1;
 while (n-- > 0)
     x = x * temp;
 return x;
}

int main()
{
    int a=5;
    int b=4;
    cout<<power(a,b)<<endl;
    cout<<a;
}

//x=5,n=3
5*5*5
```

#### Pass an array

We have to supply the length if the function needs it (as an additional argument)
```C++
int array_sum(int a[], int n){
    int i, sum = 0;
    for (i = 0; i < n; i++){
        sum += a[i];
    }
    return sum;
}
```
    
But what if we need a function to change the value of the variables?

### Pass-by-pointer
C allows passing a pointer to a function. To do so, simply declare the function parameter as a pointer type.

Following is a simple example where we pass an unsigned long pointer to a function and change the value inside the function which reflects back in the calling function:

```C++
#include <stdio.h>
#include <time.h>
 
void getSeconds(unsigned long *par);

int main () {

   unsigned long sec;
   getSeconds( &sec );

   /* print the actual value */
   printf("Number of seconds: %ld\n", sec );

   return 0;
}

void getSeconds(unsigned long *par) {
   /* get the current number of seconds */
   *par = time( NULL );
   return;
}
```

By this way, we can change the value of the parameters instead of change the value of their copy.

```C++
#include <stdio.h>
 
/* function declaration */
double getAverage(int *arr, int size);
 
int main () {

   // an int array with 5 elements
   int balance[5] = {1000, 2, 3, 17, 50};
   double avg;
 
   //pass pointer to the array as an argument
   avg = getAverage( balance, 5 ) ;
 
   // output the returned value 
   printf("Average value is: %f\n", avg );
   return 0;
}

double getAverage(int *arr, int size) {
   int sum = 0;       
   double avg;          
   for (int i = 0; i < size; i++) {
      sum += arr[i];
   }
   avg = (double)sum / size;
   return avg;
}
```
<練習> Please write a function to swap the value of given two variables. And check it by print their address.
**Input** : a(stores value x) b(stores value y)
**Output** : a(stores value y) b(stores value x)
(Hint: pass-by-pointer)
(Hint2 : The function should be like : void swap(int *a,int *b)...... )
    
<Bonus練習> Please write a function that can assign the value 0 to the array with given range

## Argument coercion
    
#### Argument promotion rule

If one argument is lower datatype, that can be converted into higher datatypes, but the reverse is not true(Like high dimension data compressed into low dimension will cause data loss).

![](https://i.imgur.com/Kkwy3lU.jpg)
[資料來源(reference)](https://www.tutorialspoint.com/argument-coercion-in-c-cplusplus)

<練習> Using function to rewrite the malloc

```C++
#include<iostream>
using namespace std;

int *GetIntSpace(int size){
    int *pget;
    // malloc 
    return pget;
}

int main(){
	int *pnum;
	pnum=GetIntSpace(10);
	free(pnum);
	return 0;
}
```

## Pointer points to function

Variables need memory to store the data value, and programs  need memory to execute. For a function, the name of it is the address stored in.

Therefore, we can also use pointer to points a function. Different type of function must be pointed by different pointers.

```C++
return_type (*pointer_name)(data_type1,data_type2,...);
```

<練習> Write two functions to complete the following program.

```C++
int main(){
    int a = 5,b = 10;
    int (*pfun)(int,int);
    pfun = add;
    res = pfun(a,b);
    cout<<res<<endl;
    pfun = product;
    res = pfun(a,b);
    cout<<res<<endl;
}
```

## Double pointer
Double pointer is the pointer that points to another pointer. To decalre a double pointer, we must type ** before the variable name.

```C++
int *pi;
int **ppi;
```

A 2-D array itself is also a double pointer.

```C++

/* row, column
0 0 0 0
0 0 0 0
0 0 0 0
*/
int arr[3][4]={0};
printf("arr[0][0] is at %p\n",arr[0]);
printf("arr[1][0] is at %p\n",arr[1]);
printf("arr[2][0] is at %p\n",arr[2]);
arr[0][0]=1;
*(arr[1]+1)=1;
//arr[1][1]=1;
*(arr[2]+2)=1;
//print and see
```

<思考> Why we need to use pointer to access the array? What is the pros by using the pointer?

<BONUS練習>(HARD) Write a program that can add up two 2D arrays. Try to make the program as fast as possible!

## Return Statement

Return statement can be in expressions.
```C++
return a+b;
return (a+b)*d;
return a>b ? a:b;
...
```

If a function returns an int, but the return statement contains a double expression, the value of the expression is converted to int.

```C++

#include <iostream>

using namespace std;

double test2(){
    return 2+5;
}

int test(){
    return 1.0+3.5;
    //4.5=>4
}

int main(){
    cout<<test2()<<endl;
}
```

We can end the function if we need by return statement, even if the function type is void
```C++
void print_int(int i){
    if (i < 0)
        return;
    printf("%d", i);
}

```

              
## Program exit
When the program exit with return value 0 is normal terminates. Using the exit() function in stdlib.h can end the main function, too.

The argument passed to exit has the same meaning as the return value of main function: both indicate the program’s status at termination. As a result, we’d pass 0 to indicate normal termination.

The difference between return and exit is that exit causes program termination regardless of which function calls it.

## Recursion
A function is recursive if it calls itself. For example:
```C++
int fact(int n){
    if (n <= 1)
        return 1;
    else
        return n * fact(n - 1);
    // return 5*fact(4);
        // return 4*fact(3);
            //return 3*fact(2);
                //return 2*fact(1);
                    //return 1
    // =>return 5*4*3*2*1
}
```


<練習>Please write a recursive function to calculate the expoential of given number.
**Funciton Input** : x y
**Function Output** : x^y^              
```C++

int power(int x, int y){
    if(y>0){
        return x*power(x,y-1); 
    }
    else{
        return 1;
    }
}
```
    
    
<Function格式複習>
![](https://i.imgur.com/j4x3l4q.png)
[image reference](https://www.geeksforgeeks.org/argument-coercion-in-c-c/)