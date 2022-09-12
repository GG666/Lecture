# Chapter 2
[TOC]

[Online IDE](https://www.onlinegdb.com/online_c++_compiler)
#### 小複習

Question1
```C++
int a[10]={1,2,3,4,5,6};
//1 2 3 4 5 6 0 0 0 0
//這樣array a現在存著什麼資料呢?
```
Question2
```C++
int a[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int b[5] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
//哪個寫法是錯的?
```

### Array(Continue)

```C++
int a[15] = {[14] = 48, [9] = 7, [2] = 29};

```

```C++
int b[] = {[5] = 10, [23] = 13, [11] = 36, [15] = 29};
// b[5]
// 0 0 0 0 0 10
```

<練習1>
請你寫一個程式來判斷一串數字中重複的數是哪個，重複幾次
```
Input : 5 2 2 8 4 2
Output : 2 3

//use a[] to store the data that appears
//set the array size to 100

a[0]=1, 0 appears one time
a[1]=10, 1 appears 10 times
```

#### 2-dimension array

```C++
int m[5][9] = {{1, 1, 1, 1, 1, 0, 1, 1, 1},
 {0, 1, 0, 1, 0, 1, 0, 1, 0},
 {0, 1, 0, 1, 1, 0, 0, 1, 0},
 {1, 1, 0, 1, 0, 0, 0, 1, 0},
 {1, 1, 0, 1, 0, 0, 1, 1, 1}}; 
```

```C++
double ident[2][2] = {[0][0] = 1.0, [1][1] = 1.0};
```

#### Constant array
```C++
const char hex_chars[] =
 {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9',
 'A', 'B', 'C', 'D', 'E', 'F'}
```
<Zerojudge練習>
[陣列應用(可能有點難)](https://zerojudge.tw/ShowProblem?problemid=a248)


### Strings(char)
Strings are arrays of characters in which a special 
character—the null character(\0)—marks the end

```C++
char str[STR_LEN+1];
//string 的宣告
```


• If the initializer is too short to fill the string variable, the 
compiler adds extra null characters:

```C++
char date2[9] = "May 21";
```

Omitting the length of a string variable is especially useful 
if the initializer is long, since computing the length by 
hand is error-prone.

```C++
char str[] = "How long will the input be?";
```

<練習2>
請寫出一個計算空格數量的程式
Input: I am a student.
Output: 3

```C++
#include <stdio.h>

int main()
{
  char string [256];
  printf ("Insert your full address: ");
  gets (string);     // warning: unsafe (see fgets instead)
  printf ("Your address is: %s\n",string);
  return 0;
}
```


```C++
char s[100];
gets(s);
```


<練習3>
呈上題，請寫出一個計算空格數量的function

#### strcpy
```C++
class string{
    operator overloading
    //when it comes to a '='
    string s="abc";
}
```

```C++
char str1[10], str2[10];
…
str1 = "abc"; /*** WRONG ***/
str2 = str1; /*** WRONG ***/
if (str1 == str2) … /*** WRONG ***/
```

```C++
//str2 contains "abcd"
strcpy(str1, str2);
/* str1 now contains "abcd" */
strcpy(str2, "abcd");
/* str2 now contains "abcd" */
```


#### strlen
strlen returns the length of a string s, not including the 
null character.

```C++
int len;
len = strlen("abc"); /* len is now 3 */
len = strlen(""); /* len is now 0 */
strcpy(str1, "abc");
len = strlen(str1); /* len is now 3 */
```


#### strcat

strcat appends the contents of the string s2 to the end of the string s1.
```C++
strcpy(str1, "abc");
strcat(str1, "def");
/* str1 now contains "abcdef" */
strcpy(str1, "abc");
strcpy(str2, "def");
strcat(str1, str2);
/* str1 now contains "abcdef" */
```

<練習4>
請將"abc","def","ghi"組合成一個string並存在名叫res的string中

<練習5>
用你們的資工實力想想辦法，請找出cstring裡的其他函式

## For-loop
Like what we have said before, for-loop is a very useful tool.

Below is the structure of a for-loop

```C++
for ( *initail condition; *break when false ; *change of condition){
    // contents...
}
```

<練習6> (不使用if else)
計算1~100中所有奇數之合
計算1~100中所有偶數之合

<Bonus> Print uppercase letters using for-loop (A~Z)

<練習7> Print a pyramid like below
    
![](https://i.imgur.com/9Oea1Qz.jpg)
    
## Switch
```C++
    char c;
    switch ( c )
      {
         case 'A':
            cout<<"We come to an A emergency !";
            break;
         case 'a':
            cout<<"We come to an A emergency !";
            break;
         default:
            cout<<"Nothing big deal~";            
      }
```
    
```C++
    int a=0;
    switch ( a )
      {
         case 0:
            cout<<"We come to an A emergency !";
    
         case 1:
            cout<<"We come to an A emergency !";
         default:
            cout<<"Nothing big deal~";            
      }
```
