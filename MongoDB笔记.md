### 基本概念

MongoDB直接存储JSON。



有了NoSQL数据库之后，可以直接在业务层将数据按照指定的结构进行存储。



|  NO  | SQL  | NoSQL           |
| :--: | :--- | --------------- |
|  1   | 数据库  | 数据库             |
|  2   | 表    | 集合              |
|  3   | 行    | 文档              |
|  4   | 列    | 成员              |
|  5   | 主键   | Object ID(自动维护) |



MongoDB跟Node.js捆绑在一起了（taobao用了Node.js）。



面向集合存储，支持索引，支持短暂保留，基于BSON应用。支持python、.net、php等。



MongoDB集合传统的mysql或者其他关系型数据库一起使用。

#### 安装配置

安装Mongo到E盘，创建mongod.cfg配置文件，设置MongoDB服务，启动MongoDB，关闭MongoDB服务。

```ini
systemLog:
 destination: file
 path: E:\MongoDB\data\log\mongod.log
storage:
 dbPath: E:\MongoDB\data\db
```

```
sc.exe create MongoDB binPath="E:\MongoDB\Server\bin\mongod.exe --service --config=\"E:\MongoDB\mongod.cfg\"" DisplayName="MongoDB" start="auto"
```

```
net start MongoDB 
```

```
net stop MongoDB  
```



更多的配置案例

```ini
systemLog:  
    quiet: false  
    path: E:\MongoDB\data\log\mongod.log  
    logAppend: false  
    destination: file  
processManagement:  
    fork: true  
    pidFilePath: E:\MongoDB\data\mongod.pid  
net:  
    bindIp: 127.0.0.1  
    port: 27017  
    maxIncomingConnections: 65536  
    wireObjectCheck: true  
    ipv6: false   
storage:  
    dbPath: E:\MongoDB\data\db 
    indexBuildRetry: true  
    journal:  
        enabled: true  
    directoryPerDB: false  
    engine: mmapv1  
    syncPeriodSecs: 60   
    mmapv1:  
        quota:  
            enforced: false  
            maxFilesPerDB: 8  
        smallFiles: true      
        journal:  
            commitIntervalMs: 100  
    wiredTiger:  
        engineConfig:  
            cacheSizeGB: 8  
            journalCompressor: snappy  
            directoryForIndexes: false    
        collectionConfig:  
            blockCompressor: snappy  
        indexConfig:  
            prefixCompression: true  
operationProfiling:  
    slowOpThresholdMs: 100  
    mode: off  
```





![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117092254984-1193540.png)

当MongoDB服务启动之后，可以使用mongo命令来连接。

```
mongo
```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117092322671-1825125872.png)



在浏览器中查看默认的端口是27017

```
http://127.0.0.1:27017/
```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117092555796-2137916447.png)

通过可视化工具连接测试

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117092825437-619987408.png)



显示数据库

```
show databases;
```

通过端口号启动

```
mongo --port=27017
```



#### 操作MongoDB

* 使用库

```
use mldn;
```

这个时候并不创建。

* 创建集合

```
db.createCollection("emp");
```

这个时候才创建库mldn。



* 查询数据

```sql
db.emp.find();
```

* 创建并插入数据

```
db.dept.insert({"deptno":10,"dname":"财务部","loc":"北京"});
```

这个时候会自动创建dept集合并且插入一条数据

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117103601874-286872049.png)

* 查看集合

```
show collections
```

* 增加不规则的数据
* ​