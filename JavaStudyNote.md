# Java

[TOC]

Java 项目结构：

​	工程

​		模块

​			包

​				类



Java入口程序规定的方法必须是静态方法，方法名必须为`main`，括号内的参数必须是String数组。

```java
public class Hello {
    public static void main(String[] args) { // 方法名是main
        // 方法代码...
    } // 方法定义结束
}
```

java的三种注释：

单行

```java
//这是注释...
```

多行

```java
/*
这是注释
blablabla...
这也是注释
*/
```

文档注释

```java
/**
 * 可以用来自动创建文档的注释
 * 
 * @auther liaoxuefeng
 */
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

对于`float`类型，需要加上`f`后缀。

```java
float f1 = 3.14f;
```

除了基本类型的变量外，剩下的都是引用类型

`String`字符串

```java
String s = "hello";
```

定义变量的时候，如果加上`final`修饰符，这个变量就变成了常量：

```java
final double PI = 3.14; // PI是一个常量
```

根据习惯，常量名通常全部大写。

**var关键字**

有些时候，类型的名字太长，写起来比较麻烦。这个时候，如果想省略变量类型，可以使用`var`关键字：

```java
StringBuilder sb = new StringBuilder();
可以写为：
var sb = new StringBuilder();
```

使用`var`定义变量，仅仅是少写了变量类型而已。

整数运算在除数为`0`时会报错，而浮点数运算在除数为`0`时，不会报错，但会返回几个特殊值：

- `NaN`表示Not a Number
- `Infinity`表示无穷大
- `-Infinity`表示负无穷大

**强制转型**

强制转型使用`(类型)`

可以将浮点数强制转型为整数。在转型时，浮点数的小数部分会被丢掉。如果转型后超过了整型能表示的最大范围，将返回整型的最大值。

Tips: 如果要进行四舍五入，可以对浮点数加上0.5再强制转型：

**位运算**

与 &

或 |

非 ~   单目运算符

异或 ^

**布尔运算**

包括以下几类：

- 比较运算符：`>`，`>=`，`<`，`<=`，`==`，`!=`
- 与运算 `&&`
- 或运算 `||`
- 非运算 `!`

**短路运算**

布尔运算的一个重要特点是短路运算。如果一个布尔运算的表达式能提前确定结果，则后续的计算不再执行，直接返回结果。

因为`false && x`的结果总是`false`，无论`x`是`true`还是`false`，因此，与运算在确定第一个值为`false`后，不再继续计算，而是直接返回`false`。

**三元运算符**

Java还提供一个三元运算符`b ? x : y` ,b为布尔表达式

**字符串连接**

可以使用`+`连接任意字符串和其他数据类型

**多行字符串**

要表示多行字符串，使用+号连接会非常不方便：

```java
String s = "first line \n"
         + "second line \n"
         + "end";
```

从Java 13开始，字符串可以用`"""..."""`表示多行字符串（Text Blocks）了。

**不可变特性**

Java的字符串除了是一个引用类型外，还有个重要特点，就是字符串不可变。

**空值null**

引用类型的变量可以指向一个空值`null`，它表示不存在，即该变量不指向任何对象。

**数组类型**

数组元素可以是值类型（如int）或引用类型（如String），但数组本身是引用类型；

```java
int[] ns = new int[5];
```

- 数组所有元素初始化为默认值，整型都是`0`，浮点型是`0.0`，布尔型是`false`；
- 数组一旦创建后，大小就不可改变。
- 要访问数组中的某一个元素，需要使用索引。数组索引从`0`开始
- 可以用`数组变量.length`获取数组大小
- 也可以在定义数组时直接指定初始化的元素，这样就不必写出数组大小，而是由编译器自动推算数组大小。

```java
int[] ns = new int[] { 68, 79, 91, 85, 62 };
```

还可以进一步简写为：

```java
int[] ns = { 68, 79, 91, 85, 62 };
```

**输出**

```java
System.out.println()  //输出并换行
System.out.print()    //输出不换行

System.out.printf("%.2f\n", d); //格式化输出，显示两位小数

%d //格式化输出整数
%x //十六进制
%f //浮点数
%e //科学技术法
%s //格式化字符串
```

**输入**

```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // 创建Scanner对象
        
        String name = scanner.nextLine(); // 读取一行输入并获取字符串

        System.out.printf("Your name: %s\n", name); // 格式化输出
    }
}
```

首先导入导入`java.util.Scanner` ，然后创建`Scanner`对象。`System.out`代表标准输出流，而`System.in`代表标准输入流。直接使用`System.in`读取用户输入虽然是可以的，但需要更复杂的代码，而通过`Scanner`就可以简化后续的代码。

有了`Scanner`对象后，要读取用户输入的字符串，使用`scanner.nextLine()`，要读取用户输入的整数，使用`scanner.nextInt()`。`Scanner`会自动转换数据类型，因此不必手动转换。

**判断引用类型相等**
在Java中，判断值类型的变量是否相等，可以使用`==`运算符。但是，判断引用类型的变量是否相等，`==`表示“引用是否相等”，或者说，是否指向同一个对象。例如两个String类型，它们的内容是相同的，但是，分别指向不同的对象，用`==`判断，结果为`false`：

要判断引用类型的变量内容是否相等，必须使用`equals()`方法：

```java
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "HELLO".toLowerCase();
        System.out.println(s1);
        System.out.println(s2);
        if (s1.equals(s2)) {
            System.out.println("s1 equals s2");
        } else {
            System.out.println("s1 not equals s2");
        }
    }
}
```

注意：执行语句`s1.equals(s2)`时，如果变量`s1`为`null`，会报`NullPointerException`：

使用**switch语句** 不要漏写了`break`语句和`default`语句

`for`循环经常用来遍历数组，因为通过计数器可以根据索引来访问数组的每个元素：
Java还提供了另一种`for each`循环，它可以更简单地遍历数组：

```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int n : ns) {
            System.out.println(n);
        }
    }
}
```

和`for`循环相比，`for each`循环的变量n不再是计数器，而是直接对应到数组的每个元素。`for each`循环的写法也更简洁。但是，`for each`循环无法指定遍历顺序，也无法获取数组的索引。

除了数组外，`for each`循环能够遍历所有“可迭代”的数据类型，包括`List`、`Map`等。

Java标准库提供了`Arrays.toString()`，可以快速打印数组内容

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 1, 2, 3, 5, 8 };
        System.out.println(Arrays.toString(ns));
    }
}

```

**数组排序**

Java的标准库已经内置了排序功能，我们只需要调用JDK提供的`Arrays.sort()`就可以排序：

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
        Arrays.sort(ns);
        System.out.println(Arrays.toString(ns));
    }
}
```

必须注意，对数组排序实际上修改了数组本身。

而对一个字符串数组进行排序，则原来的3个字符串在内存中均没有任何变化，但是`ns`数组的每个元素指向变化了。

### 命令行参数

Java程序的入口是`main`方法，而`main`方法可以接受一个命令行参数，它是一个`String[]`数组。
这个命令行参数由JVM接收用户输入并传给`main`方法：

```java
public class Main {
    public static void main(String[] args) {
        for (String arg : args) {
            System.out.println(arg);
        }
    }
}
```

命令行参数这样传递

```java
$ java Main a  //a为需要传递的命令行参数
```

**Java Bean**

**一个标准的类通常有四个组成成分：**

- 成员变量都是私有的
- 为每一个成员变量编写一对 Get/Set方法
- 包含无参构造方法
- 包含有参构造方法

### 键盘录入

```java
//第一套体系,遇到空格、制表符、回车就停止接受。
nextInt(); //接收整数
nextDouble(); //接收小数
next();//接收字符串，内部是new出来的！

//第二套体系，可以接受空格和制表符，遇到回车才停止
nextLine(); //接受字符串

Scanner sc = new Scanner(System.in);
System.out.println("请输入一个字符串");
String line = sc.nextLine();

```

**java中静态方法和动态方法的区别**

![image-20240429194942230](D:\md_image\image-20240429194942230.png)

### String 对象

<img src="D:\md_image\image-20240429194900704.png" alt="image-20240429194900704" style="zoom:80%;" />

平时建议使用直接赋值的方式

当字符串使用直接赋值方式时，系统会检查该字符串在串池中是否存在。

不存在则创建新的；存在则复用

*string 类型不可变，引用不可变*



**java的内存模型**

- 栈内存：方法运行的时候进栈，执行完毕出栈。
- 堆内存：new出来的对象都在这里
- 方法区：临时存储字节码文件
- StringTable（串池）：只有直接赋值的方法获取的字符串才存在这个串池中，new关键字获取的字符串对象还是在堆内存中。



**java中 “==”比的是什么？**

1. 基本数据类型就比的是具体的数据值
2. 对于引用数据类型就比较的是地址值

```java
String s1 = "abc";   //记录在串池中
String s2 = "abc"
System.out.println(s1 == s2);  //返回Ture
```

```java
String s1 = new String("abc");   //记录在堆中
String s2 = "abc"               //记录在串池中
System.out.println(s1 == s2);  //比较地址值，返回False
```

<img src="D:\md_image\image-20240429194843271.png" alt="image-20240429194843271" style="zoom: 67%;" />





- 数组的长度：数组名.length

- 字符串的长度：字符串对象.length()

#### StringBuilder ####

​	StringBuilder 是一个容器，创建完之后里面的内容是可以变化的。

- 作用：提高字符串的操作效率
- 使用场景：
  1. 字符串的拼接和反转

**StringBuilder构造方法**

```java
StringBuilder sb = new StringBuilder()  //空参构造
StringBuilder sb = new StringBuilder("abc")  //有参构造
```

**成员方法**

```java
public StringBuilder append(任意类型)   //添加数据，返回对象本身
public StringBuilder reverse()         //翻转容器中的内容
public int length()             //返回长度
public String toString()      //将StringBuilder转换为String
```

#### StringJoiner

也是容器，内容可变。JDK8出现

在**拼接**字符串时，可以指定间隔符号，开始符号和结束符号

**构造方法**

```java
public StringJoiner(间隔符号)
public StringJoiner(间隔符号，开始符号，结束符号)
```

**成员方法**

```java
public StringJoiner add(添加的内容)
public int length()
public String toString()
```



#### 集合

集合只能存储引用数据类型，存储基本数据类型需要把它们变成其对应的包装类。

**集合和数组的对比**

数组长度固定，集合长度可变。

集合只能存引用数据类型，数组引用和基本数据类型都可存。

**常用集合类：ArrayList**

泛型：限定集合中存储数据的类型 ArrayList<E>

`ArrayList<String> list = new ArrayList<>();`

