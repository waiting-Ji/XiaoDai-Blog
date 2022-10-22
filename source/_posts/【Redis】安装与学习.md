---
title: 【Redis】安装与学习
date: 2022-10-13 15:54:00
tags:
   运维
---
# Redis简介
Redis是基于内存进行数据查询的
Redis可用作数据库、缓存和消息中间件
NoSql，不仅仅是SQL，泛指非关系型数据库。NoSql数据库并不是取代关系型数据库，而是关系型数据库的补充。
## 应用场景

   1. 缓存（秒杀业务）
   2. 任务队列
   3. 消息队列
   4. 分布式锁

## 关系型数据库

   1. Mysql
   2. Oracle
   3. DB2
   4. SQLServer
   
## 非关系型数据库

   1. Redis
   2. Mongo db
   3. MemCacched
   
# Redis安装
镜像文件下载地址：[https://download.redis.io/releases/](https://download.redis.io/releases/)

1. 将下载的redis.tar.gz文件上传至Linux目录下（例：/usr/addFile/targz）
2. 解压redis.tar.gz文件（解压至/usr/addFile文件夹下）
:::info
tar -zxvf redis-4.0.0.tar.gz  -C /usr/addFile/
:::

3. 安装Redis的依赖环境g6c,命令：yum install gcc-c+
4. 进入/usr/addFile/redis-4.0.0,进行编译，命令：make
5. 进入redis的src目录，进行安装，命令：make install
# Redis服务启动与停止
Linux中redis服务启动，可以使用redis-server（/usr/addFile/redis-4.0.0），默认端口为6379
Ctrl+C停止Redis服务
## 修改Redis运行模式

1. 进入redis-4.0.0文件下时 vim redis-conf文件查找dae （输入：/dae）
2. daemonize no 改为 daemonize yes 则运行模式为后台运行

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25847601/1664498711764-cdc8e5dd-9916-4cd3-8196-a499d50763a6.png#clientId=u25e87111-eb16-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=516&id=u4e7324a0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=645&originWidth=1159&originalType=binary&ratio=1&rotation=0&showTitle=false&size=67757&status=done&style=none&taskId=u97e97493-3b1d-4fec-a951-b5d5bbf634c&title=&width=927.2)
## 修改Redis密码

1. 进入redis-4.0.0文件下时 vim redis-conf文件查找password （输入：/password）
2. 将下图中#取出 修改fooabred为自定义密码

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25847601/1664500114163-7ec1ecb3-8ce2-4d19-a7e7-9a5047eb41c4.png#clientId=u25e87111-eb16-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=516&id=u1b58df5c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=645&originWidth=1159&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57202&status=done&style=none&taskId=uacfc467a-0024-414c-89a6-cbc05022651&title=&width=927.2)
密码配置成功后重启服务器

1. 启动时查看配置文件：./src/redis-server ./redis.conf
2. 查看redis进程：ps -f | grep redis
3. 本地连接Redis：./src/redis-cli -h localhost -p 6379
4. 查看不输入密码是否可以对Redis进行操作：keys *（橙色框中是不允许）
5. 则需输入密码登录Redis：auth 密码
6. 登录成功

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25847601/1664501322020-1312e33d-e557-471d-829a-7b3a2ea3f25b.png#clientId=u25e87111-eb16-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=190&id=u5e262813&margin=%5Bobject%20Object%5D&name=image.png&originHeight=237&originWidth=1034&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28432&status=done&style=none&taskId=u2f518cc5-6f99-465c-83c4-df46b3e285b&title=&width=827.2)
## 修改Redis连接状态
Redis默认本地连接

1. 进入redis-4.0.0文件下时 vim redis-conf文件查找bind（输入：/bind）
2. 注释橙色框选中行（# bind 127.0.0.1）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25847601/1664501751303-7b5e20d2-4fa9-4f36-9dac-f88113eb471f.png#clientId=u25e87111-eb16-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=516&id=uef989933&margin=%5Bobject%20Object%5D&name=image.png&originHeight=645&originWidth=1159&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56473&status=done&style=none&taskId=u21454d45-ece4-4cc8-81cf-3ee3a327c6c&title=&width=927.2)
# Redis数据类型
![image.png](https://cdn.nlark.com/yuque/0/2022/png/25847601/1664503603409-7486794b-a434-4b7b-80bf-a225a541f715.png#clientId=u25e87111-eb16-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=354&id=ud29f1d42&margin=%5Bobject%20Object%5D&name=image.png&originHeight=442&originWidth=882&originalType=binary&ratio=1&rotation=0&showTitle=false&size=154743&status=done&style=none&taskId=u74c6f0f8-3960-45c0-bd1d-283bcd38b5e&title=&width=705.6)
中文教程网：[https://www.redis.net.cn/tutorial/3505.html](https://www.redis.net.cn/tutorial/3505.html)
## String（字符串）

1. string是redis最基本的类型，你可以理解成与Memcached一模一样的类型，一个key对应一个value。
2. string类型是二进制安全的。意思是redis的string可以包含任何数据。比如jpg图片或者序列化的对象 。
3. string类型是Redis最基本的数据类型，一个键最大能存储512MB。
### 理解
一个键对应一个字符串，
一个地址存储一个数据
### 实例
:::info
redis 127.0.0.1:6379> SET name "redis.net.cn"OK
redis 127.0.0.1:6379> GET name"redis.net.cn"
:::
在以上实例中我们使用了 Redis 的 **SET** 和 **GET** 命令。键为 name，对应的值为redis.net.cn。
**注意：**一个键最大能存储512MB。

---

## Hash（哈希）

1. Redis hash 是一个键值对集合。
2. Redis hash是一个string类型的field和value的映射表，hash特别适合用于存储对象。value值必须是基础类型
3. 相对于存储json序列化的字符串更加节省性能
### 理解
一个键对应一个集合，
集合中索引可存储多条个数据
### 实例
:::info
redis 127.0.0.1:6379> HMSET user:1 username redis.net.cn password redis.net.cn points 200OK
redis 127.0.0.1:6379> HGETALL user:1
1) "username"
2) "redis.net.cn"
3) "password"
4) "redis.net.cn"
5) "points"
6) "200"
redis 127.0.0.1:6379>
:::
以上实例中 hash 数据类型存储了包含用户脚本信息的用户对象。 实例中我们使用了 Redis **HMSET, HEGTALL** 命令，**user:1** 为键值。
每个 hash 可以存储 232 - 1 键值对（40多亿）。

---

## List（列表）
Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素导列表的头部（左边）或者尾部（右边）。
### 理解
呈现状态为列表状，数据不可通过标识或索引对数据进行获取，
只能通过列表名查询范围内的多条数据
### 实例
:::info
redis 127.0.0.1:6379> lpush redis.net.cn redis(integer) 1
redis 127.0.0.1:6379> lpush redis.net.cn mongodb(integer) 2
redis 127.0.0.1:6379> lpush redis.net.cn rabitmq(integer) 3
// 查询数据范围 0 -10 条
redis 127.0.0.1:6379> lrange redis.net.cn 0 10
1) "rabitmq"
2) "mongodb"
3) "redis"
redis 127.0.0.1:6379>
:::
列表最多可存储 232 - 1 元素 (4294967295, 每个列表可存储40多亿)。

---

## Set（集合）
Redis的Set是string类型的无序集合。
集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。
### sadd 命令
添加一个string元素到,key对应的set集合中，成功返回1,如果元素以及在集合中返回0,key对应的set不存在返回错误。
sadd key member
### 理解
呈现状态为列表状，数据不可通过标识或索引对数据进行获取，
只能通过命名进行数据获取，而且在数据添加时不允许出现重复插入
### 实例
:::info
redis 127.0.0.1:6379> sadd redis.net.cn redis(integer) 1
redis 127.0.0.1:6379> sadd redis.net.cn mongodb(integer) 1
redis 127.0.0.1:6379> sadd redis.net.cn rabitmq(integer) 1
redis 127.0.0.1:6379> sadd redis.net.cn rabitmq(integer) 0
redis 127.0.0.1:6379> smembers redis.net.cn 
1) "rabitmq"
2) "mongodb"
3) "redis"
:::
**注意：**以上实例中 rabitmq 添加了两次，但根据集合内元素的唯一性，第二次插入的元素将被忽略。
集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。

---

## zset(sorted set：有序集合)
Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
zset的成员是唯一的,但分数(score)却可以重复。
### zadd 命令
添加元素到集合，元素在集合中存在则更新对应score
zadd key score member 
### 实例
:::info
redis 127.0.0.1:6379> zadd redis.net.cn 0 redis(integer) 1
redis 127.0.0.1:6379> zadd redis.net.cn 0 mongodb(integer) 1
redis 127.0.0.1:6379> zadd redis.net.cn 0 rabitmq(integer) 1
redis 127.0.0.1:6379> zadd redis.net.cn 0 rabitmq(integer) 0
redis 127.0.0.1:6379> ZRANGEBYSCORE redis.net.cn 0 1000 
1) "redis"
2) "mongodb"
3) "rabitmq"
:::
