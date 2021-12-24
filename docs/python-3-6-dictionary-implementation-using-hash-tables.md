# 使用哈希表的 Python 3.6 字典实现

> 原文:[https://www . geesforgeks . org/python-3-6-字典-实现-使用-哈希表/](https://www.geeksforgeeks.org/python-3-6-dictionary-implementation-using-hash-tables/)

Python 中的 Dictionary 是数据值的集合，用于像映射一样存储数据值，与其他只保存单个值作为元素的数据类型不同，Dictionary 保存键:值对。字典中提供了键值，以使其更加优化。字典中的每个键值对由冒号分隔，而每个键由“逗号”分隔。想了解更多关于字典的信息[点击这里](https://www.geeksforgeeks.org/python-dictionary/)。

根据 Raymond Hettinger 的提议，与 python v.3.5 或更低版本相比，新的 dict()函数的内存使用量减少了 20%到 25%**。它依赖于雷蒙德·赫廷格提出的**保序**语义。这种实现使字典更加紧凑，并提供了更快的迭代。**

**早期版本词典的内存布局没有必要的低效率。它包含一个 24 字节条目的稀疏表，其中存储了哈希值、键指针和值指针。3.5 版及更低版本的字典内存布局被实现为存储在一个稀疏表中。**

****示例:****

```py
for the below dictionary:

d = {'banana':'yellow', 'grapes':'green', 'apple':'red'}

used to store as:

    entries = [['--', '--', '--'],
               [-5850766811922200084, 'grapes', 'green'],
               ['--', '--', '--'],
               ['--', '--', '--'],
               ['--', '--', '--'],
               [2247849978273412954, 'banana', 'yellow'],
               ['--', '--', '--'],
               [-2069363430498323624, 'apple', 'red']]
```

**相反，在新的 dict()实现中，数据现在被组织在由稀疏索引表引用的密集表中，如下所示:**

```py
 indices  = [None, 1, None, None, None, 0, None, 2]
 entries = [[2247849978273412954, 'banana', 'yellow']
             [-5850766811922200084, 'grapes', 'green'],
             [-2069363430498323624, 'apple', 'red']]
```

**需要注意的是，在新的 dict()实现中，只有数据布局发生了变化，哈希表算法没有发生变化。碰撞静力学和表格搜索顺序都没有改变。**

**dict()的这种新实现被认为可以根据 getdictionary 的大小显著压缩字典以节省内存。小词典从中获益最大。**

**对于具有 n 个条目的大小为 t 的稀疏表，大小为:**

```py
curr_size = 24 * t
new_size = 24 * n + sizeof(index) * t
```

**在上面的例子香蕉/葡萄/苹果中，前一个实现的大小是 192 字节(8 个 24 字节条目)，后一个实现的大小是 90 字节(3 个 24 字节条目和 8 个 1 字节索引)。这表明字典的大小压缩了大约 58%。**

**除了节省内存，新的内存布局使得迭代速度更快。现在，像 key()、items()和 values 这样的函数可以在密集表中循环，而不必跳过空槽，这与旧的实现不同。这种新实现的其他好处是更好的缓存利用率、更快的大小调整和更少的内存接触。**