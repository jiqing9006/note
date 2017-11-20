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

  ​

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

**范例**：查询课程数组中第二个内容是音乐的用户。使用索引。

```
db.getCollection('students').find({"course.1":"音乐"})
```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117164907359-398577687.png)

**范例**：查询只参加两门课程的学生

```
db.getCollection('students').find({"course":{"$size":2}})
```





![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117165130265-1853899545.png)



**范例**：返回年龄为19岁的学生信息，课程信息只返回两条。

```
db.getCollection('students').find({"age":21},{"course":{"$slice":2}})
```

也可以设置负数，取出后两门的数据。

```
db.getCollection('students').find({"age":21},{"course":{"$slice":-2}})
```

或者只取出中间部分的信息。

```
db.getCollection('students').find({"age":21},{"course":{"$slice":[1,2]}})
```

**嵌套集合运算**

再增加一些数据

```js
db.students.insert({"name":"高大拿 - A","sex":"女","age":21,"score":0,"address":"海淀区","course":["语文","数学","英语","音乐","政治"],
    "parents":
        [{"name":"高大拿 - A(父亲)","age":50,"job":"工人"},
        {"name":"高大拿 - A(母亲)","age":46,"job":"职员"}]
    });
db.students.insert({"name":"高大拿 - B","sex":"男","age":19,"score":70,"address":"朝阳区","course":["语文","数学"],
    "parents":
        [{"name":"高大拿 - B(父亲)","age":50,"job":"处长"},
        {"name":"高大拿 - B(母亲)","age":46,"job":"局长"}]
    });
db.students.insert({"name":"高大拿 - C","sex":"女","age":21,"score":56,"address":"西城区","course":["语文","数学","英语"],
    "parents":
        [{"name":"高大拿 - C(父亲)","age":50,"job":"工人"},
        {"name":"高大拿 - C(母亲)","age":46,"job":"局长"}]
    });


```

范例：查询年龄是19，父母中有职务是局长的数据

````
db.getCollection('students').find({
    "$and":[
        {"age":19},
        {"parents":{"$elemMatch":{"job":"局长"}}}
    ]
    })


````

**判断某个字段是否存在**

通过\$exists来判断某个字段是否存在



范例：查询具有parents成员的数据

```
db.getCollection('students').find({
            "parents":{"$exists":true}
})


```



范例：查询不具有course成员的数据

```
db.students.find({
            "course":{"$exists":false}
})
```



**条件过滤**

\$where

```
db.students.find({
   "$where":"this.age>20"
})
```

```
db.students.find("this.age>21");
```

```
db.students.find(function() {
    return this.age > 20
});
```

```
db.students.find({"$where":function() {
    return this.age > 20
}});
```

多条件查询

```
db.students.find({"$and":[
        {"$where":"this.age>20"},
        {"$where":"this.score>20"}
    ]});
```

这里会将MongoDB的BSON格式变为JavaScript格式，不方便使用数据库索引机制。



**正则运算**

范例：查询以“张”开头的姓名

```
db.students.find({"name":/^张/});
```

正则不要加引号了。



范例：查询姓名有“A”的数据，加上i表示不区分大小写

```
db.students.find({"name":/a/i});
```

```
db.students.find({"name":{"$regex":/a/i}});
```



除了可以单个查询之外，还可以进行数组查询。

范例：查询数组数据中包含语文的数据

```
db.students.find({"course":{"$regex":/语文/}});
```

**数据排序**

通过sort()函数，升序是1，将序-1。1和-1不要加引号。



范例：按照成绩排序，成绩高的排在前面

```
db.students.find({"course":{"$regex":/语文/}}).sort({"score":-1});
```



范例：自然排序，按照数据保存的先后顺序排序

```
db.students.find({"course":{"$regex":/语文/}}).sort({"$natural":-1});
```



**分页显示**

两个操作函数 :alarm_clock:

skip(n):表示跨过多少数据行

limit(n):表示取出多少行



范例：分页获取数据（第一页，skip(0),limit(5)。第二页，skip(5),limit(5)）



```sql
db.students.find().skip(5).limit(5);
```



---------------------------------------------

**数据更新操作**

队友MongoDB而言，数据更新是一件非常麻烦的事情。Mongo通常会存副本数据，数据有变更的时候，最好的做法是删除MongoDB的数据，重新插入。

Mongo中提供了两个函数，一个是save(),一个是update()。



范例：**更新存在的数据 --** 将年龄是19岁的人的成绩都更新为100分

只更新查询出的第一条数据，没有不增加

```
db.students.update({"age":19},{"$set":{"score":100}},false,false);
```

所有满足条件的数据都更新

```
db.students.update({"age":19},{"$set":{"score":100}},false,true);
```



范例： **更新不存在的数据 --** 将年龄是30岁的人更新他的名称name

```sql
db.students.update({"age":30},{"$set":{"name":"小李子"}},true,false);
```

第一个true表示如果不存在，则创建一条新数据。这种功能用的比较少。





**修改器**

1. inc  主要针对一个数字字段，增加某个字段的数据内容。



范例：将所有年龄为19岁的学生成绩一律减少30分。

```
db.students.update({"age":19},{"$inc":{"score":-30,"age":1}},false,true);
```



2. set 进行内容重新设置

   ​

   范例：将年龄为20的人的成绩修改为89

   ```sql
   db.students.update({"age":19},{"$set":{"score":-89}},false,true);
   ```

3. unset 删除某个成员的内容

范例：删除张三的年龄和成绩信息

```
db.students.update({"name":"张三"},{"$unset":{"age":1,"score":1}},false,true);
```



4. push 相当于将内容追加到指定的成员之中（基本上是用于数组）。一次增加一个元素，如果增加的是数组，表示一次增加一个数组。

范例：向张三添加课程信息

```
db.students.update({"name":"张三"},{"$push":{"course":["语文","数学"]}},false,true);
```

如果没有数组，就进行一个新的数组的创建，如果有则进行内容的追加。

5. pushAll与push类似，可以一次追加多个内容到数组里面

```
db.students.update({"name":"张三"},{"$pushAll":{"course":["美术","音乐"]}},false,true);

```

6. addToSet 如果已存在就不添加了

```
db.students.update({"name":"张三"},{"$addToSet":{"course":"美术"}},false,true);
```

7. pop 删除数组内的数据。文档是行，成员是列，集合是表。-1表示第一个课程。1表示最后一个课程。

```
db.students.update({"name":"张三"},{"$pop":{"course":-1}});
```

8. pull  从数组中删除指定内容的数据

```
db.students.update({"name":"张三"},{"$pull":{"course":"美术"}});
```



9. pullAll一次性删除多个内容

```
db.students.update({"name":"张三"},{"$pullAll":{"course":["音乐","舞蹈"]}});
```



10. rename 为成员名称重命名

```
db.students.update({"name":"张三"},{"$rename":{"course":"课程"}},false,true);
```

----------------------------

**删除数据**(比较常用)

范例:清空infos集合中的内容。表、文档、成员。

```
db.infos.remove({"url":/-/});
```

默认情况下都删除，第二个条件设为true，只删除一个。

```
db.infos.remove({"url":/^www/},true);
```

删除全部

```
db.infos.remove({});
```



**游标(重点)**

表示数据可以一行一行的进行操作！！！

find()返回的就是游标

通过hasNext()函数

next()取出数据



```js
var cursor = db.students.find();

while (cursor.hasNext()) {
    var doc = cursor.next();
    print("+++"+JSON.stringify(doc));
}

```

```js
var cursor = db.students.find();

while (cursor.hasNext()) {
    var doc = cursor.next();
    printjson(doc);
}
```

在这个循环中可以进一步的处理一些操作，必须修改年龄，修改成绩等等。



---------------------------

### **索引**

提升数据库检索性能的手段

**通过getIndexes()来获取已经存在的索引内容**

```js
db.students.getIndexes();
```

```json
/* 1 */
[
    {
        "v" : 1,
        "key" : {
            "_id" : 1
        },
        "name" : "_id_",
        "ns" : "mldn.students"
    }
]
```



**创建自己的索引**

范例：创建一个索引，在age列加一个将序索引

```js
db.students.ensureIndex({"age":-1});
```

```json
/* 1 */
[
    {
        "v" : 1,
        "key" : {
            "_id" : 1
        },
        "name" : "_id_",
        "ns" : "mldn.students"
    },
    {
        "v" : 1,
        "key" : {
            "age" : -1.0
        },
        "name" : "age_-1",
        "ns" : "mldn.students"
    }
]
```



**使用解释来分析索引**

```
db.students.find({"age":19}).explain();
```

```json
/* 1 */
{
    "queryPlanner" : {
        "plannerVersion" : 1,
        "namespace" : "mldn.students",
        "indexFilterSet" : false,
        "parsedQuery" : {
            "age" : {
                "$eq" : 19.0
            }
        },
        "winningPlan" : {
            "stage" : "FETCH",
            "inputStage" : {
                "stage" : "IXSCAN",
                "keyPattern" : {
                    "age" : -1.0
                },
                "indexName" : "age_-1",
                "isMultiKey" : false,
                "isUnique" : false,
                "isSparse" : false,
                "isPartial" : false,
                "indexVersion" : 1,
                "direction" : "forward",
                "indexBounds" : {
                    "age" : [ 
                        "[19.0, 19.0]"
                    ]
                }
            }
        },
        "rejectedPlans" : []
    },
    "serverInfo" : {
        "host" : "jiqing",
        "port" : 27017,
        "version" : "3.2.17-25-gae6f04a",
        "gitVersion" : "ae6f04a7cd143132fb3185669a8abc5d7c4ab3cc"
    },
    "ok" : 1.0
}
```



再分析一个没有索引的成员

```js
db.students.find({"score":{"$gt":80}}).explain();
```



```json
/* 1 */
{
    "queryPlanner" : {
        "plannerVersion" : 1,
        "namespace" : "mldn.students",
        "indexFilterSet" : false,
        "parsedQuery" : {
            "score" : {
                "$gt" : 80.0
            }
        },
        "winningPlan" : {
            "stage" : "COLLSCAN",
            "filter" : {
                "score" : {
                    "$gt" : 80.0
                }
            },
            "direction" : "forward"
        },
        "rejectedPlans" : []
    },
    "serverInfo" : {
        "host" : "jiqing",
        "port" : 27017,
        "version" : "3.2.17-25-gae6f04a",
        "gitVersion" : "ae6f04a7cd143132fb3185669a8abc5d7c4ab3cc"
    },
    "ok" : 1.0
}
```



有索引和没索引的成员一起使用呢？

```js
db.students.find({"$and":[
        {"age":{"$gt":19}},
        {"score":{"$gt":80}}
    ]}).explain();
```

and的时候用到了索引，or的时候没有用到。



**可以定义复合索引**

```js
db.students.ensureIndex({"age":-1,"score":-1},{"name":"age_score_index"});
```

```json
/* 1 */
[
    {
        "v" : 1,
        "key" : {
            "_id" : 1
        },
        "name" : "_id_",
        "ns" : "mldn.students"
    },
    {
        "v" : 1,
        "key" : {
            "age" : -1.0
        },
        "name" : "age_-1",
        "ns" : "mldn.students"
    },
    {
        "v" : 1,
        "key" : {
            "age" : -1.0,
            "score" : -1.0
        },
        "name" : "age_score_index",
        "ns" : "mldn.students"
    }
]
```



**强制使用索引**

```js
db.students.find({"$or":[
        {"age":{"$gt":19}},
        {"score":{"$gt":80}}
    ]}).hint({"age":-1,"score":-1}).explain();
```



**删除索引**

```
db.students.dropIndex({"age":-1,"score":-1});
```

删除全部索引，但是不会删除主键索引

```
db.students.dropIndexes();
```



###  **唯一索引**

主要的目的是使得某个字段上的内容不重复。

范例：创建一个唯一索引

```
db.students.ensureIndex({"name":1},{"unique":true});
```

```json
/* 1 */
[
    {
        "v" : 1,
        "key" : {
            "_id" : 1
        },
        "name" : "_id_",
        "ns" : "mldn.students"
    },
    {
        "v" : 1,
        "unique" : true,
        "key" : {
            "name" : 1.0
        },
        "name" : "name_1",
        "ns" : "mldn.students"
    }
]
```



这个时候如果插入的姓名已存在，将会报错。

```
E11000 duplicate key error collection: mldn.students index: name_1 dup key: { : "张三" }
```



### 过期索引

用于手机验证码之类的与时间期限的数据。

```
db.phones.ensureIndex({"time":1},{expireAfterSeconds:10});


db.phones.insert({"tel":"110","code":"110","time":new Date()});
db.phones.insert({"tel":"111","code":"111","time":new Date()});
db.phones.insert({"tel":"112","code":"112","time":new Date()});
db.phones.insert({"tel":"113","code":"113","time":new Date()});
db.phones.insert({"tel":"114","code":"114","time":new Date()});
db.phones.insert({"tel":"115","code":"115","time":new Date()});
db.phones.insert({"tel":"116","code":"116","time":new Date()});
db.phones.insert({"tel":"117","code":"117","time":new Date()});
```

设置过期时间10秒，但是会有延迟。时间到了后，会删除。



### 全文索引

```
db.news.insert({"title":"aaa","content":"啦啦啦"});
db.news.insert({"title":"bbb","content":"乐乐乐"});
db.news.insert({"title":"ccc","content":"咕咕咕"});
db.news.insert({"title":"ddd","content":"噜噜噜"});
db.news.insert({"title":"eee","content":"驴驴驴"});
db.news.insert({"title":"abc","content":"啦乐噜"});

```

```
db.news.ensureIndex({"title":"text","content":"text"});
```



### 地理索引

插入数据

```
db.shop.insert({loc:[10,10]});

db.shop.insert({loc:[11,10]});

db.shop.insert({loc:[10,11]});

db.shop.insert({loc:[12,15]});

db.shop.insert({loc:[16,17]});

db.shop.insert({loc:[90,90]});

db.shop.insert({loc:[120,130]});

```



范例: 为shop的集合定义2D索引

```
db.shop.ensureIndex({"loc":"2d"});
```

near,geoWithin

范例：查询[11,11]附近的点

```
db.shop.find({"loc":{"$near":[11,11]}});
```

默认返回100条

