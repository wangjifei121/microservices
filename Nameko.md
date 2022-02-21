 ## nameko官方demo
 - pip安装 `pip install nameko`
 - docker启动rabbitmq `docker run -d -p 5672:5672 rabbitmq:latest`
 - 编写python nameko service
  
  ```
  from nameko.rpc import rpc
  
  class GreetingService:
      name = "greeting_service"
      @rpc
      def hello(self, name):
          return "Hello, {}!".format(name)
   ```
 - 指定rabbitmq 启动nameko service `nameko run helloworld --broker amqp://10.0.3.19:5672`
 
 ```
(base) wangjifeideMacBook-Pro:Nameko wangjifei$ 
(base) wangjifeideMacBook-Pro:Nameko wangjifei$ nameko run helloworld --broker amqp://10.0.3.19:5672
starting services: greeting_service
Connected to amqp://guest:**@10.0.3.19:5672//
 ```
