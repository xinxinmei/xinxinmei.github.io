### 创建数据库

```
create database student;//创建一个名为student的数据库
```
### 创建数据库的表
```
create table student		//定义一个名为student的表
(
sno char(9)  primary key,				
sname char(20),
ssex char(2)  constraint s_check check(ssex in('男','女'))
);
```
### 修改基本表
```
alter table <表名>
add [column] <新列名><数据类型> [完整性约束]
add <表级完整性约束>
drop [column] <列名> [cascade|restrict]
drop constraint<完整性约束名> [cascade|restrict]
alter column <列名><数据类型>；
```
```
eg:向student表中增加'入学时间'列。
alter table student add student_time datetime;
```
```
eg:student表增加表级完整性约束。
alter table student add primary key(sno);
```
```
eg:student表删除'入学时间'列；
alter table student drop column student_time;//注意在删除时需要带上column，增加时随意。
```
```
eg:student表删除用户定义的完整性约束
alter table student drop constraint s_check;
```
```
eg：修改列的定义
alter table student alter column;
```
### 删除基本表
```
drop table student ;
```
### 索引的建立、修改、删除
```
create unique index <索引名> on <表名>（<列名> asc,<列名> desc,...）
alter index <索引名> rename to <新的索引名>
drop index <索引名>
```
### 数据查询
```
select [all|distinct] <目标列表达式> 
from <表名或视图名> 
[where <条件表达式>]
[group by <列名> [having <表达式>]  ]
[order by <列名> [asc|desc]  ]

```
##### 常用的查询条件
```
确定范围： between and ;not between and
确定集合： in ;not in
字符匹配：like ; not like("_"表示单个任意字符；"%"表示任意长度的字符串)
空值：is null;is not null
逻辑运算： and ; or ;not 
```
###### 聚集函数
```
count(*)			统计元组个数
count([distinct|all] <列名>) 		统计一列中值的个数
sum() 、avg()、max()、min()
注意：聚集函数只能用于select子句和group by 中的having 子句
```
### 数据更新
```
insert into student(sno，sname）values('1','小王');
insert into student(sno,sname) 子查询；

update <表名> set <列名>=<表达式> [where <条件>];

delete from <表名> [where <条件>];
```
## 视图
```
create view <视图名> (<列名>,<列名>,<列名>)
as 子查询
[with check option]

插、删、改 类似表
```
