# sqlserver常用函数操作


## 除法
```sql
select 100/7      --14
select 100*1.0/7  --14.285714
select ROUND(100*1.0/7,3) --14.286
select cast(100*1.0/7 as numeric(18,3)) --14.286
select convert(decimal(18, 3), 100*1.0/7) --14.286
```