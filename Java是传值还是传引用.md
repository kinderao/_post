
---
title: Java是传值还是传引用
date: 2016-09-22
---

##### 要搞懂这个问题，首先还是要先明白基本数据类型和引用数据类型的区别
``` java
int num = 10;
String str = "hello world";
Person p = new Person();
```
其中num为基本数据类型，而str 和 p 就是引用类型，基本数据类型值就存储在变量中，而引用类型，变量中保存的是实际对象的地址，所以成这种类型为引用类型。引用指向实际地址，而实际地址保存着实际的内容。有点像C语言中的指针。

<!-- more -->

##### 然后还要搞懂赋值运算符 “=”的作用
对于基本类型num，赋值运算符会直接改变变量中的值
而对于引用类型str 和 p，赋值运算符只是会改变其指向的地址，原来的地址被覆盖掉，**但是原来的对象不改变，只不过不被现在的这个变量所引用了**

### 参数传递就是一次赋值操作

``` java

第一个例子：基本类型
void foo(int value) {
    value = 100; 
} 
foo(num); // num 没有被改变 

第二个例子：没有提供改变自身方法的引用类型 
void foo(String text) {
   text = "windows"; 
}
foo(str); // str 也没有被改变 

第三个例子：提供了改变自身方法的引用类型 
StringBuilder sb = new StringBuilder("iphone");
void foo(StringBuilder builder){
   builder.append("4"); 
} 
foo(sb); // sb 被改变了，变成了"iphone4"。

第四个例子：提供了改变自身方法的引用类型，但是不使用，而是使用赋值运算符。
StringBuilder sb = new StringBuilder("iphone");
void foo(StringBuilder builder) {
    builder = new StringBuilder("ipad"); 
}
foo(sb); // sb 没有被改变，还是 "iphone"。
```