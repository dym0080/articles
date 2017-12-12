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