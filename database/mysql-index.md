# MySQL 索引

```text
    索引相当于图书馆的目录，可以快速找到需要的内容。
    
    索引的类型：
    主键索引 PRIMARY KEY：是一种唯一性的索引，每个表只能有一个主键。
    唯一索引 UNIQUE：所有值唯一，值可以为空
    普通索引 INDEX：基本的索引类型，值可以为空
    全文索引 FULLTEXT：可以在varchar、char、text类型的列上创建。全文索引不支持中文需要借sphinx(coreseek)或迅搜<、code>技术处理中文
    
    索引的命名，一般是 表名_索引名
    索引会降低写的速度。
```

## 创建和删除索引
在执行Create Table语句时可以创建索引，也可以单独用Create Index或Alter table来为表增加索引。

### 查看表中已经存在的索引

```sql
mysql> show index from table_name ;
```

### MySQL添加索引命令

- 主键索引 PRIMARY KEY

```sql
mysql>ALTER TABLE `table_name` ADD PRIMARY KEY (`column`) 
```

- 唯一索引 UNIQUE

索引列的值必须唯一，允许有空值。
1. 简化MySQL对这个索引的管理工作，这个索引也因此变得更有效率；
2. MySQL会在有新记录插入数据表的时候，自动检查新记录的这个字段的值是否已经在某个记录上的这个字段中出现过了。如果是，MySQL将拒绝插入这条新纪录。也就是说，唯一索引可以保证数据记录的唯一性。事实上，在许多场合，创建唯一索引的目的往往不是为了提高访问速度，而是为了避免数据出现重复。
```sql
create UNIQUE index index_name on table_name (`column`) ;
-- 或者
mysql>ALTER TABLE `table_name` ADD UNIQUE (`column`)
```

- 普通索引 INDEX

由关键字key或index定义的索引，唯一的任务是加快对数据的访问速度。因此，应该只为那些最经常出现在查询条件（where ...） 或 排序条件（order by ...）中的数据库列创建索引。
```sql

create INDEX index_name on table_name (`column`) ;

-- 或者
mysql>ALTER TABLE `table_name` ADD INDEX index_name (`column`)
```

- 全文索引 FULLTEXT

MySQL从3.23.23版本开始全面支持全文索引和全文检索。fulltext索引仅可用于MyISAM表。
```sql
mysql>ALTER TABLE `table_name` ADD FULLTEXT (`column`)
```

- 多列索引/联合索引/复合索引

```text
    命名规则： 表明_字段名
```

```text
    1. 最左原则： MySQL从左到右的使用索引中的字段。 如果最左字段没有使用，那联合索引没有作用。
    
    2. 每次查询只能使用一个索引，多个单列索引在多条件查询时只会生效第一个索引！所以多条件联合查询时最好建联合索引！
    
    3. 如果联合索引和单列索引同时存在（字段有重复），MySQL查询优化器策略，当一个表有多条索引可走时, Mysql 根据查询语句的成本来选择走哪条索引。
    
    4. 联合索引本质：
    当创建(a,b,c)联合索引时，相当于创建了(a)单列索引，(a,b)联合索引以及(a,b,c)联合索引 
    想要索引生效的话,只能使用 a和a,b和a,b,c三种组合。
```

```sql
mysql>ALTER TABLE `table_name` ADD INDEX index_name (`column1`, `column2`, `column3`)
```


### 删除索引

```sql
drop index index_name on table_name ;

-- 或者
alter table table_name drop index index_name ;

alter table table_name drop primary key ; -- 一个表只可能有一个PRIMARY KEY索引，因此不需要指定索引名
```

## 索引的机制
1. 为什么我们添加完索引后查询速度为变快？
    传统的查询方法，是按照表的顺序遍历的，不论查询几条数据，mysql需要将表的数据从头到尾遍历一遍。
    在我们添加完索引之后，mysql一般通过BTREE算法生成一个索引文件，在查询数据库时，找到索引文件进行遍历(折半查找大幅查询效率)，找到相应的键从而获取数据。

2. 索引的代价
    1. 创建索引是为产生索引文件的，占用磁盘空间
    2. 索引文件是一个二叉树类型的文件，可想而知我们的dml操作同样也会对索引文件进行修改，所以性能会下降。
    影响更新和插入的速度。

3. 在哪些column上使用索引？
    1. 较频繁的作为查询条件字段应该创建索引 
    2. 唯一性太差的字段不适合创建索引，尽管频繁作为查询条件，例如gender性别字段
    3. 更新非常频繁的字段不适合作为索引
    4. 不会出现在where子句中的字段不该创建索引


创建索引的条件：
- 肯定在where条经常使用
- 如果where条件中是OR关系，加索引不起作用
- 该字段的内容不是唯一的几个值
- 字段内容不是频繁变化。
- 联合索引比对每个列分别建索引更有优势，因为索引建立得越多就越占磁盘空间，在更新数据的时候速度会更慢。另外建立多列索引时，顺序也是需要注意的，应该将严格的索引放在前面，这样筛选的力度会更大，效率更高


## 索引的注意事项和优化方法

### 索引不会包含NULL值的列
只要列中包含NULL值将不会被包含在索引里，复合索引中只要有一列含有NULL值，那么这一列对于此复合索引就是无效的。

### 索引列排序
MySQL查询只使用一个索引，如果where中已经使用了索引，order by 中的列是不会使用索引的。

### like语句操作
一般情况下不鼓励使用like。
like "%XX%" 不会使用索引，like "XX%" 可以使用索引。


```text
  MySQL 只对 (<, <=, =, >, >=, between, in, 不以通配符%或_开头的like) 才使用索引。
  
  理论上每张表的索引最多可创建16个索引。 
```


## explain

```text
    explain 显示了mysql如何使用索引来处理select语句以及连接表。
    可以帮助选择更好的索引和写出更优化的查询语句。
```
