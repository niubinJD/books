# mybatis

半orm框架，封装了jdbc，开发时只需要关注sql本身
可以使用xml或注解来配置映射原生信息


优点：
    1. 基于sql语句的编程
    2. 消除jdbc代码冗余
    3. 与数据库的良好兼容
    4. 与spring的集成
    5. 数据映射

缺点：
    1. sql工作量大
    2. 可移植性差



面试点：
    1. #{}与${}的区别？
        会在处理#{}将sql中的#{}替换成？，然后调用PreparedStatement的set方法来赋值
        会在处理${}将其替换成变量的值
        使用#{}可以有效防止sql注入
    2. 当实体类中的属性名和表中的字段名不一样 ，怎么办 ？ 、
        在sql中定义别名
        在映射文件中使用<resultMap>标签来定义关系映射

Mapper接口：


Mapper.xml配置文件：
    1. mapper namespace="com.example.springboot_mybatis.mapper.UserMapper"


* mybatis中动态sql是怎么设定的？用什么语法？
    MyBatis里面的动态Sql一般是通过if节点来实现,通过OGNL语法来判断,但是如果要写的完整,必须配合where,trim节点.
    choose标签: choose when otherwise, 一个choose中至少有一个when,0或1个otherwise,如果when满足就执行when,不满足就执行otherwise  
    where标签: 判断包含节点有内容就插入where，如果where后的字符串是以and或or开头，则删除and或or
    set标签：一般是更新时使用

* mybatis一级缓存和二级缓存？