一个操作JSON更方便的库！



###jquery对数据处理不太友好

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="../org/jquery-3.2.1.min.js"></script>
</head>
<body>
    <ul id="data">
    </ul>
</body>
</html>

<script>
    $.get('1.php',function (res) {
        $(res).each(function(i) {
            var html = '<li>'+res[i].name+'</li>';
            $("#data").append(html);
//            console.log(res[i]);
        });
    },'json');
</script>
```

jquery 操作json麻烦，代码高度耦合。

jquery更倾向于效果的实现！而处理数据的话，还是angular更好一些！



### AngularJS 更好的处理数据。MVVM模式

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../org/angular-1.6.6.min.js"></script>
</head>
<body>
    <!-- ng-app是指令 定义模块 -->
    <!-- ng-controller是指令 定义控制器 -->
    <div ng-app="hd" ng-controller="ctrl">
        {{name}}

        <!-- 双向数据绑定MVVM -->
        <h2 ng-bind="name"></h2>

        <input type="text" ng-model="name">
    </div>

    <script>
        var m = angular.module('hd',[]);
        m.controller('ctrl',['$scope',function ($scope) {
            // 在控制器ctrl中展示scope

            // 视图模型$scope，正常情况下这些数据都是从后台抓回来的

            // viewModel
            $scope.name="后盾网";
        }]);
    </script>
</body>
</html>
```





![](https://images2018.cnblogs.com/blog/422101/201711/422101-20171129140215003-1052427151.png)



学程序就跟打游戏一样，需要不断的琢磨尝试！

需要时间成本，才能得到结果！

王者荣耀！

### 感受angular的魅力

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>
<body ng-app="hd">

<div ng-controller="ctrl">
    <table class="table table-hover">
        <thead>
        <tr>
            <th>商品名称</th>
            <th>商品价格</th>
            <th>购买数量</th>
            <th>总计:</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td>{{goods.title}}</td>
            <td>{{goods.price}}</td>
            <td>{{goods.num}}</td>
            <td>{{goods.num * goods.price}}</td>
        </tr>
        </tbody>
    </table>
    

    <button ng-click="add();">增加数量</button>

    <button ng-click="reduce();">减少数量</button>
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.goods = {'title':'apple mac','price':300,'num':0};

        // 增加数量
        $scope.add = function () {
//            $scope.goods.num++;
            $scope.goods.num = Math.min(++$scope.goods.num,6); // 最大值为6 ，返回两个数中较小的
        }

        // 减少数量
        $scope.reduce = function () {
            $scope.goods.num = Math.max(--$scope.goods.num,0); // 最小值为0，返回两个数中较大的
        }
    }]);

</script>
</body>
</html>
```

更好的感受angularJs



### 表单操作

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>
<body ng-app="hd">

<div ng-controller="ctrl">
    <form action="1.php" method="post" role="form">
        <legend>表单提交测试</legend>

        <div class="form-group">
            <label for="title">名称</label>
            <input type="text" class="form-control"  id="title" name="title" ng-model="data.name">
        </div>

        <div class="form-group">
            <label for="age">年龄</label>
            <input type="text" class="form-control"  id="age" name="age" ng-model="data.age">
        </div>


        <button type="submit" class="btn btn-primary">提交</button>
    </form>

</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.data = {
            'name':'后盾人',
            'age':18
        };
    }]);

</script>
</body>
</html>
```



感受一下表单提交！

### ng-value

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>
<body ng-app="hd">

<div ng-controller="ctrl">
    商品: <input type="text" ng-model="goods.title"> <br/>
    价格: <input type="text" ng-model="goods.price" readonly="readonly"> <br/>
    数量: <input type="text" ng-model="goods.num"> <br/>

    <!-- ng-value可以使用表达式 -->

    总价: <input type="text" ng-value="goods.num * goods.price" readonly="readonly"> <br/>


</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.goods = {
            title:'后盾网视频',
            price:88,
            num:2
        };
    }]);

</script>
</body>
</html>
```

> 学习案例，就像了解游戏装备。知道什么情况下出什么装备，才能更好的打好游戏。学编程就像打王者荣耀。



### radio操作

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>
<body ng-app="hd">

<div ng-controller="ctrl">
    网站开启：
    <div class="radio">
        <label>
            <input type="radio"  ng-model="status"  ng-value="1">
            开启
        </label>

        <label>
            <input type="radio"  ng-model="status"  ng-value="0">
            关闭
        </label>
    </div>

    {{status}}

    <!-- ng-show可以控制显示 可以写表达式 -->
    <div ng-show="status==0">
        <span class="label label-info">关闭原因:</span>
        
        <p class="lead">网站维护中...</p>

    </div>
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.status = 1;
    }]);

</script>
</body>
</html>
```

ng-show



### checkBox 操作

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>
<body ng-app="hd">

<div ng-controller="ctrl">
    游戏: <input type="checkbox" ng-model="data.game" ng-true-value="1" ng-false-value="0">
    电影: <input type="checkbox" ng-model="data.video" ng-true-value="1" ng-false-value="0">

    {{data}}

    <div ng-show="data.game==1">
        <h1>游戏:</h1>
        <textarea name="" id="game_area" cols="30" rows="10"></textarea>
    </div>
    <div ng-show="data.video==1">
        <h1>电影:</h1>
        <textarea name="" id="video_area" cols="30" rows="10"></textarea>
    </div>
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.data = {'game':1,'video':0};
    }]);

</script>
</body>
</html>
```

感受一下checkbox中angular的使用！



### select操作

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>

<style></style>

<body ng-app="hd">

<div ng-controller="ctrl" >
    <!--
        v in data 循环遍历 循环3次
    -->

    <select ng-options="v.value as v.name for v in data" ng-model="city">
        <option value="">请选择城市</option>
    </select>

    {{city}}
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        // 默认选中南京
        $scope.city = 'nanjing';

        $scope.data = [
            {'name':'北京',value:'beijing'},
            {'name':'南京',value:'nanjing'},
            {'name':'上海',value:'shanghai'}
        ];
    }]);

</script>
</body>
</html>
```

感受一下select的使用！

### 遍历操作

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>

<style></style>

<body ng-app="hd">

<div ng-controller="ctrl" >
    {{data}}
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {

        $scope.data = [
            {name:'后盾网',url:'houdunwang.com'},
            {name:'后盾人',url:'houdunren.com'}
        ];

        // 遍历数组
        angular.forEach($scope.data,function (v,k) {
            console.log(v);
        });

        // 遍历数组,处理数组
        angular.forEach($scope.data,function (v,k) {
            v.url = 'www.'+v.url;
        });
    }]);

</script>
</body>
</html>
```

遍历操作，感受一下！



### 结合jQuery一起使用

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <script src="../org/jquery-3.2.1.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>

<style></style>

<body ng-app="hd">

<div ng-controller="ctrl" >
    <form action="3.php" method="post" role="form">
        <legend>表单</legend>

        <div class="form-group">
            <label for="title">标题:</label>
            <input type="text" class="form-control"  ng-model="field.title" id="title">
        </div>

        <div class="form-group">
            <label for="click">点击数:</label>
            <input type="text" class="form-control"  ng-model="field.click" id="click">
        </div>

        <div class="form-group">
            <label for="content">内容:</label>
            <input type="text" class="form-control"  ng-model="field.content" id="content">
        </div>

        <div class="form-group" hidden>
            <textarea name="data" id="" cols="30" rows="10"></textarea>
        </div>


        <button type="submit" class="btn btn-primary">提交</button>
    </form>
    
    
    {{data.name}}
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.field = {title:'后盾人',click:100,content:'后盾网 人人做后盾'};

        // 结合jq一起使用，dom操作与数据操作相结合
        $('form').submit(function () {
            $("[name='data']").val(angular.toJson($scope.field));
//            return false;
        });
    }]);

</script>
</body>
</html>
```

### 常用的函数

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <script src="../org/angular-1.6.6.min.js"></script>
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>

<style></style>

<body ng-app="hd">

<div ng-controller="ctrl" >
</div>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        // 检查php分配过来的数据或者动态运算的数据是否是数组
        console.log(angular.isArray([])); // true

        console.log(angular.isArray({})); // false

        // 是否是日期
        console.log(angular.isDate(new Date())); // false

        var a;
        // 是否定义，没有定义数据就是假
        console.log(angular.isDefined(a)); // false

        var b = 'hello';
        console.log(angular.isDefined(b)); // true

        // 是否是数字
        console.log(angular.isNumber(88)); // true

        // 是否是字符串
        console.log(angular.isString(88)); // false

        // 是否是对象
        var c = {};
        console.log(angular.isObject(c)); // true

        // 是否是节点元素
        var e = document.getElementsByTagName('body').item(0);

        console.log(angular.isElement(e));

        // 比较两个数据是否相同
        var f = {};
        var g = [];
        console.log(angular.equals(f,g));
    }]);

</script>
</body>
</html>
```

### ng-trim

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>

<style></style>

<body ng-app="hd">

<div ng-controller="ctrl" >
    <form action="2.php" method="post" role="form">
        <legend>表单</legend>

        <div class="form-group">
            <label for="title">标题</label>

            <!-- ng-trim 对数据进行了过滤处理 -->
            <input type="text" class="form-control" ng-trim ng-model="title" id="title" >
        </div>

        <input type="text" name="data"><br/>

        <button type="submit" class="btn btn-primary">提交</button>
    </form>

    {{title}}
</div>

<script src="../org/angular-1.6.6.min.js"></script>
<script src="../org/jquery-3.2.1.min.js"></script>

<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {
        $scope.title = "";
        $('form').submit(function () {
            $("[name='data']").val($scope.title);
//            return false;
        });
    }]);

</script>
</body>
</html>
```

> 实践过程中出错是好事情，解决了错误，你会对知识点理解的更加透彻。
>
> angular和jquey就像是飞机和火车，可以让我们旅行过程中更好的到达目的地，原生就像是走路。走路一样可以到达目的地，只要你想走。
>
> 什么叫学会，就是不看老师的视频，不看老师的代码，自己敲出来。
>
> 你对照老师的代码敲出来，它并不属于你。



### 注册协议小案例

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="../org/css/bootstrap-3.3.7.min.css">
</head>

<style></style>

<body ng-app="hd">

<div ng-controller="ctrl" >
    <label><input type="checkbox" ng-model="status"> 接收协议</label>
    <button ng-init="copyright=false" ng-click="copyright=!copyright;">查看协议</button>
    <br/>
    <textarea ng-if="copyright">协议内容:啦啦啦</textarea>
    <br/>
    
    <button ng-disabled="!status">登录</button>
</div>


<script src="../org/angular-1.6.6.min.js"></script>
<script>
    var m = angular.module('hd',[]);
    m.controller('ctrl',['$scope',function ($scope) {

    }]);

</script>
</body>
</html>
```

