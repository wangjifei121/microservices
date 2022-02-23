## 简单模式
生产者，一个队列一个或多个消费者，当多个消费者同时监听一个队列时，他们并不能同时消费一条消息，而是随机消费消息，即一个队列中一条消息，只能被一个消费者消费。
![image](https://user-images.githubusercontent.com/40445471/155252495-7653f435-447d-4965-a098-ba70d42c09b0.png)

## 订阅与发布模式(fanout)
生产者，一个交换机(fanoutExchange)，没有路由规则，多个队列，多个消费者。生产者将消息不是直接发送到队列，而是发送到X交换机，然后由交换机发送给两个队列，两个消费者各自监听一个队列，来消费消息。
![image](https://user-images.githubusercontent.com/40445471/155252535-950a2862-1098-4fc8-9724-8cadfafbe6ba.png)

## 路由模式(direct)
生产者，一个交换机(directExchange)，路由规则，多个队列，多个消费者。主要根据定义的路由规则决定消息往哪个队列发送。
![image](https://user-images.githubusercontent.com/40445471/155252578-87295af9-9220-4910-a20a-79c03d28cbf9.png)

## 主题模式(topic)
生产者，一个交换机(topicExchange)，模糊匹配路由规则，多个队列，多个消费者。
![image](https://user-images.githubusercontent.com/40445471/155252611-22504902-693a-43a0-a6dd-484d3868f2ad.png)

## RPC模式
对于RPC请求，客户端发送一条带有两个属性的消息：replyTo,设置为仅为请求创建的匿名独占队列，和correlationId,设置为每个请求的唯一id值。

请求被发送到rpc_queue队列。
RPC工作进程(即：服务器)在队列上等待请求。当一个请求出现时，它执行任务，并使用replyTo字段中的队列将结果发回客户机。
客户机在回应消息队列上等待数据。当消息出现时，它检查correlationId属性。如果匹配请求中的值，则向程序返回该响应数据。
![image](https://user-images.githubusercontent.com/40445471/155252726-73a140d6-0333-4ee6-8992-63278df02e6d.png)

## 总结
订阅模式，路由模式，主题模式，他们的相同点就是都使用了交换机，只不过在发送消息给队列时，添加了不同的路由规则。

订阅模式没有路由规则，路由模式为完全匹配规则，主题模式为模糊匹配（正则表达式，完全匹配规则）。

在交换机模式下：队列和路由规则有很大关系，生产者只用关心交换机与路由规则即可，无需关心队列。

消费者不管在什么模式下：永远不用关心交换机和路由规则，消费者永远只关心队列，消费者直接和队列交互。
