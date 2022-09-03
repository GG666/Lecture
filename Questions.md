[TOC]

# Questions

## 1. Why we need additional space for struct
##### [64-bit Online Compiler](https://www.online-ide.com/online_c++_ide)
### Strcture padding
#### Before
![](https://i.imgur.com/Pjy9Mck.png)
#### After
![](https://i.imgur.com/EPPKBLU.png)
##### Structure padding is used to save number of CPU cycles
In 32 bit processor, it can access 4 bytes at a time which means word size is 4 bytes.
Similarly in a 64 bit processor, it can access 8 bytes at a time which means word size is 8 bytes.

```c++
#include <stdio.h>
//64-bit的環境，pointer的size是8 bytes(1byte=8 bits)
struct ABC {
    int n1; //4+padding => 8
    int* n2; //9-16
    char c1; //17+padding-24
    char* c2; //25-32
};

int main()
{
    struct ABC a;
    printf("Size of struct ABC: %lu\n", sizeof(struct ABC));
    printf("Size of object a: %lu\n", sizeof(a));
    return 0;
}
```


```
#include <stdio.h>
//64bit=一次8bytes
struct BAC {
    int* n2;//0-8
    char c1;//9
    int n1;//10-14
    char* c2;//17-24
};

int main()
{
    struct BAC b;
    printf("Size of struct BAC: %lu\n", sizeof(struct BAC));
    printf("Size of object b: %lu\n", sizeof(b));
    return 0;
}
```

```
#pragma pack(1)
#include <stdio.h>

struct BAC {
    int* n2;
    char c1;
    int n1;
    char* c2;
};

int main()
{
    struct BAC b;
    printf("Size of struct BAC: %lu\n", sizeof(struct BAC));
    printf("Size of object b: %lu\n", sizeof(b));
    return 0;
}
```
[Structure padding](https://w3cschoool.com/tutorial/structure-padding-in-c?msclkid=2128f99bcf8c11ecb9e57edcba08be68)
[資料來源](https://iq.opengenus.org/size-of-struct-in-c/)


# 2. Input and Outputs in C
## printf 

```C++
printf("Hello world %[flags][width][.precision][l|h|L]type...", variable1, varriable2)
```

#### Type : The only necessary element.

%c => char
%d => int
%s => string
%o => unsigned octal
%u => unsigned integer
%e => float in scientfic notation(%E => uppercase letter 'E')
%f => float accurate (output 6 digits after the point)
%g => output result depend on the accuracy of the float (%G=>uppercase 'E')
%x => unsigned hexidemal integer lowercase(%X => uppercase letter)

Question : What if we want to print the character '%'
:::spoiler Answer
printf("%%");
:::

```C++
#include <stdio.h>
int main(){
    int a=50;
    double d=0.003;
    double more_digits=0.000038345064;
    printf("%d in octal is %o, in hexidemal is %x\n",a,a,a);
    printf("0.003 with %%f is %f\n",d);
    printf("0.003 with %%e is %e\n",d);
    printf("0.003 with %%g is %g\n",d);
    //use above method to print out more_digits
}
```



#### width
Indicates the minimum number of output characters, when the output is less than the given width, the output will fill with spaces on the left.

Question : Please think about what outputs will the following code be? Then explain it.

```C++
#include <stdio.h>
int main(){
    printf("%5f\n",0.1);
    printf("%5E\n",0.1);
    printf("%5g\n",0.1);
}
```


#### flags
**%-** :  Align left (left-justify)

**%+** :  Print plus-minus sign on the left

**%0** :  Left-pads the number with zeroes (0) instead of spaces when padding is specified

**%SPACE** :  If no sign is going to be written, a blank space is inserted before the value.

**%#** :  Used with o, x or X specifiers the value is preceeded with 0, 0x or 0X respectively for values different than zero.
Used with a, A, e, E, f, F, g or G it forces the written output to contain a decimal point even if no more digits follow. By default, if no digits follow, no decimal point is written.

#### .precision

**For integer** specifiers (d, i, o, u, x, X): precision specifies the minimum number of digits to be written. If the value to be written is shorter than this number, the result is padded with leading zeros. The value is not truncated even if the result is longer. A precision of 0 means that no character is written for the value 0.

**For a, A, e, E, f and F** specifiers: this is the number of digits to be printed after the decimal point (by default, this is 6).

**For g and G** specifiers: This is the maximum number of **significant** digits to be printed.

**For s**: this is the maximum number of characters to be printed. By default all characters are printed until the ending null character is encountered.
If the period is specified without an explicit value for precision, 0 is assumed.


```C++
#include<iostream>

using namespace std;

int main()
{
    printf("%10.5d",5);
    //practice
}

```

#### l|h|L
%lld => long long 
%hd => short
%Ld => long double

```C++
#include<stdio.h>
#define ll long long
int main(){
    ll test = 220000000;
    printf("%lld",test);
    //practice
}

```

<練習>
    Please print a pyramid with C ( like last time we did with C++)
    
[Printf reference](https://www.cplusplus.com/reference/cstdio/printf/)

#### <Bonus> About the float in C/C++

Please read the following code and tell the what the outputs will be?
    
```C++
#include<stdio.h> 
int main() 
{ 
    float f1 = 520.02; 
    float f2 = 520.04; 
    float f3 = 0.02;
    float f4 = 0.04;
    float result = f1 - f2;
    float res2 = f3 - f4;
    float res3 = f2 - f1;
    printf("result=%f, expected -0.02\n", result);
    printf("result=%f, expected 0.02\n", res3);
    printf("result=%f, expected -0.02\n", res2);
}
```

But how...?
    
```C++
#include <stdio.h>

int main()
{
    float ff=0.000000000000000000000000000000000000000000000000000000000000000000000055;
    printf("%e\n",0.055);
    printf("%0.500f",ff);
}
```

[example reference](https://www.ibm.com/support/pages/single-precision-floating-point-accuracy)
[Chinese resources](https://docs.microsoft.com/zh-tw/cpp/c-language/type-float?view=msvc-170)
[How they encode the float](https://walkonnet.com/archives/468703)
[C++ reference about printf](https://www.cplusplus.com/reference/cstdio/printf/)
    
## Puts and putchar
puts( ) : Output the given string and an additional \n (print new line) at the end4
putchar( ) : Output a character

**<練習>** print hello world with both put and putchar

**<練習>** 請使用剛剛學到的輸出方式，設計一個程式，幫助統計家庭收入，並印出
**Input** : *Total num of famaily* , *Their year incount* 
**Output** : *Average incount of all family*, and their incount separately, remember, you have to keep the output easy to read like below:

**<restrict>** The incount of a family will less than 10^8^+1, and the numbers of family will less than 10000.

```C++
The average income of this town is 1000000
Family 1 have    500000 incount this year.
Family 2 have   1500000 incount this year.
Family 3 have  25500000 incount this year.
...
```

<複習> 請寫出printf的格式
```C++
print(???,???,???,???,???,...);
```

## Scanf
```C++
scanf("%[*][width][l|h|L]type",& variable_name);
//format
```

#### width
Indicates the upperbound of the input size. If the input size is more than given restrict, it will ignore it.

```C++
#include <stdio.h>
int main(){
    int test = 0;
    scanf( "%4d", &test);
    printf( "%d\n", test);
}
```
    
#### l|h|L
Help program to store the data.
for example:

```C++
#include <stdio.h>
int main(){
    short  test1,test2;
    scanf("%d %d",&test1,test2);
    printf("%hd %hd",test1,test2);
}
```
    

    
<練習>
    輸入兩數x,y，請輸出交換後的結果，如下所示
```C++
請輸入x和y，並使用逗號隔開輸入 : 3,5
交換後x為5，y為3
```

#### *
\* means skip this input, for example:

```C++
#include <cstdio>

int main(){
    int a, b;
    scanf("%d%*d%d", &a, &b);
    printf("%d %d\n", a, b);
}
```
    
#### How to solve the problem we meet last time? And what happend?

```C++
//case 1
#include <iostream>

using namespace std;

int main()
{
    float test=0.1;
    printf("hello!\n");
    scanf("%f\n",&test);
    printf("%f\n",test);
    scanf("%f",&test);
    printf("%f",test);
    return 0;
}
```

解釋: 處理格式串中的普通字元時，**scanf**函數採取的動作依賴於這個字元是否為' '(**Space**)或'**\n**'，或"**ENTER**"為特殊情況處理

以空白字元為例，當在格式串中遇到一個或多個連續的空白字元時，scanf函數從輸入中重複讀空白字元直到遇到一個非空白字元為止。 格式串中的一個空白字元可以與輸入中任意數量的空白字元相匹配，包括0個。

其它字元。 當在格式串中遇到非空白字元時，scanf函數將把它與下一個輸入字元進行比較。 如果兩個字元相匹配，那麼scanf函數會放棄輸入字元而繼續處理格式串。 如果兩個字元不匹配，那麼scanf函數會把不匹配的字元放回輸入中，然後異常退出。

格式串中，由於遇到了空白字元'\n'，因此還會“重複讀空白字元直到遇到一個非空白字元為止”，由於輸入緩衝已經沒有字元可讀了，因此將阻塞等待，直到讀入了一個非空白字元為止。

這個時候，如果繼續按下空格或ENTER，程式還是會阻塞，直到輸入一個非空白字元為止。

解決方式:
    0. 注意規定輸出輸入之格式
    1. 使用fflush(stdin);來清除buffer(**不建議!**)
    [原因](https://www.geeksforgeeks.org/use-fflushstdin-c/)
    2. 使用getchar()
    
```C++

#include <iostream>

using namespace std;

int main()
{
    float test=0.1,test2=0.03;
    printf("hello!\n");
    scanf("%f%f ",&test,&test2);
    printf("%f %f\n",test,test2);
    return 0;
}

```
    
```C++
//case 2
#include<cstdio>

int main(){
    char c1,c2;
    printf("Input a char: \n");
    scanf("%c",&c1);
    printf("Input a char: \n");
    scanf("%c",&c2);
    printf("c1 = %c\n",c1);
    printf("c2 = %d\n",c2);
}
```
CR = Carriage Return
LF = Line Feed

```
O  O  O
C CR LF 
```

## getchar/getche/getch

```C++
#include<stdio.h>
#include<conio.h>

int main(){
     char cx;
     printf("Input a char: ");
     cx=getchar();
     printf("The input char is : %c\n",cx);
     printf("Input a char: ");
     cx=getch();
     printf("\nThe input char is %c\n",cx);
     printf("Input a char: ");
     cx=getche();
     printf("\nThe input char is %c\n",cx);
}
```
```C++
#include<stdio.h>
 
int main()
{
    char str[80], ch;
     
    // scan input from user -
    // GeeksforGeeks for example
    scanf("%s", str);
     
    // flushes the standard input
    // (clears the input buffer)
    while ((getchar()) != '\n');
     
    // scan character from user -
    // 'a' for example
    ch = getchar();
     
    // Printing character array,
    // prints “GeeksforGeeks”)
    printf("%s\n", str);
     
    // Printing character a: It
    // will print 'a' this time
    printf("%c", ch);
 
    return 0;
}
```

## Some problems 
<練習> 輸入2個空白後輸入100NTD，並觀察輸出後的結果並使用適當方式儲存結果
    
<練習> 請寫出一個程式來讀入兩個char type的input，並於第一次輸入時輸入>=2長度的string，並觀察結果

<練習> 承上題，此時第二次input char 時使用getchar()，並觀察其結果
    
<練習>
    網站上需要核對身分，所以需要身分證來確認，但是一般情況下不能給別人看到，請你幫忙處理大家的身分證，讓輸出只有身分證的末4碼。

    
[Clear buffer](https://www.geeksforgeeks.org/clearing-the-input-buffer-in-cc/)
    
    
