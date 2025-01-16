

[TOC]



# 常用API：

* Math
* System
* Runtime :和java运行环境相关
* Object（所有类的父类）和Objects（工具类）
* BigInteger（大整数）和BigDecimal（对小数进行精确运算）
* 正则表达式：对字符串格式进行校验

---

在 Java 中，默认情况下会自动导入以下的包：

1. `java.lang`：这是 Java 核心包，包含了 Java 语言的基本类，比如 `String`、`Object` 等。这个包会被默认导入，因此不需要显式地导入就可以使用其中的类。
2. `java.util`：这个包包含了 Java 的实用工具类，例如集合框架、日期时间工具等。虽然不是完全默认导入的，但其中的部分类在许多情况下会被隐式地使用或引入。

需要注意的是，除了上述两个包以外，其他的 Java 标准库中的包都需要通过 `import` 语句显式地导入才能在代码中使用。

> 学习技巧：
>
> 记一下类名和类的作用即可，不要记方法。
>
> 养成查阅API帮助文档的习惯



**Field Summary** 表示这个类中的属性

![image-20240605170019606](D:\md_image\image-20240605170019606.png)

Math类从Object中继承到的方法：

![image-20240605170452029](D:\md_image\image-20240605170452029.png)



> 这些方法不需要背，遇到不会的去API帮助文档查！

<img src="D:\md_image\image-20240605171117036.png" alt="image-20240605171117036" style="zoom:80%;" />

## System

System也是一个工具类，提供了一些与系统相关的方法。

**常见方法：**

```java
public static void exit(int status)   //终止当前运行的Java虚拟机，status:0表示虚拟机正常停止,非0:表示异常停止

public static long currentTimeMillis()    //返回当前系统的时间毫秒值形式，从时间原点到运行这个方法一共过了多少ms
    
public static void arraycopy(数据源数组，起始索引，目的地数组，起始索引，拷贝个数)    //数组拷贝
```

`arraycopy`方法细节：

1. 如果数据源数组和目的地数组都是基本数据类型，那么两者的类型必须保持一致，否则会报错。
2. 在拷贝的时候需要考虑数组的长度，如果超出这个范围也会报错。
3. 如果数据源数组和目的地数组都是引用数据类型，那么***子类类型***可以赋值给***父类类型***。



## Runtime

这个类里的方法不是静态的，不能使用类名调用。

这个类的对象不能自己建，因为其构造方法是私有化的。

![image-20240605210216574](D:\md_image\image-20240605210216574.png)

```java
//获取Runtime对象
Runtime r1 = Runtime.getRuntime();
Runtime r2 = Runtime.getRuntime();
//结果为true，r1和r2调用的是同一个Runtime对象
System.out.println(r1 == r2);
		
//exit 停止虚拟机
Runtime.getRuntime().exit(0)  //System中的exit方法实际上底层调用的是这个

//输出cpu线程数
System.out.println(Runtime.getRuntime().availableProcessors());

//JVM能从系统中获取的总内存大小
System.out.println(Runtime.getRuntime().maxMemory());

//JVM已经从系统中获取的内存大小
System.out.println(Runtime.getRuntime().totalMemory());

//JVM剩余内存大小
System.out.println(Runtime.getRuntime().freeMemory());

//打开记事本，需要给方法声明添加异常，或者给下面这句添加try/catch
Runtime.getRuntime().exec("notepad");
```



## Object（所有类的父类）

Object 无属性，因此只有空参构造方法。

![image-20240605214506407](D:\md_image\image-20240605214506407.png)

### toString

```java
Object obj = new Object();
String str = obj.toString();
System.out.println(str);    //java.lang.Object@4eec7777  包名+类名+@+地址值
System.out.println(obj);    //直接打印对象与上面的语句效果
```

java中使用sout打印类名，默认调用的就是该类的toString方法。

toString方法的结论：

如果我们使用`System.out.println(obj);`打印一个对象，想要看到属性值的话，那么重写toString方法就可以。

在重写的方法中，把对象的属性值进行拼接。



### equals

在Object中equals方法

1. 基本数据类型比较值

2. 引用数据类型比较地址值

如果想要比较两个对象的属性值是否一样？重写equals方法。

String类中就重写了equals方法。

---

**String 中equals方法的特点**

1. String中的equals方法先判断参数是否为字符串，如果参数是字符串再比较内部属性。
2. 如果参数***不是字符串***，直接返回false。

3. StringBuilder中没有重写equals方法，默认继承Object父类的。



### clone 对象克隆

对象克隆： 把A对象的属性值完全拷贝给B对象，也叫对象拷贝，对象复制。



> 在 Java 中，并没有像 C++ 中那样的拷贝构造函数的概念。在 Java 中，对象的拷贝通常使用Cloneable接口。
>
> **Cloneable 接口**：Java 中的对象可以实现 Cloneable 接口，并重写 clone() 方法来实现对象的拷贝。然而，使用 clone() 方法进行对象拷贝需要注意深拷贝和浅拷贝的问题。



如果一个接口里面没有抽象方法，则表示当前接口是一个标记性接口。

Cloneable就是一个标记性接口，一旦实现了Cloneable接口，那么当前类的对象就可以被克隆；如果没有实现，当前类的对象就不能被克隆。



**细节：**

方法在底层会帮我们创建一个对象，并把原对象中的数据拷贝过去。

**书写细节：**

1. 重写Object中的clone方法。
2. 让javabean类实现Cloneable接口。
3. 创建原对象并调用clone就可以了。

```java
User u2 = u1.clone();
```



**浅克隆、浅拷贝**

Object中的clone是浅克隆。

基本数据类型：拷贝值

引用数据类型：拷贝地址值

![image-20240606172412375](D:\md_image\image-20240606172412375.png)

**深克隆、深拷贝**



基本数据类型：拷贝值

引用数据类型：以数组举例，重新在内存中创建一个新的数组，把原数组的内容拷贝到新数组中，然后将新数组的地址传给拷贝对象。

![image-20240606172619977](D:\md_image\image-20240606172619977.png)

深克隆**手动复制**实现：

![image-20240606173128532](D:\md_image\image-20240606173128532.png)

另一个实现深克隆的方法：

**序列化和反序列化**

导入别人写好的jar包：

<img src="D:\md_image\image-20240606173505413.png" alt="image-20240606173505413" style="zoom: 80%;" />

总结

![image-20240606195706962](D:\md_image\image-20240606195706962.png)

## Objects（工具类）

`java.utils.Obiects`

Objects是一个工具类，提供了一些方法去完成一些功能。

![image-20240606200239182](D:\md_image\image-20240606200239182.png)

上面三个方法均为静态方法，可以使用类名直接调用。



## BigInteger

Java中，整数有四种类型：byte（1字节），short（2字节），int（4字节），long（8字节）

BigInteger 上限非常大

![image-20240606201557225](D:\md_image\image-20240606201557225.png)

valueOf静态方法获取BigInteger对象。

对象一旦创建，内部记录的值不能发生改变。

**细节：**

1. 字符串中必须是整数，否则会报错。
2. 字符串中的数字必须要跟进制吻合。比如二进制中，只能写0和1，写其他的就报错。



**valueOf方法细节：**

1. 能表示的范围比较小，只能在long的取值范围内，超出long的范围就不行了。

2. 在内部对常用的数字：-16 ~ 16进行了优化

   提前把 -16 ~ 16 先创建好BigInteger的对象，如果多次获取不会重新创建新的。



**方法：**

![image-20240606203056232](D:\md_image\image-20240606203056232.png)



![image-20240606203235763](D:\md_image\image-20240606203235763.png)

![image-20240606203532432](D:\md_image\image-20240606203532432.png)

**总结：**

![image-20240606203736633](D:\md_image\image-20240606203736633.png)

## BigDecima

小数在存储过程中可能是不精确的。

![image-20240606204010401](D:\md_image\image-20240606204010401.png)

BigDecima作用：

* 用于小数的精确运算
* 用来表示很大的数

![image-20240606204736364](D:\md_image\image-20240606204736364.png)

![image-20240606204923709](D:\md_image\image-20240606204923709.png)

**创建对象方法细节：**

1. 如果要表示的数字不大，没有超出Double的取值范围，建议使用静态方法。
2. 如果要表示的数字很大，超出了Double取值范围，建议使用构造方法。
3. 如果我们传递的是0-10之间的**整数**，包含0，包含10，那么方法会返回已经创建好的对象，不会重新new。

**常用成员方法：**

![image-20240606205358820](D:\md_image\image-20240606205358820.png)

**底层存储方式：**

![image-20240606205707201](D:\md_image\image-20240606205707201.png)

**总结：**

![image-20240606205901480](D:\md_image\image-20240606205901480.png)

## 正则表达式

见下一篇笔记



## 时间类

### JDK7以前的时间相关类

![image-20240607173306898](D:\md_image\image-20240607173306898.png)

#### Date时间类

Date类是JDK写好的Javabean类，用来描述时间，精切到毫秒。

原子钟时间（UTC）

**创建时间对象：**

1. 利用空参构造创建的对象，默认表示系统当前时间。

2. 利用有参构造创建的对象，表示指定时间。

```java
Date date = new Date(); //空参构造
Date date = new Date(指定毫秒值)//带参构造
```



**修改时间对象中的毫秒值：**

`setTime(毫秒值)`

获取事件对象中的毫秒值：

`getTime()`



#### SimpleDateFormat 类

两个作用：*格式化*和*解析*



格式化：（Data类型 -> 字符串）

```java
		//空参构造
        SimpleDateFormat sdf1 = new SimpleDateFormat();
        Date d1 = new Date(0L);
        String str1 = sdf1.format(d1);
        System.out.println(str1);

        //有参构造
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy年MM月dd日HH:mm:ss EE");
        Date d2 = new Date(0L);
        String str2 = sdf2.format(d2);
        System.out.println(str2);
```

![image-20240611151113456](D:\md_image\image-20240611151113456.png)



解析：（字符串 -> Date类）

```java
		String str3 = "2024-06-11 12:34:56";
        //创建格式要与字符串格式完全一致
        SimpleDateFormat sdf3 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date d3 = sdf3.parse(str3);
        System.out.println(d3);
```

![image-20240611151839664](D:\md_image\image-20240611151839664.png)



#### Calendar 类

与日历的相关类，可以单独修改、获取时间中的年月日。更方便地以日/月为单位加减时间，而不是以毫秒为单位。

* 细节：Calendar 是一个抽象类，不能直接创建对象，使用一个静态方法获取子类对象。

![image-20240611152240146](D:\md_image\image-20240611152240146.png)

常用方法：

![image-20240611152306814](D:\md_image\image-20240611152306814.png)



```java
package day20;

import java.util.Calendar;
import java.util.Date;

public class CalendarTest {
    public static void main(String[] args) {

        //细节1：Calendar 是一个抽象类，不能直接new，要通过静态方法去获取子类对象
        //底层原理
        //根据系统的不同时区来获取不同的日历对象，默认表示当前时间
        //会把时间中的纪元、年、月、日、时、分、秒、星期，等等的都放到一个数组当中
        //0:纪元
        //1：年
        //2：月
        //3：一年中的第几周
        //4：一个月中的第几周
        //5：一个月中的第几天
        //...16

        //细节2
        //月份：范围0-11，如果获取出来的是0，那么实际上是1月，依此类推。
        //星期：在老外眼里，星期日是一周中的第一天
        //1（星期日）...7（星期6）
        Calendar c1 = Calendar.getInstance();

        //根据Data对象来修改时间
        Date d1 = new Date(0L);
        c1.setTime(d1);
        System.out.println(c1);

        //get方法
        int year = c1.get(Calendar.YEAR);
        int month = c1.get(Calendar.MONTH)+1;
        int day = c1.get(Calendar.DATE);
        System.out.println(year+"-"+month+"-"+day);

        //set方法
        c1.set(Calendar.YEAR,2000);

        year = c1.get(Calendar.YEAR);
        System.out.println(year+"-"+month+"-"+day);

        //add方法
        c1.add(Calendar.YEAR, 1);

        year = c1.get(Calendar.YEAR);               
        System.out.println(year+"-"+month+"-"+day); 

    }
}

```



总结：

掌握三点：

1. Calendar表示什么？
2. 如何获取对象
3. 常见方法
   1. setXxx：修改
   2. getXxx：获取
   3. add：在原有基础上进行增加或减少

4. 细节点
   1. 日历中的月份范围：0-11
   2. 星期日是一周的第一天

### JDK8新增时间相关类

![image-20240611160848677](D:\md_image\image-20240611160848677.png)

![image-20240611160919605](D:\md_image\image-20240611160919605.png)

![image-20240611161545026](D:\md_image\image-20240611161545026.png)



## 包装类

 包装类：基本数据类型对应的引用类型（对象）。

或者这样理解：用一个对象，把基本数据类型给包起来。

<img src="D:\md_image\image-20240611161936685.png" alt="image-20240611161936685" style="zoom:80%;" />

八种基本数据类型对应八种包装类：

![image-20240611162030263](D:\md_image\image-20240611162030263.png)

**以`Integer`为例：**

JDK5以前的<u>*两种获取Integer对象*</u>的方式：

```java
Integer i1 = new Integer(1);
Integer i2 = new Integer("1");
sout(i1);
sout(i2);
Integer i3 = Integer.valueOf(123);
Integer i4 = Integer.valueOf("123");
Integer i5 = Integer.valueOf("123",8); //指定进制
sout(i3);
sout(i4);
sout(i5);
```

这两种方式获取对象的区别（掌握）

valueOf()静态方法会提前将 -128 ~ 127的int数据创建好Integer对象。如果传入valueOf的参数范围在-128 ~ 127之间，就直接使用已创建好的对象。

如果范围超过了-128 ~ 127，则会 new Integer对象。

而new Integer() 每次都是新建对象。



### **包装类如何进行计算？**

JDK5之前，包装类不能直接进行计算。

步骤：

1. 把对象进行拆箱，变成基本数据类型。
2. 相加
3. 把得到的结果再次进行装箱（再变回包装类）。

```java
int result = i1.intValue + i2.intValue();
Integer i3 = new Integer(result);
sout(i3);
```



JDK5之后提出了一种机制，自动装箱和自动拆箱。JDK5之后可以认为Integer和Int的效果是一样的。

```java
//自动装箱：在底层，此时还会自动调用静态方法Valueof得到一个Integer对象，只不过这个动作是自动的。
Integer i1 = 10;

//自动拆箱
Integer i2 = new Integer(10);
int i = i2;
```

```java
Integer i1 = 127;
Integer i2 = 127;
System.out.println(i1 == i2); //True

Integer i1 = 128;
Integer i2 = 128;
System.out.println(i1 == i2); //False

//说明在底层还是调用静态方法Valueof
```



### Integer 常用方法

![image-20240611165200886](D:\md_image\image-20240611165200886.png)

返回值是String类型的原因：

1. 避免二进制开头是0，但int和long类型不允许开头是0的情况。
2. String类型可容纳的数据范围比int和long类型多。



**在8中包装类中，除了Character都有对应的parseXxx的方法进行类型转换。**



## Arrays

操作数组的工具类

**常用方法：**

![image-20240611170351064](D:\md_image\image-20240611170351064.png)

**binarySearch方法 :**

细节：

1. 二分查找的前提：数组中的元素必须是有序，而且必须是升序的。
2. 如果查找的元素是存在的，那么返回的是真实索引，否则返回的是 -插入点-1

为什么要-1呢？

解释：如果此时要查找数字0，那么返回的值是-插入点，即-0。为了避免这种情况，Java在这个基础上又-1。

**copyOf：拷贝数组：**

细节：

参数1：新数组；参数2：老数组1的长度

方法的底层会根据 参数2 来创建新的数组

如果新数组的长度小于老数组的长度，会部分拷贝。

如果新数组的长度等于老数组的长度，会完全拷贝。

如果新数组的长度大于老数组的长度，会补上*基本数据类型对应的默认值*。

**copyOfRange：拷贝数组（指定范围）**

细节：

包头不包尾，包左不包右。

**sort：排序**

默认情况下，给基本数据类型进行升序排列，底层使用快速排序。

除去默认情况，剩下情况使用*<u>重载的sort方法</u>*：

参数1：要排序的数组

参数2：排序的规则

细节：

​		只能给*<u>引用数据类型的数组</u>*进行排序

​		如果数组是基本数据类型的，需要变成其对应的包装类（使用自动装箱）。

​		第二个参数是一个接口，所以我们在调用方法的时候，需要传递这个接口的实现类对象，作为排序的规则。

​		但是这个实现类我们只使用一次，所有没必要单独去写一个类，直接采取***匿名内部类***的方式就可以。

第二个参数的底层原理：

​		底层利用插入排序+二分查找的方式进行排序。

​		默认把0索引的数据当作有序序列，1索引到最后认为是无序的序列。

​		遍历无序序列得到里面的每一个元素，利用二分查找确定插入点然后插入。

​		拿着要插入的元素和插入点进行比较，比较的规则就是*<u>compare里面的方法体</u>*。

​		//如果方法的返回值是负数，拿着当前要插入的元素跟前面的元素比较（降序）

​		//如果方法的返回值是正数或0，拿着当前要插入的元素跟后面的元素比较（升序）

​		//直到确定待插入元素的最终位置为止。

返回值是负数（return中参数顺序和形参中一致）从小到大；是正数，从大到小。



# Lambda表达式

作用：简写匿名内部类的书写



匿名内部类的写法：

```java
        Integer[] arr = {2,4,1,3,8,7,6,0,5};
        Arrays.sort(arr, new Comparator<Integer>() {
            public int compare(Integer o1, Integer o2) {
                return o2 - o1;
            }
        });
        
        System.out.println(Arrays.toString(arr));
```



Lambda表达式简化：

```java
		Integer[] arr = {2,4,1,3,8,7,6,0,5};
        Arrays.sort(arr, (Integer o1, Integer o2) ->{
                return o2 - o1;
            }
        );

        System.out.println(Arrays.toString(arr));
```

**Lambda表达式的标准格式：**

Lambda表达式是JDK8开始后的一种新语法形式。

```java
()->{

}
```

* ()中是形参
* ->固定格式
* {}中是方法体

**使用前提：**

* Lambda表达式只能简化***函数式接口***的匿名内部类的书写
* 函数式接口：
  * 有且***仅有一个抽象方法***的接口叫做函数式接口
  * 接口上方可以加@FunctionalInterface注解



**简写Lambda表达式**

Lambda表达式的省略规则： 

1. 参数类型可以省略不写。
2. 如果只有一个参数，参数类型可以省略，同时()也可以省略。
3. 如果Lambda表达式的<u>方法体只有一行</u>，*大括号、分号、return* 可以省略不写，需要<u>同时省略</u>。

省略核心：可推导的就可省略。



```java
//终极省略形式
		Integer[] arr = {2,4,1,3,8,7,6,0,5};
        Arrays.sort(arr, (o1, o2) ->
                 o2 - o1
        );

        System.out.println(Arrays.toString(arr));
```

