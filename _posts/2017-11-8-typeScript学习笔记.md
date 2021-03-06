---
layout: post
title:  "typeScript学习笔记"
date:   2017-11-8 21:41:45 +0800
categories: share
---
### 1.基础类型
#### 1.1 布尔值

```
let isDone: boolean = false;
```

#### 1.2 数字

```
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```

#### 1.3 字符串

```
let myName: string = `Gene`;
let age: number = 37;
let sentence: string = `Hello, my name is ${myName}.
I'll be ${ age + 1 } years old next month.`;
```

#### 1.4 数组

```
let list:number[]=[1,2,3];
let list2:Array<String> = ['1','2','3'];
```

#### 1.5 元祖Tuple

```
let x: [string,number];
x=['hello',10];
x[3] = "world";
x[4] = 100;
```

#### 1.6 枚举

```
enum Color {Red=1, Green, Blue}
let c: Color = Color.Green;
console.log(c);
```

#### 1.7 Any

```
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

#### 1.8 Void

```
let unusable: void = undefined;
```

#### 1.9 Null和undefined

```
let u: undefined = undefined;
let n: null = null;
```

#### 1.10 Never


#### 1.11 类型断言

```
//“尖括号”语法
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
//as语法
let someValue: any = "this is a string";
let strLength：number = (someValue as string).length;
```
### 2.变量声明
#### 2.1 let声明
当用let声明一个变量，它使用的是词法作用域或块作用域。
#### 2.2 const声明
声明一个常量
#### 2.3 结构赋值
1. 结构数组

```
let input = [1, 2];
let [first, second] = input;
console.log(first); // outputs 1
console.log(second); // outputs 2
```

2. 结构对象

```
let o = {
    a: "foo",
    b: 12,
    c: "bar"
};
let { a, b } = o;
```
### 3.接口interface

```
interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

var user = { firstName: "Jane", lastName: "User" };

console.log(greeter(user));
```
### 4.类class

```
class Student {
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person : Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

var user = new Student("Jane", "M.", "User");

console.log(greeter(user));
```
<blockquote>
class和interface最大的不同在于class还提供了其他内容的实现方法，而不仅仅是形状内容。


如果新建一个从服务器或类似的模型数据，最好使用interface。

不像classes，interface会在编译之后完全删除。

如果我们会在之后会多次调整使用同一个interface，那么我们最好将其转化成class来使用。
</blockquote>