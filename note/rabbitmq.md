# MQ的基本概念

## MQ概述

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/01.png)

分布式系统通信方式：

+ 远程调用

+ 借助第三方

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/02.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/03.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/04.png)

## MQ的优势

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/05.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/06.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/07.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/08.png)

## 劣势

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/09.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/10.png)

## 常见的MQ

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/11.png)

## rabbitmq

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/12.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/13.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/14.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/15.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/16.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/17.png)

# rabbit的安装

## Linux使用Docker安装

1. 下载`rabbitmq 3.7.15`的Docker镜像
   
   ```shell
   docker pull rabbitmq:3.7.15
   ```

2. 使用Docker命令启动服务
   
   ```shell
   docker run -p 5672:5672 -p 15672:15672 --name rabbitmq \
   -d rabbitmq:3.7.15
   ```

3. 进入容器并开启管理功能
   
   ```shell
   docker exec -it rabbitmq /bin/bash
   rabbitmq-plugins enable rabbitmq_management
   ```
   
   ![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/18.png)

4. 开启防火墙便于外网访问
   
   ```shell
   firewall-cmd --zone=public --add-port=15672/tcp --permanent
   firewall-cmd --zone=public --add-port=5672/tcp --permanent
   firewall-cmd --reload
   ```

5. 访问及配置，地址为localhost:15762（linux下使用），默认的账号密码：guest guest

# rabbitmq的工作模式

## 简单模式

类似于Work queues模式，只不过消费者只有一个

## Work queues

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/19.png)

依赖：

```xml
        <dependency>
            <groupId>com.rabbitmq</groupId>
            <artifactId>amqp-client</artifactId>
            <version>5.6.0</version>
        </dependency>
```

生产者

```java
   //1.创建连接工厂
        ConnectionFactory factory = new ConnectionFactory();
        //2. 设置参数
        factory.setHost("172.16.98.133");//ip  默认值 localhost
        factory.setPort(5672); //端口  默认值 5672
        factory.setVirtualHost("/itcast");//虚拟机 默认值/
        factory.setUsername("heima");//用户名 默认 guest
        factory.setPassword("heima");//密码 默认值 guest
        //3. 创建连接 Connection
        Connection connection = factory.newConnection();
        //4. 创建Channel
        Channel channel = connection.createChannel();
        //5. 创建队列Queue
        /*
        queueDeclare(String queue, boolean durable, boolean exclusive, boolean autoDelete, Map<String, Object> arguments)
        参数：
            1. queue：队列名称
            2. durable:是否持久化，当mq重启之后，还在
            3. exclusive：
                * 是否独占。只能有一个消费者监听这队列
                * 当Connection关闭时，是否删除队列
                *
            4. autoDelete:是否自动删除。当没有Consumer时，自动删除掉
            5. arguments：参数。

         */
        //如果没有一个名字叫hello_world的队列，则会创建该队列，如果有则不会创建
        channel.queueDeclare("work_queues",true,false,false,null);
        /*
        basicPublish(String exchange, String routingKey, BasicProperties props, byte[] body)
        参数：
            1. exchange：交换机名称。简单模式下交换机会使用默认的 ""
            2. routingKey：路由名称
            3. props：配置信息
            4. body：发送消息数据

         */
        for (int i = 1; i <= 10; i++) {
            String body = i+"hello rabbitmq~~~";

            //6. 发送消息
            channel.basicPublish("","work_queues",null,body.getBytes());
        }



        //7.释放资源
      channel.close();
      connection.close();
```

消费者(有两个，都类似)

```java
    public static void main(String[] args) throws IOException, TimeoutException {

        //1.创建连接工厂
        ConnectionFactory factory = new ConnectionFactory();
        //2. 设置参数
        factory.setHost("172.16.98.133");//ip  默认值 localhost
        factory.setPort(5672); //端口  默认值 5672
        factory.setVirtualHost("/itcast");//虚拟机 默认值/
        factory.setUsername("heima");//用户名 默认 guest
        factory.setPassword("heima");//密码 默认值 guest
        //3. 创建连接 Connection
        Connection connection = factory.newConnection();
        //4. 创建Channel
        Channel channel = connection.createChannel();
        //5. 创建队列Queue
        /*
        queueDeclare(String queue, boolean durable, boolean exclusive, boolean autoDelete, Map<String, Object> arguments)
        参数：
            1. queue：队列名称
            2. durable:是否持久化，当mq重启之后，还在
            3. exclusive：
                * 是否独占。只能有一个消费者监听这队列
                * 当Connection关闭时，是否删除队列
                *
            4. autoDelete:是否自动删除。当没有Consumer时，自动删除掉
            5. arguments：参数。

         */
        //如果没有一个名字叫hello_world的队列，则会创建该队列，如果有则不会创建
        channel.queueDeclare("work_queues",true,false,false,null);

        /*
        basicConsume(String queue, boolean autoAck, Consumer callback)
        参数：
            1. queue：队列名称
            2. autoAck：是否自动确认
            3. callback：回调对象

         */
        // 接收消息
        Consumer consumer = new DefaultConsumer(channel){
            /*
                回调方法，当收到消息后，会自动执行该方法

                1. consumerTag：标识
                2. envelope：获取一些信息，交换机，路由key...
                3. properties:配置信息
                4. body：数据

             */
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
              /*  System.out.println("consumerTag："+consumerTag);
                System.out.println("Exchange："+envelope.getExchange());
                System.out.println("RoutingKey："+envelope.getRoutingKey());
                System.out.println("properties："+properties);*/
                System.out.println("body："+new String(body));
            }
        };
        channel.basicConsume("work_queues",true,consumer);


        //关闭资源？不要

    }
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/20.png)

## Pub/Sub订阅模式

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/21.png)

生产者

```java
    //三步同上
    //4. 创建Channel
        Channel channel = connection.createChannel();
       /*

       exchangeDeclare(String exchange, BuiltinExchangeType type, boolean durable, boolean autoDelete, boolean internal, Map<String, Object> arguments)
       参数：
        1. exchange:交换机名称
        2. type:交换机类型
            DIRECT("direct"),：定向
            FANOUT("fanout"),：扇形（广播），发送消息到每一个与之绑定队列。
            TOPIC("topic"),通配符的方式
            HEADERS("headers");参数匹配

        3. durable:是否持久化
        4. autoDelete:自动删除
        5. internal：内部使用。 一般false
        6. arguments：参数
        */

       String exchangeName = "test_fanout";
        //5. 创建交换机
        channel.exchangeDeclare(exchangeName, BuiltinExchangeType.FANOUT,true,false,false,null);
        //6. 创建队列
        String queue1Name = "test_fanout_queue1";
        String queue2Name = "test_fanout_queue2";
        channel.queueDeclare(queue1Name,true,false,false,null);
        channel.queueDeclare(queue2Name,true,false,false,null);
        //7. 绑定队列和交换机
        /*
        queueBind(String queue, String exchange, String routingKey)
        参数：
            1. queue：队列名称
            2. exchange：交换机名称
            3. routingKey：路由键，绑定规则
                如果交换机的类型为fanout ，routingKey设置为""
         */
        channel.queueBind(queue1Name,exchangeName,"");
        channel.queueBind(queue2Name,exchangeName,"");

        String body = "日志信息：张三调用了findAll方法...日志级别：info...";
        //8. 发送消息
        channel.basicPublish(exchangeName,"",null,body.getBytes());

        //9. 释放资源
        channel.close();
        connection.close();
```

消费者

```java
  //4. 创建Channel
        Channel channel = connection.createChannel();


        String queue1Name = "test_fanout_queue1";
        String queue2Name = "test_fanout_queue2";


        /*
        basicConsume(String queue, boolean autoAck, Consumer callback)
        参数：
            1. queue：队列名称
            2. autoAck：是否自动确认
            3. callback：回调对象

         */
        // 接收消息
        Consumer consumer = new DefaultConsumer(channel){
            /*
                回调方法，当收到消息后，会自动执行该方法

                1. consumerTag：标识
                2. envelope：获取一些信息，交换机，路由key...
                3. properties:配置信息
                4. body：数据

             */
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
              /*  System.out.println("consumerTag："+consumerTag);
                System.out.println("Exchange："+envelope.getExchange());
                System.out.println("RoutingKey："+envelope.getRoutingKey());
                System.out.println("properties："+properties);*/
                System.out.println("body："+new String(body));
                System.out.println("将日志信息打印到控制台.....");
            }
        };
        channel.basicConsume(queue1Name,true,consumer);


        //关闭资源？不要
```

> 有两个消费者，第二个basicConsume的队列名是queue2Name

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/22.png)

## Routing路由模式

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/23.png)

生产者

交换机类型为DIRECT

+ routingKey指定

```java
     String exchangeName = "test_direct";
        //5. 创建交换机
        channel.exchangeDeclare(exchangeName, BuiltinExchangeType.DIRECT,true,false,false,null);
        //6. 创建队列
        String queue1Name = "test_direct_queue1";
        String queue2Name = "test_direct_queue2";

        channel.queueDeclare(queue1Name,true,false,false,null);
        channel.queueDeclare(queue2Name,true,false,false,null);
        //7. 绑定队列和交换机
        /*
        queueBind(String queue, String exchange, String routingKey)
        参数：
            1. queue：队列名称
            2. exchange：交换机名称
            3. routingKey：路由键，绑定规则
                如果交换机的类型为fanout ，routingKey设置为""
         */
        //队列1绑定 error
        channel.queueBind(queue1Name,exchangeName,"error");
        //队列2绑定 info  error  warning
        channel.queueBind(queue2Name,exchangeName,"info");
        channel.queueBind(queue2Name,exchangeName,"error");
        channel.queueBind(queue2Name,exchangeName,"warning");

        String body = "日志信息：张三调用了delete方法...出错误了。。。日志级别：error...";
        //8. 发送消息
        channel.basicPublish(exchangeName,"warning",null,body.getBytes());

        //9. 释放资源
        channel.close();
        connection.close();
```

消费者(两个都类似，只不过绑定的队列不同)

```java
         */
        // 接收消息
        Consumer consumer = new DefaultConsumer(channel){
            /*
                回调方法，当收到消息后，会自动执行该方法

                1. consumerTag：标识
                2. envelope：获取一些信息，交换机，路由key...
                3. properties:配置信息
                4. body：数据

             */
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
              /*  System.out.println("consumerTag："+consumerTag);
                System.out.println("Exchange："+envelope.getExchange());
                System.out.println("RoutingKey："+envelope.getRoutingKey());
                System.out.println("properties："+properties);*/
                System.out.println("body："+new String(body));
                System.out.println("将日志信息打印到控制台.....");
            }
        };
        channel.basicConsume(queue2Name,true,consumer);


        //关闭资源？不要
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/24.png)

## 通配符模式

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/25.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/26.png)

生产者

+ 交换机类型为Topic

+ routingKey使用通配符

```java
  //5. 创建交换机
        channel.exchangeDeclare(exchangeName, BuiltinExchangeType.TOPIC,true,false,false,null);
        //6. 创建队列
        String queue1Name = "test_topic_queue1";
        String queue2Name = "test_topic_queue2";
        channel.queueDeclare(queue1Name,true,false,false,null);
        channel.queueDeclare(queue2Name,true,false,false,null);
        //7. 绑定队列和交换机

        // routing key  系统的名称.日志的级别。
        //=需求： 所有error级别的日志存入数据库，所有order系统的日志存入数据库
        channel.queueBind(queue1Name,exchangeName,"#.error");
        channel.queueBind(queue1Name,exchangeName,"order.*");
        channel.queueBind(queue2Name,exchangeName,"*.*");

        String body = "日志信息：张三调用了findAll方法...日志级别：info...";
        //8. 发送消息
        channel.basicPublish(exchangeName,"goods.error",null,body.getBytes());

        //9. 释放资源
        channel.close();
        connection.close();
```

消费者都类似

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/27.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/28.png)

# SpringBoot整合rabbitmq

引入依赖

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-amqp</artifactId>
        </dependency>
```

编写yml配置

```yml
# 配置RabbitMQ的基本信息  ip 端口 username  password..
spring:
  rabbitmq:
    host: 172.16.98.133 # ip
    port: 5672
    username: guest
    password: guest
    virtual-host: /
```

+ 生产者
  
  定义交换机，队列及绑定关系的配置类

```java
@Configuration
public class RabbitMQConfig {

    public static final String EXCHANGE_NAME = "boot_topic_exchange";
    public static final String QUEUE_NAME = "boot_queue";

    //1.交换机
    @Bean("bootExchange")
    public Exchange bootExchange(){
        return ExchangeBuilder.topicExchange(EXCHANGE_NAME).durable(true).build();
    }


    //2.Queue 队列
    @Bean("bootQueue")
    public Queue bootQueue(){
        return QueueBuilder.durable(QUEUE_NAME).build();
    }

    //3. 队列和交互机绑定关系 Binding
    /*
        1. 知道哪个队列
        2. 知道哪个交换机
        3. routing key
     */
    @Bean
    public Binding bindQueueExchange(@Qualifier("bootQueue") Queue queue, @Qualifier("bootExchange") Exchange exchange){
        return BindingBuilder.bind(queue).to(exchange).with("boot.#").noargs();
    }
```

注入RabbitTemplate，调用方法，完成消息发送

```java
    //1.注入RabbitTemplate
    @Autowired
    private RabbitTemplate rabbitTemplate;

    @Test
    public void testSend(){

        rabbitTemplate.convertAndSend(RabbitMQConfig.EXCHANGE_NAME,"boot.haha","boot mq hello~~~");
    }
```

无法注入RabbitTemplate，方法：使用@Resource，或者@Autowired(required = false)，还是不可以，手动注入，降低SpringBoot版本

```java
   @Bean
    public RabbitTemplate rabbitTemplate(ConnectionFactory connectionFactory){
        RabbitTemplate rabbitTemplate = new RabbitTemplate(connectionFactory);
        //adding perhaps some extra confoguration to template like message convertor. etc.
        return rabbitTemplate;
```

+ 消费者，定义监听类，使用@RabbitListener注解完成队列监听

```java
@Component
public class RabbimtMQListener {                

    @RabbitListener(queues = "boot_queue")//queues为队列名
    public void ListenerQueue(Message message){
        //System.out.println(message);
        System.out.println(new String(message.getBody()));
    }

}
```

# 高级特性

## 消息可靠传递（消息丢失处理）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/29.png)

### confirm模式

yml设置

```yml
spring:
  rabbitmq:
    publisher-confirms: true
```

在rabbitTemplate定义ConfirmCallBack回调函数

```java
 //2. 定义回调
        rabbitTemplate.setConfirmCallback(new RabbitTemplate.ConfirmCallback() {
            /**
             *
             * @param correlationData 相关配置信息
             * @param ack   exchange交换机 是否成功收到了消息。true 成功，false代表失败
             * @param cause 失败原因
             */
            @Override
            public void confirm(CorrelationData correlationData, boolean ack, String cause) {
                System.out.println("confirm方法被执行了....");

                if (ack) {
                    //接收成功
                    System.out.println("接收成功消息" + cause);
                } else {
                    //接收失败
                    System.out.println("接收失败消息" + cause);
                    //做一些处理，让消息再次发送。
                }
            }
        });

        //3. 发送消息
        rabbitTemplate.convertAndSend("test_exchange_confirm111", "confirm", "message confirm....");
```

### Return模式

回退模式:当消息发送给Exchange后，Exchange路由到Queue失败是 才会执行 ReturnCallBack

添加配置

```properties
spring.rabbitmq.publisher-returns=true
spring.rabbitmq.template.mandatory=true
```

设置ReturnCallBack

```java
        //2.设置ReturnCallBack
        rabbitTemplate.setReturnCallback(new RabbitTemplate.ReturnCallback() {
            /**
             *
             * @param message   消息对象
             * @param replyCode 错误码
             * @param replyText 错误信息
             * @param exchange  交换机
             * @param routingKey 路由键
             */
            @Override
            public void returnedMessage(Message message, int replyCode, String replyText, String exchange, String routingKey) {
                System.out.println("return 执行了....");

                System.out.println(message);
                System.out.println(replyCode);
                System.out.println(replyText);
                System.out.println(exchange);
                System.out.println(routingKey);

                //处理
            }
        });


        //3. 发送消息
        rabbitTemplate.convertAndSend("test_exchange_confirm", "confirm", "message confirm....");
```

设置Exchange处理消息的模式：

+ 如果消息没有路由到Queue，则丢弃消息（默认）  
* 如果消息没有路由到Queue，返回给消息发送方ReturnCallBack
  
  * 设置
    
    ```properties
    spring.rabbitmq.template.mandatory=true
    ```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/30.png)

### [RabbitMQ 弄丢了数据](https://doocs.github.io/advanced-java/#/docs/high-concurrency/how-to-ensure-the-reliable-transmission-of-messages?id=rabbitmq-%e5%bc%84%e4%b8%a2%e4%ba%86%e6%95%b0%e6%8d%ae)

就是 RabbitMQ 自己弄丢了数据，这个你必须**开启 RabbitMQ 的持久化**，就是消息写入之后会持久化到磁盘，哪怕是 RabbitMQ 自己挂了，**恢复之后会自动读取之前存储的数据**，一般数据不会丢。除非极其罕见的是，RabbitMQ 还没持久化，自己就挂了，**可能导致少量数据丢失**，但是这个概率较小。

设置持久化有**两个步骤**：

- 创建 queue 的时候将其设置为持久化。这样就可以保证 RabbitMQ 持久化 queue 的元数据，但是它是不会持久化 queue 里的数据的。

- 第二个是发送消息的时候将消息的 `deliveryMode` 设置为 2。就是将消息设置为持久化的，此时 RabbitMQ 就会将消息持久化到磁盘上去。

必须要同时设置这两个持久化才行，RabbitMQ 哪怕是挂了，再次重启，也会从磁盘上重启恢复 queue，恢复这个 queue 里的数据。

注意，哪怕是你给 RabbitMQ 开启了持久化机制，也有一种可能，就是这个消息写到了 RabbitMQ 中，但是还没来得及持久化到磁盘上，结果不巧，此时 RabbitMQ 挂了，就会导致内存里的一点点数据丢失。

所以，持久化可以跟生产者那边的 `confirm` 机制配合起来，只有消息被持久化到磁盘之后，才会通知生产者 `ack` 了，所以哪怕是在持久化到磁盘之前，RabbitMQ 挂了，数据丢了，生产者收不到 `ack` ，你也是可以自己重发的。

### Consumer  Ack

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/31.png)

> 原因：消费者打开了 autoAck机制（消费到一条消息，还在处理中，还没处理完，此时消费者自动 autoAck了，通知 rabbitmq说这条消息已经消费了，此时不巧，消费者系统宕机了，那条消息丢失了，还没处理完，而且 rabbitmq还以为这个消息已经处理掉了）
> 
> 解决方案：关闭 autoAck,自己处理完了一条消息后，再发送 ack给 rabbitmq,如果此时还没处理完就宕机了，此时rabbitmq没收到你发的ack消息，然后 rabbitmq 就会将这条消息重新分配给其他的消费者去处理。

* 1. 设置手动签收。acknowledge="manual"  
* 2. 让监听器类实现ChannelAwareMessageListener接口  
* 3. 如果消息成功处理，则调用channel的 basicAck()签收  
* 4. 如果消息处理失败，则调用channel的basicNack()拒绝签收，broker重新发送给consumer

> 注意：在yaml文件配置manual后，
> 
> @RabbitListener(queues = RabbitMQConfig.QUEUE_NAME,ackMode = "MANUAL")
> 
> `@RabbitListener`注解会自动ACK，如果方法中再手动ACK会造成重复ACK

```yml
spring:
  rabbitmq:
    listener:
      direct:
        acknowledge-mode: manual
```

```java
@Component
public class AckListener implements ChannelAwareMessageListener {

    @Override
    public void onMessage(Message message, Channel channel) throws Exception {
        long deliveryTag = message.getMessageProperties().getDeliveryTag();

        try {
            //1.接收转换消息
            System.out.println(new String(message.getBody()));

            //2. 处理业务逻辑
            System.out.println("处理业务逻辑...");
            int i = 3/0;//出现错误
            //3. 手动签收，移除消息
            channel.basicAck(deliveryTag,true);
        } catch (Exception e) {
            //e.printStackTrace();

            //4.拒绝签收
            /*
            第三个参数：requeue：重回队列。如果设置为true，则消息重新回到queue，broker会重新发送该消息给消费端
             */
            channel.basicNack(deliveryTag,true,true);
            //channel.basicReject(deliveryTag,true);
        }
    }
}
```

> long deliveryTag：唯一标识 ID，当一个消费者向 RabbitMQ 注册后，会建立起一个 Channel ，RabbitMQ 会用 basic.deliver 方法向消费者推送消息，这个方法携带了一个 delivery tag， 它代表了 RabbitMQ 向该 Channel 投递的这条消息的唯一标识 ID，是一个单调递增的正整数，delivery tag 的范围仅限于 Channel。
> 
> boolean multiple：是否批处理，当该参数为 true 时，则可以一次性确认 delivery_tag 小于等于传入值的所有消息
> 
> boolean requeue：如果 requeue 参数设置为 true，则 RabbitMQ 会重新将这条消息存入队列，以便发送给下一个订阅的消费者； 如果 requeue 参数设置为 false，则 RabbitMQ 立即会还把消息从队列中移除，而不会把它发送给新的消费者。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/32.png)

> 发送消息时可以将对象序列化为json，然后再接收时再反序列化

## 消费端限流

设置消费端一次拉取多少消息

```yml
spring:
    listener:
      direct:
        consumers-per-queue: 1000#消费端每次从mq拉去一条消息来消费，直到手动确认消费完毕后，才会继续拉去下一条消息
```

确保ack机制为手动确认

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/33.png)

## TTL

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/34.png)

1. 队列统一过期
   
   在配置类中利用withArgument方法
   
   ```java
   public Queue getTtlQueue(){
           // 设置 ttl 队列，并设定 x-message-ttl 参数，表示 消息存活最大时间，单位  ms
           return QueueBuilder.durable(ttl_queue_name).withArgument("x-message-ttl",10000).build();
   ```

2. 消息单独过期
   
   ```java
   // 消息后处理对象，设置一些消息的参数信息
           MessagePostProcessor messagePostProcessor = new MessagePostProcessor() {
   
               @Override
               public Message postProcessMessage(Message message) throws AmqpException {
                   //1.设置message的信息
                   message.getMessageProperties().setExpiration("5000");//消息的过期时间
                   //2.返回该消息
                   return message;
               }
           }; 
           //消息单独过期
           rabbitTemplate.convertAndSend("test_exchange_ttl", "ttl.hehe", "message ttl....",messagePostProcessor);
   ```
   
   > 如果设置了消息的过期时间，也设置了队列的过期时间，它以时间短的为准。  
   > 
   > * 队列过期后，会将队列所有消息全部移除。  
   > * 消息过期后，只有消息在队列顶端，才会判断其是否过期(移除掉)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/35.png)

## 死信队列

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/36.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/37.png)

“死信”消息会被RabbitMQ进行特殊处理，如果配置了死信队列信息，那么该消息将会被丢进死信队列中，如果没有配置，则该消息将会被丢弃。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/38.png)

> 两个routingkey应该是一样的

1. 声明正常的队列(test_queue_dlx)和交换机(test_exchange_dlx)  

2. 声明死信队列(queue_dlx)和死信交换机(exchange_dlx)  

3. <mark>正常队列绑定死信交换机</mark>  
    设置两个参数：  
   
   + x-dead-letter-exchange：死信交换机名称  
   
   + x-dead-letter-routing-key：发送给死信交换机的routingkey

```java
@Configuration
public class RabbitMQConfig {

    public static final String BUSINESS_EXCHANGE_NAME = "dead.letter.demo.simple.business.exchange";
    public static final String BUSINESS_QUEUEA_NAME = "dead.letter.demo.simple.business.queuea";
    public static final String BUSINESS_QUEUEB_NAME = "dead.letter.demo.simple.business.queueb";
    public static final String DEAD_LETTER_EXCHANGE = "dead.letter.demo.simple.deadletter.exchange";
    public static final String DEAD_LETTER_QUEUEA_ROUTING_KEY = "dead.letter.demo.simple.deadletter.queuea.routingkey";
    public static final String DEAD_LETTER_QUEUEB_ROUTING_KEY = "dead.letter.demo.simple.deadletter.queueb.routingkey";
    public static final String DEAD_LETTER_QUEUEA_NAME = "dead.letter.demo.simple.deadletter.queuea";
    public static final String DEAD_LETTER_QUEUEB_NAME = "dead.letter.demo.simple.deadletter.queueb";

    // 声明业务Exchange
    @Bean("businessExchange")
    public FanoutExchange businessExchange(){
        return new FanoutExchange(BUSINESS_EXCHANGE_NAME);
    }

    // 声明死信Exchange
    @Bean("deadLetterExchange")
    public DirectExchange deadLetterExchange(){
        return new DirectExchange(DEAD_LETTER_EXCHANGE);
    }

    // 声明业务队列A
    @Bean("businessQueueA")
    public Queue businessQueueA(){
        Map<String, Object> args = new HashMap<>(2);
//       x-dead-letter-exchange    这里声明当前队列绑定的死信交换机
        args.put("x-dead-letter-exchange", DEAD_LETTER_EXCHANGE);
//       x-dead-letter-routing-key  这里声明当前队列的死信路由key
        args.put("x-dead-letter-routing-key", DEAD_LETTER_QUEUEA_ROUTING_KEY);
        return QueueBuilder.durable(BUSINESS_QUEUEA_NAME).withArguments(args).build();
    }

    // 声明业务队列B
    @Bean("businessQueueB")
    public Queue businessQueueB(){
        Map<String, Object> args = new HashMap<>(2);
//       x-dead-letter-exchange    这里声明当前队列绑定的死信交换机
        args.put("x-dead-letter-exchange", DEAD_LETTER_EXCHANGE);
//       x-dead-letter-routing-key  这里声明当前队列的死信路由key
        args.put("x-dead-letter-routing-key", DEAD_LETTER_QUEUEB_ROUTING_KEY);
        return QueueBuilder.durable(BUSINESS_QUEUEB_NAME).withArguments(args).build();
    }

    // 声明死信队列A
    @Bean("deadLetterQueueA")
    public Queue deadLetterQueueA(){
        return new Queue(DEAD_LETTER_QUEUEA_NAME);
    }

    // 声明死信队列B
    @Bean("deadLetterQueueB")
    public Queue deadLetterQueueB(){
        return new Queue(DEAD_LETTER_QUEUEB_NAME);
    }

    // 声明业务队列A绑定关系
    @Bean
    public Binding businessBindingA(@Qualifier("businessQueueA") Queue queue,
                                    @Qualifier("businessExchange") FanoutExchange exchange){
        return BindingBuilder.bind(queue).to(exchange);
    }

    // 声明业务队列B绑定关系
    @Bean
    public Binding businessBindingB(@Qualifier("businessQueueB") Queue queue,
                                    @Qualifier("businessExchange") FanoutExchange exchange){
        return BindingBuilder.bind(queue).to(exchange);
    }

    // 声明死信队列A绑定关系
    @Bean
    public Binding deadLetterBindingA(@Qualifier("deadLetterQueueA") Queue queue,
                                    @Qualifier("deadLetterExchange") DirectExchange exchange){
        return BindingBuilder.bind(queue).to(exchange).with(DEAD_LETTER_QUEUEA_ROUTING_KEY);
    }

    // 声明死信队列B绑定关系
    @Bean
    public Binding deadLetterBindingB(@Qualifier("deadLetterQueueB") Queue queue,
                                      @Qualifier("deadLetterExchange") DirectExchange exchange){
        return BindingBuilder.bind(queue).to(exchange).with(DEAD_LETTER_QUEUEB_ROUTING_KEY);
    }
}
————————————————
版权声明：本文为CSDN博主「半桶水的码农」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_44688301/article/details/116237294
```

```yml
spring:
  rabbitmq:
    host: localhost
    password: guest
    username: guest
    listener:
      type: simple
      simple:
          default-requeue-rejected: false#设置为false
          acknowledge-mode: manual
```

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/39.png)

## 延迟队列

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/40.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/41.png)

> 在设置ttl的队列中加入设置死信队列的参数

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/42.png)

## 日志监控

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/43.png)

## 消息追踪（了解）

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/44.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/45.png)

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/46.png)

## 消息可靠性保障

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/47.png)

## 消息重复消费

首先，比如 RabbitMQ、RocketMQ、Kafka，都有可能会出现消息重复消费的问题，正常。因为这问题通常不是 MQ 自己保证的，是由我们开发来保证的。

消息的一条消息被重复消费情况：在保证MQ消息不重复的情况下，消费者消费消息成功后，在给MQ发送消息确认的时候出现了网络异常(或者是服务中断)，MQ没有接收到确认，此时MQ不会将发送的消息删除，  
为了保证消息被消费，当消费者网络稳定后，MQ就会继续给消费者投递之前的消息。这时候消费者就接收到了两条一样的消息。

所以消息重复也就出现在**两个阶段**，**1**、生产者多发送了消息给MQ；**2**、MQ的一条消息被消费者消费了多次。

第一种场景很好控制，只要保证消息生成者不重复发送消息给MQ即可

如何解决消息重复消费的问题：
为了保证消息不被重复消费，首先要保证每个消息是唯一的，所以可以给每一个消息携带一个全局唯一的id，类似订单 id 之类的东西，流程如下：

1、消费者监听到消息后获取id，先去查询这个id是否存在redis中

2、如果不存在，则正常消费消息，并把消息的id存入 数据库或者redis中

3、如果存在则丢弃此消息

原文链接：https://blog.csdn.net/chenping1993/article/details/114580954

唯一约束：

- 业务判断法：通常数据消费后都需要插入到数据库中，使用数据库的唯一性约束防止重复消费。每次消费直接尝试插入数据，如果提示唯一性字段重复，则直接丢失消息。一般都是通过这个业务判断的方法就可以简单高效地避免消息的重复处理了。

## 消息的顺序性

队列是先进先出的

RabbitMQ 的问题是由于不同的消息都发送到了同一个 queue 中，多个消费者都消费同一个 queue 的消息。

> [消息队列（五）如何保证消息的顺序性？_Java_奈何花开_InfoQ写作社区](https://xie.infoq.cn/article/c84491a814f99c7b9965732b1)
> 
> [如何保证消息的顺序性？ (doocs.github.io)](https://doocs.github.io/advanced-java/#/docs/high-concurrency/how-to-ensure-the-order-of-messages)

拆分多个 queue，每个 queue 一个 consumer，就是多一些 queue 而已，确实是麻烦点，这样也会造成吞吐量下降，可以在消费者内部采用多线程的方式取消费。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/48.png)

就一个 queue 但是对应一个 consumer，然后这个 consumer 内部用内存队列做排队，然后分发给底层不同的 worker 来处理。

这里消费者不直接消费消息，而是将消息根据关键值（比如：订单 id）进行哈希，哈希值相同的消息保存到相同的内存队列里。也就是说，需要保证顺序的消息存到了相同的内存队列，然后由一个唯一的 worker 去处理。

![](https://markdown-m.oss-cn-hangzhou.aliyuncs.com/rabbitmq/49.png)
