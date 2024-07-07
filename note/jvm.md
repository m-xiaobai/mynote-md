# 简介

## 虚拟机与Java虚拟机

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-30-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-30-24-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-30-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-31-04-image.png)

## JVM的整体架构

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-32-21-image.png)

## JVM的生命周期

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-33-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-33-39-image.png)

# 类加载子系统

## JVM架构

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第02章_JVM架构-中.jpg)

## 类加载器子系统作用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-08-54-image.png)

## 类加载器ClassLoader角色

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-10-12-image.png)

## 类加载过程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-11-04-image.png)

> 类加载过程包括这几个流程，其中第一个也是加载(Loading)；其实就是狭义和广义的关系

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第02章_类的加载过程.jpg)

### 加载(Loading)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-19-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-19-32-image.png)

### 链接

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-20-32-image.png)

> 验证如字节码开头是不是CAFEBABE等

### 初始化

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-24-33-image.png)

> ![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-23-09-image.png)
> 
> 另外，如果没有类变量或者静态代码块则没有<clinit>代码

## 类加载器分类

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-14-50-20-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-14-51-50-image.png)

之间的关系是上下级关系，第二个框是自定义类加载器，他们都继承了ClassLoader

### 引导类加载器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-15-24-49-image.png)

### 扩展类加载器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-15-25-31-image.png) 

### 系统类加载器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-15-26-44-image.png)

## ClassLoader

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-15-28-31-image.png)

### 获取ClassLoader的方式

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-15-29-25-image.png)

> clazz是Class类的一个实例

## 双亲委派机制

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-16-57-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-15-43-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-16-58-30-image.png)

> 如果自定义核心类如java.lang包下的String类，则会报错

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-00-09-image.png)

## 其他

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-02-21-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-02-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-17-02-56-image.png)

> 主动使用会导致类的初始化，而被动使用则不会

# 运行时数据区

## 概述

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-56-12-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-56-48-image.png)

> 一个JVM实例对应于一个Runtime实例，每个JVM只有一个Runtime实例

## 线程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-59-00-image.png)

> 线程有普通线程和守护线程，JVM是否终止要看还有没有普通线程

## PC寄存器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-01-49-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-02-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-02-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-03-24-image.png)

> 即PC寄存器没有GC机制和OOM问题

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-04-38-image.png)

## 虚拟机栈

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-07-27-image.png)

### 基本内容

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-09-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-09-37-image.png)

> 栈没有垃圾回收问题，但会有溢出问题

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-10-52-image.png)

> ![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-22-11-43-image.png)

### 栈的存储单位

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-15-35-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-15-35-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第05章_方法与栈桢.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-15-38-14-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-15-39-31-image.png)

#### 局部变量表

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-15-58-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-15-59-09-image.png)

#### 字节码中方法内部结构剖析

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-41-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-42-36-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-44-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2022-12-31-21-50-02-image.png)

#### slot的理解

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-00-45-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-01-35-image.png)

```java
    public String test2(Date dateP, String name2) {
        dateP = null;
        name2 = "songhongkang";
        double weight = 130.5;//占据两个slot
        char gender = '男';
        return dateP + name2;
    }
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-07-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-08-14-image.png)

```java
    public void test4() {
        int a = 0;
        {
            int b = 0;
            b = a + 1;
        }
        //变量c使用之前已经销毁的变量b占据的slot的位置
        int c = a + 1;
    }
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-09-41-image.png)

#### 静态变量与局部变量

按照数据类型分：

+ 基本数据类型  

+ 引用数据类型

按照在类中声明的位置分：

+ 成员变量：在使用前，都经历过默认初始化赋值  
  
  + 类变量： linking的prepare阶段：给类变量默认赋值  ---> initial阶段：给类变量显式赋值即静态代码块赋值  
  
  + 实例变量：随着对象的创建，会在<mark>堆空间中分配实例</mark>变量空间，并进行默认赋值  

+ 局部变量：在使用前，必须要进行显式赋值的！否则，编译不通过

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-29-55-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-16-30-11-image.png)

#### 操作数栈

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-30-07-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-30-22-image.png)

#### 动态链接

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-31-22-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-32-24-image.png)

#### 方法调用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-33-22-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-33-59-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-34-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-34-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-36-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-37-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-19-37-45-image.png)

> 蓝色的未被重写，所以指向Object，白色的被重写，指向重写方法的类

#### 方法返回地址

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-20-19-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-20-19-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-20-20-41-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-01-20-20-56-image.png)

## 本地方法栈

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-03-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-03-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-04-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-04-46-image.png)

## 堆

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-06-45-image.png)

> 虚拟机栈每个线程都有一份，所有的线程共享堆，

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-08-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-08-57-image.png)

### 内存细分

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-09-53-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第08章_堆空间-java8.jpg)

> JAVA8的堆空间布局，方法区是一个概念，而元空间是方法区的一个实现，在java7中是永久代

### 设置堆的大小

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-13-20-image.png)

> 在实际情况下初始内存是小于物理内存/64，在年轻代中只会计算s0和s1的其中一个
> 
> -Xms 用来设置堆空间（年轻代+老年代）的初始内存大小
> 
>  -X 是jvm的运行参数  
> 
> ms 是memory start
> 
> 开发中建议将初始堆内存和最大的堆内存设置成相同的值。

### 年轻代与老年代

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-16-35-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-17-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-17-41-image.png)

> 在实际中并不是8:1:1，因为自适应内存分配策略

### 对象分配过程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-22-53-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-23-08-image.png)

> 幸存区满并不会触发GC，只有Eden满才会触发GC，顺带把幸存区GC

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第08章_新生代对象分配与回收过程.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-31-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-02-16-31-17-image.png)

### GC

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-21-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-22-16-image.png)

Eden代满才会触发young gc

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-23-03-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-23-20-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-23-54-image.png)

### 内存分配策略

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-24-49-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-25-04-image.png)

### TLAB

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-25-58-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-26-20-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第08章_TLAB.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-27-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第08章_对象分配过程.jpg)

### 堆空间的参数设置

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-28-47-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-29-07-image.png)

### 其他

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-30-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-30-39-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-03-19-30-53-image.png)

## 方法区

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第08章_方法区的演进细节-hotspot.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-22-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-22-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-23-12-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-23-30-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-23-51-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-24-44-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-25-03-image.png)

### 设置方法区大小

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-25-48-image.png)

### 方法区的内部结构

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-27-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-27-29-image.png)

#### 类型信息

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-28-18-image.png)

#### 域信息

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-29-00-image.png)

#### 方法信息

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-29-30-image.png)

#### 类变量

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-30-12-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-30-42-image.png)

### 运行时常量池与常量池

#### 常量池

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-31-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-32-53-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-33-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-33-33-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-33-46-image.png)

#### 运行时常量池

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-35-00-image.png)

### 方法区演进

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-38-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-38-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-38-58-image.png)

### 方法区的垃圾回收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-39-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-13-40-12-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-14-02-13-image.png)

### 小结

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第09章_小结.jpg)

## 对象的实例化，内存布局与访问方式

### 对象的实例化

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第10章_对象的实例化.jpg)

### 内存布局

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第10章_对象的内存布局.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第10章_图示对象的内存布局.jpg)

### 对象访问定位

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第10章_对象访问定位.jpg)

#### 句柄访问

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第10章_方式1：句柄访问.jpg)

#### 直接访问

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第10章_方式2：使用直接指针访问.jpg)

> Hotspot采用

### 直接内存

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-29-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-31-01-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-31-45-image.png)

## 执行引擎

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-32-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-32-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-33-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-33-33-image.png)

### Java代码编译和执行过程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-34-06-image.png)

> 绿色的是解释执行，蓝色的是编译；

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-36-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-36-55-image.png)

> 即java代码既有解释执行也有编译过程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-37-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-37-57-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第12章_理解执行引擎.jpg)

### 字节码

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第12章_机器语言、汇编、高级语言.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-40-41-image.png)

### 解释器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-41-45-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-41-57-image.png)

### JIT编译器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-42-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-43-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-43-37-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-44-47-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-45-11-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-46-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-04-23-46-54-image.png)

## StringTable

### String的基本特性

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-13-19-35-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-14-43-56-image.png)

> 通过new的方式创建在堆中

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-14-44-45-image.png)

### String的内存分配

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-14-45-28-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-14-45-43-image.png)

```java
public class StringTest5 {
    @Test
    public void test1(){
        String s1 = "a" + "b" + "c";//编译期优化：等同于"abc"
        String s2 = "abc"; //"abc"一定是放在字符串常量池中，将此地址赋给s2
        /*
         * 最终.java编译成.class,再执行.class
         * String s1 = "abc";
         * String s2 = "abc"
         */
        System.out.println(s1 == s2); //true
        System.out.println(s1.equals(s2)); //true
    }

    @Test
    public void test2(){
        String s1 = "javaEE";
        String s2 = "hadoop";

        String s3 = "javaEEhadoop";
        String s4 = "javaEE" + "hadoop";//编译期优化
        //如果拼接符号的前后出现了变量，则相当于在堆空间中new String()，
//具体的内容为拼接的结果：javaEEhadoop
        String s5 = s1 + "hadoop";
        String s6 = "javaEE" + s2;
        String s7 = s1 + s2;

        System.out.println(s3 == s4);//true
        System.out.println(s3 == s5);//false
        System.out.println(s3 == s6);//false
        System.out.println(s3 == s7);//false
        System.out.println(s5 == s6);//false
        System.out.println(s5 == s7);//false
        System.out.println(s6 == s7);//false
        //intern():判断字符串常量池中是否存在javaEEhadoop值，如果存在，
        //则返回常量池中javaEEhadoop的地址；
        //如果字符串常量池中不存在javaEEhadoop，
        //则在常量池中加载一份javaEEhadoop，并返回次对象的地址。
        String s8 = s6.intern();
        System.out.println(s3 == s8);//true
    }

    @Test
    public void test3(){
        String s1 = "a";
        String s2 = "b";
        String s3 = "ab";
        /*
        如下的s1 + s2 的执行细节：(变量s是我临时定义的）
        ① StringBuilder s = new StringBuilder();
        ② s.append("a")
        ③ s.append("b")
        ④ s.toString()  --> 约等于 new String("ab")

        补充：在jdk5.0之后使用的是StringBuilder,
        在jdk5.0之前使用的是StringBuffer
         */
        String s4 = s1 + s2;//
        System.out.println(s3 == s4);//false
    }
    /*
    1. 字符串拼接操作不一定使用的是StringBuilder!
       如果拼接符号左右两边都是字符串常量或常量引用，
        则仍然使用编译期优化，即非StringBuilder的方式。
    2. 针对于final修饰类、方法、基本数据类型、引用数据类型的量的结构时，
    能使用上final的时候建议使用上。
     */
    @Test
    public void test4(){
        final String s1 = "a";
        final String s2 = "b";
        String s3 = "ab";
        String s4 = s1 + s2;
        System.out.println(s3 == s4);//true
    }
    //练习：
    @Test
    public void test5(){
        String s1 = "javaEEhadoop";
        String s2 = "javaEE";
        String s3 = s2 + "hadoop";
        System.out.println(s1 == s3);//false

        final String s4 = "javaEE";//s4:常量
        String s5 = s4 + "hadoop";
        System.out.println(s1 == s5);//true

    }

    /*
    体会执行效率：通过StringBuilder的append()的方式添加字符串的效率要远高于使用
    String的字符串拼接方式！
    详情：① StringBuilder的append()的方式：自始至终中只创建过一个
            StringBuilder的对象
          使用String的字符串拼接方式：创建过多个StringBuilder和String的对象
         ② 使用String的字符串拼接方式：内存中由于创建了较多的StringBuilder
                                                                                和String的对象，内存占用更大；如果进行GC，需要花费额外的时间。

     改进的空间：在实际开发中，如果基本确定要前前后后添加的字符串长度不高于某个限定值
        highLevel的情况下,建议使用构造器实例化：
               StringBuilder s = new StringBuilder(highLevel);
                //new char[highLevel]
     */
    @Test
    public void test6(){

        long start = System.currentTimeMillis();

//        method1(100000);//4014
        method2(100000);//7

        long end = System.currentTimeMillis();

        System.out.println("花费的时间为：" + (end - start));
    }

    public void method1(int highLevel){
        String src = "";
        for(int i = 0;i < highLevel;i++){
            src = src + "a";//每次循环都会创建一个StringBuilder、String
        }
//        System.out.println(src);

    }

    public void method2(int highLevel){
        //只需要创建一个StringBuilder
        StringBuilder src = new StringBuilder();
        for (int i = 0; i < highLevel; i++) {
            src.append("a");
        }
//        System.out.println(src);
    }
}
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-14-49-40-image.png)

### intern()的使用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-16-31-58-image.png)

```java
/**
 * 题目：
 * new String("ab")会创建几个对象？看字节码，就知道是两个。
 *     一个对象是：new关键字在堆空间创建的
 *     另一个对象是：字符串常量池中的对象"ab"。 字节码指令：ldc
 *
 *
 * 思考：
 * new String("a") + new String("b")呢？
 *  对象1：new StringBuilder()
 *  对象2： new String("a")
 *  对象3： 常量池中的"a"
 *  对象4： new String("b")
 *  对象5： 常量池中的"b"
 *
 *  深入剖析： StringBuilder的toString():
 *      对象6 ：new String("ab")
 *       强调一下，toString()的调用，在字符串常量池中，没有生成"ab"
 *
 * @author shkstart  shkstart@126.com
 * @create 2020  20:38
 */
public class StringNewTest {
    public static void main(String[] args) {
//        String str = new String("ab");

        String str = new String("a") + new String("b");
    }
}
```

```java
/**
 * 如何保证变量s指向的是字符串常量池中的数据呢？
 * 有两种方式：
 * 方式一： String s = "shkstart";//字面量定义的方式
 * 方式二： 调用intern()
 *         String s = new String("shkstart").intern();
 *         String s = new StringBuilder("shkstart").toString().intern();
 *
 * @author shkstart  shkstart@126.com
 * @create 2020  18:49
 */
public class StringIntern {
    public static void main(String[] args) {

        String s = new String("1");
        s.intern();//调用此方法之前，字符串常量池中已经存在了"1"
        String s2 = "1";
        System.out.println(s == s2);//jdk6：false   jdk7/8：false


        String s3 = new String("1") + new String("1");//s3变量记录的地址为：new String("11")
        //执行完上一行代码以后，字符串常量池中，是否存在"11"呢？答案：不存在！！
        s3.intern();//在字符串常量池中生成"11"。如何理解：jdk6:创建了一个新的对象"11",也就有新的地址。
                                            //         jdk7:此时常量中并没有创建"11",而是创建一个指向堆空间中new String("11")的地址
        String s4 = "11";//s4变量记录的地址：使用的是上一行代码代码执行时，在常量池中生成的"11"的地址
        System.out.println(s3 == s4);//jdk6：false  jdk7/8：true
    }


}
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-16-52-20-image.png)

> JDK6的代码图

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-16-52-44-image.png)

#### 总结

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-16-53-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-16-54-39-image.png)

```java
        String s = new String("a") + new String("b");//new String("ab")
        //在上一行代码执行完以后，字符串常量池中并没有"ab"

        String s2 = s.intern();//jdk6中：在串池中创建一个字符串"ab"
                               //jdk8中：串池中没有创建字符串"ab",而是创建一个引用，指向new String("ab")，将此引用返回

        System.out.println(s2 == "ab");//jdk6:true  jdk8:true
        System.out.println(s == "ab");//jdk6:false  jdk8:true
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-05-16-54-53-image.png)

# 垃圾回收

## 概述

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-44-52-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-45-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-45-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-46-02-image.png)

## 垃圾回收算法

### 标记阶段（判断对象存活）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-47-53-image.png)

#### 引用计数法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-48-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-48-28-image.png)

> 循环引用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-49-11-image.png)

#### 可达性分析算法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-49-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-50-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-50-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-50-45-image.png)

> 前四个要记住

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-51-14-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-51-33-image.png)

### 垃圾清除阶段算法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-53-40-image.png)

#### 标记-清除算法(重要)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-54-30-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第14章_标记-清除算法.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-06-22-55-35-image.png)

#### 复制算法(重要)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-56-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/第14章_复制算法.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-57-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-57-51-image.png)

#### 标记-压缩算法(重要)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-58-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-58-47-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-59-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-19-59-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-08-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-08-26-image.png)

### 分代收集算法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-09-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-09-33-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-09-45-image.png)

### 增量收集算法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-10-26-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-10-39-image.png)

### 分区算法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-11-26-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-11-57-image.png)

## 垃圾回收相关概念

### System.gc()

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-25-12-image.png)

### 内存溢出OOM

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-25-52-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-26-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-26-35-image.png)

### 内存泄露

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-27-03-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-27-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-27-46-image.png)

### stop the world

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-28-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-28-38-image.png)

### 垃圾回收的并行与并发

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-29-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-29-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-29-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-30-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-30-21-image.png)

### 安全点与安全区域

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-31-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-31-30-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-31-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-07-20-32-03-image.png)

### 引用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-18-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-18-32-image.png)

#### 强引用（不回收）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-19-22-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-19-41-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-27-59-image.png)

#### 软引用（内存不足即回收）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-28-55-image.png)

```java
//软引用例子
        //创建对象，建立软引用
//        SoftReference<User> userSoftRef = new SoftReference<User>(new User(1, "songhk"));
        //上面的一行代码，等价于如下的三行代码
        User u1 = new User(1,"songhk");
        SoftReference<User> userSoftRef = new SoftReference<User>(u1);
        u1 = null;//取消强引用


        //从软引用中重新获得强引用对象
        System.out.println(userSoftRef.get());
```

#### 弱引用（发现即回收）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-31-41-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-32-10-image.png)

#### 虚引用（对象回收跟踪）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-33-08-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-33-53-image.png)

## 垃圾回收器

### GC分类与性能指标

#### GC分类

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-37-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-37-22-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-37-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-37-54-image.png)

#### GC性能指标

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-38-21-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-39-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-39-30-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-39-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-40-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-40-19-image.png)

> 红字意思是指定一个暂停时间，使得吞吐量最大

### 不同垃圾回收器概述

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-42-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-49-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-50-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-50-18-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-50-33-image.png)

#### Serial回收器：串行回收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-52-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-52-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-52-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-52-45-image.png)

#### ParNew回收器：并行回收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-53-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-54-02-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-54-20-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-08-16-54-41-image.png)

#### Parallel回收器：吞吐量优先

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-44-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-44-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-45-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-45-21-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-45-49-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-46-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-46-19-image.png)

#### CMS回收器：低延迟

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-47-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-47-33-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-47-49-image.png)

##### 工作原理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-48-53-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-49-07-image.png)

[JVM垃圾收集之三色标记算法详解 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzI4ODE1MTQwNg==&mid=2247484000&idx=1&sn=fc62a47fbed801264e3192008df95537&chksm=ebc38061dcb40977160f274e766c76a60e1835fa851821d4c9ed359a619678f6abc9280015aa&scene=27)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-49-28-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-49-44-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-50-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-50-18-image.png)

##### 可设置参数

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-51-26-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-51-44-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-52-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-52-22-image.png)

#### G1回收器：区域化分代式

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-54-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-54-31-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-54-59-image.png)

##### 优势

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-55-28-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-55-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-56-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-56-41-image.png)

##### 参数设置

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-57-18-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-57-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-58-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-58-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-59-01-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-22-59-19-image.png)

##### 垃圾回收过程（记忆集）（可以参考深入理解java虚拟机）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-00-26-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-00-41-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-01-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-01-24-image.png)

> 上页提到的Remebered Set就是上述Reset，上页提到的Reference类型就是引用类型，其中Reset的作用是记录当前Region中哪些对象被外部引用指向，比如Old区中的对象会指向Eden区的对象，然后当我们要回收某个Region的时候，直接遍历遍历当前Region中的所有对象就可以了，然后针对性的去找到那些指向当前对象的其他对象，最终发现当前对象是否是根可达的，如果不是，那就应该被删除，其实之前的垃圾回收器都涉及到这个问题，当进行MinorGC的时候，通过GC Roots查找的时候还需要遍历Old区的对象，毕竟Old区对象也可能会指向Eden区对象，但是G1通过Rset避免了全堆的扫描，当引用类型数据写操作时，先暂时中断，然后判断当前引用类型数据是否被其他对象所指向，如果不被指向，那就直接放在Region中就可以了；如果被其他对象指向，那么还要判断这个对象是在当前要插入的Region中，还是在其他Region中；如果在其他Region中，那就需要使用CardTable把当前引用类型数据的指向信息放在Rset中，也就是形成上面的虚线连线，如果在当前Region中，那就不需要指向了，毕竟到时候我们会进行遍历查找根可达对象，那肯定会找到的，所以这种情况也是直接放在Region中就可以了；

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-03-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-03-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-03-57-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-04-16-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-04-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-05-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-05-26-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-05-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-06-03-image.png)

#### 垃圾回收器总结

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-07-52-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-08-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-08-39-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-08-51-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-09-10-image.png)

### GC日志分析

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-11-29-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-20-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-21-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-21-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-21-59-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-22-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-22-53-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-23-08-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/jvm/2023-01-09-23-23-29-image.png)
