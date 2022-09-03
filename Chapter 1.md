[TOC]
# Chapter 1

## Operator
**比較常用的有加(+)、減(-)、乘(*)、除(/)、取餘(%)，
還有(++)、(- -) 、 (!)，以及比大小的 <,>,<=,>=,==,!=等等
當然還有許多一樣相當有用的Operator，我們之後有機會會再提到**
[詳細資訊(WIKI)](https://zh.wikipedia.org/zh-tw/C%E5%92%8CC%2B%2B%E9%81%8B%E7%AE%97%E5%AD%90)

## if, else if, else

```C++=
#include<iostream>
using namespace std;
int main(){
    bool flag;
    if(flag){ //有沒有立flag
        //立旗了....
    }
    //scope
    int a=1;
    for(int i=0;i<10;i++){
        //scope
        int b=2;
    }
    cout<<b<<endl;
    //error
}
```
**從上面的程式碼我們可以觀察到**
1. if是不用搭配著else一起出現
2. if後面的小括號()裡頭放的是判斷式
3. 大括號{ }裡則是程式內容，我們也發現{ }通常代表著一個scope的產生

**<練習1>**

請你們寫一個C/C++程式來判斷輸入是奇數還是偶數吧~
**input : Some number
output : It's odd/even!**

**<練習2>**

請你們寫一個C/C++程式來判斷輸入是3的倍數、5的倍數、7的倍數、或同時是他們的倍數吧~
**input : Some number
output : It's odd/even!**
****
## while
**while的語法跟if很像，差別在於while會一直執行直到()中的條件不成立為止，所以可能會產生無窮迴圈的問題，使用的時候務必注意**
```C++=
#include<iostream>
using namespace std;
int main(){
    int a=10;
    bool flag;
    cin>>flag;
    while(flag){
        while(a--){
            cout<<a<<endl;
        }
    }
}
```
**<練習3>**
請你們寫個程式來幫助教授決定哪些人要收到期中預警吧，(期中考低於60分的會收到預警)
input : 教授會先給你班上的總人數，接下來的數字依序是他們的分數
output : x
```
輸入:
5 
95 
77 
68 
32 
51
```
```
輸出:
4 5
```

## Array(陣列)
**在C/C++ 中，array是一種資料結構，我們可以簡單地把array想成是一排格子，格子裡可以放其他的資料，包括int, char, bool 甚至是其他array**

```C++=
#include<iostream>
#define size 10
using namespace std;
int main(){
    int arr[size]={1,2,3,4,5,6,7,8,9,10};
}
```

**<練習4>**
小明養了很多貓，他想要將他們的資料編號並紀錄下來，請你幫助小明建立一個表，讓小明能快速地找到貓咪的資料吧
input : 貓的數量,每隻貓咪的資料
output : 某隻貓的資料
