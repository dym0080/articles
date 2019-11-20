

## `collections`

### `collections.namedtuple()`

自`Python 2.6` 开始，`namedtuple` 就加入到 `Python` 里，用以构建只有少数属性但是没有方法的对象，比如数据库条目。

`collections.namedtuple()` 函数通过使用一个普通的元组对象来帮你解决这个问题。 这个函数实际上是一个返回 Python 中标准元组类型子类的一个工厂方法。 你需要传递一个类型名和你需要的字段给它，然后它就会返回一个类，你可以初始化这个类，为你定义的字段传递值等。 代码示例：

```python
>>> from collections import namedtuple
>>> Subscriber = namedtuple('Subscriber', ['addr', 'joined'])
>>> sub = Subscriber('jonesy@example.com', '2012-10-19')
>>> sub
Subscriber(addr='jonesy@example.com', joined='2012-10-19')
>>> sub.addr
'jonesy@example.com'
>>> sub.joined
'2012-10-19'
>>>
```

```python
>>> from collections import namedtuple
>>> Card = namedtuple('Card', ['rank', 'suit']) # 扑克纸牌类
>>> ranks = [str(n) for n in range(2, 11)] + list('JQKA')
>>> suits = 'spades diamonds clubs hearts'.split()
>>> card = [Card(rank, suit) for suit in suits 
                        for rank in ranks]
>>> print(card) # 打印出所有牌
```

命名元组的一个主要用途是将你的代码从下标操作中解脱出来。 因此，如果你从数据库调用中返回了一个很大的元组列表，通过下标去操作其中的元素， 当你在表中添加了新的列的时候你的代码可能就会出错了。但是如果你使用了命名元组，那么就不会有这样的顾虑。

## `itertools`

### `itertools.compress()`

以一个 `iterable` 对象和一个相对应的 `Boolean` 选择器序列作为输入参数。 然后输出 `iterable` 对象中对应选择器为 `True` 的元素。 当你需要用另外一个相关联的序列来过滤某个序列的时候，这个函数是非常有用的。 比如，假如现在你有下面两列数据：

```python
addresses = [
    '5412 N CLARK',
    '5148 N CLARK',
    '5800 E 58TH',
    '2122 N CLARK',
    '5645 N RAVENSWOOD',
    '1060 W ADDISON',
    '4801 N BROADWAY',
    '1039 W GRANVILLE',
]
counts = [ 0, 3, 10, 4, 1, 7, 6, 1]
```
现在你想将那些对应 `count` 值大于 `5` 的地址全部输出，那么你可以这样做：

```python
>>> from itertools import compress
>>> more5 = [n > 5 for n in counts]
>>> more5
[False, False, True, False, False, True, True, False]
>>> list(compress(addresses, more5))
['5800 E 58TH', '1060 W ADDISON', '4801 N BROADWAY']
>>>
```

这里的关键点在于先创建一个 `Boolean` 序列，指示哪些元素符合条件。 然后 `compress()` 函数根据这个序列去选择输出对应位置为 `True` 的元素。

和 `filter()` 函数类似， `compress()` 也是返回的一个迭代器。因此，如果你需要得到一个列表， 那么你需要使用 `list()` 来将结果转换为列表类型。


### `itertools.dropwhile()`

## `functools`

### `functools.partial()`
>todo

### `functools.reduce()`
>todo

## `re`

`string` 对象的 `split()` 方法只适应于非常简单的字符串分割情形， 它并不允许有多个分隔符或者是分隔符周围不确定的空格。 当你需要更加灵活的切割字符串的时候，最好使用 `re.split()` 方法：

```python
>>> line = 'asdf fjdk; afed, fjek,asdf, foo'
>>> import re
>>> re.split(r'[;,\s]\s*', line)
['asdf', 'fjdk', 'afed', 'fjek', 'asdf', 'foo']
```

函数 `re.split()` 是非常实用的，因为它允许你为分隔符指定多个正则模式。

## `random`

### `random.choice()`

随机抽取序列中的值。

```python
>>> from random import choice
>>> l = [0,1,2,3,4,5,6,7,8,9,10]
>>> choice(l)
10
>>> choice(l)
3
>>> 
```

### `random.shuffle()`

> todo

## `operator`
> todo