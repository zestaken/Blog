---
title: JavaScript
date: 2020-12-13 21:02:41
tags:
---

# JavaScript概述

[参考资料](https://www.w3school.com.cn/js/index.asp)

* 概念：一门客户端脚本语言
  * 运行在客户端浏览器中。每一个浏览器都有JavaScript的解析引擎。
  * **脚本语言**；不需要编译，直接就可以被浏览器解析执行。
* 功能：可以用来**增强用户与html页面的交互过程**，可以控制html元素，让页面有一些动态效果。
* JavaScript发展史：
  1. 1992年，Nombase公司，开发出第一门客户端脚本语言，专门用于表单的校验。命名为：c--，后来更名为ScriptEase。
  2. 1995年，Netbase（网景）公司，开发出一门客户端脚本语言：LiveScript；之后，该公司请来Sun公司的专家，修改LiveScript，命名为JavaScript。
  3. 1996年，微软抄袭了JavaScript开发出了JScript语言；
  4. 1997年，ECMA（欧洲计算机制造商协会），制定了ECMAScript，就是所有客户端脚本语言的标准。
* JavaScript=ECMAScript + JavaScript自己特有的东西(BOM+DOM)。

# ECMAScript

## 基本语法

### 与html结合的方式

1. 内部JS
   1. 定义一个`<script></script>`标签，标签体内容就是js代码。
   2. 示例：
```html
<script>
    alert("hello world");
</script>
```
2. 外部JS
   1. 定义一个`<script></script>`标签，通过src属性引入外部的js文件。
   2. 示例：
```html
<script src="js/a.js"></script>
```
* `<script>`标签可以写在html页面的任何位置，但是定义的位置的先后会**影响执行顺序**。
* 同一个html页面**可以定义多个`<script>`标签**。

### 注释

* 单行注释：//注释内容
* 多行注释：/* 注释内容 */

### 数据类型

* 原始数据类型（类似java中的基本数据类型）
  * number:数字。
    * 整数
    * 小数
    * NaN(not a number 一个不是数字的数字类型)
  * string:字符串
    * "abc","a",'a'都是字符串，没有字符类型。
  * null:一个对象为空的占位符。
  * undefined:未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined。
  * boolean：布尔值类型，值为true或者false。
* 引用数据类型：对象。

### 变量

* 变量定义：一小块存储数据的内存空间
* java是强类型语言，JavaScript是弱类型语言
  * 强类型：在开辟变量存储空间时，定义了空间将来存储的数据类型。**只能存储固定类型的数据**。
  * 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，**可以存放任意类型的数据**。
* 语法:`var 变量名;`或者`var 变量名 = 初始化值;`
* 查看数据类型：`typeof(变量名);`,会返回变量的类型。
* 输出数据到页面中`document.write(输出的数据);`,如：`document.write(a+"我是a"+"<br>");`

### 运算符

* 一元运算符：
  * `++`:自增
  * `--`:自减（同java一样，也有放在前后的问题）
  * `+/-`:正负号。
* 算数运算符：
  * `+`:加法
  * `-`:减法
  * `*`:乘法
  * `/`:除法，与java不同的是，除法的结果**可以为小数**.
  * `%`:取余运算。
* 赋值运算符：
  * `=`；赋值
  * `+=`
  * `-=`:与java相同。
* 比较运算符：
  * 类型相同，直接比较，如果是字符串则按照字典顺序**按位逐个比较**，直到得出大小。
  * 类型不同，**转换后再相比**。
  * `>,<，>=，<=`:大于、小于,大于等于，小于等于
  * `===`:比较之前先判断类型，如果**类型不相同则直接返回false**。
* 逻辑运算符：
  * `&&`:与，有短路效果(如果左边能够确定表达式的值，那么右边就不会再运算)
  * `||`:或，也有短路效果。
  * `!`:非，该运算符要求变量类型是boolean。
* 三元运算符：
  * `?:`:
    * 语法：`表达式?值1:值2`
    * 判断表达式的值，如果是true则取值1，否则取值2；
    * 示例：`a > b ? 1:0;`
* 在JavaScript中如果运算数不是运算符所要求的类型，那么js引擎会自动地将运算数进行类型转换。
  * 其它类型转number：
    * String转number：会按照字面值转换，如果**字面值不是数字，那么转换为NaN**.（NaN与任何数运算的结果还是NaN）
    * boolean转number：true转为1，false转为0。
    * 其它类型转换为number就是**NaN**。
  * 其它类型转boolean：
    * number转为boolean：**0或NaN**为false，其它为true。
    * string转为boolean：**空字符串**为false，其它都为true。空字符串：`string str="";`
    * null和undefined转为boolean：**都是false**。

### 特殊语法

* 语句以分号结尾，如果一行只有一条语句，则分号可以省略（但是一般不建议）；
* 变量的定义使用var关键字，也可以不使用：（不建议使用）
  * 使用var定义的局部变量
  * 不使用var定义的是全局变量

### 流程控制语句

* `if...else`:与java中相同
* `switch`:
  * 在java中，switch可以接收的数据类型：byte，int,short ,char ,枚举(1.5之后)，string(1.7之后)；
  * 在JavaScript中，switch可以接收任意类型的变量。
```javascript

var a = "hello";
switch(a) {
  case 1:
      alert("number");
      break;
  case "hello":
      alert("string");
      break;
  case undefined:
      alert("undefined");
      break;
}
```
* `while`:与java一样。
* `for`:与java一样
* `do...while`:与java一样。

### 示例：99乘法表

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>99乘法表</title>

    <style>
        td{
            border: 1px solid ;
        }
    </style>
    
    <script>
        document.write("<table align='center'>"); //在JavaScript的字符串中嵌套html的语句中如果含有双引号，则全部使用单引号，防止和字符串的双引号起冲突

        for(var i = 1; i <= 9; i++) {
            document.write("<tr>");
            for(var j = 1; j <= i; j++) {
                document.write("<td>");
                document.write(i + "*" + j + "=" + i * j + "&nbsp;&nbsp;&nbsp;&nbsp;");//&nbsp
                document.write("</td>");
            }
            document.write("</tr>");
        }

        document.write("</table>");
    </script>
</head>
<body>

</body>
</html>
```
* 效果：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201214170043.jpg)
* 在html代码中，使用转义字符`&nbsp`表示1个空格,在html代码中每输入一个转义字符`&nbsp`就表示一个空格，输入十个`&nbsp`，页面中就显示10个空格位置。而在html代码中输入空格，**不管输入多少个空格，最终在页面中显示的空格位置只有一个**。
* 在JavaScript的字符串中嵌套html的语句中如果含有双引号，则全部**使用单引号**，防止和字符串的双引号起冲突。

## 基本对象

### Function对象

* Function对象：函数（方法）对象
* 创建：
  1. 不常用：`var fun = new Function(形式参数列表，方法体);`
  2. 常用1：`function 函数名(形式参数列表) {方法体}`示例：
```javascript
function fun1(a,b) {
  alert(a + b);
}
```
  3. 常用2：`var 方法名 = function(形式参数列表) {方法体}`示例：
```javascript 
var fun2 = function(a, b) {
  alert(a + b);
}
```
* 特点：
  * 方法定义时，**不用写形参的类型**，也不用写**返回值类型**。
  * **方法是一个对象**，如果定义名称相同的方法，会覆盖而不会报错。
  * 在js中，方法的调用只与方法名有关，和**形参列表无关**（即使传入的参数不符合形参列表，也没有问题，如果传少了，则默认传了undefined，如果传多了，则不管多的）。
  * 在方法声明中有一个隐藏的内置对象（数组对象）`arguments`,封装了所有传进函数的**参数**。
* 属性：
  * length；方法对象中**形参**的个数。
* 调用：
  * `方法名(实际参数列表);`

### Array对象

* Array:数组对象
* 创建：
  1. `var arr = new Array(元素列表);`
  2. `var arr = new Array(默认长度);`
  3. `var arr = [元素列表];`