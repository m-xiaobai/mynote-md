# Java8新特性

## lamda表达式

1. 举例： (o1,o2) -> Integer.compare(o1,o2);

2. 格式：
   
   * -> :lambda操作符 或 箭头操作符  
   * ->左边：lambda形参列表 （其实就是接口中的抽象方法的形参列表）  
   * ->右边：lambda体 （其实就是重写的抽象方法的方法体）

3. Lambda表达式的使用：（分为6种情况介绍）

4. 总结：  
   
   * ->左边：lambda形参列表的参数类型可以省略(类型推断)；如果lambda形参列表只有一个参数，其一对()也可以省略  
   * ->右边：lambda体应该使用一对{}包裹；如果lambda体只有一条执行语句（可能是return语句），省略这一对{}和return关键字

5. Lambda表达式的本质：作为<mark>函数式接口的实例</mark>，其实还是一个对象，使用条件是一个接口仅有一个未实现的方法

6. 如果一个接口中，只声明了一个抽象方法，则此接口就称为函数式接口。我们可以在一个接口上使用 @FunctionalInterface 注解，这样做可以检查它是否是一个函数式接口。

7. 所以以前用匿名实现类表示的现在都可以用Lambda表达式来写

8. * java内置的4大核心函数式接口  
   * 消费型接口 Consumer<T>     void accept(T t)  
   * 供给型接口 Supplier<T>     T get()  
   * 函数型接口 Function<T,R>   R apply(T t)  
   * 断定型接口 Predicate<T>    boolean test(T t)

```java
//语法格式一：无参，无返回值
@Test
public void test1(){
    Runnable r1 = new Runnable() {
        @Override
        public void run() {
            System.out.println("我爱北京天安门");
        }
    };
    r1.run();
    System.out.println("***********************");

    Runnable r2 = () -> {
        System.out.println("我爱北京故宫");
    };
    r2.run();
}
```

```java
//语法格式二：Lambda 需要一个参数，但是没有返回值。
    @Test
    public void test2(){

        Consumer<String> con = new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(s);
            }
        };
        con.accept("谎言和誓言的区别是什么？");

        System.out.println("*******************");

        Consumer<String> con1 = (String s) -> {
            System.out.println(s);
        };
        con1.accept("一个是听得人当真了，一个是说的人当真了");

    }
```

```java
    //语法格式三：数据类型可以省略，因为可由编译器推断得出，称为“类型推断”
    @Test
    public void test3(){

        Consumer<String> con1 = (String s) -> {
            System.out.println(s);
        };
        con1.accept("一个是听得人当真了，一个是说的人当真了");

        System.out.println("*******************");

        Consumer<String> con2 = (s) -> {
            System.out.println(s);
        };
        con2.accept("一个是听得人当真了，一个是说的人当真了");
    }
```

```java
    //语法格式四：Lambda 若只需要一个参数时，参数的小括号可以省略
    @Test
    public void test5(){
        Consumer<String> con1 = (s) -> {
            System.out.println(s);
        };
        con1.accept("一个是听得人当真了，一个是说的人当真了");

        System.out.println("*******************");

        Consumer<String> con2 = s -> {
            System.out.println(s);
        };
        con2.accept("一个是听得人当真了，一个是说的人当真了");
    }
```

```java
    //语法格式五：Lambda 需要两个或以上的参数，多条执行语句，并且可以有返回值
    @Test
    public void test6(){
        Comparator<Integer> com1 = new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                System.out.println(o1);
                System.out.println(o2);
                return o1.compareTo(o2);
            }
        };
        System.out.println(com1.compare(12,21));
        System.out.println("*****************************");
        Comparator<Integer> com2 = (o1,o2) -> {
            System.out.println(o1);
            System.out.println(o2);
            return o1.compareTo(o2);
        };
        System.out.println(com2.compare(12,6));
    }
```

```java
    //语法格式六：当 Lambda 体只有一条语句时，return 与大括号若有，都可以省略
    @Test
    public void test7(){

        Comparator<Integer> com1 = (o1,o2) -> {
            return o1.compareTo(o2);
        };

        System.out.println(com1.compare(12,6));

        System.out.println("*****************************");

        Comparator<Integer> com2 = (o1,o2) -> o1.compareTo(o2);

        System.out.println(com2.compare(12,21));

    }
```

## 方法引用

使用情境：当要传递给Lambda体的操作，已经有实现的方法了，可以使用方法引用！，即用lambda的操作代替要实现的方法

方法引用，本质上就是Lambda表达式，而Lambda表达式作为函数式接口的实例。所以方法引用，也是函数式接口的实例。

- 使用格式： <mark> 类(或对象) :: 方法名 </mark> 

具体分为如下的三种情况：  

* 情况1     对象 :: 非静态方法  
* 情况2     类 :: 静态方法  
* 情况3     类 :: 非静态方法  

方法引用使用的要求：要求接口中的抽象方法的形参列表和返回值类型与方法引用的方法的形参列表和返回值类型相同！（针对于情况1和情况2）

```java
    //Function中的R apply(T t)
    //Math中的Long round(Double d)
    @Test
    public void test4() {
        Function<Double,Long> func = new Function<Double, Long>() {
            @Override
            public Long apply(Double d) {
                return Math.round(d);
            }
        };

        System.out.println("*******************");

        Function<Double,Long> func1 = d -> Math.round(d);
        System.out.println(func1.apply(12.3));

        System.out.println("*******************");

        Function<Double,Long> func2 = Math::round;
        System.out.println(func2.apply(12.6));
    }
```

```java
    // 情况三：类 :: 实例方法  (有难度)
    // Comparator中的int comapre(T t1,T t2)
    // String中的int t1.compareTo(t2)，即第一个方法的参数充当第二个方法的调用者
    @Test
    public void test5() {
        Comparator<String> com1 = (s1,s2) -> s1.compareTo(s2);
        System.out.println(com1.compare("abc","abd"));

        System.out.println("*******************");

        Comparator<String> com2 = String :: compareTo;
        System.out.println(com2.compare("abd","abm"));
    }
```

## Stream API

使用Stream API对集合数据进行操作，就类似于使用SQL执行的数据库查询

目的：实际开发中，项目中多数数据源都来自Mysql，Nosql的数据需要Java层面处理，即sql语句是数据库层面处理，而Stream在java层面处理

Stream关注的是对数据的运算，与CPU打交道；集合关注的是数据的存储，与内存打交道

* ①Stream 自己不会存储元素。  
* ②Stream 不会改变源对象。相反，他们会返回一个持有结果的新Stream。  
* ③Stream 操作是延迟执行的。这意味着他们会等到需要结果的时候才执行

Stream的执行流程：

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/java8-001.png)

1. 创建方式：注意：一旦使用后就不能再次使用了

```java
  //创建 Stream方式一：通过集合
    @Test
    public void test1(){
        List<Employee> employees = EmployeeData.getEmployees();

//        default Stream<E> stream() : 返回一个顺序流
        Stream<Employee> stream = employees.stream();

//        default Stream<E> parallelStream() : 返回一个并行流
        Stream<Employee> parallelStream = employees.parallelStream();

    }

    //创建 Stream方式二：通过数组
    @Test
    public void test2(){
        int[] arr = new int[]{1,2,3,4,5,6};
        //调用Arrays类的static <T> Stream<T> stream(T[] array): 返回一个流
        IntStream stream = Arrays.stream(arr);

        Employee e1 = new Employee(1001,"Tom");
        Employee e2 = new Employee(1002,"Jerry");
        Employee[] arr1 = new Employee[]{e1,e2};
        Stream<Employee> stream1 = Arrays.stream(arr1);

    }
    //创建 Stream方式三：通过Stream的of()
    @Test
    public void test3(){
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6);

    }
```

2. 中间操作

```java
    //1-筛选与切片
    @Test
    public void test1(){
        List<Employee> list = EmployeeData.getEmployees();
//        filter(Predicate p)——接收 Lambda ， 从流中排除某些元素。
//Prediate其实是java的一个函数式接口，见上面
        Stream<Employee> stream = list.stream();
        //练习：查询员工表中薪资大于7000的员工信息
        stream.filter(e -> e.getSalary() > 7000).forEach(System.out::println);

        System.out.println();
//        limit(n)——截断流，使其元素不超过给定数量。
        list.stream().limit(3).forEach(System.out::println);
        System.out.println();

//        skip(n) —— 跳过元素，返回一个扔掉了前 n 个元素的流。若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补
        list.stream().skip(3).forEach(System.out::println);

        System.out.println();
//        distinct()——筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素

        list.add(new Employee(1010,"刘强东",40,8000));
        list.add(new Employee(1010,"刘强东",41,8000));
        list.add(new Employee(1010,"刘强东",40,8000));
        list.add(new Employee(1010,"刘强东",40,8000));
        list.add(new Employee(1010,"刘强东",40,8000));

//        System.out.println(list);
        list.stream().distinct().forEach(System.out::println);
```

```java
    //映射
    @Test
    public void test2(){
//        map(Function f)——接收一个函数作为参数，将元素转换成其他形式或提取信息，该函数会被应用到每个元素上，并将其映射成一个新的元素。
        List<String> list = Arrays.asList("aa", "bb", "cc", "dd");
        list.stream().map(str -> str.toUpperCase()).forEach(System.out::println);

//        练习1：获取员工姓名长度大于3的员工的姓名。
        List<Employee> employees = EmployeeData.getEmployees();
//map返回的还是一个Stream   
        Stream<String> namesStream = employees.stream().map(Employee::getName);
        namesStream.filter(name -> name.length() > 3).forEach(System.out::println);
        System.out.println();
        //练习2：
        Stream<Stream<Character>> streamStream = list.stream().map(StreamAPITest1::fromStringToStream);
        streamStream.forEach(s ->{
            s.forEach(System.out::println);
        });
        System.out.println();
//        flatMap(Function f)——接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流。
        Stream<Character> characterStream = list.stream().flatMap(StreamAPITest1::fromStringToStream);
        characterStream.forEach(System.out::println);

    }

    //将字符串中的多个字符构成的集合转换为对应的Stream的实例
    public static Stream<Character> fromStringToStream(String str){//aa
        ArrayList<Character> list = new ArrayList<>();
        for(Character c : str.toCharArray()){
            list.add(c);
        }
       return list.stream();
```

map与flatMap的区别：即Stream套Stream用flatmap比较简单

```java
    @Test
    public void test3(){
        ArrayList list1 = new ArrayList();
        list1.add(1);
        list1.add(2);
        list1.add(3);

        ArrayList list2 = new ArrayList();
        list2.add(4);
        list2.add(5);
        list2.add(6);

//        list1.add(list2);[1,2,3,[4,5,6]]，类似于map
        list1.addAll(list2);//[1,2,3,4,5,6]，类似于flatmap
        System.out.println(list1);
    }
```

3. 终止操作

```java
    //1-匹配与查找
    @Test
    public void test1(){
        List<Employee> employees = EmployeeData.getEmployees();

//        allMatch(Predicate p)——检查是否匹配所有元素。
//          练习：是否所有的员工的年龄都大于18
        boolean allMatch = employees.stream().allMatch(e -> e.getAge() > 18);
        System.out.println(allMatch);

//        anyMatch(Predicate p)——检查是否至少匹配一个元素。
//         练习：是否存在员工的工资大于 10000
        boolean anyMatch = employees.stream().anyMatch(e -> e.getSalary() > 10000);
        System.out.println(anyMatch);

//        noneMatch(Predicate p)——检查是否没有匹配的元素。
//          练习：是否存在员工姓“雷”
        boolean noneMatch = employees.stream().noneMatch(e -> e.getName().startsWith("雷"));
        System.out.println(noneMatch);
//        findFirst——返回第一个元素
        Optional<Employee> employee = employees.stream().findFirst();
        System.out.println(employee);
//        findAny——返回当前流中的任意元素
        Optional<Employee> employee1 = employees.parallelStream().findAny();
        System.out.println(employee1);

    }

    @Test
    public void test2(){
        List<Employee> employees = EmployeeData.getEmployees();
        // count——返回流中元素的总个数
        long count = employees.stream().filter(e -> e.getSalary() > 5000).count();
        System.out.println(count);
//        max(Comparator c)——返回流中最大值
//        练习：返回最高的工资：
        Stream<Double> salaryStream = employees.stream().map(e -> e.getSalary());
        Optional<Double> maxSalary = salaryStream.max(Double::compare);
        System.out.println(maxSalary);
//        min(Comparator c)——返回流中最小值
//        练习：返回最低工资的员工
        Optional<Employee> employee = employees.stream().min((e1, e2) -> Double.compare(e1.getSalary(), e2.getSalary()));
        System.out.println(employee);
        System.out.println();
//        forEach(Consumer c)——内部迭代
        employees.stream().forEach(System.out::println);

        //使用集合的遍历操作
        employees.forEach(System.out::println);
    }
```

```java
    //2-归约
    @Test
    public void test3(){
//        reduce(T identity, BinaryOperator)——可以将流中元素反复结合起来，得到一个值。返回 T
//        练习1：计算1-10的自然数的和
        List<Integer> list = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
        Integer sum = list.stream().reduce(0, Integer::sum);
        System.out.println(sum);


//        reduce(BinaryOperator) ——可以将流中元素反复结合起来，得到一个值。返回 Optional<T>
//        练习2：计算公司所有员工工资的总和
        List<Employee> employees = EmployeeData.getEmployees();
        Stream<Double> salaryStream = employees.stream().map(Employee::getSalary);
//        Optional<Double> sumMoney = salaryStream.reduce(Double::sum);
        Optional<Double> sumMoney = salaryStream.reduce((d1,d2) -> d1 + d2);
        System.out.println(sumMoney.get());

    }
```

```java
    //3-收集
    @Test
    public void test4(){
//        collect(Collector c)——将流转换为其他形式。接收一个 Collector接口的实现，用于给Stream中元素做汇总的方法
//        练习1：查找工资大于6000的员工，结果返回为一个List或Set
    //Collectors实用类提供了很多静态方法，可以方便的创建常见收集器实例
//主要是toList()和toSet()
        List<Employee> employees = EmployeeData.getEmployees();
        List<Employee> employeeList = employees.stream().filter(e -> e.getSalary() > 6000).collect(Collectors.toList());

        employeeList.forEach(System.out::println);
        System.out.println();
        Set<Employee> employeeSet = employees.stream().filter(e -> e.getSalary() > 6000).collect(Collectors.toSet());

        employeeSet.forEach(System.out::println);
```

### grouping by
https://www.cnblogs.com/henuyuxiang/p/14989223.html

https://juejin.cn/post/7115262024849817607
# Comparator

**`compare(Integer o1, Integer o2)` 方法 `return o1 - o2` 是升序，`return o2 - o1` 是降序**

- **`compare`方法返回值大于0，会交换前后两个数位置**
- **`compare`方法返回值小于等于0，位置不交换**

[Comparator比较器返回值理解 - 掘金 (juejin.cn)](https://juejin.cn/post/7153629177713786887)

# IDEA Debug教程

## Debug界面

+ (3)Debug窗口：访问请求到达第一个断点后，会自动激活Debug窗口。如果没有自动激活，可以去设置里设置

+ (4) 调试按钮：一共有8个按钮，调试的主要功能就对应着这几个按钮，鼠标悬停在按钮上可以查看对应的快捷键。在菜单栏Run里可以找到同样的对应的功能

+ (5)服务按钮：可以在这里关闭/启动服务，设置断点等

+ (6)方法调用栈：这里显示了该线程调试所经过的所有方法，勾选右上角的[Show All Frames]按钮，就不会显示其它类库的方法了，否则这里会有一大堆的方法。

+ (7)Variables：在变量区可以查看当前断点之前的当前方法内的变量

+ (8)Watches：查看变量，可以将Variables区中的变量拖到Watches中查看

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug002.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug003.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug004.png)

## 基本用法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug005.png)

1前面那一个：Show Execution Point (Alt + F10)：如果你的光标在其它行或其它页面，点击这个按钮可跳转到当前代码执行的行。

1. Step Over (F8)：步过，一行一行地往下走，如果这一行上有方法不会进入方法。

2.  Step Into (F7)：步入，如果当前行有方法，可以进入方法内部，一般用于进入自定义方法内，不会进入官方类库的方法

3. Force Step Into (Alt + Shift + F7)：强制步入，能进入任何方法，查看底层源码的时候可以用这个进入官方类库的方法

4. Step Out (Shift + F8)：步出，从步入的方法内退出到方法调用处，此时方法已执行完毕，只是还没有完成赋值。

5. Drop Frame (默认无)：回退断点，后面章节详细说明。

6. Run to Cursor (Alt + F9)：运行到光标处，你可以将光标定位到你需要查看的那一行，然后使用这个功能，代码会运行至光标行，而不需要打断点。

7.  Evaluate Expression (Alt + F8)：计算表达式，后面章节详细说明

8. Trace Current Stream Chain

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug006.png)

1. Rerun 'xxxx'：重新运行程序，会关闭服务后重新启动程序。

2. Modify Run Configuration

3. Resume Program (F9)：恢复程序，比如，你在第20行和25行有两个断点，当前运行至第20行，按F9，则运行到下一个断点(即第25行)，再按F9，则运行完整个流程，因为后面已经没有断点了。

4. Pause Program：暂停程序，启用Debug。目前没发现具体用法

5. Stop 'xxx' (Ctrl + F2)：连续按两下，关闭程序。有时候你会发现关闭服务再启动时，报端口被占用，这是因为没完全关闭服务的原因，你就需要查杀所有JVM进程了。

6. View Breakpoints (Ctrl + Shift + F8)：查看所有断点，后面章节会涉及到。

7. Mute Breakpoints：哑的断点，选择这个后，所有断点变为灰色，断点失效，按F9则可以直接运行完程序。再次点击，断点变为红色，有效。如果只想使某一个断点失效，可以在断点上右键取消Enabled

## 断点类型

### 行断点（Line Breakpoints）

图标：红色圆形

功能：最常用的断点，在断点所在行进行暂停。

### **方法断点（Method Breakpoint）**

图标：红色菱形

功能：在方法入口（entry）和出口（exit）都会自动暂停。在方法入口暂停可以让我们从头调试整个方法，而在方法出口处暂停可以让我们看到方法执行完毕时，方法内各个变量的数据情况。

有时候我们的一个接口会存在很多实现类，我们短时间内难以分析究竟是运行到了哪个实现类中，这个时候就可以使用方法断点，**我们将断点打在接口方法上，运行到该方法时，会自动跳到实际执行的实现类**，无需通过上下文环境去分析是哪个实现类

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug011.png)

### **字段断点（Field Watchpoints）**

图标：红色眼睛

功能：在字段发生变更（默认）或者被访问（需要额外设置）时暂停。

如果我们想知道某个属性在什么时候被修改，从入口处开始调试太麻烦，我们可以直接在字段上打上字段断点，这样字段被修改的时候就会自动暂停。

而如果我们想在字段被访问时也暂停，则可以右键字段断点，将【Field access】勾选上即可。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug012.png)

### **异常断点（Exception Breakpoints）**

图标：红色闪电

功能：可以在抛出异常的地方进行暂停

异常断点是无需在具体的代码上打断点的，而是在断点详情页中直接添加，后续在执行时，如果抛出我们监听的异常，则会自动暂停在抛出异常的地方。

在view breakpoints设置

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug013.png)

## 变量查看

1. 在IDEA中，参数所在行后面会显示当前变量的值

2. 光标悬停到参数上，显示当前变量信息。

3. 在Variables里查看，这里显示当前方法里的所有变量

4. 在Watches里，点击New Watch，输入需要查看的变量。或者可以从Variables里拖到Watche里查看

## 计算表达式

Evaluate Expression (Alt + F8) 。可以使用这个操作在调试过程中计算某个表达式的值，而不用再去打印信息。

1. 按Alt + F8或按钮，或者，你可以选中某个表达式再Alt + F8，弹出计算表达式的窗口，如下，回车或点击Evaluate计算表达式的值。这个表达式不仅可以是一般变量或参数，也可以是方法，当你的一行代码中调用了几个方法时，就可以通过这种方式查看查看某个方法的返回值。

2. 设置变量，在计算表达式的框里，可以改变变量的值，这样有时候就能很方便我们去调试各种值的情况了

## 智能步入

想想，一行代码里有好几个方法，怎么只选择某一个方法进入。之前提到过使用Step Into (Alt + F7) 或者 Force Step Into (Alt + Shift + F7)进入到方法内部，但这两个操作会根据方法调用顺序依次进入，这比较麻烦。

那么智能步入就很方便了，智能步入，这个功能在Run里可以看到，Smart Step Into (Shift + F7)

<img src="https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug008.png" title="" alt="" data-align="inline">

按Shift + F7，会自动定位到当前断点行，并列出需要进入的方法，如图5.2，点击方法进入方法内部。　　如果只有一个方法，则直接进入，类似Force Step Into。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug009.png)

## 断点条件设置

通过设置断点条件，在满足条件时，才停在断点处，否则直接运行。

通常，当我们在遍历一个比较大的集合或数组时，在循环内设置了一个断点，难道我们要一个一个去看变量的值？那肯定很累，说不定你还错过这个值得重新来一次。

+ 方式1：在断点上右键直接设置当前断点的条件，设置exist为true时断点才生效

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug010.png)

+ 方式2：点击View Breakpoints (Ctrl + Shift + F8)，查看所有断点。

Java Line Breakpoints 显示了所有的断点，在右边勾选Condition，设置断点的条件。

勾选Log message to console，则会将当前断点行输出到控制台，

勾选Evaluate and log，在执行这行代码是计算表达式的值，并将结果输出到控制台。

## 降帧（Drop Frame）

功能：当我们 Debug 从 A 方法进入 B 方法时，通过降帧（退帧）可以返回到调用 B 方法前，这样我们就可以再一次调用 B 方法。

通常用于当我们快执行完 B 方法后，发现某个重要流程被我们跳过了，想再看一下，则此时可以先回退到 A 方法，然后再次进入 B 方法。

我们知道方法的执行和结束在 JVM 中对应的是栈帧的入栈和出栈，因此栈帧描述的就是方法对应的模型，而降帧（退帧）则对应的就是回退到上一个方法。

在IDEA里测试无法一行一行地回退或回到到上一个断点处，而是回到上一个方法。选择Drop Frame后，程序会跳转回调用当前这个方法的地方，当然已经改变的值是不会恢复的。但是当该方法再次被调用时，你可以观察到某个变量什么时候被改变，至少我们不用再去重新运行一遍程序

## 强制返回（Force Return）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug014.png)

功能：强制结束当前程序运行流程，直接返回。

有些时候，我们看到传入的参数有误后，不想走后面的流程了，怎么中断这次请求呢(后面的流程要删除数据库数据呢…)，难道要关闭服务重新启动程序？

当我们调试时，发现继续往下执行就要将错误的数据写入数据库时，我们可以通过 Force Return 来强行结束当前流程。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug015.png)

而如果我们是通过 Stop 按钮来结束，此时结束的是 Debug 流程，而程序流程还是会往下执行，从而将错误数据写入数据库。

## **Stream 调试（Trace Current Stream Chain）**

功能：当我们暂停在 Stream 的处理代码行时，可以将 Stream 的整个处理流程以图形化界面的形式展示

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/java/debug016.png)

合理的使用 Stream 会让我们的代码更加简洁，但是现在存在大量滥用 Stream 的情况，Stream 本身就比较抽象，大量滥用会使得 Stream 的代码难以理解和调试。

当我们发现问题出在 Stream 的处理流程中时，我们可以通过该功能来看到每个步骤处理前和处理后的数据，方便我们定位排查是哪一步出了问题。

## 临时断点

所谓临时断点就是只断一次，IDEA默认断点会一致存在。如果你只需要暂停一次，那么使用临时断点会比较方便，因为暂停一次之后断点就自动消失了，不用手动取消。

临时断点可以通过在打断点时按住 Alt 或者 option 键，然后创建断点。也可以通过右键断点处，选择 more 然后在窗口中选中 Remove once hit

## hello

