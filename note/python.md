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

多个返回值

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-22-14-38-31-image.png)

本质上是将返回值封装成元组

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

## 列表

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-21-20-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-23-02-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-11-23-31-image.png)

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

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-58-51-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-59-04-image.png)

![](https://mobsidian.oss-cn-beijing.aliyuncs.com/2024-04-23-10-59-53-image.png)

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
