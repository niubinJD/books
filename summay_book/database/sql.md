# sql

* 表操作：
    
    drop table tableName; 删除表
    
    create table tableName(clomnkey...) engine=InnoDB; // 创建表，并指定工作引擎
    
    alter table add clomnKey;  新增表字段
    
    alter table drop clomnKey; 删除表字段
    
    rename table a to b; 重命名表
    
    show index from table; 查看索引
    
    show columns from tabel; 查看表信息

* mysql配置文件： /etc/my.cnf


* 触发器：
   1. 语法： 
    ```
    create trigger triggerName alter | before(定义触发器执行时间) insert | update | delete (定义触发的动作) on table (定义触发的表)
    for each row
    begin 
        sql语句;
    end;
    ```


* insert:

  1. insert low_priority into table  降低数据插入执行优先级，降低等待处理select的性能,同样适用于update和delete操作

  2. insert into table(clonm) values(value),(value); 优于多条insert语句插入

  3. insert into table(clonm) select (clomn) from oldTable;  insert select将oldTable中的数据导入到table中


* update:  

  1. 更新语法： update table set clomnKey_1 = '1', clomnKey_2 = '2' where id = 1;  注意过滤条件where省略会导致更新全表

  2. update ignore table； 多行更新时，忽略出现更新错误的行

  3. update中可使用子查询的结果来更新字段的值

* delete:

  1. delete语法： delete from table where id = 1; 注意过滤条件where省略会导致删除全表数据

  2. truncate table； 删除表内容操作，比delete快；过程：删除表，然后创建新表，delete是逐条删除数据



* 字符集校对：

  1. show character set; 查看所支持的字符集完整列表

  2. show collation; 查看所支持校对的完成列表

  3. show variables like 'character%'; 查看使用的字符集

  4 show variables like 'collation%' 查看使用的校对

  5. 在创建表时指定字符集及校对： create table table() default character set hebrew collation hebrew_general_ci;


* 访问控制：

  1. 创建新用户： create user username identified by 'password';

  2. 修改用户名： rename user username to newName 或使用 update user set username = 'newName' where username='username';

  3. 删除用户及相关权限： drop user username;

  4. 查看用户权限： show grants for username;

  5. 权限授予： grants select on table.*(所要授予的具体权限) to username;    grants all 授予所有权限    grants database.* 授予指定数据库的所有权限   grants database.tabel.* 授予指定表的所有权限

  6. 撤销权限： revoke select on table.*(所要授予的具体权限) from username;  revoke all 取消所有授权...

  7. 修改密码：set password for username = password('newpassword');


* 数据备份：

  1. mysqldump

  2. mysqlhotcopy
   
  3. backup table 或 select into outfie, 使用restore table来恢复数据


* mysql慢查询(在my.ini中配置)：

  1. slow_query_log = on;  可以捕获执行时间超过一定数值的SQL语句

  2. long_query_time = 1; 当SQL语句执行时间超过此数值时，就会被记录到日志中，建议设置为1或者更短

  3. slow_query_log_file; 慢查询记录日志的文件名

  4. log_queries_not_using_indexes=on; 可以捕获到所有未使用索引的SQL语句，尽管这个SQL语句有可能执行得挺快




面试sql:

 1. 查询人数最多的部门ID
 
    ```
    select dept as ID from people where dept in (select dept from people group by dept having count(*) >= All(select count(*) from people group by dept));
    ```
 2. 表复制

    ```
    inset into table1(name, sex) select name, sex from table;
    ```