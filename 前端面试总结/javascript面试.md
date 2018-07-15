
## 基础知识
JS中typeof能得到的哪些类型
```js
typeof undefined//undefined
typeof 'abc'//string
typeof 123//number
typeof true //boolean
typeof {} //object
typeof [] //object
typeof mull //object
typeof console.log //function
```
何时使用\==和===
```js
if(object.a==null){
    //obj.a===null||obj.a===undefined
}
```
JS中的内置函数
```js
Object
Array
Boolean
Number
String
Function
Date
RegExp
Error
```
Math是内置对象不是内置函数

JS变量按照存储方式区分为哪些类型，并描述其特点

//值类型
```js
var a=10;
var b=a;
a=11;
console.log(b);//10
```
//引用类型
```js
var obj1={x:100};
var obj2 = obj1;
obj1.x=200;
console.log(obj2.x); //200
```
值类型和引用类型的特点，值类型存储的是值，引用类型存储的是地址。值类型的赋值是值得拷贝，引用类型的赋值是地址的拷贝。

如何理解JSON？
//JSON只不过是一个JS对象而已
JSON 是JavaScript中的内置对象，也是一种数据格式
```js
JSON.stringify({a:10,b:20});
JSON.parse('{"a":10,"b":20}');
```
### 原型
构造函数
```js
function Foo(name,age){
    this.name=  name;
    this.age = age;
    this.class = 'class-1';
    //return this //默认有这一行
}
var f = new Foo("zhangsan",20);
var f1 = new Foo('lisi',22);
```
构造函数-扩展
```js
var a = {};
//其实是var a = new Object()的语法糖
var b = [];
//是var b = new Array()的语法糖
function Foo(){};
//是var Foo = new Function()
```
使用instanceof判断一个函数是否是一个变量的构造函数
原型规则和示例
原型链
### 原型链
### 作用域
### 闭包
### 异步
### 单线程
## JS API
### DOM操作
## 开发环境
### 版本管理

面试技巧

