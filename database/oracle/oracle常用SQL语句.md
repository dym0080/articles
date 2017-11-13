
## 一、Oracle数据库操作
#### 1. 创建数据库
create database dbname
#### 2. 删除数据库
 drop database dbname
#### 3. 备份数据库
- 完全备份
```sql
 exp user/pwd@orcl buffer=1024 file=d:\bck.dmp full=y
```
user/pwd：用户名/密码
buffer: 缓存大小
file: 具体的备份文件地址
full: 是否导出全部文件
ignore: 忽略错误，如果表已经存在，则也是覆盖
- 将数据库中system用户与sys用户的表导出
```sql
exp user/pwd@orcl file=d:\backup\bck.dmp owner=(system,sys)
```
- 按过滤条件，导出
```sql
 exp user/pwd@orcl file=d:\bck.dmp tables=（table1） query=\" where filed1 like 'fg%'\"
```
 导出时可以进行压缩；命令后面 加上 compress=y ；如果需要日志，后面： log=d:\log.txt
 - 备份远程服务器的数据库
   exp 用户名/密码@远程的IP:端口/实例 file=存放的位置:\文件名称.dmp full=y
 #### 4. 数据库还原
 - 完整还原
 ```sql
   imp user/pwd@orcl file=d:\bck.dmp full=y ignore=y log=D:\implog.txt
 ```
 指定log很重要，便于分析错误进行补救。
 - 导入指定表
 ```sql
 imp user/pwd@orcl file=d:\bck.dmp tables=(teacher,student)
 ```
 - 还原到远程服务器
  imp 用户名/密码@远程的IP:端口/实例 file=存放的位置:\文件名称.dmp full=y
  
  ## 二、Oracle表操作
  #### 1.创建表
  ```sql
  create table tablename(col1 type1 [not null] [primary key],col2 type2 [not null],..)
  ```
  根据已有的表创建新表：
  - 使用旧表创建新表
  ```sql
  select * into table_new from table_old
  ```
  #### 2. 删除表
  ```sql
  drop table tablename
  ```
  #### 3. 重命名表
  ```sql
  alter table tablename_old rename to tablename_new
  ```
  #### 4. 增加字段
  说明：alter table 表名 add (字段名 字段类型 默认值 是否为空)，例如：
  ```sql
  alter table tablename add (ID int);
  alter table tablename add (ID varchar2(30) default '空' not null);
  ```
  #### 5. 修改字段
  说明：alter table 表名 modify (字段名 字段类型 默认值 是否为空);
  ```sql
  alter table tablename modify (ID number(4));
  ```
  #### 6. 重名字段
  说明：alter table 表名 rename column 列名 to 新列名 （其中：column是关键字）
  ```sql
  alter table tablename rename column ID to newID;
  ```
  #### 7. 删除字段
  alter table 表名 drop column 字段名;
  ```sql
  alter table tablename drop column ID;
  ```
  #### 8. 添加主键
  ```sql
  alter table tablename add primary key(col)
  ```
  #### 9. 删除主键
  ```sql
  alter table tabname drop primary key(col)
  ```
  #### 10. 创建索引
  ```sql
  create [unique] index idxname on tabname(col….)
  ```
  #### 11. 删除索引
  索引是不可更改的，想更改必须删除重新建。
  ```sql
  drop index idxname
  ```
  #### 12. 创建视图
  ```sql
  create view viewname as select statement
  ```
  #### 13. 删除视图
  ```sql
  drop view viewname
  ```
  ## 三、Oracle操作数据
  #### 1. 数据查询
  select <列名> from <表名> [where <查询条件表达试>] [order by <排序的列名>[asc或desc]]
  #### 2. 插入数据
  insert into 表名 values(所有列的值);
  ```sql
  insert into test values(1,'zhangsan',20);
  ```
  insert into 表名(列) values(对应的值);
  ```sql
  insert into test(id,name) values(2,'lisi');
   ```
  #### 3. 更新数据
  根据条件更新满足该条件下的所有数据:
  ```sql
  update test set name='zhangsan2' where name='zhangsan'
  ```
  更新所有的数据:
  ```sql
  update test set age =20;
  ```
  #### 4. 删除数据
  - delete from 表名 where 条件 -->删除满足条件的记录
     delete from test where id = 1;
     delete from test -->删除所有
     commit; -->提交数据
     rollback; -->回滚数据
     delete方式可以恢复删除的数据，但是提交了，就没办法了 delete删除的时候，会记录日志 -->删除会很慢很慢
  - truncate table 表名
  删除所有数据，不会影响表结构，不会记录日志，数据不能恢复 -->删除很快
  - drop table 表名
  删除所有数据，包括表结构一并删除，不会记录日志，数据不能恢复-->删除很快
  #### 5. 数据复制
  - 表数据复制
  ```sql
  insert into table1 (select * from table2);
  ```
  - 复制表结构
  ```sql
  create table table1 select * from table2 where 1>1;
  ```
  - 复制指定字段
  ```sql
  create table table1 as select id, name from table2 where 1>1;
  ```
  - 复制表结构及其数据：
  ```sql
  create table table_name_new as select * from table_name_old
  ```
  - 只复制表结构
  ```sql
  create table table_name_new as select * from table_name_old where 1=2; 或者： create table table_name_new like table_name_old 
  ```
  - 只复制表数据：
   如果两个表结构一样：
  ```sql
  insert into table_name_new select * from table_name_old 
  ```
  如果两个表结构不一样：
  ```sql
  insert into table_name_new(column1,column2...) select column1,column2... from table_name_old
  ```
  ## 四、Oracle其他常用操作
    
    
  ##### 参考
  - [Oracle 数据库常用操作语句大全](http://www.cnblogs.com/1312mn/archive/2017/11/09/7799732.html) 
