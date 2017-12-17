## `range()`与 `list()`
range()函数，可以生成一个整数序列。比如range(101)就可以生成0-100的整数序列。通过list()函数可以把序列转换成list。
```py
list(range(5)) # [0,1,2,3,4]
```
## `enumerate`

Python内置的`enumerate`函数可以把一个list变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身：

```py
for i, value in enumerate(['A', 'B', 'C']):
     print(i, value)

```
输出：
0 A
1 B
2 C

## `callable()`
通过`callable()`函数，我们就可以判断一个对象是否是“可调用”对象。在Python中函数也是属于对象。

一个对象实例可以有自己的属性和方法，当我们调用实例方法时，我们用`instance.method()`来调用。能不能直接在实例本身上调用呢？在Python中，答案是肯定的。任何类，只需要定义一个`__call__()`方法，就可以直接对实例进行调用,比如下面的`s()`。
```py
class Student(object):
    def __init__(self, name):
        self.name = name

    def __call__(self):
        print('My name is %s.' % self.name)
s=Student()
callable(Student()) # True
callable(s())       # True

callable(abs)       # True
callable([1, 2, 3]) # False
callable(None)      # False
callable('abc')     # False
```