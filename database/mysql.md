# MySQL
```text
    MySQL 是一个关系型数据库管理系统。
    由瑞典MySQL AB 公司开发，目前属于 Oracle 旗下产品。
    最流行的关系型数据库管理系统之一。
```



### MySQL索引
```text
    索引相当于图书馆的目录，可以快速找到需要的内容。
    
    索引的类型：
    主键索引 PRIMARY KEY：是一种唯一性的索引，每个表只能有一个主键。
    唯一索引 UNIQUE：所有值唯一，值可以为空
    普通索引 INDEX：基本的索引类型，值可以为空
    全文索引 FULLTEXT：可以在varchar、char、text类型的列上创建。全文索引不支持中文需要借sphinx(coreseek)或迅搜<、code>技术处理中文
```
#### 查看表中已经存在的索引
```sql
mysql> show index from table_name ;
```
#### MySQL添加索引命令
1. 主键索引 PRIMARY KEY
```sql
mysql>ALTER TABLE `table_name` ADD PRIMARY KEY (`column`) 
```
2. 唯一索引 UNIQUE
```sql
create UNIQUE index index_name on table_name (`column`) ;
-- 或者
mysql>ALTER TABLE `table_name` ADD UNIQUE (`column`)
```
3. 普通索引 INDEX
```sql
create INDEX index_name on table_name (`column`) ;
-- 或者
mysql>ALTER TABLE `table_name` ADD INDEX index_name (`column`)
```
4. 全文索引 FULLTEXT
```sql
mysql>ALTER TABLE `table_name` ADD FULLTEXT (`column`)
```
5. 多列索引
```sql
mysql>ALTER TABLE `table_name` ADD INDEX index_name (`column1`, `column2`, `column3`)
```

#### 删除索引
```sql
drop index index_name on table_name ;
-- 或者
alter table table_name drop index index_name ;

alter table table_name drop primary key ; -- 一个表只可能有一个PRIMARY KEY索引，因此不需要指定索引名
```

#### 索引的机制
1. 为什么我们添加完索引后查询速度为变快？
    传统的查询方法，是按照表的顺序遍历的，不论查询几条数据，mysql需要将表的数据从头到尾遍历一遍。
    在我们添加完索引之后，mysql一般通过BTREE算法生成一个索引文件，在查询数据库时，找到索引文件进行遍历(折半查找大幅查询效率)，找到相应的键从而获取数据。

2. 索引的代价
    1. 创建索引是为产生索引文件的，占用磁盘空间
    2. 索引文件是一个二叉树类型的文件，可想而知我们的dml操作同样也会对索引文件进行修改，所以性能会下降

3. 在哪些column上使用索引？
    1. 较频繁的作为查询条件字段应该创建索引 
    2. 唯一性太差的字段不适合创建索引，尽管频繁作为查询条件，例如gender性别字段
    3. 更新非常频繁的字段不适合作为索引
    4. 不会出现在where子句中的字段不该创建索引

创建索引的条件：
- 肯定在where条经常使用
- 该字段的内容不是唯一的几个值
- 字段内容不是频繁变化。

---
#### 常见的参数设置
#### 存储引擎怎么去选择
#### 了解常见的索引引擎
#### 怎么去设计表
#### 怎么优化sql
#### 怎么根据执行计划去调优
#### 分库分表的设计和优化
#### 读写分离 垂直与水平拆分