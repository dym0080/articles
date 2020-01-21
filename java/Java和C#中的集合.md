## C#

数组的大小是固定的。如果元素的个数是动态的，那么就应该应用集合。

大多数集合类都可在`system.Collections`和`system.Collections.Genenc`名称空间中找到。泛型集
合类位于`system.Collections.Genenc`名称空间中，专用于特定类型的集合类位于`system.Collections.Specialized`名称空间中，线程安全的集合类位于`system.Collections.Concurrent`名称空
间中。

集合和列表实现的接口如下表：
![集合和列表实现的接口](../assets/java/set_interface.png)

各集合类和接口的关系如下表：
![各集合类和接口的关系](../assets/java/sets.png)

各集合及执行不同操作的性能如下表：
![](../assets/java/diff_sets.png)

### 列表： `List<T>`，`ArrayList`

`List<T>` 是泛型类，实现了 `IList`、`ICollection`、`IEnumerable`,`IList<T>`、`ICollection<T>` 和 `IEnumerable<T>` 接口。

`ArrayList` 是非泛型类，可以将任何 `Object` 类型作为其元素,存在装箱拆箱的操作开销，尽量少用，以提高性能。

### 队列： `Queue<T>`

先进先出（FIFO）。如同生活中在餐厅排队打饭，先到先得，排在前面的先打。

队列使用 `system.Collections.Genenc` 名称空间中的泛型类   `Queue<T>` 实现。在内部， `Queue<T>` 类使用 `T` 类型的数组，这类似于 `List<T>` 类型。它实现 `ICollection` 和  `IEnumerable<T>` ，但没有实现 `ICollection<T>` 接口，因为这个接口定义的 `Add()` 和 `Rmove()` 方法不能用于队列。

因为 `Queue<T>` 没有实现 `IList<T>` 接口,所以不能用索引器访问队列。队列只允许在队列中添加元素,该元素会放在队列的尾部(使用 `Enqueue()` 方法),从队列的头部获取元素(使用 `Dequeue()` 
方法)。

`Queue<T>`类成员如下表：

![](../assets/java/queue_members.png)

### 栈： `Statck<T>`

后进先出（LIFO）。

与 `Queue<T>` 类相同， `Statck<T>` 类实现 `ICollection` 和  `IEnumerable<T>` 接口。

`Statck<T>`类成员如下表：
![](../assets/java/statck_members.png)

### 链表：`LinkedList<T>`

`LinkedList<T>`是一个双向链表。

### 有序表：`SortedList<TKey,TValue>`

### 字典： `Dictionary<TKey,TValue>`, `Lookup<TKey,TValue>`, `SortedDictionary<TKey,TValue>`

`SortedDictionary<TKey,TValue>`类是一个二叉搜索树。

### 集： `HashSet<T>`, `SortedSet<T>`

`HashSet<T>` 集包含不重复元素的无序列表。`SortedSet<T>` 集包含不重复元素的有序列表，它们都实现了 `ISet<T>`接口。

### 可观察集合： `ObservableCollection<T>`

### 位数组： `BitArray`, `BitVector32`

### 并发集合：


## Java

集合框架的接口关系如下表：
![](../assets/java/java_set_interface.png)

java库中具体的集合类如下表:
![](../assets/java/java_set_class.png)

java库中集合框架中的类关系如下表:
![](../assets/java/java_set_class2.png)

### 链表：`LinkedList`

### 数据列表： `ArrayList`

### 散列表：  `HashSet`

### 树集： `TreeSet`

### 队列与双端队列

### 映射(键值对)： `HashMap`, `TreeMap`

> C#中没有 `HashMap`，但可以使用字典。

Java 类库为映射提供了两个通用的实现：`HashMap` 和 `TreeMap`。这两个类都实现了`Map` 接口。

### HashTable

### 枚举

### 栈

### 位集