# SQL 中Group by 的使用

## 在多表查询中使用Group by ##

> 有三张表，一张是部门表-dept，一张是餐厅表-dinner，还有一张是员工消费明细表-cost(**含餐厅、部门外键**)
> 现在需要一张报表，需求如下:
>
|部门名称|餐厅名称|消费总次数|消费总金额|
|-----|-----|------|-------|
|部门1|餐厅1|2000|20000|
|部门1|餐厅2|2000|20000|
|部门2|餐厅1|2000|20000|
 
```sql
select dept.deptname,dinner.name,cost1.countsum,cost2.money from cost as c 
left join (select dining_id,dept_id,count(*) as countsum from  cost group by dining_id,dept_id) as c1 on c1.dining_id = c.dining_id and c1.dept_id=c.dept_id
left join (select dining_id,dept_id,sum(money) as money from  cost group by dining_id,dept_id) as c2 on c2.dining_id = c.dining_id and c2.dept_id=ic.dept_id
left join dinner as d on d.id= c.dining_id
left join dept as dept on dept.deptid= c.dept_id ;

```

**注意：**

> 当使用`group by`时，`select` 指定的字段要么作为分组
分组依据，写在`group by` 后边，要吗已经被包含在聚合函数中。
如果不是这两种情况的话会跳出错误：

> *选择列表中的列 'xxx' 无效，因为该列没有包含在聚合函数或 GROUP BY 子句中。*
