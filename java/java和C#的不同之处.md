# java和C#的不同之处
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
