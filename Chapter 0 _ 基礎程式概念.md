# Chapter 0 : 基礎程式概念

[TOC]

#### 有什麼問題，隨時都歡迎提出來

### Hello World複習
```C++=
#include<iostream>
using namespace std;
int main(){
    string s="Hello World!"
    cout<<s<<'\n';
}
```


#### 在上面的Hello World code(程式碼)中，我們注意到這個程式本身主要由三個部分構成

**1. #inlcude<iostream>**

**2. using namespace std;**

**3. int main(){
    //content....
}**

## **標頭檔** and **Function**(函式)
### Function
#### 在數學等領域常常會碰到function此一名詞，數學中的function定義了input(輸入)與output(輸出)之間的關係，同理C/C++中的function也需要input, output，更具體的形容的話，我們可以將我們的程式想成一個畫出一台汽車的工作，而函式就是畫好的輪子，我們只需要畫一次，之後就可以在需要的地方使用這些輪子，舉例練習如下

```C++=

#include<iostream>
using namespace std;

//我是function
int BMI(float height , int weight){
    int temp;
    temp=(BMI算法...)
    return ??
}
    
int main(){
    int height,weight;
    cout<<"請輸入小明身高體重";
    cin>>小明身高體重;
    ...
    ...
    cout<<小明BMI
    cout<<小美BMI
    ...
}
```

### 標頭檔
#### 第一行中的 #include<iostream> 表示我們載入需要使用的的標頭檔，C中的標準函式庫都是以".h"為附檔名(如stdio.h, stdlib.h等)，又因為C++是向下相容(C++由C發展而來)，所以我們可以在C++中使用C的function，而C的標頭檔(stdio.h)皆可以去掉副檔名並在開頭加上'c'來向程式宣告載入
    
    e.g.
        #include <math.h> 等於 #include <cmath>
        #include <time.h> 等於 #include <ctime>
    
#### 而標頭檔就是定義了許多function(函式)的地方，以剛剛的例子來說，我們可以將標頭檔想成包含許多汽車零件的繪圖軟體，善用這些零件，就能幫助我們省下許多時間
    
```C++=

#include<iostream>
//#include<cmath>
using namespace std;

int main(){
    int height,weight;
    float h;
    cout << "請輸入小明身高體重";
    cin >> height >> weight;
    h=float(height)/100;
    cout << weight/pow(h, 2)<<endl;//h的二次方
}
```
    
```C++=
int main(){
    return 0;
}
```
    
## Namepsace(命名空間)
    
### Identifier(ID)
#### 是一個用來識別物件的名稱，識別對象可能是概念、具體可數的物體或是不可數的物質。標識符可能是字、編號、字母、符號，也可能是由上述元素所組成。

1. 由字母（A-Z,a-z）、數字（0-9）、下劃線「_」組成，並且首字符不能是數字，但可以是字母或者下劃線。

2. 不能把關鍵字、預定義標識符、標準庫函數名等作為用戶標識符

3. 標識符命名應做到「見名知意」

#### (Above information from wiki pedia, you can check the link below for more informationds)

[英文這裡](https://en.wikipedia.org/wiki/Identifier)
[中文這裡](https://zh.wikipedia.org/wiki/%E6%A8%99%E8%AD%98%E7%AC%A6)    
### Scope
#### 在C/C++中，Scope表示了一個variable(變數)可使用的範圍，舉例練習如下

```C++=
int main(){
    int A=10;
    int B=100;
    int C=1000;
    for(int B=0;B<10;B++){
        int A=20;
        for(int C=0;C<20;C++){
            int A=30;
            cout<<A,B,C...
        }
        cout<<A,B,C...
    }
    cout<<A,B,C...
}
```
由上面的練習我們可以知道每個variable都有其使用的範圍

### Namespace
#### 命名空間（英語：Namespace），它表示著一個識別碼（identifier）的***可見範圍***。一個識別碼可在多個命名空間中定義，它在不同命名空間中的含義是互不相干的。這樣，在一個新的命名空間中可定義任何識別碼，它們不會與任何已有的識別碼發生衝突，因為已有的定義都處於其他命名空間中。

#### 例如，設Bill是X公司的員工，工號為123，而John是Y公司的員工，工號也是123。由於兩人在不同的公司工作，可以使用相同的工號來標識而不會造成混亂，這裡每個公司就表示一個獨立的命名空間。如果兩人在同一家公司工作，其工號就不能相同了，否則在支付工資時便會發生混亂。

[更多資訊(英文)](https://en.wikipedia.org/wiki/Namespace)
[更多資訊(中文)](https://zh.wikipedia.org/wiki/%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)


## Main function
#### 如同所有function，在main之前需有一個Type代表函式回傳值的資料型別，而main function 特別的地方在於他是C/C++的預設進入點，當程式載入記憶體後就是從這裡開始執行，直到main function 結束(以{}圍住的部分)

以上就是一個.c/.cpp檔的組成元素，接下來我們來看其他更細部的東西
    

## Variable and Constant
### Variable
#### variable就是可以改變的數，最常見且貼切的形容就是抽屜，我們需要先決定資料要放在哪種抽屜(Type)的第幾格(Memory location)，當然，具體位置是交給CPU決定的，我們能做的就是declare(宣告)和assign(賦值)，C/C++中對於等號運用在variable的規則有下列兩個
    1. 等號左邊只能是*一個*變數，且不能是運算式
    2. 等號右邊的運算結果儲存到等號左邊之變數中
    
```C++=
#include<iostream>
using namespace std;

int main(){
    int a=10;
    //在這裡印a觀察
    a=a++;
    //在這裡印a觀察;
    int b=a*5+3;
    //在這裡印b觀察
}
```
    
* 注意!同一個Scope中不能有相同名稱之variable(會導致compiler無法判斷哪一個)
#### 同樣的我們不能使用 'for', 'break' 等詞作為變數名稱
    
### Constant
#### 有時候我們會遇到一些固定不變的數值(圓周率)、名稱等，為了方便管理、節省程式碼開發時間，我們會使用Constant。常數的宣告模式如下 : 
    #define Constant_name Constant_value

```C++=
#include<iostream>
#define pi 3.14
#define my_name "Bob"
using namespace std;
int main(){
    cout<<pi<<endl;
    cout<<my_name<<endl;
}
```

    
## Type(型別)
#### 我們知道，在目前大部分計算機(computer)上都是以位元(BITS)，來儲存資料。而1bit 能代表兩種情況(0或1)，那麼問題來了?我們該怎麼儲存平常生活中會用到的數字、單字呢?

:::spoiler Answer
ASCII CODE編碼(C/C++)，2進位表示數字

![](https://i.imgur.com/vsDDkNm.png)
    
:::

#### 透過上面的編碼，我們可以使用1bytes(8bits)的空間來儲存所有字符，更進一步，我們希望可以用最少的空間儲存最大資料量，假如我們已經確定我們要處理的資料類別的話，我們就可以更好的利用空間，比如int的大小為 4 bytes (32 bits)，那麼根據2進位表示法，我們最多能表示2^32^個不同的數字，在C/C++中int的範圍為-2^31^~2^31^-1。
    

```C++=

#include<iostream>
using namespace std;

struct node{
    int test,test2;
    bool TT;
    float FF;
};

struct node2{
    int test,test2;
    float FF;
};


int main(){
    int int_size_test,arr_size_test[10];
    char char_size_test;
    bool bool_size_test;
    double double_size_test;
    float float_size_test;
    long long long_long_size_test;
    string string_size_test="It's a test string.....";
    cout << "The size of int is " << sizeof(int_size_test) << " bytes." << endl;
}
```

這樣我們就對基本的Type有了概念了
    
[更多TYPE資料請參考這裡](https://en.cppreference.com/w/cpp/language/sizeof)    


## From .c/.cpp to .exe

### 編譯
#### 編譯就是將我們的程式碼從英文句子轉換為CPU可執行的程式，因此在這裡會檢查語法錯誤(Compile Error)，如果沒有錯誤，Source Code (程式碼) 會轉成Object file (目的檔) ，並以 .o/.obj 為附檔名，目的檔包含了 Source Code 對記憶體的使用需求，以及使用到的外部函式(需在#include中表明)，並在此載入標頭檔
    
### Linker(連結器)
#### Linker的主要工作是將程式所需之外部資源都整合進來，比如使用了printf或scanf等函式，雖然在編譯後的Object file 中已載入標頭檔 stdio.h，但是這個標頭檔僅包含printf與scanf的定義與使用規則，實際負責執行的主體放在 .lib 檔中，Linker的工作就是依照object file 指名所需要的函式，從相對應的函式庫中找出來，並將其與object file 連結在一起，建置出程式的.exe檔

那麼到這邊基礎程式概念就到一段落了
#### 到這裡，有什麼問題嗎?
#### 如果沒有的話我這裡有個小問題，請問下面程式會跑出什麼結果?

```C++=
#include<iostream>
#define for 3.14
using namespace std;
int main(){
    cout<<for<<endl;
}
```

:::spoiler Explain
   #### 在這裡我們注意到Constant 的宣告需要在前面加上'#'這個符號，這代表這段敘述與#include<標頭檔>一樣，都是交由preprocesser處理，而preprocesser處理時，會在編譯前將所有與其相同的詞語，直接替換成我們定義的值，在這個案例中，preprocesser執行後程式碼會直接變成
```C++=
#include<iostream>
#define for 3.14
using namespace std;
int main(){
    cout<<3.14<<endl;
}
```
因此編譯時不會產生錯誤，同理

```C++=
#include<iostream>
#define for 3.14
using namespace std;
int main(){
    for(int i=0;i<10;i++){
        cout<<i<<endl;
    }
}
```

#### 則會產生錯誤，這是因為所有的for在preprocesser執行後都已經變成3.14的關係，至於Preprocesser，之後有機會再介紹
:::

:::spoiler 那如果沒有問題就....
:::success
~~耶!可以下課了~  :tada:~~

    

#### 等一等，在下課之前，我們先來練習一下八
[第零題](https://zerojudge.tw/ShowProblem?problemid=d498)
[第一題](https://zerojudge.tw/ShowProblem?problemid=a244)
[第二題](https://zerojudge.tw/ShowProblem?problemid=a058)
[第三題](https://zerojudge.tw/ShowProblem?problemid=a065)
[第四題](https://zerojudge.tw/ShowProblem?problemid=a038)
[online IDE(線上C++)](https://www.onlinegdb.com/online_c++_compiler)

:::
<!--     
## 基本語法規則

### 註解方式
#### //單行註解 and /* */多行註解 -->