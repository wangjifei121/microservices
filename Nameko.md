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
- 命令行客户端
```
(base) wangjifeideMacBook-Pro:microservices wangjifei$ nameko shell  --broker amqp://10.0.3.19:5672
Nameko Python 3.6.7 (v3.6.7:6ec5cf24b7, Oct 20 2018, 03:02:14) 
[GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.57)] shell on darwin
Broker: amqp://10.0.3.19:5672
>>> n.rpc.greeting_service.hello(name="hello")
'Hello, hello!'
>>> 
```
- 客户端调用代码

```
from nameko.standalone.rpc import ClusterRpcProxy

CONFIG = {'AMQP_URI': "amqp://guest:guest@10.0.3.19"}


def compute():
    with ClusterRpcProxy(CONFIG) as rpc:
        result = rpc.greeting_service.hello('wangjifei')

    return result

if __name__ == '__main__':
    result = compute()
    print(result)
    
## 执行
(base) wangjifeideMacBook-Pro:Nameko wangjifei$ python3 producter.py 
Hello, wangjifei!
(base) wangjifeideMacBook-Pro:Nameko wangjifei$ 
```
