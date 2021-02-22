title: Redis基本数据类型
author: Luka Chun
tags:
  - 技术
  - Redis
categories:
  - 技术
date: 2021-02-22 23:09:00
---
redis是一个key-value形式的nosql存储系统，redis的所有操作都是原子性的。

1、String
string是二进制安全的，可以存储图片文件等，也可以利用incr用作计数统计。

set key value

get key

incr key



2、List
list类型是一个双向链表结构，亦可实现一个队列。

lpush key  value

rpush key  value

lrange key start end

lpop key 



3、Hash
散列类型，适合存储对象，即将对象的每个属性存成单个string类型。一个对象存储在hash类型中会占用更少的内存，并且可以更方便的存取整个对象，其底层数据结构是一个HashMap，如果属性个数不超过指定个数或者大小，则底层采用一维数组紧凑存储该MAP，如果超过该阈值，则转为真正的HashMap。

hset key field value

hmset key field value[field value...]

hget key field

hmget key field....

hgetall key

hexists key field 

hsetnx key field value        当且仅当 field不存在的时候才设置值

hincrby key field increment       返回增加后的数字，当value不为整数时，报错

hdel key field....       返回被删除个数

hkeys key          返回所有字段名

hvals key       返回所有键值

hlen key     返回字段总数



4、Set
set是一个不可重复的无序集合。可以快速查找元素是否存在，可以求两个set的差集。实际项目中切记set集合的大小不要过大，否则容易导致节点内存不均匀，redis访问阻塞，影响服务质量。

sadd key value...   添加一个或多个

smembers key      返回所有集合元素

sismember key     查询指定key是否存在

srem key...            删除一个或者多个key

scard key              查看集合中元素个数

srandmember key num  随机返回集合中的指定个数元素

spop key               随机删除一个元素，并返回元素信息



5、ZSet
zadd key score value[scre value]

zscard key

zrange key start end        查看指定位置的成员  加上 withscores即可返回分数

zrank key value            获取指定成员下标

zcount key score score        获取指定分数之间成员个数

zrem key value...     删除一个或者多个元素

zscore key value      获取指定元素的score

zincrby key score value       对指定元素的score加上指定分数

zrangebyscore key score  score   获取score范围之间的数据

zremrangebyscore  key score  score  删除指定score范围内的数据

zremrangebyrank   key  rank   rank    删除指定下标内的数据



