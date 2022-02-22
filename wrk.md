## wrk介绍
  wrk是一款简单的HTTP压测工具,托管在Github上,https://github.com/wg/wrk, 基于系统自带的高性能 I/O 机制，如 epoll, kqueue, 利用异步的事件驱动框架，通过很少的线程就可以压出很大的并发量
 
## wrk安装
```
git clone https://github.com/wg/wrk.git  
cd wrk  
make  
```
## wrk压测命令
```
# 12线程  100连接 压测30s  输出分布情况
wrk -t12 -c100 -d30s --latency http://www.baidu.com

(base) wangjifeideMacBook-Pro:wrk wangjifei$ wrk -t12 -c100 -d30s --latency http://www.baidu.com
Running 30s test @ http://www.baidu.com
  12 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   204.30ms  287.90ms   1.97s    88.61%
    Req/Sec    71.43     67.59   810.00     89.77%
  Latency Distribution
     50%   14.76ms
     75%  296.79ms
     90%  545.03ms
     99%    1.40s 
  23676 requests in 30.03s, 346.84MB read
  Socket errors: connect 0, read 42, write 0, timeout 46
Requests/sec:    788.29
Transfer/sec:     11.55MB

```
