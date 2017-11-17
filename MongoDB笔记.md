####基本概念

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
sc.exe create MongoDB binPath= "E:\MongoDB\Server\bin\mongod.exe --service --config=\"E:\MongoDB\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"  
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

------------------------------------------------------------------------

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

  ```
  var deptData = {
          "deptno":20,
          "dname":"研发部",
          "loc":"深圳",
          "count":20,
          "avg":8000.0
      };
  db.dept.insert(deptData);
  ```

  ![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117120224609-1663303948.png)

mongo里面没有查看集合结构的操作，因为集合的结构是没有规则的。

* 关于ID的问题

  组成：时间戳+机器码+PID+计数器

* 查看第一个,删除数据

  ```
  db.dept.findOne();
  ```

  ```
  db.dept.remove({"_id":ObjectId("5a0e4aeb24a45ab4ab1259da")});
  ```

  ​

* 修改数据

  ```
  var deptData = {
          "deptno":50,
          "dname":"乞讨部",
          "loc":"家里蹲",
          "count":20,
          "avg":8000.0
      };
  db.dept.update({"_id":ObjectId("5a0e5f1424a45ab4ab1259db")},deptData);
  ```

  ​

* 删除集合

  db.集合名称.drop();

* 删除数据库，在哪个数据库下执行，就会删除哪个数据库

  ```
  db.dropDatabase()
  ```

  ---------------------------------------------

#### 数据操作（重点）

MongoDB中出了增加之外，其他的操作都很麻烦。

* 数据增加

  **例子**:

  1.简单的

  ```
  db.infos.insert({"url":"www.baidu.com"});
  ```

  2.数组，将插入多条数据

  ```
  db.infos.insert([{"url":"www.baidu.com"},{"url":"www.sina.com"},{"url":"www.taobao.com"}]);
  ```

  mongo中，查询多条数据，竟然可以使用JavaScript进行循环操作。简直威武。

  ```
  for (var x = 0 ;x<10;x++) {
      db.infos.insert({"url":"mldn - " + x});
  }
  ```

  ​

  ![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117140337921-1601357481.png)

* 数据查询

  ​

```
db.infos.find();
```

```
db.infos.find({"url":"www.baidu.com"});
```

id不要显示出来

```
db.infos.find({"url":"www.baidu.com"},{"_id":0});
```

##### **关系运算**  

大于\$gt 小于 \$lt 大于等于\$gte 小于等于\$lte 不等于 \$ne

准备测试数据

```js
db.students.insert({"name":"张三","sex":"男","age":19,"score":89,"address":"海淀区"});
db.students.insert({"name":"李四","sex":"女","age":20,"score":59,"address":"朝阳区"});
db.students.insert({"name":"王五","sex":"女","age":19,"score":99,"address":"西城区"});
db.students.insert({"name":"赵六","sex":"男","age":20,"score":100,"address":"东城区"});
db.students.insert({"name":"孙七","sex":"男","age":19,"score":20,"address":"海淀区"});
db.students.insert({"name":"王八","sex":"女","age":21,"score":0,"address":"海淀区"});
db.students.insert({"name":"刘九","sex":"男","age":19,"score":70,"address":"朝阳区"});
db.students.insert({"name":"钱十","sex":"女","age":21,"score":56,"address":"西城区"});

```



查询姓名为张三的学生的数据

```
db.students.find({"name":"张三"});
```

查询性别是男的学生的信息

```
db.students.find({"sex":"男"});
```

查询年龄大于19岁的学生

```
db.students.find({"age":{"$gt":19}});
```

查询成绩大于等于60分的学生

```
db.students.find({"score":{"$gte":60}});
```

查询姓名不是王五的信息

```
db.students.find({"name":{"$ne":"王五"}});
```

**逻辑运算**

三种类型 与 \$and 或 \$or  非\$nor

查询年龄在19到20之间的数据

```
db.students.find({"age":{"$gte":19,"$lte":20}});
```

查询年龄不是19的数据

```
db.students.find({"age":{"$ne":19}});
```

查询年龄大于19岁，或者成绩大于90分的学生的信息

```
db.students.find({
    "$or": [
        {"age":{"$gt":19}},
        {"score":{"$gt":90}}
    ]
    });

```

查询年龄不大于19或者成绩不大于90的学生的信息

```
db.students.find({
    "$nor": [
        {"age":{"$gt":19}},
        {"score":{"$gt":90}}
    ]
    });

```

**模运算**

查询年龄模20余1的数据，也就是21或者41的学生信息

```
db.students.find({"age":{"$mod":[20,1]}});
```



![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117152802749-2071170216.png)

**范围查询**

\$in 、\$nin

查询姓名是“张三”、“李四”、“王五”的信息。

多个数据用数组表示。

```
db.students.find({"name":{"$in":["张三","李四","王五"]}})
```

```
db.students.find({"name":{"$nin":["张三","李四","王五"]}})
```



**数组查询**

mongoDB支持数组保存，也支持数组匹配查询。

再插入一些数据

```
db.students.insert({"name":"大神 - A","sex":"女","age":21,"score":0,"address":"海淀区","course":["语文","数学","英语","音乐","政治"]});
db.students.insert({"name":"大神 - B","sex":"男","age":19,"score":70,"address":"朝阳区","course":["语文","数学"]});
db.students.insert({"name":"大神 - C","sex":"女","age":21,"score":56,"address":"西城区","course":["语文","数学","英语"]});
db.students.insert({"name":"大神 - D","sex":"女","age":21,"score":0,"address":"海淀区","course":["语文","数学","英语"]});
db.students.insert({"name":"大神 - E","sex":"男","age":19,"score":70,"address":"朝阳区","course":["英语","音乐"]});
db.students.insert({"name":"大神 - F","sex":"女","age":21,"score":56,"address":"西城区","course":["语文","数学","英语","音乐"]});
```

查询同时参加语文和数学课程的学生



```
db.students.find({"course":{"$all":["语文","数学"]}});
```

\$all 可以用在数组查询上，也可以用于一个数据的匹配上。

查询地址是“海淀区”的信息。

```
db.students.find({"address":{"$all":["海淀区"]}});
```

例子：查询课程数组中第二个内容是音乐的用户。使用索引。

```
db.getCollection('students').find({"course.1":"音乐"})
```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117164907359-398577687.png)

范例：查询只参加两门课程的学生

```
db.getCollection('students').find({"course":{"$size":2}})
```





![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117165130265-1853899545.png)



范例：返回年龄为19岁的学生信息，课程信息只返回两条。

```
db.getCollection('students').find({"age":21},{"course":{"$slice":2}})
```

也可以设置负数，取出后两门的数据。

```
db.getCollection('students').find({"age":21},{"course":{"$slice":-2}})
```

或者只取出中间部分的信息。

