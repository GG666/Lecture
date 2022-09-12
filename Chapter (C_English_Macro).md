# New Chapter 

[TOC]


## Macro

The #define is used to define macro. There are two types of macro that can be defined by it:

**Review**

```C++
#define MacroName Replace_Code
```

```C++
#define Pi 3.14159265358979323846
#define Pi2 2*Pi
#define Input_String "Please input your info\n\
Name, Age, Gender.\n"
```

### function-like macro

Function-like macro can help to improve the readability of our program. In contrast to functions, macro is faster because it reduces the function call, which causes function overhead.
[function overhead](http://www.angelcode.com/dev/callconv/callconv.html)

```C++
#define SQUARE(x) x*x
#define MIN(a,b) a>b ? b:a
#define CUBE(x) x*x*x
```

<問題>
However, the macro above will be insecure cause the preprocessor just unfolds the macro into the program. For example, call the SQUARE macro with the argument x=2+2, and see what happened.

```C++
SQUARE(2+2) => 2+2*2+2
#define SQUARE(x) (x)*(x)
```

### Preprocessor

Preprocessor can do many things ,like below:
```C++
1.
#include 
2.
#define
3.
#ifdef,#ifndef.....

#include "file_name"
```
When writing a much more complex program, we need to separate the different functions and different codes in different files. In that way, we can manage our program more efficiently.

Let's try to write a program that defines many macros as a .h(標頭檔) file, and includes it in the other file. Remember that the two files must be in the same folder.

## Struct

When we need to store data with certain struct(like students have their names, grades, numbers, ...). We may not want to store it in different arrays, cause it will cost more time to access different arrays and more code to implement it.

Therefore, C provides a way to deal with the problem.
Below is the prototype of writing a struct.

```C++
struct struct_name{
    type1 variable_name1;
    type2 variable_name1;
    type3 variable_name1;
    type1 variable_name1;
};
// notice that the declare of struct is still a statement, like other declarations, it must have ; in the end  
```

<練習> Please write a struct that includes the math grade, English grade, gender, number, and name of a student.


To change the value of a struct variable, we have to use the '.' operator.
like below:

```C++
struct Students s1;
s1.eng_grade = 75;
s1.name = "Bob";
s1.math_grade = 71;
scanf("%d",&s1.chem_grade);
...
```


There is also a different way to initialize a struct. In addition, struct supplies the '=' operator.

```C++
struct Student{
    char Name[10];
    bool Gender;
    int Age;
} stu1 = {"Bob",1,15}, stu2 = {"Alice",0,16};
int main(){
    //print something
    stu1=stu2;
    //print something
    ...
}
```

### Struct array

Like other types, struct type can also form an array. Like other types of arrays, a struct-type array stores a struct in every entry. In other words, every block is a struct.

```C++
struct struct_name array_name[array_size];
```

<練習> Please write a struct that contains an array to store grades of 3 different subjects (Like Math, English, Chemistry) and students' names.

<練習> Following the previous question, please write a program that let users input the data of students.

### Struct pointer

The way to use a struct pointer is very similar to other pointers. It is like those pointers that point to an array. A struct variable has the same address as its first element. 

```C++
struct Student *sp; //student pointer
sp = &s1;
cout<<sp->eng_grade<<" <=English Math=> "<<sp->math_grade<<endl;
cout<<(*sp).eng_grade<<endl;// equal to s1.eng_grade
...
```

We can use the  **->** instead of **'*'** to dereference an address.

### Nested struct

When a struct contains another struct, we can call it a nested struct.

```C++
struct People{
    char Name[10];
    int Age;
};

struct Student{
    struct People p;
    int Class_number;
    int Grade;
};
```

Remember the operator '.' is to access the member of a struct.

<練習> The Fibonacci sequence is famous in math and computer science.
Please write a function to calculate F(15) where F(0)=1 and F(1)=1

### Union and typedef

#### union
Union is a way to save your space. When an element in the union is declared, other elements will be deleted.

```C++
union example{
    v_type v_name;
    v_type v_name;
    v_type v_name;
    ...
};
```

For example, a person is most likely to be a student or a teacher when we meet in school. However, a teacher in the school can not be a student at the same time, therefore, when we say a person is a student, we store the data. In that case, we don't need a space to store the information of the teacher.

```C++
struct Teacher{
    int ID;
    int Years;
};

struct Student{
    int Number;
    int Grade;
}

struct PersonalInfor{
    char Name[10];
    bool StudentOrTeacher;
    union{
        struct Teacher t;
        struct Student s;
    }
}
int main(){
    //input and see what happened!
}
```
