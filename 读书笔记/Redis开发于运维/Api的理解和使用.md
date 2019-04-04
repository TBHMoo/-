# API的理解和使用
 redis 提供了5中数据结构，理解每种数据结构的特点对于redis开发运维非常重要，
 同时掌握redis 的单线程命令处理机制，会是数据结构和命令的选择事半功倍。
 
 ## 预备知识
 * 全局命令
 * 数据结构 和 内部编码
 * 单线程命令处理机制分析
 
### 全局命令
#####1 查看所有键 keys * 
O(n)
~~~
 127.0.0.1:6379> set hello world
 OK
 127.0.0.1:6379> set java jedis
 OK
 127.0.0.1:6379> set python redis-py
 OK
 127.0.0.1:6379> keys * 
 1) "python"
 2) "java"
 3) "hello"

 ~~~
 
#####2 键总数 dbsize  
O(1)
dbsize 命令在计算键总数时不需要遍历所有键

~~~
 127.0.0.1:6379> rpush mylist a b c d e f g
(integer) 7
 127.0.0.1:6379> dbsize
(integer) 4
~~~

#####3 检查键是否存在
exists key
如果键存在则返回1，不存在则返回0:
~~~
 127.0.0.1:6379> exists java
 (integer) 1
127.0.0.1:6379> exists not_exist_key
 (integer) 0
~~~
#####4 删除键
del key [key ...]

del 是一个通用命令，无论值时什么数据结构类型 ，del 命令都可以删除
~~~
127.0.0.1:6379> del java
 (integer) 1
127.0.0.1:6379> exists java
 (integer) 0
127.0.0.1:6379> del mylist
 (integer) 1
127.0.0.1:6379> exists mylist
(integer) 0

del 命令删除多个键
127.0.0.1:6379> set a 1
OK
127.0.0.1:6379> set b 2
OK
127.0.0.1:6379> del a b
(integer) 2
~~~
#####5 键过期
expire key seconds
redis 支持对键添加过期时间，当超过过期时间后，会自动删除键。
~~~
127.0.0.1:6379> set hello world
OK
127.0.0.1:6379> expire hello 10
(integer) 1
~~~

ttl 命令会返回键的剩余过期时间，他有3中返回值：
* 大于等于0的整数：键剩余的过期时间。
* -1： 键没设置过期时间
* -2： 键不存在
~~~
127.0.0.1:6379> ttl hello
(integer) 7
~~~

#####6 键的数据类型
type key
~~~
 127.0.0.1:6379> set hello world
 OK
  127.0.0.1:6379> type hello
  string
 127.0.0.1:6379> rpush mylist a b c d e f g
(integer) 7
  127.0.0.1:6379> type mylist
  list

~~~
