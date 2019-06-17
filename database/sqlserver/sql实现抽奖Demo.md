

最近在做小程序的时候，需要一个这样的需求
> 小程序界面有九宫格抽奖、转盘抽奖界面，总共有8个抽奖产品，每个产品的中奖概率是确定的，需要根据抽奖概率进行抽奖。

## 数据准备

已知奖品1-8（笔记本电脑、小米手机、100元话费、0元话费、20元话费、10元话费、3元话费、谢谢惠顾）的中奖概率分别为：0.05%、0.15% 、9.8% 、10%、 10% 、15%、 25%、 30%。根据中奖概率可以在数据库表中配置odds字段的数值。
```sql
-- 奖品表
CREATE TABLE [dbo].[tblPrize] (
  [Id] int  IDENTITY(1,1) NOT NULL, -- 主键
  [ProductName] nvarchar(50) COLLATE Chinese_PRC_CI_AS  NULL, --奖品名称
  [odds] int  NULL --奖率
)
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'1', N'笔记本电脑', N'5')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'2', N'小米手机', N'15')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'3', N'100元话费', N'980')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'4', N'50元话费', N'1000')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'5', N'20元话费', N'1000')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'6', N'10元话费', N'1500')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'7', N'3元话费', N'2500')
INSERT INTO [dbo].[tblPrize] ([Id], [ProductName], [odds]) VALUES (N'8', N'谢谢惠顾', N'3000')
```

## 两种实现方式（sqlserver存储过程实现）
实现思想：根据中奖概率取整(odds字段中的8个整数)，把整数求和得到一个整数和A，根据这个整数和生成一个随机数B,看随机数B是在哪个范围就是中到了哪个奖品。

> 下面两个实现方式的B为10000。
### 方式一
```sql
ALTER PROCEDURE [dbo].[LuckyDraw]
AS
BEGIN
-- 九宫格抽奖        
DECLARE @randnum int
DECLARE @rownum int
DECLARE @num1 int
DECLARE @num2 int
DECLARE @num3 int
DECLARE @num4 int
DECLARE @num5 int
DECLARE @num6 int
DECLARE @num7 int
DECLARE @num8 int            
DECLARE @ptid int            

select @num1=odds from tblPrize where  id=1
select @num2=odds from tblPrize where  id=2
select @num3=odds from tblPrize where  id=3
select @num4=odds from tblPrize where  id=4  
select @num5=odds from tblPrize where  id=5
select @num6=odds from tblPrize where  id=6
select @num7=odds from tblPrize where  id=7
select @num8=odds from tblPrize where  id=8


set @randnum= cast(ceiling(rand() * 10000) as int)
if (@randnum>0 and @randnum<=@num1)
            set @rownum=1
else if(@randnum>@num1 and @randnum<=@num1+@num2)
            set @rownum=2
else if(@randnum>@num1+@num2 and @randnum<=@num1+@num2+@num3)
            set @rownum=3
else if(@randnum>@num1+@num2+@num3 and @randnum<=@num1+@num2+@num3+@num4)
             set @rownum=4
else if(@randnum>@num1+@num2+@num3+@num4 and @randnum<=@num1+@num2+@num3+@num4+@num5)
                set @rownum=5
else if(@randnum>@num1+@num2+@num3+@num4+@num5 and @randnum<=@num1+@num2+@num3+@num4+@num5+@num6)
             set @rownum=6
else if(@randnum>@num1+@num2+@num3+@num4+@num5+@num6 and @randnum<=@num1+@num2+@num3+@num4+@num5+@num6+@num7)
             set @rownum=7
else
             set @rownum=8
      

select @ptid=id from (select row_number() over(order by id) as rownum,id from tblPrize )t where t.rownum=@rownum   
    
select @ptid id, @randnum randnum --得到中奖的奖品ID和随机数
        
END
```

### 方式二：使用游标
```sql
ALTER PROCEDURE [dbo].[LuckyDraw_cur]
AS
BEGIN
-- 九宫格抽奖        
DECLARE @randnum int        
DECLARE @idnum int
DECLARE @oddsnum int
declare @beginindex int=0
declare @endindex int


set @randnum= cast(ceiling(rand() * 10000) as int)

declare cur cursor  for select id,odds from tblPrize  order by id;
	open cur 
	fetch next from cur into @idnum,@oddsnum 
	while @@fetch_status=0
	begin
		set @endindex=@beginindex + @oddsnum
		if(@randnum>@beginindex and @randnum<=@endindex)
		begin
			break;
		end
		set @beginindex=@endindex
		fetch next from cur into @idnum,@oddsnum 
	end
	close cur
	DEALLOCATE cur     


       
select @idnum id, @randnum randnum --得到中奖的奖品ID和随机数
END
```

## 两种方式的优劣
方式二更灵活，比如假如奖品数量变少和增多（比如奖品变成5个或10个），不需要修改存储过程的代码。而方式一种的数量是写死的，增加或减少数量需要修改代码。