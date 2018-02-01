谷歌v8引擎。

c++编写的js的运行环境。

提供了系统级别的api，文件的读写，进程的管理，网络通信等等。

思路打通了，很多技术细节也就不必太纠结了。

在gitbash中查看安装情况，

```
Administrator@USERCHI-NE52IC9 MINGW64 ~
$ node -v
v8.9.3

Administrator@USERCHI-NE52IC9 MINGW64 ~
$ npm -v
5.5.1

```

在命令行窗口也可以查看，

```
C:\Users\Administrator>node -v
v8.9.3

C:\Users\Administrator>npm -v
5.5.1
```

两种退出方式，

```
[root@local nodeSpace]# node
> console.log('你好%s', '世界');
你好世界
undefined
> process.exit()

```

```
[root@local nodeSpace]# node
> const {PI} = Math
undefined
> console.log({PI});
{ PI: 3.141592653589793 }
undefined
> .exit
```

引用的使用，

新建circle.js

```js
const { PI } = Math;

exports.area = (r) => PI * r ** 2;

exports.circumference = (r) => 2 * PI * r;
```

新建foo.js

```js
const circle = require('./circle.js');
console.log(`半径为 4 的圆的面积是 ${circle.area(4)}`);
```

执行，

```js
[root@local nodeSpace]# node foo.js
半径为 4 的圆的面积是 50.26548245743669
```

Node与浏览器的区别在于全局变量不一样。

说千遍，道万遍，不如动手做一遍。

