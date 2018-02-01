01

传统开发的痛点

1.人员稀缺

2.开发成本高

3.代码复用率低

4.无法动态更新



02

React Native的优点

1.跨平台

2.性能高

3.低投入

4.支持动态更新



03

开发环境搭建

1.安装nodejs

2.安装命令行工具

````
npm install -g react-native-cli
````

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131135341703-924204687.png)

3.安装Android Studio

4.生成App，在命令行中生成app，它会自动初始化一些第三方包（在npm服务器上），可以设置一个淘宝镜像服务器

```
npm config set registry https://registry.npm.taobao.org
```

```
react-native init FirstApp
```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131142231031-579863072.png)

如果出现上面的情况，就表示初始化成功了。

5.运行，一种是通过命令行工具（确保有设备连接到电脑，或者模拟器）。一种是通过Android Studio。

```
react-native run-android
```



![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131174241671-1713949524.png)



![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131174354000-1664655527.png)



这里面会出现很多问题。

第一个就是gradle下载很慢的问题。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131175156578-299151501.png)

可以下载到本地，

```
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=file\:///D:/Android/gradle/gradle-2.14.1-all.zip
```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131175253265-1830234700.png)

还有一个就是sdk问题，新建local.properties

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131175429921-2043814261.png)

```
sdk.dir = D\:\\Android\\SDK
```

指定SDK位置。

还有就是指定好，版本。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180131175944375-237666277.png)

经过千辛万苦，终于执行成功了。还是在模拟器中执行成功的，真机中还是搞不定。

--------------------------------------------------------------

Webstorm配置运行React Native

1.选择配置



![](http://images2017.cnblogs.com/blog/422101/201802/422101-20180201110553281-1767632415.png)

2.选择npm，设置package等参数

![](http://images2017.cnblogs.com/blog/422101/201802/422101-20180201110642343-1737886981.png)

3.添加拓展工具

![](http://images2017.cnblogs.com/blog/422101/201802/422101-20180201110718671-1589423011.png)

4.配置拓展工具（核心啊）



![](http://images2017.cnblogs.com/blog/422101/201802/422101-20180201110803343-248566308.png)

5.运行测试，ok的。

![](http://images2017.cnblogs.com/blog/422101/201802/422101-20180201110933843-236078679.png)

![](http://images2017.cnblogs.com/blog/422101/201802/422101-20180201111000640-1359492545.png)

----------------------------

