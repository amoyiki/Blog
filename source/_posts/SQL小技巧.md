---
title: SQL小技巧
date: 2016-08-18 11:03:00
categories: "SQL"
---
### 重置表自增长ID值 ###
有时候我们需要清空一张表的数据，又不想删除增长表。除了删除数据外，还需要将自增长ID重置为0。相关的SQl操作如下
1. 方法一
  ```sql
  truncate table tb
  ```
  但是`truncate`方法不能清空含有`Foreign Key`约束的表，这个时候就需要用到方法二了。
2. 方法二
  ```sql
DBCC CHECKIDENT(TB,RESEED,0)
  ```
<!-- more -->
### 循环插入10万条测试数据 ###
```sql
declare @i int
set @i=1
while @i<100000
begin
    insert into test(title,date_time) values('test'+cast(@i as nvarchar(10)),getdate())
    set @i=@i+1
end
go
```
**注意**:  
1. `cast()`函数是强制类型转换与`convert()`用法一致
2. `declare` 用于声明变量
