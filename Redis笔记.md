Memcache专注缓存



KV                // KEY VALUE

Cache          // 缓存

Persistence // 持久层



冷数据，存储在关系型数据库中（mysql）。

商品描述、详情、评价等信息存储在文档类数据库中（mongodb）。

商品图片存储在分布式文件系统，如Hadoop的HDFS中。

商品的关键字ISearch。

高频词汇热点信息（Tair、Redis、Memcache）内存数据库。

商品的交易，价格计算，积分累计（外部系统，第三方支付接口）。

面向接口编程，来解决多数据源多数据类型问题（统一数据服务层）。













