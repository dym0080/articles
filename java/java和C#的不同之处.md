# java和C#的不同之处

> 这篇文章在学习[Java核心技术卷一基础知识第10版]时开始编写的，也是我首次学习Java。在学习一个新知识的时候多跟自己已知的知识做比较和联系，这样在学到新知识的同时还可以温习和加深已知知识，更好的增强自己的知识体系网路。

## for each 循环

无需多说，看代码便知。
### c#

```csharp
int[] a = {1,2,3,4,5,6,7,8,9};
foreach (var item in a)
{
    Console.WriteLine(item);
    Console.ReadKey();
}
```
### java
```java
int[] a = {1,2,3,4,5,6,7,9};
for (int item : a) 
{
    System.out.println(item);
}
```

## 定义一个常量

一般是在类中定义为一个**静态**常量。这是由于只要设置为 `static` 后，这个常量只能通过类名访问，不能通过对象访问。换句话说静态常量是属于类不属于对象。如果不设置 `static`，那么就是说每个对象身上都会有这个常量。

### c#

```csharp
public static const double PI = 3.14;
```

### java

```java
public static final double PI = 3.14;
```

## 初始化块 （initialization block）

### c#
无此概念。

### java

java中有三种初始化数据域的方法：

- 在构造器中设置值
- 在声明中赋值
- 初始化块

在一个类的声明中，可以包含多个初始化块，分为**静态初始化块**和**对象初始化块**，只要构造类的对象，这些块就会执行。

下面这段代码(代码来源Java核心技术卷一)展示了java很多特性。重点关注静态初始化块和对象初始化块。

- 重载构造函数
- 用 this(...)掉用另一个构造器
- 无参构造器
- 静态初始化块
- 对象初始化块
- 实例域初始化块

```java
import java.util.*;

/**
 * This program demonstrates object construction.
 * @version 1.02 2018-04-10
 * @author Cay Horstmann
 */
public class ConstructorTest
{
   public static void main(String[] args)
   {
      // fill the staff array with three Employee objects
	  Employee[] staff = new Employee[3];

      staff[0] = new Employee("Harry", 40000);
      staff[1] = new Employee(60000);
      staff[2] = new Employee();

      // print out information about all Employee objects
      for (Employee e : staff)
         System.out.println("name=" + e.getName() + ",id=" + e.getId() + ",salary="
            + e.getSalary());
   }
}

class Employee
{
   private static int nextId;
   
   // instance field initialization
   private int id;
   private String name = ""; 
   private double salary;
   
   // object initialization block 对象初始化块
   {
	  System.out.println("object initialization block");
      id = nextId;
      nextId++;
   }
  
   // static initialization block 静态初始化块
   static
   {
	  System.out.println("static initialization block");
	  Random generator = new Random();
      // set nextId to a random number between 0 and 9999
      nextId = generator.nextInt(10000);
   }

   

   // three overloaded constructors
   public Employee(String n, double s)
   {
      name = n;
      salary = s;
   }

   public Employee(double s)
   {
      // calls the Employee(String, double) constructor
      this("Employee #" + nextId, s);
   }

   // the default constructor
   public Employee()
   {
      // name initialized to ""--see above
      // salary not explicitly set--initialized to 0
      // id initialized in initialization block
   }

   public String getName()
   {
      return name;
   }

   public double getSalary()
   {
      return salary;
   }

   public int getId()
   {
      return id;
   }
}
```
代码执行结果:
```bash
static initialization block
object initialization block
object initialization block
object initialization block
name=Harry,id=1802,salary=40000.0
name=Employee #1803,id=1803,salary=60000.0
name=,id=1804,salary=0.0
```
从结果来看：即使静态初始化块的位置在对象初始化块的前面，但还是静态初始化块先执行，只执行一次，对象初始化块后执行，执行了3次（因为构造了三个对象）。

## 包 和 命名空间

C#中叫命名空间，java中叫包。用来组织类的，确保类名唯一性。假如两个程序员恰巧定义一个相同的类名，只要包名不一样就不会冲突了。

### C#

命名空间使用关键字 `namespace`，导入使用关键字 `using`。一般 `namespace` 的位置放在 `using` 下面。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace com.horstmann.corejava
{
    public class Person
    {
    }
}
```

### java

包使用关键字 `package`，导入使用关键字 `import`。 `package` 的位置必须放在 `import` 上面。
```java
package com.horstmann.corejava;

// the classes in this file are part of this package
import java.util.*;
import java.time.*;

// import statements come after the package statement

public class Person {

}
```


## 继承

### c#
```csharp
// 类同时继承类和多接口
class Dog : Animal,IComparable,ILoger
{

}

// 接口继承接口
interface IPowered : IMoveable
{

}
```

### java
```java
// 类同时继承类和多接口
class Dog extends Animal implements Comparable,Loger
{

}

// 接口继承接口
interface Powered extends Moveable
{

}
```

## 调用父类的构造函数和方法
### c#
使用 `base` 关键字

### java
使用 `super` 关键字

## 重写父类的方法

### c#

父类使用关键字 `virtual` 标记方法，子类使用关键字 `override` 重写父类的方法。

### java

只在子类使用 `super.` 子类方法即可。

子类重写父类方法也可以增加关键字，使用 `@override` 放在方法名的上面作为修饰，而不像c#那样是跟方法名在同一行的。

## 类或方法不允许被继承

C#中使用 `sealed`，成为密封类/密封方法。java中使用 `final`。不同之处只是修饰类或方法的关键字不同。

## 枚举

### c#
如果需要向java那样设置 `S,M,L,XL`，就需要添加如 `Description` 来装饰。

可以给第一项设置一个初始值，后面的则是递增。不设置默认是从 `0` 开始

```csharp
enum ClothSize
   {
      [Description("S")]
      SMALL=2,
      [Description("M")]
      MEDIUM,
      [Description("L")]
      LARGE,
      [Description("XL")]
      EXTRA_LARGE
   }

```

### java

java的枚举类型中可以有构造器、方法和域。而C#没有。

```java
enum ClothSize
{
   SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

   private Size(String abbreviation) { this.abbreviation = abbreviation; }
   public String getAbbreviation() { return abbreviation; }

   private String abbreviation;
}
```

## 接口中的默认方法

假如接口开始只有方法 `Size`，后面因需要新增了方法 `IsEmpty`,如果这个方法被设置为接口的默认方法，那么所有继承该接口的类都不需要去实现这个新增的方法。如果新增的不是默认方法，那么所有继承该接口的类都需要去实现该新增方法，不然不会编译通过。

默认方法可以调用接口中其他的方法。

### C#
C#8.0才开始支持。
```csharp
public interface ICollection
{
   int Size();
   Boolean IsEmpty() //后面新增的
   {
      return Size() == 0;
   }
}
```

### java

需要使用关键字 `default` 标记，而C#不需要。
```java
public interface Collection
{
   int Size();
   default boolean IsEmpty() //后面新增的
   {
      return Size() == 0;
   }
}
```