
- sqlserver常用的日期转换字符串
```sql
Select CONVERT(varchar(100), GETDATE(), 23)   --'2019-04-22'
Select CONVERT(varchar(100), GETDATE(), 111)  --'2019/04/22'
Select CONVERT(varchar(100), GETDATE(), 121)  --'2019-04-22 17:28:37.627'
```