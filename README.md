# 微服务框架原理
## 微服务架构的实现方式
  微服务架构最重要的就是使用什么方式进行服务间通信（也称作服务调用），按照通信方式的不同，主要可以分为同步通信和异步通信两种方式
- 同步通信

  同步调用比较简单，一致性强，但是容易出调用问题，性能体验上也会差些。同步通信最常用的两种协议是RESTful和RPC，而目前使用最广泛，最有名的两种微服务框架Spring Cloud和Dubbo分别使用了RESTful和RPC协议。RESTful和RPC两种协议各有优势，具体使用要看业务场景。
  
  Dubbo框架是一个非常流行的采用同步通信的分布式微服务框架，下图就是Dubbo框架的工作原理图
  ![20191101225938900 jpg](https://user-images.githubusercontent.com/40445471/155142648-aae55297-c91d-4690-8fe7-dc212fdf777c.png)
  首先一个微服务应用程序需要有服务的生产者和服务的消费者，另外还需要一个注册中心（常见的有zookeeper和rabbitmq等）来管理和调度服务。微服务架构的程序运行的一般步骤为：
    - 服务提供方，即生产者启动服务，并将服务提交到注册中心注册服务
    - 服务需求方，即消费者连接到注册中心，向注册中心发出请求，申请需要的服务
    - 注册中心根据消费者发出的请求来调度服务，将对应的服务提供者（生产者）的信息发送给消费者
    - 消费者和生产者之间建立连接，消费者调用服务
    - 记录服务调用过程中的信息
- 异步通信
 
 异步通信一般通过消息中间件来进行服务间通信，消息中间件能为调用之间提供的缓冲，确保消息积压不会冲垮被调用方，同时能保证调用方的服务体验，继续干自己该干的活，不至于被后台性能拖慢。不过需要付出的代价是一致性的减弱。
 
 nameko框架就是一个采用异步通信方式的微服务框架，采用RabbitMQ消息队列作为消息中间件，原理非常简单，使用起来也很方便。
 ![image](https://user-images.githubusercontent.com/40445471/155143131-323a1309-5de2-4f8a-b51b-dc8831a38e5d.png)
