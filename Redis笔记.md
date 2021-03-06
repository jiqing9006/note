### 商城数据存储位置

冷数据，存储在关系型数据库中（mysql）。

商品描述、详情、评价等信息存储在文档类数据库中（mongodb）。

商品图片存储在分布式文件系统，如Hadoop的HDFS中。

商品的关键字ISearch。

高频词汇热点信息（Tair、Redis、Memcache）内存数据库。

商品的交易，价格计算，积分累计（外部系统，第三方支付接口）。

面向接口编程，来解决多数据源多数据类型问题（统一数据服务层）。

代码，让世界更美好。

我的算法，我的程序，让这个系统更美好一点点。

**把高频热数据放到redis中。**

大公司有体量和成本来试错，小公司没有。小公司成立一个研发部试错两次，估计就倒闭了。

学习具有相通和传递性。



### CAP

C 强一致性

A 高可用性

P 分布式容忍性

CA Oracle

AP 大多数网站架构的选择

CP Redis/Mongodb



------------------

Redis 安装

#### 是什么

Redis（Remote Dictionary Server）远程字典服务器

开源免费

C语言编写的

key/value分布式内存数据库，基于内存运行



Redis支持数据的持久化，可以将内存中的数据保持在磁盘中，重启的时候可以继续加载使用

不仅仅支持key-value，还支持list，set，zset，hash等数据结构，比memcache要丰富

Redis支持数据的备份



#### 能干嘛用

内存的存储和持久化

发布、订阅消息系统

定时器、计数器



师傅领进门，修行靠个人。（上千个API，老师不能一一演示。演示部分之后，剩下的自己去查阅。）



#### 安装使用

#### windows下安装

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233310144-1298557001.png)

下载，windows版本。这个版本由微软进行维护。

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233454253-1357859869.png)
进行安装。

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233517941-1566059626.png)

配置连接密码。

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233542347-1556276035.png)

查看服务是否开启，重启服务使得配置生效。

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233705441-2088859460.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233715409-1382203488.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233728284-1795342096.png)

尝试连接和使用。

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233827722-607711525.png)
下载可视化管理后台。
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233914738-1851251763.png)


![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233925034-1722354724.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233950909-312239945.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171206233958613-630014964.png)





但是企业中，99%都是在Linux中运用和安装的。Windows中可以自己玩，Linux中才是实战。



```
tar -zxvf redis-4.0.1.tar.gz
```





#### Linux下安装

企业中，99%都是在Linux中运用和安装的。Windows中可以自己玩，Linux中才是实战。

学会linux安装redis很有用。

1.下载copy到opt目录中
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207012507956-1126680614.png)

2.解压
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207012548691-2003056342.png)

```
tar -zxvf redis-4.0.1.tar.gz
```

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207012701191-1956478636.png)



3.进入文件夹下，尝试make。有可能会因为不存在gcc而失败。

GCC是linux下的编译程序，是C程序的编译工具。
```
yum install gcc gcc+c++
```


![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207012740550-739074227.png)


![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207012752847-2121953402.png)


4.make install
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207012855534-995800626.png)


5.make test测试发现需要安装tcl

```
wget http://downloads.sourceforge.net/tcl/tcl8.6.1-src.tar.gz

sudo tar xzvf tcl8.6.1-src.tar.gz -C /usr/local/

cd /usr/local/tcl8.6.1

sudo ./configure

sudo make

sudo make install
```

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013053956-296540241.png)



6.查看安装后的bin目录
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013210894-390712671.png)


7.新建myredis目录，存储配置文件
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013251050-1777147905.png)

8.增加用户名密码配置
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013552925-878099774.png)


9.检查服务是否开启
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013610925-695986788.png)

10.启动服务
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013639363-2137147551.png)


![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013648347-1740039817.png)

11.关闭服务
![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207013930831-1022980102.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207010034644-303544749.png)



**配置外部访问**

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207015942222-215577154.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207015948847-1019898035.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207015955409-680972768.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171207020001034-224763947.png)





-----------------------------

### 杂项基础

```
redis-benchmark -h 192.168.1.66
```

可以进行性能测试。

redis默认16个库，可以通过select index进行切换库。

```
select index
```

切换库

```
keys *
```

获取所有key的内容



```
FLUSHALL 
```

清空所有的库

```
FLUSHDB
```

清空当前的库



面试官，也是把他经常用的知识来问你的。



一个redis字符串value最多可以是512M。

Redis五大数据类型，String、Hash、List、Set（无序集合）、Zset（有序集合）。



掌握一些常用的指令就可以了。不常用的可以查字典。



学语言，就像学语文一样，认识3000多个常用的字就可以了。其他的可以查字典。

```
EXISTS k1
```

判断key值是否存在

活动期间，将热点数据导入到redis中，活动结束后，进行清空。



```
ttl key
```

查看还有多久过期，-1表示永不过期，-2表示已过期。



```
EXPIRE key 时间
```

给key设置生命期限

```
TYPE key
```

查看类型
```
192.168.1.66:6379> lpush mylist 1 2 3 4 5
(integer) 5
192.168.1.66:6379> LRANGE mylist 0 -1
1) "5"
2) "4"
3) "3"
4) "2"
5) "1"
```

查看list



### STRING

```
192.168.1.66:6379> get k1
"v1"
192.168.1.66:6379> append k1 12345
(integer) 7
192.168.1.66:6379> get k1
"v112345"

```

append的使用

```
192.168.1.66:6379> STRLEN k1
(integer) 7
```

获取长度

```
192.168.1.66:6379> set k1 1
OK
192.168.1.66:6379> incr k1
(integer) 2
192.168.1.66:6379> incr k1
(integer) 3
192.168.1.66:6379> get k1
"3"
192.168.1.66:6379> type k1
string

```

incr 设置自增

```
192.168.1.66:6379> decr k1
(integer) 2
192.168.1.66:6379> decr k1
(integer) 1
192.168.1.66:6379> get k1
"1"

```

decr 自减

```
192.168.1.66:6379> get k1
"9"
192.168.1.66:6379> decrby k1 2
(integer) 7
192.168.1.66:6379> decrby k1 2
(integer) 5
192.168.1.66:6379> get k1
"5"

```

跨越式自减decrby

```
192.168.1.66:6379> get k1
"0123456"
192.168.1.66:6379> getrange k1 0 -1
"0123456"
192.168.1.66:6379> getrange k1 0 3
"0123"
```

getrange获取范围数据



```
192.168.1.66:6379> get k1
"0123456"
192.168.1.66:6379> setrange k1 0 xxx
(integer) 7
192.168.1.66:6379> get k1
"xxx3456"

```

setrange 设置内容



```
192.168.1.66:6379> setex k4 10 v4
OK
192.168.1.66:6379> ttl k4
(integer) 4
192.168.1.66:6379> ttl k4
(integer) 3
192.168.1.66:6379> ttl k4
(integer) 1
192.168.1.66:6379> ttl k4
(integer) -2

```

setex 设置key 同时设置存活周期



```
192.168.1.66:6379> setnx k1 v11
(integer) 0
192.168.1.66:6379> get k1 
"xxx3456"
192.168.1.66:6379> setnx k11 v11
(integer) 1
192.168.1.66:6379> get k11
"v11"

```

setnx 只有不存在的时候，才能设置

```
192.168.1.66:6379[1]> mset k1 v1 k2 v2 k3 v3 k4 v4
OK
192.168.1.66:6379[1]> keys *
1) "k3"
2) "k2"
3) "k4"
4) "k1"
```

mset 批量设置

```
192.168.1.66:6379[1]> keys *
1) "k3"
2) "k2"
3) "k4"
4) "k1"
192.168.1.66:6379[1]> msetnx k4 v4 k5 v5
(integer) 0
192.168.1.66:6379[1]> keys *
1) "k3"
2) "k2"
3) "k4"
4) "k1"

```

msetnx 只要有一个失败，全部失败

```
192.168.1.66:6379[1]> keys *
1) "k3"
2) "k2"
3) "k4"
4) "k1"
192.168.1.66:6379[1]> msetnx k4 v4 k5 v5
(integer) 0
192.168.1.66:6379[1]> keys *
1) "k3"
2) "k2"
3) "k4"
4) "k1"
192.168.1.66:6379[1]> msetnx  k5 v5 k6 v6
(integer) 1
192.168.1.66:6379[1]> keys *
1) "k3"
2) "k4"
3) "k5"
4) "k2"
5) "k6"
6) "k1"

```

msetnx 都不存在，才成功





### LIST



```
192.168.1.66:6379> LPUSH list01 1 2 3 4 5
(integer) 5
192.168.1.66:6379> lrange list01 0 -1
1) "5"
2) "4"
3) "3"
4) "2"
5) "1"
192.168.1.66:6379> RPUSH list02 1 2 3 4 5
(integer) 5
192.168.1.66:6379> lrange list02 0 -1
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"

```

> 先进先出队列（拉shi）
>
> 先进后出栈（喝多了，吐了）



```
192.168.1.66:6379> lrange list01 0 -1
1) "5"
2) "4"
3) "3"
4) "2"
5) "1"
192.168.1.66:6379> lpop list01
"5"
192.168.1.66:6379> lrange list01 0 -1
1) "4"
2) "3"
3) "2"
4) "1"

```

lpop 把左侧的先剔除了

> 老师语录：你自己敲一次，胜过听我讲十次。



```
192.168.1.66:6379> lrange list01 0 -1
1) "5"
2) "4"
3) "3"
4) "2"
5) "1"
192.168.1.66:6379> lpop list01
"5"
192.168.1.66:6379> lrange list01 0 -1
1) "4"
2) "3"
3) "2"
4) "1"
192.168.1.66:6379> RPOP list01
"1"
192.168.1.66:6379> lrange list01 0 -1
1) "4"
2) "3"
3) "2"
192.168.1.66:6379> LINDEX list01 2
"2"

```

LINDEX 获取特定的位置的数据



```
192.168.1.66:6379> lrange list01 0 -1
1) "4"
2) "3"
3) "2"
192.168.1.66:6379> llen list01
(integer) 3

```

llen 获取长度

```
192.168.1.66:6379> RPUSH list03 1 1 1 2 2 2 3 3 3 4 4 4 5 6 7
(integer) 15
192.168.1.66:6379> lrem list03 2 3
(integer) 2
192.168.1.66:6379> lrange list03 0 -1
 1) "1"
 2) "1"
 3) "1"
 4) "2"
 5) "2"
 6) "2"
 7) "3"
 8) "4"
 9) "4"
10) "4"
11) "5"
12) "6"
13) "7"

```

lrem 移除多个值

```
192.168.1.66:6379> lrange list03 0 -1
 1) "1"
 2) "1"
 3) "1"
 4) "2"
 5) "2"
 6) "2"
 7) "3"
 8) "4"
 9) "4"
10) "4"
11) "5"
12) "6"
13) "7"
192.168.1.66:6379> LTRIM list03 3 5
OK
192.168.1.66:6379> lrange list03 0 -1
1) "2"
2) "2"
3) "2"

```

LTRIM 从第几个开始，截取到第几个之后赋值给list

```
192.168.1.66:6379> lrange list01 0 -1
1) "4"
2) "3"
3) "2"
192.168.1.66:6379> lrange list02 0 -1
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
192.168.1.66:6379> RPOPLPUSH list01 list02
"2"
192.168.1.66:6379> lrange list02 0 -1
1) "2"
2) "1"
3) "2"
4) "3"
5) "4"
6) "5"

```

RPOPLPUSH 将某个值压入

```
192.168.1.66:6379> lrange list02 0 -1
1) "2"
2) "1"
3) "2"
4) "3"
5) "4"
6) "5"
192.168.1.66:6379> lset list02 0 0
OK
192.168.1.66:6379> lrange list02 0 -1
1) "0"
2) "1"
3) "2"
4) "3"
5) "4"
6) "5"

```

lset 设定特定位置的list值

```
192.168.1.66:6379> LINSERT list02 before 2 java
(integer) 7
192.168.1.66:6379> lrange list02 0 -1
1) "0"
2) "1"
3) "java"
4) "2"
5) "3"
6) "4"
7) "5"
192.168.1.66:6379> LINSERT list02 after 2 php
(integer) 8
192.168.1.66:6379> lrange list02 0 -1
1) "0"
2) "1"
3) "java"
4) "2"
5) "php"
6) "3"
7) "4"
8) "5"
192.168.1.66:6379> LINSERT list03 after 2 php
(integer) 4
192.168.1.66:6379> lrange list03 0 -1
1) "2"
2) "php"
3) "2"
4) "2"
192.168.1.66:6379> LINSERT list03 before 2 php
(integer) 5
192.168.1.66:6379> lrange list03 0 -1
1) "php"
2) "2"
3) "php"
4) "2"
5) "2"

```

LINSERT 在特定位置插入内容，默认查找出第一个作为参照。

### SET

```
192.168.1.66:6379> sadd set01 1 1 2 2 3 3
(integer) 3
192.168.1.66:6379> SMEMBERS set01 
1) "1"
2) "2"
3) "3"

```

set 也是集合，但是不允许有重复的

```
192.168.1.66:6379> SISMEMBER set01 1
(integer) 1
192.168.1.66:6379> SISMEMBER set01 x
(integer) 0

```

sismember查看是否是成员

```
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "3"
192.168.1.66:6379> SCARD set01
(integer) 3

```

scard 查看集合中有多少个元素



```
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "3"
192.168.1.66:6379> SCARD set01
(integer) 3
192.168.1.66:6379> srem set01 3
(integer) 1
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"

```

srem 删除某个元素



```
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
192.168.1.66:6379> sadd set01 1 2 3 4 5 6 7
(integer) 5
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
6) "6"
7) "7"

```

set的好处就是自动去重，保证数据的唯一性

```
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
6) "6"
7) "7"
192.168.1.66:6379> SRANDMEMBER set01 3
1) "6"
2) "7"
3) "2"
192.168.1.66:6379> SRANDMEMBER set01 3
1) "7"
2) "2"
3) "4"
192.168.1.66:6379> SRANDMEMBER set01 3
1) "3"
2) "7"
3) "1"
192.168.1.66:6379> SRANDMEMBER set01 3
1) "5"
2) "2"
3) "4"

```

SRANDMEMBER 随机出三个数字

```
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
6) "6"
7) "7"
8) "8"
9) "9"
192.168.1.66:6379> spop set01 2
1) "4"
2) "3"
192.168.1.66:6379> spop set01 2
1) "5"
2) "6"
192.168.1.66:6379> spop set01 2
1) "8"
2) "9"
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "7"

```

spop 随机出栈，高并发，速度快

```
192.168.1.66:6379> SMEMBERS set01
1) "1"
2) "2"
3) "7"
192.168.1.66:6379> SMEMBERS set02
1) "z"
2) "y"
3) "x"
192.168.1.66:6379> smove set01 set02 1
(integer) 1
192.168.1.66:6379> SMEMBERS set01
1) "2"
2) "7"
192.168.1.66:6379> SMEMBERS set02
1) "z"
2) "y"
3) "x"
4) "1"

```

smove 移动值



```
192.168.1.66:6379> SMEMBERS set01 
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
192.168.1.66:6379> SMEMBERS set02 
1) "a"
2) "3"
3) "2"
4) "1"
5) "b"
192.168.1.66:6379> sdiff set01 set02
1) "4"
2) "5"
192.168.1.66:6379> sdiff set02 set01
1) "a"
2) "b"


```

sdiff 找出set01中比set02中多出的内容（差集）

```
192.168.1.66:6379> SMEMBERS set01 
1) "1"
2) "2"
3) "3"
4) "4"
5) "5"
192.168.1.66:6379> SMEMBERS set02 
1) "a"
2) "3"
3) "2"
4) "1"
5) "b"
192.168.1.66:6379> sdiff set01 set02
1) "4"
2) "5"
192.168.1.66:6379> sdiff set02 set01
1) "a"
2) "b"
192.168.1.66:6379> SINTER set01 set02
1) "1"
2) "2"
3) "3"
192.168.1.66:6379> SUNION set01 set02
1) "a"
2) "3"
3) "5"
4) "b"
5) "4"
6) "2"
7) "1"

```

SINTER 交集 SUNION 并集（去重）

> 万丈高楼平地起，肚子里要有货
>
> 学以致用，学在用前



### Hash 哈希 （非常，及其重要，非常及其重要）

> kv模式不变，但是v是一个键值对

```
192.168.1.66:6379> hset user id 11
(integer) 1
192.168.1.66:6379> hget user id
"11"
192.168.1.66:6379> keys *
1) "user"

```

hset hget基本使用

```
192.168.1.66:6379> hmset customer id 11 name li4 age 26
OK
192.168.1.66:6379> hmget customer id name age
1) "11"
2) "li4"
3) "26"

```

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171208140049031-1789373739.png)

hmset hmget 的使用

```
192.168.1.66:6379> hgetall customer
1) "id"
2) "11"
3) "name"
4) "li4"
5) "age"
6) "26"

```

hgetall 获取全部的键值对数据

```
192.168.1.66:6379> hdel customer age
(integer) 1
192.168.1.66:6379> hgetall customer
1) "id"
2) "11"
3) "name"
4) "li4"

```

hdel 删除某个键值

```
192.168.1.66:6379> HLEN customer
(integer) 2
192.168.1.66:6379> HEXISTS customer id
(integer) 1
192.168.1.66:6379> HEXISTS customer email
(integer) 0

```

HLEN 查看长度，HEXISTS 查看是否存在

> 横向关联之后，其实发现没什么新技术，都是你抄我的，我抄你的

```
redis-cli -h 192.168.1.66 -a 123456
```

直接连接redis，密码也加入了，不需要再次密码验证了

```
192.168.1.66:6379> HKEYS customer
1) "id"
2) "name"
192.168.1.66:6379> HVALS customer
1) "11"
2) "li4"

```

HKEYS 获取共有多少个key，HVALS 获取值

```
192.168.1.66:6379> HVALS customer
1) "11"
2) "li4"
3) "18"
192.168.1.66:6379> HINCRBY customer age 2
(integer) 20
192.168.1.66:6379> HINCRBY customer age 2
(integer) 22
192.168.1.66:6379> HINCRBY customer age 2
(integer) 24
192.168.1.66:6379> HVALS customer
1) "11"
2) "li4"
3) "24"

```

HINCRBY 设置某个值增长

```
192.168.1.66:6379> hset customer score 92
(integer) 1
192.168.1.66:6379> HVALS customer
1) "11"
2) "li4"
3) "24"
4) "92"
192.168.1.66:6379> HINCRBYFLOAT customer score 0.5
"92.5"
192.168.1.66:6379> HVALS customer
1) "11"
2) "li4"
3) "24"
4) "92.5"

```

HINCRBYFLOAT 增加浮点数数值



### ZSet（有序集合）

zset，在set的基础上加了一个score的值。

知识是基础，基础之上是业务，掌握知识，分析业务，开发项目。

```
192.168.1.66:6379> zadd zset01 60 v1 70 v2 80 v3 90 v4 100 v5
(integer) 5
192.168.1.66:6379> ZRANGE zset01 0 -1 
1) "v1"
2) "v2"
3) "v3"
4) "v4"
5) "v5"
192.168.1.66:6379> ZRANGE zset01 0 -1 withscores
 1) "v1"
 2) "60"
 3) "v2"
 4) "70"
 5) "v3"
 6) "80"
 7) "v4"
 8) "90"
 9) "v5"
10) "100"

```

zadd zrange 

```
192.168.1.66:6379> ZRANGEBYSCORE zset01 60 90
1) "v1"
2) "v2"
3) "v3"
4) "v4"

```

ZRANGEBYSCORE 按分数范围查找

```
192.168.1.66:6379> ZRANGEBYSCORE zset01 60  (90
1) "v1"
2) "v2"
3) "v3"
192.168.1.66:6379> ZRANGEBYSCORE zset01 (60  (90
1) "v2"
2) "v3"

```

```
192.168.1.66:6379> ZREM zset01 v5
(integer) 1
192.168.1.66:6379> ZRANGE zset01 0 -1 
1) "v1"
2) "v2"
3) "v3"
4) "v4"

```

ZREM 删除某个元素

```
192.168.1.66:6379> zcard zset01
(integer) 4
192.168.1.66:6379> zcount zset01 60 80
(integer) 3
192.168.1.66:6379> zrank zset01 v4
(integer) 3
192.168.1.66:6379> zscore zset01 v4
"90"

```

zcard获取数量，zcount获取 范围数量，zrank获取key zscore 获取分数

```
192.168.1.66:6379> ZREVRANK zset01 v4
(integer) 0
```

ZREVRANK 逆序获取下标值

```
192.168.1.66:6379> ZRANGE zset01 0 -1 
1) "v1"
2) "v2"
3) "v3"
4) "v4"
192.168.1.66:6379> ZREVRANGE zset01 0 -1 
1) "v4"
2) "v3"
3) "v2"
4) "v1"

```

ZREVRANGE 逆序获取数据





------



在linux下，配置大于编码。

redis采用的是单进程多线程的模式。当redis.conf中选项daemonize设置成yes时，代表开启守护进程模式。在该模式下，redis会在后台运行，并将进程pid号写入至redis.conf选项pidfile设置的文件中，此时redis将一直运行，除非手动kill该进程。但当daemonize选项设置成no时，当前界面将进入redis的命令行界面，exit强制退出或者关闭连接工具(putty,xshell等)都会导致redis进程退出。
服务端开发的大部分应用都是采用后台运行的模式。

> 周阳语录：老员工，需要新兵蛋子能够成为得力助手。知识充足，才能更好的跟着老员工交流和玩耍。

在linux下输入错误的命令，退不出来要怎么办？

答案：按ctrl+c ，或者ctrl+d 退出。

热点、常用的查询数据，放入redis中。

### redis持久化（重点）

RDB(Redis DataBase)

AOF(Append Only File)

> 周阳语录：能撑过面试经理头一分钟最重要。头一分钟，决定人家还是否想跟你继续聊下去。

RDB就是在指定的时间内，将内存中的数据集写入磁盘。恢复时，将快照文件直接读到内存。

> 周阳语录：一定要跟上老员工的脚步，跟上了，人家才带你玩。想进步，就要有人带，就要跟对人。

save命令会强制备份，flushall也会强制备份！生成dump.rdb文件！

正常情况下，备份的机器和生产的机器不是同一个机器！

正常情况下，备份和恢复工作，或升级系统都在凌晨去处理！

rdb适合大规模的文件恢复，但是对于数据的完整性和一致性要求不高。

意外down掉的话，就会丢失最后一次快照。

新技术的出现，一定会借鉴老技术，并弥补老技术的不足。新技术是老技术的子集。AOF就这样诞生了！

AOF，记录所有的写操作语句。

```
df -h
```

查看磁盘空间。

AOF是以日志的形式记录每个写操作。将Redis执行过的所有写操作指令记录下来，只允许追加文件。redis启动之初会读取该文件重新构建数据，以完成数据恢复工作。

AOF保存的是appendonly.aof文件。

主从复制，读写分离比AOF更牛逼。

AOF和RDB是否可以同时存在？可以同时共同，但是如果开启AOF，优先查找AOF恢复数据，如果AOF出现数据错误，将无法启动REDIS服务。

```
redis-check-aof --fix appendonly.aof
```

可以修复出问题的aof文件！

> 周阳语录：面试老师通常都是一个大问题，下面跟一堆小问题。层层推进。

```
free -m
```

实用指令查看linux系统内存实用情况！

> 周阳语录：程序员三级，高级升职加薪，中级加薪不升职，低级老黄牛，只有苦劳。

Rewrite是什么，AOF采用文件追加方式，导致文件会越来越大。新增了重写机制，当AOF文件的大小超过所设定的阙值时，Redis就会启动AOF文件的内容压缩，只保留可以恢复数据的最小指令集。可以使用指令bgrewriteaof。

> 周阳语录：PPT、文档、脑图都是软实力的体现。逻辑清晰，条理分明，口齿伶俐。

Redis会记录上次重写时的AOF的大小，默认配置是当AOF文件大小是上次Rewrite后大小的一倍且大于64M时触发。

> 周阳语录：学技术要多跟大牛接触。大牛也是牛某个方面的。他们牛在于，他们有那个环境，去提升！事成就人，没有事就自己创造事。



--------------------------------------------------

#### redis事务

**是什么**

可以一次执行多个命令，本质是一组命令的集合。一个事务中的所有命令都会序列化，不许加塞！

可以一口气攒着，不需要立刻知道结果。但是一定要确保数据的准确性！分红就是这样的！

排好队，一次性的执行多个redis的命令！

**能干嘛**

一个队列中，一次性的、顺序性的、排他性的执行一系列的命令。要么一起成功，要么一起失败。

**怎么玩**

通过**MULTI**指令开启，之后输入多个命令！Redis将它们加入到队列当中，所有的命令通过**EXEC**来开启执行！

通过**DISCARD**来放弃本次的批处理操作！

例子：银行转账，要么成功，要么失败。

```
192.168.1.66:6379> MULTI
OK
192.168.1.66:6379> set k1 v1
QUEUED
192.168.1.66:6379> set k2 v2
QUEUED
192.168.1.66:6379> set k3 v3
QUEUED
192.168.1.66:6379> set k4 v4
QUEUED
192.168.1.66:6379> get k2
QUEUED
192.168.1.66:6379> EXEC
1) OK
2) OK
3) OK
4) OK
5) "v2"

```

好比购物先加入购物车，最后EXEC统一结账。

```
192.168.1.66:6379> MULTI
OK
192.168.1.66:6379> set k1 11
QUEUED
192.168.1.66:6379> set k2 22
QUEUED
192.168.1.66:6379> set k3 33
QUEUED
192.168.1.66:6379> DISCARD
OK
192.168.1.66:6379> get k1 
"v1"

```

DISCARD 撤销所有操作！

```
192.168.1.66:6379> MULTI
OK
192.168.1.66:6379> set k1 v1
QUEUED
192.168.1.66:6379> set k2 v2
QUEUED
192.168.1.66:6379> getset k3
(error) ERR wrong number of arguments for 'getset' command
192.168.1.66:6379> set k4 v4
QUEUED
192.168.1.66:6379> EXEC
(error) EXECABORT Transaction discarded because of previous errors.

```

加入时只要有一个出错误，统统的不执行！

> 周阳语录:年轻的时候，就是练级打怪的时候，勇敢的上！挑战自己！30以前不要怕，30岁以后不要悔！有机会就跳进去干！

```
192.168.1.66:6379> set k1 1
OK
192.168.1.66:6379> set k2 2
OK
192.168.1.66:6379> set k3 3
OK
192.168.1.66:6379> set k4 4
OK
192.168.1.66:6379> MULTI
OK
192.168.1.66:6379> incr k1 
QUEUED
192.168.1.66:6379> decr k2
QUEUED
192.168.1.66:6379> EXEC
1) (integer) 2
2) (integer) 1
192.168.1.66:6379> get k1
"2"
192.168.1.66:6379> get k2
"1"

```

k1增加了，k2减小了！通过事物处理，妥妥的不出错！

```
192.168.1.66:6379> set k1 v1
OK
192.168.1.66:6379> set k2 v2
OK
192.168.1.66:6379> set k3 v3
OK
192.168.1.66:6379> set k4 v4
OK
192.168.1.66:6379> MULTI
OK
192.168.1.66:6379> incr k1
QUEUED
192.168.1.66:6379> set k2 22
QUEUED
192.168.1.66:6379> set k3 33
QUEUED
192.168.1.66:6379> set k4 44
QUEUED
192.168.1.66:6379> get k4
QUEUED
192.168.1.66:6379> EXEC
1) (error) ERR value is not an integer or out of range
2) OK
3) OK
4) OK
5) "44"
```

加入队列时不出错，下面的都将正常运行，执行时出错不影响其他语句！

**Watch监控** 重要

悲观锁、乐观锁、CAS（check and set）

行锁，表锁，并发性与一致性的对立！表锁，并发性及其差，但是一致性非常好！

工作中，正常用乐观锁！并发性会更好！

悲观锁每次拿数据的时候都会上锁（行锁，表锁）。并发性差！

乐观锁，每次去拿数据不会上锁，但是更新的时候，使用版本号机制。判断一下在此期间别人有没有去更新这个数据。

乐观锁策略：提交版本必须大于记录当前版本才能执行更新。

一旦执行了exec之前加的监控锁都会被取消掉！

Watch指令类似于乐观锁！如果key值已经被客户端改变，整个事务队列都不会被执行！把最新的数据拿下来，再次执行！

开启，入队，执行。（事务的三个阶段）

------------------------------------------------------

**主从复制，读写分离** Master/Slave

**是什么**

master写入

slave读取

**能干嘛**

读写分离，更加安全，性能提升

**怎么玩**

一主二仆、薪火相传、反客为主

> 周明老师，能够把长篇大论总结的很精辟。

1. 配从不配主
2. slaveof 主库ip 主库端口

准备三台机器

一主，二从

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171212132518691-1777562429.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171212132522660-1746428185.png)

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171212132526816-836478889.png)



66是主机，61、62作为从机。

通过info replication 进行查看身份。

```
192.168.1.66:6379> info replication
# Replication
role:master
connected_slaves:0
master_replid:ba9a0c9d5cbeb6f7ce375b4c3559f5e848fc7025
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

```

设置61、62跟随66

```
192.168.1.61:6379> slaveof 192.168.1.66 6379
OK
192.168.1.61:6379> info replication
# Replication
role:slave
master_host:192.168.1.66
master_port:6379
master_link_status:down
master_last_io_seconds_ago:-1
master_sync_in_progress:0
slave_repl_offset:1
master_link_down_since_seconds:1513056594
slave_priority:100
slave_read_only:1
connected_slaves:0
master_replid:ba9a0c9d5cbeb6f7ce375b4c3559f5e848fc7025
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

```

```
192.168.1.62:6379> slaveof 192.168.1.66 6379
OK
192.168.1.62:6379> info replication
# Replication
role:slave
master_host:192.168.1.66
master_port:6379
master_link_status:down
master_last_io_seconds_ago:-1
master_sync_in_progress:0
slave_repl_offset:1
master_link_down_since_seconds:1513056636
slave_priority:100
slave_read_only:1
connected_slaves:0
master_replid:ff1f0f120165c6673a797e65aa0d82e3ccbe9a6c
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0

```

> tips:MASTER aborted replication with an error: NOAUTH Authentication required. 出现了这个错误。需要从服务器中添加配置。masterauth 123456 (123456是主redis的密码，此参数是当与主连接时的密码验证)

设置了主从复制之后，此时在主机中，

```
192.168.1.66:6379> set k4 v4
OK
```

在从机中查看，

```
192.168.1.61:6379> get k4
"v4"
```

```
192.168.1.62:6379> get k4
"v4"

```

只要变为从机，主机中数据都会被弄过来！

> 周阳老师语录：学的不是指令，而是探寻知识的过程！指令分分钟讲完！但是思考知识更重要！
>
> 不停的破坏，不停的做实验，不停的尝试！折腾！才能更好的理解知识！



> 周明老师语录：读书或者看视频，产生争议和思考了，比不思考要有收获。带着思考学习，带着问题读书。

在主从复制中，如果主机宕机了，从机还是从机！原地待命中！

主机恢复之后，主从体系不会被破坏！



薪火相传 66 传61，61传62

```
192.168.1.66:6379> info replication
# Replication
role:master
connected_slaves:1
slave0:ip=192.168.1.61,port=6379,state=online,offset=3288,lag=1
master_replid:dddb7b383d4153816d28377f65c6ed7d688ac8bf
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:3288
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:3288

```



```
192.168.1.61:6379> info replication
# Replication
role:slave
master_host:192.168.1.66
master_port:6379
master_link_status:up
master_last_io_seconds_ago:7
master_sync_in_progress:0
slave_repl_offset:6197
slave_priority:100
slave_read_only:1
connected_slaves:1
slave0:ip=192.168.1.62,port=6379,state=online,offset=6197,lag=0
master_replid:dddb7b383d4153816d28377f65c6ed7d688ac8bf
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:6197
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:573
repl_backlog_histlen:5625

```



```
192.168.1.62:6379> info replication
# Replication
role:slave
master_host:192.168.1.61
master_port:6379
master_link_status:up
master_last_io_seconds_ago:3
master_sync_in_progress:0
slave_repl_offset:5931
slave_priority:100
slave_read_only:1
connected_slaves:0
master_replid:dddb7b383d4153816d28377f65c6ed7d688ac8bf
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:5931
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:5819
repl_backlog_histlen:113


```

注意了，master_link_status:up表示成功，master_link_status:down表示失败。原因可能是主机的端口号没有打开！

```
iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 6379 -j ACCEPT
```



反客为主命令

```
192.168.1.61:6379> SLAVEOF no one
OK
192.168.1.61:6379> set k11 v11
OK
```

```
192.168.1.62:6379> get k11
"v11"
192.168.1.62:6379> set k12 v12
(error) READONLY You can't write against a read only slave.
```

前提是，你下面要有小弟，你才能反客为主！



主从复制，第一次会全量复制，之后是增量复制。只要重新连接master，都会执行一次全量复制。



哨兵模式，反客为主的自动版本！主机挂了，会自动从从机中选择一个牛人，作为新的主机。在哨兵模式中，主机回归之后，变成从机了。

**怎么玩**

在从机中新建一个哨兵配置sentinel.conf

```
sentinel monitor mymaster 192.168.1.61 6379 1
sentinel auth-pass mymaster 123456
```

开启哨兵监控！

```
redis-sentinel /myredis/sentinel.conf 
```

```

[root@localhost bin]# redis-sentinel /myredis/sentinel.conf 
4880:X 12 Dec 16:15:34.969 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
4880:X 12 Dec 16:15:34.969 # Redis version=4.0.1, bits=64, commit=00000000, modified=0, pid=4880, just started
4880:X 12 Dec 16:15:34.969 # Configuration loaded
4880:X 12 Dec 16:15:34.970 * Increased maximum number of open files to 10032 (it was originally set to 1024).
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 4.0.1 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                   
 (    '      ,       .-`  | `,    )     Running in sentinel mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 26379
 |    `-._   `._    /     _.-'    |     PID: 4880
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           http://redis.io        
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

4880:X 12 Dec 16:15:34.973 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
4880:X 12 Dec 16:15:34.992 # Sentinel ID is 5bdc4c724103019a7d987848ce6a8af91341ee1d
4880:X 12 Dec 16:15:34.992 # +monitor master mymaster 192.168.1.66 6379 quorum 1
4880:X 12 Dec 16:15:46.522 * +slave slave 192.168.1.61:6379 192.168.1.61 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:15:46.593 * +slave slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:16:16.655 # +sdown slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.014 # +sdown master mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.014 # +odown master mymaster 192.168.1.66 6379 #quorum 1/1
4880:X 12 Dec 16:17:02.014 # +new-epoch 1
4880:X 12 Dec 16:17:02.014 # +try-failover master mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.024 # +vote-for-leader 5bdc4c724103019a7d987848ce6a8af91341ee1d 1
4880:X 12 Dec 16:17:02.024 # +elected-leader master mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.024 # +failover-state-select-slave master mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.125 # +selected-slave slave 192.168.1.61:6379 192.168.1.61 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.125 * +failover-state-send-slaveof-noone slave 192.168.1.61:6379 192.168.1.61 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:02.184 * +failover-state-wait-promotion slave 192.168.1.61:6379 192.168.1.61 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:03.085 # +promoted-slave slave 192.168.1.61:6379 192.168.1.61 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:03.085 # +failover-state-reconf-slaves master mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:03.184 * +slave-reconf-sent slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:03.184 # +failover-end master mymaster 192.168.1.66 6379
4880:X 12 Dec 16:17:03.184 # +switch-master mymaster 192.168.1.66 6379 192.168.1.61 6379
4880:X 12 Dec 16:17:03.185 * +slave slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.61 6379
4880:X 12 Dec 16:17:03.185 * +slave slave 192.168.1.66:6379 192.168.1.66 6379 @ mymaster 192.168.1.61 6379
4880:X 12 Dec 16:17:33.238 # +sdown slave 192.168.1.66:6379 192.168.1.66 6379 @ mymaster 192.168.1.61 6379
4880:X 12 Dec 16:17:33.238 # +sdown slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.61 6379
4880:X 12 Dec 16:22:14.045 # -sdown slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.61 6379
4880:X 12 Dec 16:25:14.815 * +fix-slave-config slave 192.168.1.62:6379 192.168.1.62 6379 @ mymaster 192.168.1.61 6379

```

哨兵配置文件可以放在任意一个从服务器中。



> 周阳语录：这些牛逼的技术，公司不一定让你去做，但是你要懂！懂了才有机会去做！

主从复制的缺点，是有一定的延迟，主数据更新到从数据库有一定的延迟。

-------------------------------------

jedis 操作redis

```java
package com.company;
import redis.clients.jedis.Jedis;

public class Main {

    public static void main(String[] args) {
	    // write your code here
        Jedis jedis = new Jedis("192.168.0.66",6379);
        jedis.auth("123456");
        System.out.println(jedis.ping());
    }
}
```



```java
package com.company;
import redis.clients.jedis.Jedis;

public class TestAPI {

    public static void main(String[] args) {
        // write your code here
        Jedis jedis = new Jedis("192.168.0.66",6379);
        jedis.auth("123456");

        jedis.set("k1","v1");
        jedis.set("k2","v2");
        jedis.set("k3","v3");
        jedis.set("k4","v4");
        jedis.set("k5","v5");


        System.out.println(jedis.get("k5"));
    }
}

```

> 获取数据，通常这些工作不是由java程序员处理。而是由运维人员处理。将热点高频数据，灌入redis数据库中。





































