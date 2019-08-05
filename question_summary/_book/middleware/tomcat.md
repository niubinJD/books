# tomcat

* tomcat目录结构：
    /bin : 存放tomcat命令
    /conf : 存放配置文件
    /lib : 存放tomcat的依赖jar包
    /logs : 存放tomcat运行过程中产生的依赖文件
    /temp ： 存放临时文件
    /work : 存放运行时编译后的文件，如jsp编译后的文件
    /webapps : 发布web应用, 在默认情况下将Web应用的文件存放在此目录中

* tomcat配置
    server.xml:
        1. 修改http服务端口：server.service.Connector(协议为http) .port属性
        2. 修改Tomcat 监听的关闭端口：server.port属性
        3. 接受其他服务器转发过来的请求端口：server.service.Connector(协议为ajp) .port属性
        4. 修改编码：server.service.Connector(协议为http).URIEncoding
    tomcat-users.xml: 配置权限相关信息

* tomcat优化：
    1. 优化线程数：在server.xml中相关的Connector标签上调整属性acceptCount（处于请求队列的数量），maxThreads（最大线程数），minSpareThreads（最小空闲线程数），maxSpareThreads（最大空闲线程数）的值
    2. 使用线程池:  先定义线程池<Executor name="tomcatThreadPool" namePrefix="req-exec-"maxThreads="1000" minSpareThreads="50"maxIdleTime="60000"/>
        然后在Connector上使用：<Connector port="8080" protocol="HTTP/1.1"executor="tomcatThreadPool"/>
    3. 使用NIO或APR模式（Connector的三种运行模式BIO, NIO, APR）: 默认使用BIO(一个请求一个线程)， 使用<Connector port="8080"protocol="org.apache.coyote.http11.Http11NioProtocol" connectionTimeout="20000"redirectPort="8443"/>
        切换到NIO，它使用java的异步IO处理，可以使用少量线程处理大量请求。apr是从系统层面解决io问题，需要安装额外的包
    4. 修改tomcat启动参数，优化jvm