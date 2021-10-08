# EECS280-Note

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



考点：

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

## Pointers

Object to store address: 

```c++
int *ptr = &x;
```

也算object也会被存储进memory diagram

get the object a pointer points to use * operator. 

考点：

- 不同data之间的pointer type不能相等：compiler error

## Arrays

## Strings, Streams and I/O

## Compound Objects

## Abstract Data Types in C

## ADT in C++

## Inheritance 

## Polymorphism

## Container ADTs I

## Container ADTs II

## Memory Models and Dynamic Memory





