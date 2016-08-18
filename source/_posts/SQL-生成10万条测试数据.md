---
title: SQL 生成10万条测试数据
date: 2016-08-18 11:03:00
categories: "SQL"
---
### 循环插入10万条测试数据 ###
```sql
declare @i int
set @i=1
while @i<100000
begin
    insert into test(title,date_time) values('test'+cast(@i as ncahr(10)),getdate())
    set @i=@i+1
end
go

```
**注意**:  
1. `cast()`函数是强制类型转换与`convert()`用法一致
2. `declare` 用于声明变量
<!-- more -->
