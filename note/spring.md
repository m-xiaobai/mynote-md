## 

## IOC

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-10-22-image.png)

在java中，万物皆对象，这些对象都需要创建，如果创建的时候直接new该对象，就会对该对象耦合严重，假如我们要更换对象，所有new对象的地方都需要修改一遍，这显然违背了软件设计的开闭原则。如果我们使用工厂来生产对象，我们就只和工厂打交道就可以了，彻底和对象解耦，如果要更换对象，直接在工厂里更换该对象即可，达到了与对象解耦的目的；所以说，工厂模式最大的优点就是：**解耦**。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-10-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-46-57-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-47-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-48-54-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-49-05-image.png)

### BeanFactory快速入门

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-14-12-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-14-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-19-46-image.png)

### ApplicationContext

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-16-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-16-42-image.png)

> 注意第四点
> 
> 另外，applicationContext内部维护着beanFactory的引用

ApplicationContext除了<mark>继承</mark>了BeanFactory外，还继承了ApplicationEventPublisher（事件发布器）、
ResouresPatternResolver（资源解析器）、MessageSource（消息资源）等。但是ApplicationContext的核心功
能还是BeanFactory。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-20-07-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-20-16-image.png)

### 事件发布与监听

`Spring` 的事件驱动模型基于 `ApplicationEvent` 和 `ApplicationListener` ，通过事件驱动的方式来实现业务模块之间的交互，交互的方式也有同步和异步两种。事件的发布者仅负责发布事件无需关心事件的接收者，有可能存在一个，也有存在多个接收者。同样，接受者也不知道是谁在发布事件。
Spring的事件驱动模型主要由三部分组成，包括发送消息的生产者，消息，事件监听的消费者，这三者是绑定在一起的，有点类似于RabbitMQ的消息模型

作者：阿劲  
链接：https://juejin.cn/post/6939505372549873678  
来源：稀土掘金  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### Bean的配置详解

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-21-20-image.png)

---

#### 基础配置

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-22-10-image.png)

作用域配置

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-22-42-image.png)

延迟加载

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-23-25-image.png)

初始化和销毁

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-23-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-24-11-image.png)

#### 实例化配置

Spring的实例化方式主要如下两种：
⚫ 构造方式实例化：底层通过构造方法对Bean进行实例化
⚫ 工厂方式实例化：底层通过调用自定义的工厂方法对Bean进行实例化

构造方式实例化

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-26-29-image.png)

工厂方式实例化Bean，又分为如下三种：
⚫ 静态工厂方法实例化Bean
⚫ 实例工厂方法实例化Bean
⚫ 实现FactoryBean规范延迟实例化Bean

静态工厂方法实例化Bean

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-27-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-13-57-24-image.png)

> 当有factor-method时，并不是返回这个FactoryBean这个对象，而是返回getUserDao的返回值作为对象，id是userDao，Object是返回值
> 
> 另外，getUserDao有参数也是通过constructor-arg设置

实例工厂方法实例化Bean

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-29-11-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-29-42-image.png)

> 通过断点观察单例池singletonObjects，发现单例池中既有工厂Bean实例，也有目标Bean实例，且都是在Spring容器创建时，就完成了Bean的实例化

实现FactoryBean规范延迟实例化Bean

![](C:\Users\mqh\Desktop\markdown\spring\assets\2023-04-21-15-30-46-image.png)

![](C:\Users\mqh\Desktop\markdown\spring\assets\2023-04-21-15-31-07-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-32-58-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-33-24-image.png)

> 注意：getBean的是userDao，在singleonObjects中factorybean的name是userDao，
> 
> 为什么getObject尚未执行呢？因为上面是用applicationcontext调用的，而factorybean是在getbean方法的调用的

#### BeanFactory与FactoryBean

BeanFactory，以Factory结尾，表示它是一个工厂类(接口)，用于管理Bean的一个工厂。在Spring中，BeanFactory是IOC**[**容器**](https://cloud.tencent.com/product/tke?from_column=20065&from=20065)**的核心接口，它的职责包括：实例化、定位、配置应用程序中的对象及建立这些对象间的依赖。

FactoryBean以Bean结尾，表示它是一个Bean，不同于普通Bean的是：它是实现了FactoryBean<T>接口的Bean，根据该Bean的ID从BeanFactory中获取的实际上是FactoryBean的getObject()返回的对象，而不是FactoryBean本身，如果要获取FactoryBean对象，请在id前面加一个&符号来获取。

另外，getObject()返回的对象不会放到singletonobject中，而是会放到factoryBeanObjectCache中（看上面）

[【小家Spring】一文读懂Spring中的BeanFactory和FactoryBean（以及它和ObjectFactory的区别）的区别-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1497577)

#### 依赖注入

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-33-53-image.png)

依赖注入的数据类型有如下三种：
⚫ 普通数据类型，例如：String、int、boolean等，通过value属性指定。
⚫ 引用数据类型，例如：UserDaoImpl、DataSource等，通过ref属性指定。
⚫ 集合数据类型，例如：List、Map、Properties等。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-35-37-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-36-04-image.png)

自动装配

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-36-51-image.png)

Spring的get方法

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-15-37-55-image.png)

#### 配置非自定义Bean

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-27-01-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-27-18-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-27-32-image.png)

> 无参构造

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-31-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-31-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-34-08-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-34-21-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-34-41-image.png)

### Spring的后处理器

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-21-17-49-10-image.png)

> Bean工厂后处理器，只执行一次，而Bean后处理器执行多次

BeanFactoryProcessor

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-44-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-46-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-46-48-image.png)

BeanPostProcessor

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-47-35-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-47-57-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-48-34-image.png)

> 动态代理进行增强

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-54-27-image.png)

### Bean的生命周期

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-51-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-52-02-image.png)

> 注意：InitializingBean的初始化方法先于自定义初始化方法init执行

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-53-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/prototype-bean.png)

> mini-spring实现的生命周期
> 
> ***实例化之后应该还有个属性填充***

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/spring-framework-ioc-source-102.png)

### 循环引用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-55-12-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-56-38-image.png)

三级缓存

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-57-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-20-57-20-image.png)

> 关键是实例化后在设置属性前马上放入缓存中<mark>（重点）</mark>
> 
> 如果有代理的话，如UserService有代理，代理创建时机是三级缓存getObject，移入二级缓存中，也就是有循环依赖代理创建时机在设置属性之前
> 
> ~~如果UserDao也有代理应该是在初始化之后，UserDao成为一个完整的Bean就没有循环依赖了（个人理解）~~
> 
> [Spring 解决循环依赖必须要三级缓存吗？ - 掘金 (juejin.cn)](https://juejin.cn/post/6882266649509298189#heading-1)

**因此，Spring 一开始提前暴露的并不是实例化的 Bean，而是将 Bean 包装起来的 ObjectFactory。为什么要这么做呢？**

这实际上涉及到 AOP，如果创建的 Bean 是有代理的，那么注入的就应该是代理 Bean，而不是原始的 Bean。但是 Spring 一开始并不知道 Bean 是否会有循环依赖，通常情况下（没有循环依赖的情况下），Spring 都会在完成填充属性，并且执行完初始化方法之后再为其创建代理。但是，如果出现了循环依赖的话，Spring 就不得不为其提前创建代理对象，否则注入的就是一个原始对象，而不是代理对象。因此，这里就涉及到应该在哪里提前创建代理对象？

Spring 的做法就是在 ObjectFactory 中去提前创建代理对象。它会执行 `getObject()` 方法来获取到 Bean。

作者：好学的康达姆机器人  
链接：https://juejin.cn/post/6882266649509298189  
来源：稀土掘金  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

---

**初始化的时候是对A对象本身进行初始化，而容器中以及注入到B中的都是代理对象，这样不会有问题吗？**

答：不会，这是因为不管是cglib代理还是jdk动态代理生成的代理类，内部都持有一个目标类的引用，当调用代理对象的方法时，实际会去调用目标对象的方法，A完成初始化相当于代理对象自身也完成了初始化

**三级缓存为什么要使用工厂而不是直接使用引用？换而言之，为什么需要这个三级缓存，直接通过二级缓存暴露一个引用不行吗？**

答：这个工厂的目的在于延迟对实例化阶段生成的对象的代理，只有真正发生循环依赖的时候，才去提前生成代理对象，否则只会创建一个工厂并将其放入到三级缓存中，但是不会去通过这个工厂去真正创建对象

即使没有循环依赖，也会将其添加到三级缓存中，而且是不得不添加到三级缓存中，因为到目前为止Spring也不能确定这个Bean有没有跟别的Bean出现循环依赖。

**假设我们在这里直接使用二级缓存的话，那么意味着所有的Bean在这一步都要完成AOP代理。这样做有必要吗？**

不仅没有必要，而且违背了Spring在结合AOP跟Bean的生命周期的设计！Spring结合AOP跟Bean的生命周期本身就是通过`AnnotationAwareAspectJAutoProxyCreator`这个后置处理器来完成的，在这个后置处理的`postProcessAfterInitialization`方法中对初始化后的Bean完成AOP代理。

如果出现了循环依赖，那没有办法，只有给Bean先创建代理，但是没有出现循环依赖的情况下，设计之初就是让Bean在生命周期的最后一步完成代理而不是在实例化后就立马完成代理

作者：redeemer  
链接：https://juejin.cn/post/7217653855445893177  
来源：稀土掘金  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

> 二级缓存问题：如果采用二级缓存来解决循环依赖问题，那么所有的bean都要在二级缓存中生成代理。否则注入的是原始对象。这样做违背了Spring在结合AOP跟Bean的生命周期的设计！Spring结合AOP跟Bean的生命周期的结合是在对初始化后的Bean完成AOP代理。如果出现了循环依赖，那没有办法，只有给Bean先创建代理，但是没有出现循环依赖的情况下，设计之初就是让Bean在生命周期的最后一步完成代理而不是在实例化后就立马完成代理。
> 
> 三级缓存：先将object封装成objectfactory放入三级缓存中，如果生成代理存在循环依赖则生成代理对象存放到二级缓存中，如果不存在循环依赖则直接返回原有对象。

---

出现循环依赖的情况：

(1)通过构造方法进行依赖注入时产生的循环依赖问题。
(2)通过setter方法进行依赖注入且是在单例模式下产生的循环依赖问题。
(3)通过setter方法进行依赖注入且是在多例模式下产生的循环依赖问题。(对于"prototype"作用域的bean，Spring容器并不进行缓存，每次都会生成一个新对象，所以Spring无法通过提前暴露解决"prototype"作用域的setter循环依赖。)
在Spring中，只有第2种方式单例模式的循环依赖问题被解决了，其他两种方式在遇到循环依赖问题时依然会产生异常。

### Aware接口

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-00-25-image.png)

Aware 接口提供了一种【内置】 的注入手段，例如

- BeanNameAware 注入 bean 的名字
- BeanFactoryAware 注入 BeanFactory 容器
- ApplicationContextAware 注入 ApplicationContext 容器
- EmbeddedValueResolverAware 注入 ${} 解析器

### IOC整体流程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-01-05-image.png)

### Bean注解开发

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-08-59-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-09-17-image.png)

> @Component注解的value属性指定当前Bean实例的beanName，也可以省略不写，不写的情况下为当前类名首字母小写

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-10-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-11-11-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-11-34-image.png)

### Bean的线程安全问题

结论：Spring中的Bean不是线程安全的。

Spring容器中的Bean是否线程安全，容器本身并没有提供Bean的线程安全策略，因此可以说Spring容器中的Bean本身不具备线程安全的特性

+ 原型bean：对于原型Bean,每次创建一个新对象，也就是线程之间并不存在Bean共享，自然是不会有线程安全的问题。

+ 单例bean：对于单例Bean,所有线程都共享一个单例实例Bean,因此是存在资源的竞争。
  
  如果单例Bean,是一个无状态Bean，也就是线程中的操作不会对Bean的成员执行**「查询」**以外的操作，那么这个单例Bean是线程安全的。比如Spring mvc 的 Controller、Service、Dao等，这些Bean大多是无状态的，只关注于方法本身。

[面试：Spring 中的bean 是线程安全的吗？-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1743283)

有状态就是有数据存储功能（比如在bean中方法外定义了变量）
无状态就是不会保存数据

小结

1. 在 `@Controller/@Service` 等容器中，默认情况下，scope值是单例-singleton的，也是线程不安全的。
2. 尽量不要在`@Controller/@Service` 等容器中定义静态变量，不论是单例(singleton)还是多实例(prototype)他都是线程不安全的。
3. 默认注入的Bean对象，在不设置`scope`的时候他也是线程不安全的。
4. 一定要定义变量的话，用`ThreadLocal`来封装，这个是线程安全的。

### 依赖注入注解开发

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-13-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-13-47-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-14-21-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-14-41-image.png)

> 也就是说Autowired会去找UserDao类型的bean

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-15-07-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-15-27-image.png)

#### Autowired注解原理

定义一个Beanprocessor，在实例化Bean后设置属性前，查看有哪个属性上有autowire注解，注入到bean中；value注解也是同理。

#### @Component 和 @Bean 的区别是什么？

- `@Component` 注解作用于类，而`@Bean`注解作用于方法。
- `@Component`通常是通过类路径扫描来自动侦测以及自动装配到 Spring 容器中（我们可以使用 `@ComponentScan` 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。`@Bean` 注解通常是我们在标有该注解的方法中定义产生这个 bean,`@Bean`告诉了 Spring 这是某个类的实例，当我需要用它的时候还给我。
- `@Bean` 注解比 `@Component` 注解的自定义性更强，而且很多地方我们只能通过 `@Bean` 注解来注册 bean。比如当我们引用第三方库中的类需要装配到 `Spring`容器时，则只能通过 `@Bean`来实现。

---

著作权归Guide所有
原文链接：https://javaguide.cn/system-design/framework/spring/spring-knowledge-and-questions-summary.html#%E4%BB%80%E4%B9%88%E6%98%AF-spring-bean

#### 非自定义Bean

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-18-08-image.png)

> 在Bean中没加名字，就以方法名作为Bean的名字
> 
> 方法所在的类也需要加Component

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-18-23-image.png)

> 根据名称注入时也可以省掉autowire，只需加qualifier

Bean配置类

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-19-01-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-19-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-19-52-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-22-21-20-25-image.png)

### 注解解析原理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-37-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-37-55-image.png)

## AOP

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-06-31-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-07-14-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-07-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-08-50-image.png)

> //目的：对UserServiceImpl中的show1和show2方法进行增强，增强方法存在与MyAdvice中  
> //问题1：筛选service.impl包下的所有的类的所有方法都可以进行增强，解决方案if-else  
> //问题2：MyAdvice怎么获取到？解决方案：从Spring容器中获得MyAdvice

### AOP相关概念

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-10-35-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-10-47-image.png)

### AOP应用场景

Spring Boot中的AOP（面向切面编程）是一种重要的编程技术，它可以帮助我们将各种横切关注点从业务逻辑中抽离出来，使得应用程序的代码更加简洁，易于维护。以下是一些Spring Boot中使用AOP的应用场景：

1. 记录日志：使用AOP，我们可以将日志记录的逻辑从业务代码中分离出来，这样我们就可以更加灵活地控制哪些方法需要被记录日志。例如，在每个方法调用前后记录方法的入参和出参。

2. 权限控制：使用AOP，我们可以实现在方法执行前检查用户权限。例如，在某个方法调用前，检查用户是否有足够的权限执行该方法。如果没有权限，可以返回错误信息或者抛出异常。

3. 性能监控：使用AOP，我们可以记录方法执行的时间和资源占用情况，这样可以帮助我们发现性能瓶颈和优化应用程序的性能。

4. 事务管理：使用AOP，我们可以将事务管理逻辑从业务代码中分离出来。这样可以确保所有数据库操作都处于同一事务中，并且可以根据需要进行回滚或提交。

总之，Spring Boot中的AOP是一种非常强大的编程技术，可以帮助我们将各种横切关注点从业务代码中分离出来，使得代码更加清晰、易于维护。

### XML配置AOP

通过配置文件的方式去解决上述问题
⚫ 配置哪些包、哪些类、哪些方法需要被增强
⚫ 配置目标方法要被哪些通知方法所增强，在目标方法执行之前还是之后执行增强
配置方式的设计、配置文件（注解）的解析工作，Spring已经帮我们封装好了

---

xml方式配置AOP的步骤：
1、导入AOP相关坐标；
2、准备目标类、准备增强类，并配置给Spring管理；
3、配置切点表达式（哪些方法被增强）；
4、配置织入（切点被哪些通知方法增强，是前置增强还是后置增强）。

---

1、导入AOP相关坐标；

```xml
<dependency>
<groupId>org.aspectj</groupId>
<artifactId>aspectjweaver</artifactId>
<version>1.9.6</version>
</dependency>
```

2、准备目标类、准备增强类，并配置给Spring管理；

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-14-41-image.png)

3、配置切点表达式（哪些方法被增强）；
4、配置织入（切点被哪些通知方法增强，是前置增强还是后置增强）。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-15-13-image.png)

#### 切点表达式

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-16-01-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-16-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-17-09-image.png)

#### 通知类型

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-14-17-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-11-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-12-24-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-12-46-image.png)

### advisor配置通知

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-14-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-14-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-15-01-image.png)

### aspect和advisor配置区别

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-15-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-16-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-16-30-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-16-44-image.png)

### 动态代理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-18-12-image.png)

> 代理类和目标类的关系
> 
> 1. jdk代理：代理类和目标类都实现了同样的接口
> 
> 2. cglib代理：代理是子类，目标类是父类，也就是说代理类继承了目标类

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-18-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-19-15-18-47-image.png)

- <mark>代理的创建时机</mark>
  - 初始化之后 (无循环依赖时)，增强逻辑在bean后置处理器的后置方法中
  - 实例创建后, 依赖注入前 (有循环依赖时), 并暂存于二级缓存
- 依赖注入与初始化不应该被增强, 仍应被施加于原始对象(也就是说初始化方法还是使用原始对象的初始化方法)

### 注解配置AOP

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-44-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-44-41-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-06-12-20-59-05-image.png)

在spring中的核心配置文件中配置aspectj的自动代理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-45-28-image.png)

> 注意：环绕通知还要执行目标方法，而其他通知则不用

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-57-31-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-12-58-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-17-01-08-image.png)

## Spring事务

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-12-42-47-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-12-43-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-19-58-15-image.png)

### xml配置事务

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-19-58-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-19-58-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-19-59-19-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-19-59-44-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-00-07-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-01-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-01-35-image.png)

> 有一个匹配就返回

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-02-09-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-02-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-19-22-46-image.png)

> 传播行为主要解决的是事务嵌套问题，A和B都有事务，A调用B，用谁的事务
> 
> 表的前提是A调用B，B看A

### 声明式事务控制原理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-04-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-04-51-image.png)

> 本质上还是使用AOP增强，Interceptor其实就是通知

就是通过 AOP/动态代理。

- **在 Bean 初始化阶段创建代理对象**：Spring 容器在初始化每个单例 bean 的时候，会遍历容器中的所有 BeanPostProcessor 实现类，并执行其 postProcessAfterInitialization 方法，在执行 AbstractAutoProxyCreator 类的 postProcessAfterInitialization 方法时会遍历容器中所有的切面，查找与当前实例化 bean 匹配的切面，这里会获取事务属性切面，查找@Transactional 注解及其属性值，然后根据得到的切面创建一个代理对象，默认是使用 JDK 动态代理创建代理，如果目标类是接口，则使用 JDK 动态代理，否则使用 Cglib。

- **在执行目标方法时进行事务增强操作**：当通过代理对象调用 Bean 方法的时候，会触发对应的 AOP 增强拦截器，声明式事务是一种环绕增强，对应接口为`MethodInterceptor`，事务增强对该接口的实现为`TransactionInterceptor`，类图如下：

![图片来源网易技术专栏](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-97493c7f-c596-4e98-a6a8-dab254d6d1ab.png)

图片来源网易技术专栏

事务拦截器`TransactionInterceptor`在`invoke`方法中，通过调用父类`TransactionAspectSupport`的`invokeWithinTransaction`方法进行事务处理，包括开启事务、事务提交、异常回滚。

### 注解配置事务

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-23-20-06-37-image.png)

> 在每个方法上使用transactional注解，就是对这个方法使用事务，如果在类上使用这个注解，就是对类中的所有方法使用事务，如果类上和方法上都有，遵循就近原则，使用方法上的。

全注解

```java
@Configuration  //标注当前类是一个配置类（替代配置文件）+@Component
//<context:component-scan base-package="com.itheima"/>
@ComponentScan("com.itheima")
//<context:property-placeholder location="classpath:jdbc.properties"/>
@PropertySource("classpath:jdbc.properties")
//<import resource=""></import>
//@Import(OtherBean.class)
//@Import({MyImportSelector.class})
//@Import(MyImportBeanDefinitionRegistrar.class)
//Mapper的接口扫描
@MapperScan("com.itheima.mapper")
@MyMapperScan
public class SpringConfig {

    @Bean
    public DataSource dataSource(
            @Value("${jdbc.driver}") String driver,
            @Value("${jdbc.url}") String url,
            @Value("${jdbc.username}") String username,
            @Value("${jdbc.password}") String password
    ){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }

    @Bean
    public SqlSessionFactoryBean sqlSessionFactoryBean(DataSource dataSource){
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSource);
        return sqlSessionFactoryBean;
    }
    @Bean
    public PlatformTransactionManager tansactionManager(DataSource dataSource){
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }

}
```

### 事务失效

[8个Spring事务失效的场景，你碰到过几种？ - 掘金 (juejin.cn)](https://juejin.cn/post/7179080622504149029#heading-3)

## Spring整合web环境

### Javaweb三大组件

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-14-19-25-image.png)

```java
@WebServlet(urlPatterns = "/accountServlet")
public class AccountServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        ServletContext servletContext = request.getServletContext();
        ApplicationContext app = WebApplicationContextUtils.getWebApplicationContext(servletContext);
        AccountService accountService = app.getBean(AccountService.class);
        accountService.transferMoney("tom","lucy",500);

    }



}
```

```xml
    <!--定义全局参数-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>
    <!--配置Listener-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
```

> web.xml配置，也就是在web.xml配置一个监听器listener，在listener执行applicationContext的创建

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-14-20-55-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-14-21-50-image.png)

### Spring的web开发组件spring-web

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-50-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-52-08-image.png)

> 也就是说不用自己写listener，listener会创建指定位置的applicationContext，目的是使用spring容器

### MVC框架思想

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-53-15-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-53-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-53-52-image.png)

## SpringMVC

### 快速入门

`@Controller` 注解标记一个类为 Spring Web MVC **控制器** Controller。Spring MVC 会将扫描到该注解的类，然后扫描这个类下面带有 `@RequestMapping` 注解的方法，根据注解信息，为这个方法生成一个对应的**处理器**对象，在上面的 HandlerMapping 和 HandlerAdapter组件中讲到过

MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，其核心思想是通过将业务逻辑、数据、显示分离来组织代码。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-55-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-55-39-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-56-00-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-56-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-14-54-17-image.png)

> 在使用注解时，要扫描包，加载spring-xml文件，就可以在启动前端控制器,读取参数去扫描xml文件，contextConfigLocation是固定值
> 
> web.xml是Javaweb的配置文件，而spring-mvc.xml是SpringMVC的配置文件

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-57-40-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-59-08-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-59-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-16-59-45-image.png)

### SpringMVC关键组件浅析

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-00-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-00-39-image.png)

> <mark>重要</mark>

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-01-17-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-01-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-01-46-image.png)

### SpringMVC的请求处理

#### 请求映射路径的配置

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-02-18-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-02-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-03-22-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-03-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-03-59-image.png)

#### 请求数据的接收

#### 基础接收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-04-23-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-04-32-image.png)

> 一般用这个

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-04-55-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-05-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-05-37-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-24-17-05-50-image.png)

> 还有这个

#### Json格式接收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-08-55-image.png)

> RequestBody是将请求体的数据转换为body

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-09-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-11-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-11-43-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-10-49-02-image.png)

> 形参有request，SpringMVC自动注入request

#### Restful风格数据接收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-12-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-12-49-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-13-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-13-25-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-13-38-image.png)

#### 文件上传数据接收

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-15-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-16-01-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-16-16-image.png)

> 注意：形参的myFile要和表单的name一致

#### HTTP请求头的接收

HTTP请求报文由3部分组成（请求行+请求头+请求体）：

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/http.jpg)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-17-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-17-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-18-15-image.png)

#### 乱码解决方案

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-18-43-image.png)

> 在web.xml配置，因为是Filter属于Javaweb组件

#### Java常用对象获取

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-19-17-image.png)

#### 请求静态资源

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-20-02-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-20-51-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-21-05-image.png)

> 用第三种
> 
> 第二种的mapping是url中的路径，而location是文件在服务器中的路径

#### 注解驱动 标签

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-22-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-22-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-23-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-24-04-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-24-21-image.png)

### SpringMVC响应处理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-24-38-image.png)

#### 传统同步业务数据响应

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-25-13-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-25-33-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-14-10-41-image.png)

> ModelAndView封装模型数据和视图名

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-25-53-image.png)

#### 前后端分离异步业务数据响应

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-26-50-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-27-10-image.png)

> 回写普通数据使用ResponseBody标注，也就是返回字符串，MVC不对字符串进行视图解析

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-28-49-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-29-04-image.png)

### SpringMVC的拦截器

#### 简介

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-30-05-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-30-14-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-30-26-image.png)

> postHandle不一定执行，只有preHandle返回true，然后执行业务方法，执行完后执行postHandle，如果业务方法没执行，postHandle也不执行
> 
> 最后执行afterCompletion，在视图渲染完后，preHandle返回false也不执行

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-30-35-image.png)

#### 快速入门

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-31-47-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-31-56-image.png)

> 在spring-mvc.xml中配置，Interceptor是springmvc技术

#### 拦截器执行顺序

拦截器执行顺序取决于 interceptor 的配置顺序

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-32-14-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-32-24-image.png)

#### 拦截器执行原理

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-33-32-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-33-51-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-34-19-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-34-27-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-34-38-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-34-48-image.png)

### SpringMVC的全注解开发

#### spring-mvc.xml转化为注解

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-39-37-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-40-20-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-40-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-40-56-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-41-08-image.png)

> 或者在springMVCConfig中实现WebMVCConfigurer，就不用单独写

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-41-27-image.png)

以下可以不用管，后面web.xml也用注解了

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-43-02-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-43-13-image.png)

#### 消除web.xml

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-44-06-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-44-37-image.png)

> 第一点的文件名就是上面的，而内容是实现类的全类名
> 
> 第二点：spring已经帮你实现好了
> 
> 第三点也就是我们自己实现那个类就行

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-16-44-50-image.png)

> 第一个提供Spring容器的核心配置类，第二个提供提供SpringMVC容器的核心配置类，第三个提供前端控制器的映射路径
> 
> 如果添加过滤器
> 
> ```java
>     /**
>      * 添加过滤器
>      * @return
>      */
>     @Override
>     protected Filter[] getServletFilters() {
>         CharacterEncodingFilter encodingFilter = new CharacterEncodingFilter();
>         encodingFilter.setEncoding("UTF-8");
>         encodingFilter.setForceRequestEncoding(true);
>         HiddenHttpMethodFilter hiddenHttpMethodFilter = new HiddenHttpMethodFilter();
>         return new Filter[]{encodingFilter, hiddenHttpMethodFilter};
>     }
> ```

## SpringMVC的组件原理剖析

### 前端控制器初始化

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-40-10-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-40-22-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-40-49-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-41-08-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-41-31-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-41-42-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-41-54-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-42-39-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-42-52-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-43-20-image.png)

### 前端控制器执行主流程

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-43-46-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-44-34-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-44-48-image.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/2023-04-25-20-45-00-image.png)

> 也就是说最终执行doDispatch方法
> 
> 注意handleadapter只执行Handler，而handleExecutionChain执行Interceptor的方法

## SpringBoot

是什么

`SpringBoot` 的诞生就是为了简化 `Spring` 中繁琐的 `XML` 配置，其本质依然还是Spring框架，使用SpringBoot之后可以不使用任何 XML 配置来启动一个服务，使得我们可以更加快速的建立一个应用。

简单来说就是SpringBoot其实不是什么新的框架，它默认配置了很多框架的使用方式。

特点

- 提供了固定的配置来简化配置，即`约定大于配置`
- 尽可能地自动配置 Spring 和第三方库，即能`自动装配`
- 完全不需要生成代码，也不需要 XML 配置。
- 在开发web应用程序时，springboot会配置一个嵌入式Tomcat服务器，以便它可以作为独立的应用程序运行。

---

在使用Spring框架进行开发的过程中，需要配置很多Spring框架包的依赖，如spring-core、spring-bean、spring-context等，而这些配置通常都是重复添加的，而且需要做很多框架使用及环境参数的`重复配置`，如开启注解、配置日志等。Spring Boot致力于弱化这些不必要的操作，提供默认配置，当然这些默认配置是可以按需修改的，快速搭建、开发和运行Spring应用。

以下是使用SpringBoot的一些好处：

- 自动配置，使用基于类路径和应用程序上下文的智能默认值，当然也可以根据需要重写它们以满足开发人员的需求。
- 创建Spring Boot Starter 项目时，可以选择选择需要的功能，Spring Boot将为你管理依赖关系。
- SpringBoot项目可以打包成jar文件。可以使用Java-jar命令从命令行将应用程序作为独立的Java应用程序运行。
- 在开发web应用程序时，springboot会配置一个嵌入式Tomcat服务器，以便它可以作为独立的应用程序运行。（Tomcat是默认的，当然你也可以配置Jetty或Undertow）
- SpringBoot包括许多有用的非功能特性（例如安全和健康检查）。

### Boot启动过程

阶段一：SpringApplication 构造

1. 记录 BeanDefinition 源
2. 推断应用类型（非web应用，servlet应用，reactive应用）
3. 记录 ApplicationContext 初始化器（对applicationcontext做功能扩展）// 创建 ApplicationContext->调用初始化器，对 ApplicationContext 做扩展 -》
   // ApplicationContext.refresh
4. 记录监听器
5. 推断主启动类（main方法所在的类是哪个类）

阶段二：执行 run 方法

1. 配置环境
2. 创建容器
3. 准备容器（即初始化容器）
4. 加载bean定义
5. refresh容器
6. 执行runner

### 注解

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/spring/springbootapplication.png)

> **@AutoConfigurationPackage 就是将主配置类（@SpringBootApplication 标注的类）所在的包下面所有的组件都扫描注冊到 spring 容器中。**

自动配置简单说就是把所有的配置类都定义出来，配置类定义是在spring.factories中，然后是否真的加载进入ioc容器中还要判断是否满足某些条件，只有满足条件的配置类才加载进去

https://juejin.cn/post/7046554366068654094#heading-11

### 统一全局异常处理

SpringBoot中，@ControllerAdvice 即可开启全局异常处理，使用该注解表示开启了全局异常的捕获，我们只需在自定义一个方法使用@ExceptionHandler注解然后定义捕获异常的类型即可对这些捕获的异常进行统一的处理。
