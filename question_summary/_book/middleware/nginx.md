# nginx

* nginx用途？
    http静态服务器和反向代理服务器。

* 修改nginx监听端口？ nginx.config中server里面的listen 字段
  
* 负载均衡配置？ 定义upstream，且在upstream中可定义每个服务的权重（权重越大，访问的几率越高）

* 反向代理配置？ proxy_pass