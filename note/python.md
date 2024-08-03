参考

https://docs.python.org/zh-cn/3/tutorial/index.html

https://www.bilibili.com/video/BV1qW4y1a7fU/

# 基础语法

## 字面量

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-42-36-image.png)

查看变量的类型

```python
type(被查看类型的数据)
```

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-45-37-image.png)

数据类型转换

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-46-44-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-47-02-image.png)

标识符命名规则

1. 内容限定

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-48-31-image.png)

2. 大小写敏感

3. 不可使用关键字

变量命名规范--下划线命名法

1. 多个单词组合变量名，要使用下划线做分隔

2. 命名变量中的英文字母，应全部小写

算术运算符

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-51-58-image.png)

字符串

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-53-14-image.png)

•可以使用转移字符（\）来将引号解除效用，变成普通字符串

字符串拼接

使用“+”号连接字符串变量或字符串字面量即可

无法和非字符串类型进行拼接

字符串格式化

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-57-33-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-57-56-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-13-59-32-image.png)

[`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法的基本用法如下所示：

```python
print('We are the {} who say "{}!"'.format('knights', 'Ni'))
```

花括号及之内的字符（称为格式字段）被替换为传递给 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法的对象。花括号中的数字表示传递给 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法的对象所在的位置。

获取键盘输入

```python
input()
```

•使用input()语句可以从键盘获取输入

无论键盘输入何种类型的数据，最终的结果都是：**字符串类型的数据**

[Python ACM 模式下的输入输出 - 文山湖的猫 - 博客园 (cnblogs.com)](https://www.cnblogs.com/jfchen/p/python-acm-input-and-output.html)

## 模块

[6. 模块 — Python 3.12.3 文档](https://docs.python.org/zh-cn/3/tutorial/modules.html)

[__main__ ——顶层代码环境 — Python 3.12.3 文档](https://docs.python.org/zh-cn/3/library/__main__.html#main-py-in-python-packages)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-16-08-15-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-24-14-59-52-image.png)

import后需要用到模块名.方法

from ... import ... 则不需要用到模块名

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-24-15-03-10-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-24-15-03-51-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-24-15-04-27-image.png)

# 函数

## 函数定义

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-07-37-image.png)

## 函数返回值

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-08-18-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-08-46-image.png)

### 多个返回值

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-38-31-image.png)

本质上是将返回值封装成元组

### 返回函数

<https://liaoxuefeng.com/books/python/functional/return-function/index.html>

## 函数参数种类

1. 位置参数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-40-41-image.png)

2. 关键字参数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-41-22-image.png)

注意：是在实参时使用键值对

缺省参数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-03-38-image.png)

不定长参数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-08-39-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-08-54-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-09-06-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-10-59-image.png)

> [4. 更多控制流工具 — Python 3.12.3 文档](https://docs.python.org/zh-cn/3/tutorial/controlflow.html#keyword-arguments)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-16-10-image.png)

函数作为参数传递

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-17-15-image.png)

lamda匿名函数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-18-06-image.png)

函数注解

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-15-18-34-image.png)

# 数据容器

## 迭代器

[迭代器文档1](https://docs.python.org/zh-cn/3/tutorial/classes.html#iterators)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407292049195.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407292051274.png)
> iter()是内置函数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407292046573.png)
> https://docs.python.org/zh-cn/3/library/stdtypes.html#typeiter

## 列表

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-21-20-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-23-02-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-23-31-image.png)

### 列表表达式

> https://docs.python.org/zh-cn/3/tutorial/datastructures.html#list-comprehensions

列表表达式还支持多层嵌套，如下面的例子中第一个 for 为外层循环，第二个为内层循环

```python
[m+'_'+n for m in ['a', 'b'] for n in ['c', 'd']]
Out[6]: ['a_c', 'a_d', 'b_c', 'b_d']
```

## 元组

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-24-47-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-25-02-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-26-40-image.png)

## 字符串

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-27-29-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-28-06-image.png)

## 序列

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-29-56-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-30-09-image.png)

## 集合

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-30-49-image.png)

注意：空集合不可使用{}

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-31-16-image.png)

首先，因为集合是无序的，所以集合不支持：下标索引访问

## 字典

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-32-24-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-34-07-image.png)

当对字典执行循环时，可以使用 [`items()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#dict.items "dict.items") 方法同时提取键及其对应的值。

```python
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
    print(k, v)
```

## 总结

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-15-22-08-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-15-23-30-image.png)

# 类

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-56-27-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-56-53-image.png)



![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-57-46-image.png)

## 类方法与静态方法

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202408032034962.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202408032038894.png)

## 魔法方法

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-58-51-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-59-04-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-59-53-image.png)

### \__call\__

object.__call__(self[, args...])
此方法会在实例作为一个函数被“调用”时被调用；如果定义了此方法，则 x(arg1, arg2, ...) 就大致可以被改写为 type(x).__call__(x, arg1, ...)。

[call解释](https://lulaoshi.info/python/builtin-methods-variables/call.html)
> 注意这个文档的Callable解释不对，看下面的Callable

### \__setattr__

是 Python 中的一个特殊方法，用于在对象属性被设置时自定义行为。它在你通过 `obj.attr = value` 这种方式设置属性时被自动调用。

```python
class MyClass:
    def __init__(self, name):
        self.name = name

    def __setattr__(self, name, value):
        print(f"Setting {name} to {value}")
        super().__setattr__(name, value)

obj = MyClass("Alice")
obj.age = 30  # 这将触发 __setattr__ 方法

```

在这个例子中，每次设置属性时，都会打印一条消息，然后调用 `super().__setattr__(name, value)` 来实际设置属性值.

需要注意的是，如果在 `__setattr__` 方法中直接使用 `self.attr = value`，会导致无限递归。因此，应该使用 `super().__setattr__(name, value) `来避免这个问题

除了使用` super().__setattr__ `函数，我们还可以直接操作对象的实例字典来避免无限递归的问题。Python 中的每个对象都有一个名为` __dict__ `的属性，它是一个字典，用于存储对象的属性和对应的值。
>https://geek-docs.com/python/python-ask-answer/342_python_how_to_use___setattr___correctly_avoiding_infinite_recursion.html
## 封装

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-02-57-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-03-10-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-03-30-image.png)



## 继承

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-05-01-image.png)

多个父类中，如果有同名的成员，那么默认以继承顺序（从左到右）为优先级。

即：先继承的保留，后继承的被覆盖

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-06-32-image.png)

## 类型注解

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-07-16-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-08-33-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-09-13-image.png)

# 其他

## Callable

[标注可调用对象](https://docs.python.org/zh-cn/3/library/typing.html)

```python
#即Callable是用来标注__call__方法的，用来表示他是可调用的
__call__ : Callable[..., Any] = _wrapped_call_impl
```

## 函数式编程

[函数式编程指引](https://docs.python.org/zh-cn/3/howto/functional.html#)

### 装饰器

Python 装饰器（decorators）是一种高级功能，允许你在不修改函数或方法源代码的情况下，**动态**地修改其行为。装饰器本质上是一个函数，它接受另一个函数作为参数，并返回一个新的函数或修改后的函数。
> copilot编写，也就是说装饰器是返回函数的函数

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/202408031753967.png)
>[python文档](https://docs.python.org/zh-cn/3/whatsnew/2.4.html#pep-318-decorators-for-functions-and-methods)
> [廖雪峰文档](https://liaoxuefeng.com/books/python/functional/decorator/index.html#0)


# 常用包

## numpy
### axis理解
Axes are numbered left to right; axis 0 is the first element in the shape tuple.  
> 也就是说ndarray中的shape，axis 0 指的是shape中的第一个元素

![axis](https://mobsidian.oss-cn-beijing.aliyuncs.com/202407202325026.png)
> axis 0 是沿着行往下计算，axis 1沿着列往下计算，即对于一个二维数组（矩阵），axis=0 表示沿着行的方向（垂直方向）操作，而 axis=1 表示沿着列的方向（水平方向）操作。

对于多维数组，如三维数组，

```python
arr_3d = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
```

axis=0 表示沿着最外层的维度操作。
axis=1 表示沿着第二层维度操作。
axis=2 表示沿着最内层的维度操作。

axis 0:这里是将每个二维数组对应位置的元素相加。
axis 1:这里是将每个二维数组的每一行相加。
axis 2:这里是将每个二维数组的每一列相加。

> https://blog.csdn.net/u012219371/article/details/93697240
> https://superlova.github.io/2020/05/19/numpy%E4%B8%ADaxis%E7%9A%84%E7%AE%80%E5%8D%95%E7%90%86%E8%A7%A3/


### reshape

reshape函数有个order：可选参数，表示读取元素的顺序。‘C’ 表示按行读取（C语言风格），‘F’ 表示按列读取（Fortran风格），‘A’ 表示按内存中的存储顺序读取。

都返回一个修改后的数组，但不会更改原始数组：

## Pandas

### Series结构

Series是一种类似于一维数组的对象，可通过`values`和`index`属性获取数组形式和索引

也可以在创建Series时指定索引

```python
 obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
```

Series对象和索引有`name`属性

### DataFrame

建DataFrame的办法有很多，最常用的一种是直接传入一个由等长列表或NumPy数组组成的字典：

```python
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],

'year': [2000, 2001, 2002, 2001, 2002, 2003],

'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

frame = pd.DataFrame(data)
```

#### 属性

`index`和 `columns`，表示行索引和列索引；`values`属性也会以二维ndarray的形式返回DataFrame中的数据

#### 方法

+ `reindex`:其作用是创建一个新对象，它的数据符合新的索引

+ `head`:返回前几行

+ `drop`:丢弃指定轴上的项drop，只要有一个索引数组或列表即可，方法返回的是一个在指定轴上删除了指定值的新对象。用法`new_obj = obj.drop('c')`。对于DataFrame，可以删除任意轴上的索引值。用标签序列调用drop会从行标签（axis 0）删除值：`data.drop(['Colorado', 'Ohio'])`，即不指定axis，默认是行；删列：通过传递axis=1或axis='columns'可以删除列的值

+ `apply`：函数应用到由各列或行所形成的一维数组上，即这里的函数f，计算了一个Series的最大值和最小值的差，在frame的每列都执行了一次。结果是一个Series，使用frame的列作为索引。<u>如果传递axis='columns'到apply，这个函数会在每行执行</u>

  ` f = lambda x: x.max() - x.min()` `frame.apply(f)`

#### 获取列方式

通过类似字典标记的方式或属性的方式，可以将DataFrame的列获取为一个Series：如`frame['state']`;

用一个值或序列对DataFrame进行索引其实就是获取一个或多个列：`data[['three', 'one']]`，也就是说传入一个`数组索引`可以获取多列。

利用标签的切片运算与普通的Python切片运算不同，如`obj['b':'c']`其末端是包含的：即[ ]，而不是python的[ )

`del`方法删除列，如`del frame2['eastern']`，永久删除该列

> 注意：通过索引方式返回的列只是相应数据的视图而已，并不是副本。因此，对返回的Series所做的任何就地修改全都会反映到源DataFrame上。通过Series的copy方法即可指定复制列。

#### 获取行方式

使用轴标签（loc）：`data.loc['Colorado', ['two', 'three']]`，第一个表示行索引，第二个表示列索引

整数索引（iloc）：`data.iloc[2, [3, 0, 1]]`

### 读取文本格式数据：

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/3.png)

如果只想读取几行（避免读取整个文件），通过nrows进行指定即可

利用DataFrame的to_csv方法，我们可以将数据写到一个以逗号分隔的文件中；加入参数sep可以指定分隔符

### 处理缺失数据

#### 删掉缺失值

`dropna`：对于一个Series，dropna返回一个仅含非空数据和索引值的Series；对于DataFrame对象，dropna默认丢弃任何含有缺失值的行，如`cleaned = data.dropna()`，cleaned不包含缺失值，但data却不会改变；传入`how='all'`将只丢弃全为NA的那些行；丢去列只需传入`axis=1`，如果同时加入how=‘all’，丢去全为NA的列。

#### 填充缺失数据

`fillna`：通过一个常数调用fillna就会将缺失值替换为那个常数值，如`df.fillna(0)`，若是通过一个字典调用fillna，就可以实现对不同的列填充不同的值：`df.fillna({1: 0.5, 2: 0})`，即对第一列填充0.5，第二列填充0；fillna默认会返回新对象，但也可以对现有对象进行就地修改，`_ = df.fillna(0, inplace=True)`，即inplace修改调用者本身而不产生副本。此外还有参数`axis`，默认是0。

#### 移除重复数据

`duplicated`方法返回一个布尔型Series，表示各行是否是重复行（前面出现过的

行）

`drop_duplicates`方法，它会返回一个DataFrame，重复的数组会标为False；

这两个方法默认会判断全部列，你也可以指定部分列进行重复项判断，`data.drop_duplicates(['k1'])`

#### 替换值

`replace`：替换值，`data.replace(-999, np.nan)`，将-999替换为NA；如果你希望一次性替换多个值，可以传入一个由待替换值组成的列表以及一个替换值，即`data.replace([-999, -1000], np.nan)`，将-999,和-1000替换为   NA；要让每个值有不同的替换值，可以传递一个替换列表：`data.replace([-999, -1000], [np.nan, 0])`或者`data.replace({-999: np.nan, -1000: 0})`

### Pandas绘图

#### plot

Series和DataFrame都有一个用于生成各类图表的plot方法。默认情况下，它们所生成的是线型图。该Series对象的索引会被传给matplotlib，并用以绘制X轴。可以通过`use_index`=False禁用该功能。

X轴的刻度和界限可以通过xticks和xlim选项进行调节，Y轴就用yticks和ylim。

pandas的大部分绘图方法都有一个可选的ax参数，它可以是一个matplotlib的subplot对象，这使你能够在网格布局中更为灵活地处理subplot的位置，也就是说你plot在哪个subplot上；

label如果不指定默认是DataFrame的列索引

具体参数如下：

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/4.png)

DataFrame的plot方法会在一个subplot中为各列绘制一条线，并自动创建图例。

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/5.png)

#### 在同一个图中用不同的颜色、标签和标记绘制每列数据

```python
import pandas as pd

import numpy as np

import matplotlib.pyplot as plt



df = pd.DataFrame(np.random.randint(1, 10, (10, 3)))

list_label=['A', 'B', 'C']

list_color=['tab:red', 'tab:green', 'tab:blue']

list_marker=['o', 's', 'v']

fig, ax = plt.subplots()



for i, col in enumerate(df):

    df[col].plot(color=list_color[i], marker=list_marker[i], label=list_label[i], ax=ax)



plt.legend()    

plt.show()
```

效果如下:

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/1.png)

#### 轴标签，标题参数

+ x轴标签：`xlabel`, y轴标签：`ylabel`，标题:`title`，在plot里添加即可

+ 又或者使用ax设置，如`ax.set_xlabel("xxx")`，`ax.set_ylabel("yy")`，`ax.set_title("title")`，往plot加入`ax`参数

### 柱状图

`plot.bar()`和`plot.barh()`分别绘制水平和垂直的柱状图。这时，Series和DataFrame的索引将会被用作X（bar）或Y（barh）刻度





## Matplotlib

### figure

figure就是显示一个图片的窗口，在plt.figure()下面所画的所有数据都属于这个figure,num参数即序号，figsize即大小，传入(8,5)即长为8，宽为5；

```python
import matplotlib.pyplot as plt

import numpy as np



x = np.linspace(-3, 3, 50)

y1 = 2*x + 1

y2 = x**2

plt.figure()

plt.plot(x, y1)#属于上一个figure

plt.show()




plt.figure(num=3, figsize=(8, 5),)

plt.plot(x, y2)

plt.plot(x, y1, color='red', linewidth=1.0, linestyle='--')

plt.show()
```

### plot参数

matplotlib的`plot`函数接受一组X和Y坐标，还可以接受一个表示颜色和线型的字符串缩写。即`ax.plot(x, y, 'g--')`相当于`ax.plot(x, y, linestyle='--', color='g')`

`linestyle`：线的格式，'-'表示实线，'--'表示虚线；`color`表示颜色；`marker`表示标记的格式，如'o'表示数据都用圆点标出来；`label`表示图例的标签

~~我们可以创建一个plot图例，指明每条使用`plt.legend`的线。~~

> ~~笔记：你必须调用plt.legend（或使用ax.legend，如果引用了轴的话）来创建图例，无论你绘图时是否传递label标签选项。~~

pyplot接口的设计目的就是交互式使用，含有诸如xlim、xticks和xticklabels之类的方法。它们分别

控制图表的范围、刻度位置、刻度标签等。其使用方式有以下两种：

+ 调用时不带参数，则返回当前的参数值（例如，`plt.xlim()`返回当前的X轴绘图范围）。

+ 调用时带参数，则设置参数值（例如，`plt.xlim([0,10])`会将X轴的范围设置为0到10）。

### 设置坐标轴

`plt.xlim((-1,2))`设置坐标轴的取值范围为-1到2，y轴类似

`plt.xlabel('x')`：x轴的label，

`xticks`设置x轴刻度

```python
new_ticks = np.linspace(-1, 2, 5)

print(new_ticks)

plt.xticks(new_ticks)
```

使用`plt.yticks`设置y轴刻度以及名称：刻度为[-2, -1.8, -1, 1.22, 3]；对应刻度的名称为['really bad','bad','normal','good', 'really good']. 使用`plt.show`显示图像.

```python
plt.yticks([-2, -1.8, -1, 1.22, 3],[r'$really\ bad$', r'$bad$', r'$normal$', r'$good$', r'$really\ good$'])

plt.show()
```

### 改变坐标轴的位置

spines指的是四个边框

```python
#gca='get current axis'

ax = plt.gca()

#即让右边的轴消失

ax.spines['right'].set_color('none')

ax.spines['top'].set_color('none')

plt.show()
```

([设置坐标轴2 | 莫烦Python (mofanpy.com)](https://mofanpy.com/tutorials/data-manipulation/plt/axis2)

### Legend图例

最简单的方式是在`plot`加入参数`label`，然后使用`legend`方法显示

又或者：

```python
l1, = plt.plot(x, y1, label='linear line')

l2, = plt.plot(x, y2, color='red', linewidth=1.0, linestyle='--', label='square line')

#loc表示图例的位置

plt.legend(loc='upper right')
```

### Annotation标注

参数太多，直接ps，详细[2.6 Annotation 标注_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Jx411L7LU?p=8&vd_source=287680e91dcebf5883fc989d2b40edbf)

### 绘图种类

#### Scatter散点图

`plt.scatter`：输入`X`和`Y`作为location，`size=75`，颜色为`T`，`color map`用默认值，透明度`alpha` 为 50%。 x轴显示范围定位(-1.5，1.5)，并用`xtick()`函数来隐藏x坐标轴，y轴同理，即在xtick中传入空()

```python
import matplotlib.pyplot as plt

import numpy as np



n = 1024    # data size

X = np.random.normal(0, 1, n) # 每一个点的X值

Y = np.random.normal(0, 1, n) # 每一个点的Y值

T = np.arctan2(Y,X) # for colorvalue

plt.scatter(X, Y, s=75, c=T, alpha=.5)

plt.xlim(-1.5, 1.5)

plt.xticks(())  # ignore xticks

plt.ylim(-1.5, 1.5)

plt.yticks(())  # ignore yticks



plt.show()
```

#### Bar柱状图

`plt.bar`：`facecolor`设置主体颜色，`edgecolor`设置边框颜色为白色

接下来我们用函数`plt.text`分别在柱体上方（下方）加上数值，用`%.2f`保留两位小数，横向居中对齐`ha='center'`，纵向底部（顶部）对齐`va='bottom'`

```python
import matplotlib.pyplot as plt

import numpy as np



n = 12

X = np.arange(n)

Y1 = (1 - X / float(n)) * np.random.uniform(0.5, 1.0, n)

Y2 = (1 - X / float(n)) * np.random.uniform(0.5, 1.0, n)



plt.bar(X, +Y1, facecolor='#9999ff', edgecolor='white')

plt.bar(X, -Y2, facecolor='#ff9999', edgecolor='white')

for x, y in zip(X, Y1):

    # ha: horizontal alignment，即横向对齐

    # va: vertical alignment，即纵向对齐

    plt.text(x + 0.4, y + 0.05, '%.2f' % y, ha='center', va='bottom')

#zip把两个列表的元素封装成元组对

for x, y in zip(X, Y2):

    # ha: horizontal alignment

    # va: vertical alignment

    plt.text(x + 0.4, -y - 0.05, '%.2f' % y, ha='center', va='top')



plt.xlim(-.5, n)

plt.xticks(())

plt.ylim(-1.25, 1.25)

plt.yticks(())



plt.show()python
```

绘制多柱并列的柱状图

关键在于 第二个柱的x轴要加第一个柱的width

```python
plt.rcParams["font.sans-serif"] = ['Microsoft YaHei']

path="./data/coverage.xlsx"

data=pd.read_excel(path)

df=pd.DataFrame(data)

fig, ax = plt.subplots()

label=["Lines","Functions","Branches"]

index = np.linspace(1, 3, 3)

print(index)

y2=df["SAGAN-AFL"]

y1=df["AFL"]

plt.ylabel("coverage")

width=0.2

ax.bar(index,y1,label="AFL",width=0.2,)

ax.bar(index+width,y2,label="SAGAN-AFL",width=0.2,)

plt.legend()

# tick会显示0.5，重新设置tick

ax.set_xticks(index)

ax.set_xticklabels(label)



for x,y in zip(index,y1):

    plt.text(x, y, '%.3f' % y, ha='center', va='bottom')

for x,y in zip(index,y2):

    plt.text(x+0.2, y, '%.3f' % y, ha='center', va='bottom')

plt.show()
```

#### Contorus等高线图

[Contours 等高线图 | 莫烦Python (mofanpy.com)](https://mofanpy.com/tutorials/data-manipulation/plt/contours)

### Image图片

[Image 图片 | 莫烦Python (mofanpy.com)](https://mofanpy.com/tutorials/data-manipulation/plt/image)

#### Subplot多合一显示

matplotlib 是可以组合许多的小图, 放在一张大图里面显示的. 使用到的方法叫作 subplot.

使用`plt.subplot`来创建小图. `plt.subplot(2,2,1)`表示将整个图像窗口分为2行2列, 当前位置为1.`plt.subplot(2,2,2)`表示将整个图像窗口分为2行2列, 当前位置为2.

#### Subplot分格显示

在使用`subplot`后，设置`xlabel`，`ylabel`，`title`方法都是`set_xlabel`这种形式的，这和一个图不同

由`fig.add_subplot`所返回的对象是`AxesSubplot`对象，直接调用它们的实例方法就可以在其它空着的格子里面画图了，

#### subplot2grid

`subplot2grid`：使用`plt.subplot2grid`来创建第1个小图, `(3,3)`表示将整个图像窗口分成3行3列, `(0,0)`表示从第0行第0列开始作图，`colspan=3`表示列的跨度为3, `rowspan=1`表示行的跨度为1. `colspan`和`rowspan`缺省, 默认跨度为1。

```python
import matplotlib.pyplot as plt

plt.figure()

ax1 = plt.subplot2grid((3, 3), (0, 0), colspan=3)

ax1.plot([1, 2], [1, 2])    # 画小图

ax1.set_title('ax1_title')  # 设置小图的标题

#同理，ax2从(1,0)开始，跨越2列

ax2 = plt.subplot2grid((3, 3), (1, 0), colspan=2)

ax3 = plt.subplot2grid((3, 3), (1, 2), rowspan=2)

ax4 = plt.subplot2grid((3, 3), (2, 0))

ax5 = plt.subplot2grid((3, 3), (2, 1))

plt.tight_layout()#防止刻度遮挡

plt.show()
```

#### gridspec

`gridspec.GridSpec`将整个图像窗口分成3行3列

使用`plt.subplot`来作图, `gs[0, :]`表示这个图占第0行和所有列, `gs[1, :2]`表示这个图占第1行和第2列前的所有列, `gs[1:, 2]`表示这个图占第1行后的所有行和第2列, `gs[-1, 0]`表示这个图占倒数第1行和第0列, `gs[-1, -2]`表示这个图占倒数第1行和倒数第2列.

```python
import matplotlib.pyplot as plt

import matplotlib.gridspec as gridspec

plt.figure()

gs = gridspec.GridSpec(3, 3)

ax6 = plt.subplot(gs[0, :])

ax7 = plt.subplot(gs[1, :2])

ax8 = plt.subplot(gs[1:, 2])

ax9 = plt.subplot(gs[-1, 0])

ax10 = plt.subplot(gs[-1, -2])
```

#### subplots

适合共享轴的做法

使用`plt.subplots`建立一个2行2列的图像窗口，`sharex=True`表示共享x轴坐标, `sharey=True`表示共享y轴坐标. `((ax11, ax12), (ax13, ax14))`表示第1行从左至右依次放`ax11`和`ax12`, 第2行从左至右依次放`ax13`和`ax14`.`f`指的是figure对象，ax11其实就是subplot对象

```python
import matplotlib.pyplot as plt

f, ((ax11, ax12), (ax13, ax14)) = plt.subplots(2, 2, sharex=True,

sharey=True)

ax11.scatter([1,2], [1,2])

plt.tight_layout()

plt.show()
```

`plt.tight_layout()`表示紧凑显示图像, `plt.show()`表示显示图像.

调整subplot周围的间距，默认情况下，matplotlib会在subplot外围留下一定的边距，并在subplot之间留下一定的间距。利用Figure的`subplots_adjust`方法可以轻而易举地修改间距，wspace和hspace用于控制宽度和高度的百分比，可以用作subplot之间的间距，

`plt.subplots_adjust(wspace=0, hspace=0)`，即所有的subplot都紧贴在一起

### 图中图

[图中图 | 莫烦Python (mofanpy.com)](https://mofanpy.com/tutorials/data-manipulation/plt/plot-in-plot)

#### 次坐标轴

有时候我们会用到次坐标轴，即在同个图上有第2个y轴存在。

```python
import matplotlib.pyplot as plt

import numpy as np



x = np.arange(0, 10, 0.1)



y1 = 0.05 * x**2



y2 = -1 * y1

ax2 = ax1.twinx()

ax1.plot(x, y1, 'g-')   # 'g-'为样式，g为green, -为solid line,--表示虚线  



ax1.set_xlabel('X data')



ax1.set_ylabel('Y1 data', color='g')



ax2.plot(x, y2, 'b-') # blue



ax2.set_ylabel('Y2 data', color='b')

plt.show()
```

对`ax1`调用`twinx()`方法，生成如同镜面效果后的`ax2`：twinx可以理解为共享x轴，y轴则相反
