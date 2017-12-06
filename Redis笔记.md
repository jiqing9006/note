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































