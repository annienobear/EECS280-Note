# EECS 280

## Machine Model/Procedural Abstraction

### Lecture:

Abstraction: 把功能浓缩进简单的代码里而非每次重复implement全部

Procedure Abstraction: why we use so many files, cpp/h file, separate of interface from implementation

- Local: The implementation of an abstraction can be understood without examining any other abstraction implementation
- Substitutable:  可以给同一个hfile写不同的cpp implementation

#### Compile time terminology:

No missing ingredients (function definitions)

No expired ingredients (syntax error)

- ***Difference between variable and object***
  - Variable: compile time stuff, name that refer to an object in memory
  - Object: Piece of data in memory, runtime stuff



- Scope: area of code where it can be used.
- Declaration: introduce a name and begins its scope
- Name: refer to something

#### Runtime terminology:

Object. Lives at an address in memory

- Lifetime: you can use an object during its lifetime
- Lifetime managed according to storage duration, by compiler
  - Static: lives for the whole program
  - Automatic: local
  - Dynamic: you control

#### Reference semantics

Declare like &+name

```c++
int x = 42;
int z = 3;
int &y = x; // sharing same object/address
```

#### Call Stack: Function Calls

每次call新的function都是往stack里面加，运行完之后移除

#### Pass By Value/Reference

By value:

```c++
void abc(int x)
```

By reference: modify object outside the function

```c++
void abc(int &x)
```

#### Comment ?

#### Tests

ASSERT: check the require clause from REM, do not assume any activity except from REM

Type: 

- Unit testing
  - One piece at a time
  - Fix and find bug early
- System testing
  - After unit testing
  - Test the whole project
- Regression testing
  - code change后自动跑所有unit和system



### 考点：

- Variable 不等于object

- 给一段code看什么是variable什么是object

  - 如果有相同的address那就是一个object，但是可以有多个variable

- memory diagram指runtime perspective

- value之间相等是copy 数值

- reference

  - 不能rebind reference variable

  - ```c++
    int &x = y; // & is part of the type
    cout << &x << endl; // & is an operator returns the address
    ```

  - 

- Memory Using: 给每个variable/function占的大小算最多用多少空间

  - Lecture 2，45mins左右

## Object kinds

- Atomic
  - Primitive
  - int, doublt, char, etc
  - Pointer
- Arrays (homogeneous)
  - A contiguous sequence of objects of the ***same type***
- Class-type (heterogeneous)
  - A compound object made up of member subobjects
  - struct/class

## Pointers & Arrays

Object to store address: 

```c++
int *ptr = &x;
```

也算object也会被存储进memory diagram

get the object a pointer points to use * operator. 

考点：

- 不同data之间的pointer type不能相等：compiler error

#### Reference and Pointer

<table>
    <tr>
    	<th>Reference</th>
        <th>Pointers</th>
    </tr>
    <tr>
    	<td>An alias for an object</td>
        <td>Stores address of an object</td>
    </tr>
    <tr>
    	<td>Cannot rebind to another object</td>
        <td>Can change where it points</td>
    </tr>
    <tr>
    	<td>Cannot refer to NULL</td>
        <td>Can point to NULL</td>
    </tr>
</table>

#### Array

- collection of objects

- fixed size

- index always starts at 0

- occupy a contiguous chunk of memory

- ```c++
  int arr[4] = {initializer list};
  ```

#### Array Decay

- when you try to read the value of the whole array
  - it decays into a pointer to its first element
  - doesn't apply for "*" or "[]"
  - doesn't apply if array appears to left of "="

#### Pointer Arithmetic

#### Array Indexing

- ptr[i] is defined as *(ptr + i)

#### Array Traversal

- Index:

  - ```c++
    for (int i = 0; i < size; ++i)
    ```

- Pointer:

  - ```c++
    for (int *ptr = arr; ptr < arr + size; ++ptr)
    ```

如果pointer指到了array外面：undefined behavior/给一个random address 储存的值

### 考点：

- array的size在init的时候需要是一个已经设置好的值：hardcoded/const when using variable，不能是未知的
- array decay
  - Lecture 4, page 19
  - 什么时候会出现array decay
- Undefined behavior

## Strings, Streams and I/O

<table>
    <tr>
    	<th>C-style</th>
        <th>C++ strings</th>
    </tr>
    <tr>
    	<td>cstring</td>
        <td>string</td>
    </tr>
    <tr>
    	<td>array with special rules</td>
        <td>custom data type with special functions</td>
    </tr>
    <tr>
    	<td>1. type char in the array <br>
        	2. last element is '\0'
        </td>
    </tr>
    <tr>
    	<td>1. char str[2] = {'a', '\0'}; <br>
            2. char str[2] = "a"; <br>
            3. const char *str = "a";
        </td>
        <td>string str</td>
    </tr>
    <tr>
    	<td>strlen(): 不包含\0的长度 <br>
            strcpy(): copy from one location to another <br>
            strcmp(): compare 2 strings<br>
            strcat(cstr1, cstr2) 
        </td>
        <td>str.length() <br>
            str1 = str2 <br>
            str1 == str2 <br>
           	str1 += str2
        </td>
    </tr>
    <tr>
    	<td>1. char values are numbers in ASCII codes <br>
            2. If you declare as an array it can be modified<br>
            3. If you declare as a pointer it must be const<br>
            4. You can print out C-style string although it is an array -- cout treats all char* as C-style strings
        </td>
    </tr>

   

```c++
const char* cstr = str.c_str(); // string to c-string
string str = string(cstr); // c-string to string
```



### 考点：

- C-style最后一个char一定是\0
- 如果char*不是被declare成C-style那么还是会出现array decay
- print的问题：只需要看cout接受的是不是pointer就可以
  - 是pointer的话用decay
  - 不是的话print指向的那个位置的值
- array decay: 47min lecture 5

## Command Line Arguments

argc and argv

```c++
int main(int argc, char *argv[])
```

argv的size是argc，从index1开始算因为0是program名字

atoi：treat input c-string as integers

```c++
#include <cstdlib>
atoi(const char *s)
```

## Const

The const word refers to whatever data type to its left unless there is nothing to its left.

可以point const pointer到non-const object但是不能反过来因为你不应该去change一个const object通过pointer



## Streams

<table>
    <tr>
    	<th>input</th>
        <th>output</th>
    </tr>
    <tr>
        <td>cin: standard input</td>
        <td>cout: standard output</td>
    </tr>
    <tr>
    	<td>ifstream: read from file<br>
        </td>
        <td>ofstream: write to a file</td>
    </tr>
    <tr>
    	<td>&gt&gt</td>
        <td>&lt&lt</td>
    </tr>
</table>

ifstream:

```c++
#include <>
string filename = "a.txt";
ifstream fin;
fin.open(filename);
if (!fun.is_open()) {
    return 1;
}  
string word;
while (fin >> word) {
    //do something
}
fin.close();
```

ofstream:

```c++
#include <>
string filename = "a.txt";
ofstream fout;
fout.open(filename);
if (!fout.is_open()) {
    return 1;
}
fout.close();
```



### 考点：

- argv是array of char pointer 也就是c-style string lec6 25mins page11
  - 所以有时候会出现array decay的现象
- declaration的读法：inside-out

## Compound Objects

a struct can be declared const, neither it nor its member may be assigned to.

Pass struct as parameters: use pointer or reference / add const

## Abstract Data Types in C/C++

separate interface from implementation

respect interface

<table>
    <tr>
        <th>C struct</th>
        <th>C ++class</th>
    </tr>
    <tr>
    	<td>public by default</td>
        <td>private by default</td>
    </tr>
    <tr>
    	<td>有default constructor但是如果你写了就不会有default</td>
    </tr>
    <tr>
    	<td>use . to access number<br>
        	for pointer, use ->
        </td>
        <td>this->member, "this" is a pointer
        </td>
    </tr>
    <tr>
    	<td>contains only data</td>
        <td>contains data and functions</td>
    </tr>
    <tr>
    	<td>undefined by default</td>
        <td>constructors can be used to init</td>
    </tr>
    <tr>
        <td>notation is cumbersome <br>
        	declaration of object is always separate from initialization
        </td>
        <td>include public and private, private只能在同一个class里面用。也可以access其他object的private只要是相同类型
        </td>
    </tr>
</table>

```c++
double a() const {
    //这里的const指的是this，在这里我们不能modify this/里面的member
}
```

#### Scope resolution :: operator

:: tells the compiler where to find a definition of something: to define out of scope(class) function

#### Constructors

Define:

```c++
Classname(type variable): variable(variable_in) {
    //same order!
}
```

可以有多个constructor

可以在一个constructor里面call另一个

```c++
A(type a) : A (a, b, c) {}
```



#### Class as member

default init: 如果没有default就会compiler error

### 考点：

- 什么情况下会break interface
- class：
  - const function里面只能call const function
  - 什么情况下compiler error
    - 有没有matched constructor
    - 会不会access private
    - 有没有是const的情况下call const function

## Inheritance & **Polymorphism**

Reduce code duplication 

Base class -- derived class

A constructor in a derived class ***always*** call the base constructor

```c++
class ToClass : public FromClass {
    public:
    	ToClass() : FromClass(), newVariable() {
            
        }
    void something() {
        FromClass::talk(); //对于同名function来讲
    }
}
```

#### Varieties 

1. public: only for this class
2. protected
3. private

#### Static vs Dynamic Types

<table>
    <tr>
    	<th>Static type</th>
        <th>Dynamic type</th>
    </tr>
    <tr>
    	<td>whatever the pointer was declared to point to</td>
        <td>whatever the pointer is actually pointing right now</td>
    </tr>
**by default, c++ use static binding function calls**

else, use virtual function:

```c++
virtual void fuc() {
    // virtial是自动继承的
}

```



### 考点：

- 继承者对base的权限

  - derived不能access base的private

- Object slicing：

  - Creating an instance of a base class only allocates room for the base member variables

  - base type = derived type slice the object

    - only base members are copied
    - any function will use base version 

  - Pointer

    - derived pointer可以被赋给base pointer

      ```c++
      base ptr = derived obj
      ```

      - 但跟slice类似，可以compile但是access被sliced掉的会报错

    - 反过来不行因为不是所有derive都是base

      ```c++
      derived ptr = base obj \\ err
      ```

      - dynamic_cast<derived>ptr 可以因为promise了是derived

- override跟overload的区别

  - 如果是const的区别也是overload

  

#### abstract class

- 相当于interface的class（？）
- pure virtual function

## Container ADTs I

Factory Pattern

A container is an ADT to hold other objects

static keyword: share among all instance of the class. 

Representation Invariant

## Container ADTs II

## Memory Models and Dynamic Memory





