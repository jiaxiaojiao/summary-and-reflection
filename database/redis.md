# Redis

> NoSQL 数据库

> Redis的数据类型：字符串、列表（lists）、集合（sets）、有序集合（sorts sets）、哈希表（hashs）

## 安装Redis

> 默认端口6379

- [Linux下安装Redis](redis-installL.md)

- [Windows下安装Redis](redis-installW.md)


## 命令

- Key 键

- String 字符串

- Hash 哈希表

- List 列表

- Set 集合

- SortedSet 有序集合

- Pub/Sub 发布/订阅

- Transaction 事务

- Script 脚本

- Connection 连接

- Server 服务器

## 原理

> 了解原理、调整参数


## 使用
- [Java使用RedisTemplate](redis-installW.md)
#### Java使用RedisTemplate


## 其他

```text
Redis介绍
Redis主从模式：一主一从，一主多从、树型主从

Redis常用命令及应用场景
set get lpush lrange hmget hmset pipeline
String List Hash Set Zset类型的使用场景
排行榜、点赞数、时间轴、队列实战
Redis客户端
Jedis
Jedispool
JedisCluster
JedisCluster + Spring MVC整合
Redis持久化
RDB
AOF
数据恢复与转移实战
哨兵核心机制： 选举原理，主观下线，客观下线，Java与哨兵如何工作
高可用集群：槽的介绍，键槽关系，分布式存储，重定向，搭建Redis高可用集群，动态扩容 缩减集群节点实战
原子性：Lua语言结合开发，弱事务体现，multi watch discard exec，

```

