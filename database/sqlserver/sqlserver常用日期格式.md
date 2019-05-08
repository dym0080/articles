Sqlserver常用日期操作
====================

### 常用的日期转换字符串
```sql
Select CONVERT(varchar(100), GETDATE(), 23)   --'2019-04-22'
Select CONVERT(varchar(100), GETDATE(), 111)  --'2019/04/22'
Select CONVERT(varchar(100), GETDATE(), 121)  --'2019-04-22 17:28:37.627'
```

### 小于某个日期
一般在where条件里面
```sql
where CONVERT(varchar(100), CreatDate, 23)<='2019-04-30' -- CreatDate 为时间字段
```

### 获取日期部分
- `Datepart()`：返回代表指定日期的指定日期部分的整数。
语法：`Datepart(datepart,date)`  返回类型：`int`
- `DateName()`：返回代表指定日期的指定日期部分的字符串。
语法：`DateName(datepart,date)` 返回类型：`nvarchar`
```sql
select datepart(week,GETDATE()) 
select Datename(week,GETDATE())
select datepart(day,GETDATE()) 
select Datename(day,GETDATE())
```