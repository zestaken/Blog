---
title: java
date: 2020-09-11 16:39:07
tags:
---

# 输入和输出

* 使用`Scanner in = new Scanner(System.in);`可以定义一个可以接受输入的东西`in`（名字是任取的。）。之后要接受输入时，就使用形如`in.nextline()``in.nextint()`的语句。（其中line与int表示接受的输入的数据类型，line是字符串，int是整型）。
* 使用` System.out.println();`可以直接输出字符串并且在每一次输出后都换行，还有`System.out.print()`，它与前者的区别是在每一次输出后不换行。
* `System.out.prinf()`这个输出的用法与c语言中的printf()类似，可以有`System.out.printf("%.2f",i)`这样的类似c语言的格式限制。
* Java的注释和c语言一样，可以用`//`和`/**/`
# 变量

* 变量的定义：<类型名称> <变量名>;
* 变量的名字(又叫做标识符）只能由字母，数字和下划线组成，且数字不可以出现在第一个位置上。Java的内置的关键字不可以用作变量名。
* Java是一种强类型语言，变量在使用前必须声明，且变量具有确定的类型。

# 常量

* 类似变量的定义声明，常量只需要在定义时在类型前加上关键词`final`。常量只能在定义时赋值初始化，之后不能再赋值。

# 运算

## 赋值

* 同c语言一样，Java依旧使用`=`来进行赋值。
* 在定义变量的时候可以进行赋值（此时叫做变量的初始化）。
* 赋值运算是自右向左。

### 复合赋值

* 同c语言一样，Java中也有复合赋值，即`+=, -=, *=, /=`。用法与c语言完全一致。`a += b + c`与`a = a + (b + c)`完全相同。

## 四则运算
  
* 当浮点数和整数放在一起运算时，Java会将整数先转化为浮点数，之后进行浮点数的运算。
* `+，-，*,/ , %`的运算优先级和惯常的优先级一致。
* 赋值号`=`的优先级很低，以保持和正常思维一样的运算顺序。
* Java中同样有`i++, ++i`这种运算，用法与c语言完全相同。

## 单目运算符

* 取正`+`和取负`-`,运算优先级高于普通的双目运算符。


# 数据类型

## 整型

* 整数类型不能表达有小数部分的数。整数与整数的运算结果还是整数。
* `int`型：

## 浮点型

* 浮点数就是通常所说的小数。
* `double`型的浮点数：

## 布尔类型

* Java中的布尔类型是用`boolean`定义的，其含义与用法与c语言中的bool类型一致。

## 字符类型

* 单个字符类型是char，其字符字面量是用单引号来表示的，如'a','4'等。Java中的字符使用的是Unicode标准，支持汉字在内的多种文字。
* 类似C语言中的字符类型，可以对字符变量进行加减运算。如`i = 'A' - 'D'`中的i为3，也可以强制将字符类型转换为int类型。
* **逃逸字符**：有些没有办法打印出来的字符，这些字符由一个反斜杠`\`开头，后面跟上一个字符，由这两个字符合起来组成一个字符。常见逃逸字符：

|字符|意义|
|-|-|
|\b|回退一格|
|\t|到下一个表格位|
|\n|换行|
|\r|回车|
|\"|双引号|
|\'|单引号|
|`\\`|反斜杠本身|


## 包裹类型

* 每种基础类型（如，int，double，char）都有对应的包裹类型。
* 包裹类型除了具有和基础类型一样的功能外（如定义变量），还有许多可以实现的功能。如`Integer.MAX_VALUE`,可以得到int类型的最大值。即使用包裹类型可以调用许多java内置的方法。
* 包裹类型的第一个字母是大写的。
* 各种基础类型对应的包裹类型。

|基础类型|包裹类型|
|-|-|
|int|Integer|
|double|Double|
|char|Character|
|boolean|Boolean|

## 字符串变量

* **字符串字面量**：用双引号括起来的0或者多个字符为一个字符串字面量。如："hello"
* **字符串类型**：`String`是字符串类型（第一个字母为大写，是一种包裹类型），String是一个类，String类型的变量是字符串的管理者而非所有者（就和数组变量和数组一样。）
* **字符串变量的创建**：`String s = new String(字符串字面量)`.用字符串字面量初始化字符串变量。也可以直接初始化一个字面量，如`String s = "hello"`。
* **字符串的连接**：

## 强制类型转换

* Java同c语言一样，有很多隐式转换。例如整型在某些条件下会自动转为浮点型。
* 但是浮点型不会自动转换为整型。我们可以进行强制类型转换。例如：`int a = (int)(32 /5 .0)`。

# 关系运算

* 关系运算符：`==, >, <, >=, <=, !=`与C语言一致。
* 关系运算符的优先级比算术运算符低，但是比赋值运算高。例如：`7 > 3 + 2`。
* 判等和判不等`==, !=`的优先级比`<, <=, >, >=`低.例如：`5 > 3 == 6 > 4`是可行的（但是和c语言一样，尽量不要连续使用关系运算。）
* `<, >, >=, <=`是不能连续使用的，例如：`a > b > c`是和你的想象完全不同的。

## 浮点数的比较

* 整型是可以与浮点数进行比较的。
* 浮点数的运算有误差。所以判断两个浮点数是否相等是用`Math.abs(a -b) < 1e-6`.先用`Math.abs(a - b)`算出两个浮点数之间的差值，在让这个差值和一个很小的数比较。`1e-6`表示的是1的负6次方。


# 控制语句

## 条件语句

### if语句  

* 与c语言类似，只有一个语句时可以不用花括号（但是建议不管多少语句都用花括号），但是有多条语句时必须括起来。
* 类似c语言，Java中的if语句同样可以与else连用，进行级联条件判断。

### swich语句

* Java中同样有switcl-case语句。用法也与c语言相同。
* 示例：
```java
switch (控制表达式) {
    case 常量：
        语句
        ...
        break;
    case 常量：
        语句
        ...
        break；
    ...
    default:
        语句
        ...
        break;
}
```
* 控制表达式，只能是整型的结果；
* 每个case后面都要有**break**语句。
* 如果所有的case都不匹配，就执行default后面的语句；如果没有设置default语句，就什么也不做。(default后面直接接冒号，没有条件。default后面的语句也可以放break来终止。）

## 循环语句

### while

* 与c语言中的while基本一致。 while是当条件满足时执行循环内的语句。
* 与c语言一样，Java中也有`do-while`循环，这个循环至少执行一次。

### for循环

* Java中也有for循环，用法与c语言基本相似。
* 但是Java可以在循环条件语句中定义变量，并且在for循环中定义的变量只能在for循环中使用，在循环体外并没有那个变量的定义。例如：`for(int i =  1; i <= n; i = i + 1 ){}`。（for循环适合有明确结束条件的循环。）
* `break`语句在Java中与c语言中一致，用于跳出循环。
* `continue`语句也是与c语言一样，用于到达循环尾。(但是continue语句不会跳过for循环的步进语句，例如：`for(int i = 0; i <= n; i++){continue;}`， 每次continue语句之后还是要执行i++之后再开启下一轮循环。)。
* **循环的标号**：可以在循环前设置一个标号（例如;`out:`）来标示循环。使用`break  标号`和`continue 标号`可以使break和continue对标号标示的循环起作用。示例：
```java
OUt:
for(int i = 0; i <= n1; i++){
    for(int j = 0; j <= n2; j++){
        break OUT;
    }
}
```
OUT标示的循环是最外层的循环，使用`break OUT`能直接跳出最外层的循环。
* **for-each**循环：形如:`for (int i : numbers){}`,意思是每一次循环，一次将数组numbers中的元素值赋给变量i。常用于遍历数组。 示例：
```java
int[] numbers = new int[100];

// 依次遍历数组中每个元素，并在数组遍历完之后停止循环。
for (int i : numbers) {
    if (i == 23) {
        System.out.println("numbers数组中有23这个数")；
        break；
    }
}

```
# 逻辑类型

* 关系运算的结果是一个逻辑值，true或者false。这个值保存在一个对应的逻辑类型的变量中，这个类型是boolean。与c语言的布尔类型一样，Java中的布尔类型也只有true和false这两种值。

## 逻辑运算

* **!**:逻辑非。
* **&&**：逻辑与。
* **||**：逻辑或。三者都与c语言中的逻辑运算的用法一致。

# 数组

* 数组定义：形如`int[] numbers = new int[100]`。格式范式：`<类型>[] <名字> = new <类型>[元素个数]`（同c语言一样，数组的下标是从0开始的，后面方括号中是数组中元素的个数(可以为变量，但是必须有）。但是实际只有numbers[99], 而没有numbers[100].)
* 数组一旦创建，不能被改变大小。
* 数组中的所有元素是同一类型。
* java中的每个数组有一个内部成员length,这个变量中存储了数组中元素的个数（即创建数组时确定的元素个数）。使用示例；
```java
int[] numbers = new int[100];

for(int i = 0; i < numbers.length; i++) {
    ...
}
```
* 数组的直接初始化：形如：`int[] numbers = {1, 2, 3, 4, 5};`
* 数组变量之间可以做赋值。例如：`int[] numbers = {1, 2, 3, 4, 5}; int[] b = numbers;`.数组变量的实质与c语言类似，是指向实际存储空间的“指针”，但是Java中不使用指针的概念，可以把数组变量看作是实际存储空间的管理者。所以数组变量之间的赋值，其实质是将对实际存储空间的管理权共享了出去，而不是把整个数组复制过去。因此，如果改变了b数组中，某个元素的值，numbers数组中相应的元素也会跟着改变。如`b [2] = 3;`之后会有`numbers[2] == 3`.
* 数组变量之间的比较，是在比较两个数组变量是否管理同一个数组，而不是比较两个数组是否是每个元素都对应相等。
* 刚创建的int类型数组，数组中的元素默认都是0。
* **二维数组**：定义形如`int[][] numbers = new int[3][5];`;与c语言类似，通常理解为矩阵。二维数组初始化：
```java

int[][] numbers = {
    {1, 2, 3, 4}, //每一行用逗号，分隔。
    {5, 6, 7}, //第二行比第一行少了一个元素，编译器会自动补上0；
};//别忘了最后的分号。
```
* 二维数组中仍然有length变量表示数组的长度。`numbers.length`表示数组的的行数。而每一行有多少个元素需要用`numbers[i].length`。


# Math类

* Math类提供的很多数学操作，如取绝对值等。
* `abs`提供取绝对值操作，`.round`提供四舍五入的操作，`.random`提供取随机数（0到1之间）的操作，`.pow`可以进行幂运算。
* 使用示例：
```java

Math.abs(-12); //结果为12
Math.round(10.2343); //结果为10
Math.random(); 
Math.pow(2, 3); //结果为2的3次方：8