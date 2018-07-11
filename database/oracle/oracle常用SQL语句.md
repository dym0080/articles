


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

  #### 5. 用户操作

  - 查询用户
  使用plsql连接某个数据库后查询该数据库下的用户：

  ```sql
  select * from dba_users a where a.account_status='OPEN';
  ```

  - 删除用户

  使用plsql连接某个数据库后，删除该数据库下的用户user123。删除用户，及级联关系也删除掉。

  ```sql
  drop user user123 cascade;
  ```

  #### 6. 表空间操作
  
  - 查看表空间
  ```sql
  select * from dba_tablespaces
  ```
  - 查看表空间路径
  ```sql
  select * from dba_data_files; 
  ```

  - 删除表空间
  使用plsql连接某个数据库后，参数该数据库下的命名空间TBS_123。删除表空间，及对应的表空间文件也删除掉。
  ```sql
  drop tablespace TBS_123 including contents and datafiles cascade constraint;
  ```

  
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

### 提高oracle更新效率的四种解决方案

#### 标准update语法

当你需要更新的表是单个或者被更新的字段不需要关联其他表带过来，则最后选择标准的`update`语句，速度最快，稳定性最好，并返回影响条数。如果`where`条件中的字段加上索引，那么更新效率就更高。但对需要关联表更新字段时，`update`的效率就非常差。
  
#### inline view更新法（没有实践过）

inline view更新法就是更新一个临时建立的视图。括号里通过关联两表建立一个视图，set中设置好更新的字段。这个解决方法比写法较直观且执行速度快。但表tb2的主键一定要在where条件中，并且是以“=”来关联被更新表，否则报一下错误

```sql
update (select a.code as code1 ,b.code as code2 from tb1 a,tb2 b where a.id=b.id )set code1=code2
```
#### merge更新法
MERGE INTO是Oracle 9i以后才出现的新的功能。那这个功能 是什么呢？简单来说，就是：“有则更新，无则插入”,用来合并UPDATE和INSERT语句.通过MERGE语句，根据一张表或子查询的连接条件对另外一张表进行查询，连接条件匹配上的进行UPDATE，无法匹配的执行INSERT。这个语法仅需要一次全表扫描就完成了全部工作，执行效率要高于INSERT＋UPDATE。
语法：
MERGE INTO [your table-name] [rename your table here]

USING ( [write your query here] )[rename your query-sql and using just like a table]

ON ([conditional expression here] AND [...]...)

WHEN MATHED THEN [here you can execute some update sql or something else ]

WHEN NOT MATHED THEN [execute something else here ! ]

例子
```sql
-- eg1:两个表fzq1和fzq
--更新表fzq1使得id相同的记录中chengji字段＋1，并且更新name字段。  
--如果id不相同，则插入到表fzq1中.  
--将fzq1表中男生记录的成绩＋1，女生插入到表fzq1中  
merge into fzq1  aa     --fzq1表是需要更新的表  
using fzq bb            -- 关联表  
on (aa.id=bb.id)        --关联条件  
when matched then       --匹配关联条件，作更新处理  
update set  
aa.chengji=bb.chengji+1,  
aa.name=bb.name         --此处只是说明可以同时更新多个字段。  
when not matched then    --不匹配关联条件，作插入处理。如果只是作更新，下面的语句可以省略。  
insert values( bb.id, bb.name, bb.sex,bb.kecheng,bb.chengji);  
--可以自行查询fzq1表。  
```
```sql
-- eg2:三个表
/*涉及到多个表关联的例子，我们以三个表为例，只是作更新处理，不做插入处理。当然也可以只做插入处理*/  
--将fzq1表中女生记录的成绩＋1，没有直接去sex字段。而是fzq和fzq2关联。  
merge into fzq1  aa     --fzq1表是需要更新的表  
using (select fzq.id,fzq.chengji   
       from fzq join fzq2  
       on fzq.id=fzq2.id) bb  -- 数据集  
on (aa.id=bb.id)        --关联条件  
when matched then       --匹配关联条件，作更新处理  
update set  
aa.chengji=bb.chengji+1  
--可以自行查询fzq1表。  
```

```sql
-- eg3: 不能做的事情,不能更新条件字段
merge into fzq1  aa      
using fzq bb             
on (aa.id=bb.id)          
when matched then         
update set  
aa.id=bb.id+1  
/*系统提示：  
ORA-38104: Columns referenced in the ON Clause cannot be updated: "AA"."ID"  
我们不能更新on (aa.id=bb.id)关联条件中的字段*/  
update fzq1   
set  id=(select id+1 from fzq where fzq.id=fzq1.id)  
where id in  
(select id from fzq)  
--使用update就可以更新.  
```

```sql
-- eg: 原表中不想更新的字段
merge into t_eir_feetmp  aa       
using t_eir_feetmp2 bb              
on (aa.eir_fee_id=bb.eir_fee_id)  
when matched then        
update set  
aa.fee_amt='0',  
aa.currency_cd='B'  
where aa.fee_nm<>'单证费'   --不更新这一列的值  
when not matched then     
insert values(bb.eir_fee_id,bb.fee_cd,bb.fee_nm,bb.currency_cd,bb.fee_amt,null);  
```
#### 快速游标更新法

语法：

begin
for crin (查询语句)loop –-循环
--更新语句（根据查询出来的结果集合）
end loop; --结束循环
end;

oracle支持快速游标，不需要定义直接把游标写到for循环中，这样就方便了我们批量更新数据。再加上oracle的rowid物理字段（oracle默认给每个表都有rowid这个字段，并且是唯一索引），可以快速定位到要更新的记录上。

例如：
```sql
begin
for crin (select a.rowid,b.join_statefrom t_join_situation a,t_people_info b
where a.people_number=b.people_number
and a.year='2011' and a.city_number='M00000' and a.town_number='M51000')loop
update t_join_situationset join_state=cr.join_statewhere
rowid = cr.rowid;
end loop;
end;
```
使用快速游标的好处很多，可以支持复杂的查询语句，更新准确，无论数据多大更新效率仍然高，但执行后不返回影响行数。

四种方案对比：
| 方案            | 建议          |
| ----------------|:-------------:|
|标准update语法   |单表更新或较简单的语句采用使用此方案更优。|
|inline view更新法|两表关联且被更新表通过关联表主键关联的，采用此方案更优。|
|merge更新法      |两表关联且被更新表不是通过关联表主键关联的，采用此方案更优。|
|快速游标更新法    |多表关联且逻辑复杂的，采用此方案更优。|
    
## 参考资料
* [Oracle 数据库常用操作语句大全](http://www.cnblogs.com/1312mn/archive/2017/11/09/7799732.html) 
