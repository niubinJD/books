# 注解

* 什么是Spring Boot?

* spring常用注解？
    @Component， @Service， @Repository， @Controller， @Autowired， @Inject， @Resource， @Configuration， @Bean, @ComponentScan,
    @Aspect, @After, @PointCut, @Value, @PropertySource, @EnableAsync, @Async, @EnableScheduling, @Scheduled, @EnableTransactionManagement,
    @Transactional

* spring 中单例的beans是线程安全的吗？
    不是，spring没有对beans做多线程的特殊处理，又因为大多数情况下beans是无状态的，所以可以认为他是线程安全的，如果beans是有状态的，则需要你为它添加额外的多线程处理

* 什么是事务控制？spring是如何实现事务控制的？
    事务控制就是将一系列操作当成一个不可拆分的逻辑单元，保证这些操作要么都成功，要么都失败。在关系数据库中，一个事务可以是一条SQL语句，一组SQL语句或整个程序
    spring并不直接支持事务，只有当数据库支持事务时，他才支持，只不过简化了开发过程。spring提供两种事务的实现：声明式和编程式。
        1. 声明式使用注解开启事务@EnableTransactionManagement和应用事务@Transactional（使用这个直接时，在调用所注解的方法时会自动开启事务，提交事务或者回滚）
        2. 编程式需要在事务执行的地方加入transactionTemplate.execute(new TransactionCallbackWithoutResult() {}）代码，并将事务过程卸载TransactionCallbackWithoutResult的相应实现中

* @Autowired和@Resource的区别?

* spring boot如何实现自动配置？

* spring boot中bean的生命周期？
  
* AOP都有哪些要素？

* 什么时AOP?
  
* 什么时IOC容器？

* Spring boot核心注解是什么?有哪些组成？
    启动类上面的注解是@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下 3 个注解：

    @SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。

    @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })。

    @ComponentScan：Spring组件扫描。

* Spring boot需要独立容器运行吗？可以不需要。内置了tomcat/jetty容器

* Spring boot启动方式？ 1. main方法 2. jar包 