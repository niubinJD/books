# Java基础问题

* HashSet如何保证不重复？
  
    HashSet底层使用HashMap中的key位置来存储Set中的值，HasHMap中key是不重复的，所以可以保证HashSet中的值是不重复的

* 衍生问题： HashMap如何保证key不重复？
   
    HashMap中维护了一个hashtable, 每次添加元素都会先判断是不是已经存在与hashtable中，使用hasCode()方法比较，然后使用equals()比较，如果相同的话。就认为key存在
    
* 亿条数据获得top10方法（java topN问题）?
   
    使用小堆排序

* 小数计算（java）？
   
    BigDecimal。使用BigDecimal(String)构造器，而不是用 BigDecimal(double)来构造（也不能将float或double型转换成String再来使用BigDecimal(String)来构造，因为在将float或double转换成String时精度已丢失）

* 方法签名包含返回值？
   
    方法签名 = 方法名 + 参数列表。当两个方法的方法签名一致，但返回值不同时，编译报错，应为同一类中方法签名一致的方法是同一方法，不能多次定义

* int与integer的区别？默认值是什么？
   
    1. integer为int的封装类， int是基本数据类型
    
    2. integer必须实例化才能使用
    
    3. integer实际上是对象的引用，而int是直接存储数据类型
    
    4. integer默认值是null, int默认值是0

*  ThreadLocal是什么？有什么用？
    
    Theadlocal是线程本地变量，他为每个使用该变量的线程提供独立的变量副本，而不会影响其他线程中的变量副本

*  什么是泛型？举个例子？
    
    泛型的本质是参数化类型。也就是说所操作的数据类型被指定为一个参数。这种参数类型可以用在类、接口和方法的创建中，分别称为泛型类、泛型接口、泛型方法。
    
    泛型类定义：public class Example<T>{}

*  java gc机制（作用 + 发生的时间 + 对谁 + 做了什么事情 + 种类及各自特点）?
    
    1. 作用：回收堆区（主要）中的垃圾对象（应用不到的对象）
    
    2. 发生的时间： 在手动调用System.gc()方法时； 当jvm无法为一个新对象分配内存（eden 区满了）时触发 minor gc； 老年代空间不足时，触发fullgc

*  内存结构及其存储的数据？
    
    内存结构： 
    
    1. 方法区（存储class文件信息。 包含类的名称、类的类型（枚举、类、接口）、字段、方法等等）
    
    2. 堆区（new的对象实例、 this指针，或者数组都放在堆中， gc主要作用区域），
    
    3. 栈区（线程独占， 保存当前线程状态， 具有先进后出的特性），
    
    4. pc寄存器（线程独占， 存放指令），
    
    5. 本地方法栈（其他语言本地方法的执行区域）

*  java父类和子类中的静态代码块，非静态代码块，构造函数执行顺序？
    
    父类静态代码块 -> 子类静态代码块 -> 父类非静态代码块 -> 父类构造器（如果子类实例化时，没有手动调用有参的，则默认使用无参， 如果父类总没有定义无参构造器，则会报错） -> 子类非静态代码块 
    
    -> 子类构造器

*  a = a + b 与 a += b有什么区别？ a+=b在计算过程中可能会有一个隐式的类型转换

*  线程状态？如何进入阻塞状态？线程什么时候结束？
    
    五大线程状态： 新建（new之后）， 就绪（调用start方法后）， 运行， 休眠（阻塞）， 终止。
    
    进入休眠状态的方法: 1. 主动调用sleep方法 2. 当前线程试图获取一个锁时，而该锁正在被其他线程使用 3. 线程正在等待某个触发条件 4. 线程调用一个在io上被阻塞的操作
    
    线程结束： 1. run执行完成后自动结束 2. 出现一个未捕获的异常时终止
    
    如何进入就绪状态： 调用start方法后进入就绪状态

*  sleep与wait的区别？
    
    1. sleep方法属于Thread类，wait属于object类
    
    2. sleep方法调用后，会导致线程暂停执行等待的时间，让出cpu给其他线程，但他的不会释放对象锁，监控状态还在保持，当seelp时间到后，会恢复运行状态；当调用wait()方法时，线程会释放掉对象锁
    
    进入阻塞状态，只有针对此对象调用notify()或notifyAll()方法后，等待此对象锁的线程进入就绪状态

*  noify()与notifyAll()的区别？notify通知的线程是哪一个？
    
    他们都是指当前线程放弃它所占用的对象锁，同时通知其他等待线程来争夺对象锁，但notify()只通知一个，notifyAll()则会通知所有需要该对象锁的线程（会造成资源的浪费）。

    notify()方法唤醒线程时，会随机通知等待队列中的一个线程。

*  什么时常量池？在哪？如何操作？
    
    常量池是对jvm创建字符串对象的一种优化，它维护了一个字符串池。当通过String a = "a"创建一个字符串时，他会去常量池中寻找，如果有直接返回，没有则在常量池中新增一个，然后返回，
    
    使用new 创建一个字符串时，他会先去常量池中寻找，如果有， 则直接在堆中创建一个拷贝，没有则在常量池中新增一个，然后在堆中创建一个拷。
    
    字符串常量池位于方法区，可以使用String的成员方法intern将堆区的字符串指向常量池中的字符串

* 变量存储位置？
    
    字符串常量池位于方法区
    
    局部变量的数据存储与栈中，随着方法的消失而销毁
    
    成员变量存储在堆中的对象里，由gc负责回收

* String为什么是不可变的？
    
    string内部采用char数组存储数据，而char数组使用的是private final修饰符，那么此时我们只能在String类中用char[0] = '0'来修改char数据的值，
    
    但String类也是final的，使其无法通过继承来改变,

* String使用+拼接时为什么效率低下？
    
    String在使用+拼接时低效率主要发生在循环，大批量数据引起。在循环时拼接时，会先将string转换为StringBuilder然后在拼接，
    
    之后再toString()转换为string对象，一直循环，会创建大量的StringBuilder对象，导致堆空间浪费

* final关键字？
    
    1. 修饰类时，类无法被继承
    
    2. 修饰方法时，方法无法被重写
    
    3. 修饰变量，该变量只能被赋一次只，且无法修改，对于成员变量来说，我们可以在申明时或构造函数中对其赋值


* 线程池有哪些?
    
    Java通过Executors提供四种线程池: 
    
    1. newCachedThreadPool(创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程)
    
    2. newFixedThreadPool(创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待)
    
    3. newScheduledThreadPool(创建一个定长线程池，支持定时和周期性任务执行)
    
    4. newSingleThreadExecutor(创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序（FIFO，LIFO，优先级）执行。)

* lock与synchronized的区别？
  
  synchronized是java关键字可用在方法和代码块上，通过jvm来控制和释放锁，它提供的是非公平锁，不能手动释放，当执行完毕或异常后有jvm控制释放；lock是juc下的一个接口，他的实现类为reentrentlock，与synchronized一样默认是非公平锁，可设置为公平锁，需要手动加锁，释放锁


* ArrayList, Vector, LinkedList区别？

    ArrayList与Vector底层都是用数组实现，LinedList使用双向链表实现

    Vector是线程安全的，ArrayList与LinkedList不是

* HashMap在使用可变对象作为key时，会丢失数据（即对象数据修改后，hashcode改变，map.get(obj)无法获取到value）

* serialVersionUID是类的版本,在进行反序列化的时候会验证serialVersionUID，如果不一致，会抛出异常

  final 属性初始化只能在构造函数中或在定义时显示赋值


* 反射：
    1. class.forName(className) 加载类并返回其对象引用
    2. 类反射： class.getSimpleName() -> 类名； class.getModifiers() -> 获得修饰符； class.getSuperClass() -> 获得父类； class.getInterface() -> 获得接口
    3. 反射创建对象： 先获取构造参数，但会调用newInstance()方法；

* 线程创建：
    1. 继承Thread
    2. 实现Runnable
    3. Callable 或 Future 接口
   
* Callable与Future的区别？
    callable类似于runnable接口，但runnable不会返回结果，并且无法抛出返回结果的异常，而callable被线程执行后，可以通过Future拿到返回值

* 线程状态： 新建, 运行， 就绪， 休眠， 终止

* 动态代理与静态代理的区别： 动态代理使用反射，只能代理基于接口实现的类

* java8新特性：
    1. lambda表达式和函数式接口
    2. 接口的默认方法和静态方法。默认方法使用default定义，可以覆盖
    3. 方法引用。 system.out::println
    4. 重复注解.使用@Repeatable注解实现
    5. 更好的类型推断
    6. 扩宽注解的应用场景
    7. Optional， Streams
    8. 新的date/time api
    9. 对base64编码的原生支持
    10. 新的Nashorn JavaScript引擎
    11. 并行数组
    12. 使用元空间（MetaSpace）替代永久代(PermGen space)
    13. 类依赖分析器jdeps。使用方法：jdeps org.springframework.core-3.0.5.RELEASE.jar


* switch(param) 接受的参数类型包含int, char, byte, short, String, enum, 

* 使用jdbc对事务进行管理？
    jdbc中事务都是由Connection对象控制。需要先获取到Connection对象，然后关闭事务的自动提交(conn.setAutoCommit(false))，
    然后执行事务, 在事务执行过程中可以设置保存点（connection.setSavepoint()),如果发生异常可以选择回滚到保存点（connection.rollback(savepoint))也可以全部回滚（connect.rollabck()）,
     最后提交事务（connect.commit()）.

* 死锁排查？ 使用jps -l查看进程号,然后使用jstack -l pid


