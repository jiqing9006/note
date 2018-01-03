技术不分年龄高低，只分水平高低。

搞技术25k以下是不看天赋的，25k以上是要看天赋的。

1U服务器，2U服务器，刀片服务器。程序都是运行在服务器上的。

榜样的力量是无穷的。--MK。

汇编语言跟硬件息息相关，汇编语言开发的程序，如果硬件变了，有可能就不能运行了。

1969年，UNIX诞生，第一版用的是汇编语言写的。1972年C语言诞生（UNIX的大神造出来的）。1973年，UNIX用C语言改写完成。

1990年，UNIX收费。1991年Linux诞生。

GUN(gcc编译器，shell脚本，bash，窗口，内核)。

Linux内核（https://www.kernel.org/）+gcc+shell等就诞生了Linux系统。

兴趣，开发+linux=技术总监

网络，测试+linux=平台架构

兴趣+赚钱结合是最好的结果。

斯诺登事件之后，中国出台了方案“自主可控”，去IOE，IBM、Oracle、EMC。使得服务器可控。银行、Alibaba等都进行了去IOE活动，选择Linux系统，更可控。



---------------

桥接模式，给一台物理机，有自己独立的IP。

boot分区，引导分区，系统启动，内核文件。

swap分区，内存扩展分区。1.5或2倍。内存不够的时候，会写入其中。正常给8G或者16G就够了。不需要非要1.5或2倍。

```/``` 根。所有文件的根。

腾讯课堂毕业证颁发的证书，跟大学毕业证一样是所有企业都认可的。

知识面，决定你有没有思路。当你一切方法都解决不了问题的时候，从内核出发，一定能解决问题。

一个月拿个4,5千，确实不应该是一个男人拿的薪资。--MK

```
Ctrl+L
```

清屏

```
nmtui
```

管理网卡（确保是桥接模式，ip配置成局域网中的ip）

```
[root@local ~]# systemctl status NetworkManager
● NetworkManager.service - Network Manager
   Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)
   Active: active (running) since 二 2018-01-02 16:17:18 CST; 18h ago
 Main PID: 1064 (NetworkManager)
   CGroup: /system.slice/NetworkManager.service
           └─1064 /usr/sbin/NetworkManager --no-daemon
```

查看模块NetworkManager运行状态！

```
systemctl restart NetworkManager
```

重启NetworkManager服务。

```
vi /etc/sysconfig/network-scripts/ifcfg-eno16777736
```

修改网络配置。

```
[root@local ~]# systemctl status firewalld.service
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since 二 2018-01-02 16:17:18 CST; 21h ago
 Main PID: 885 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─885 /usr/bin/python -Es /usr/sbin/firewalld --nofork --nopid
```

查看防火墙状态！

```
systemctl stop firewalld.service
```

关闭防火墙！

```
systemctl disable firewalld.service
```

禁止防火墙开机启动。

再一个，关闭selinux，方便进行linux的学习。
```
getenforce
```
查看selinux状态，点击滚轮粘贴

```
setenforce 0
```
临时关闭selinux

永久关闭的话，需要设置配置
```
vi /etc/selinux/config
```
或者
```
vi /etc/sysconfig/selinux
```
将SELINUX=enforcing改为SELINUX=disabled

```
Esc+u
```
可以撤销vi的操作。

重启系统后生效。
```
reboot
```

------------------------------

设置光盘，开机自动挂载。

挂载， 在linux操作系统中， 挂载是指将一个设备（通常是存储设备）挂接到一个已存在的目录上。 我们要访问存储设备中的文件，必须将文件所在的分区挂载到一个已存在的目录上， 然后通过访问这个目录来访问存储设备。

```
vi /etc/fstab
```

Linux下，一切皆文件。光驱也是文件。```/dev/```  下面的文件是设备文件,```/mnt``` 是用来挂载设备的，挂载后，就可以查看挂载设备中的内容了。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103143220815-266300953.png)

```
mount -a 
```

验证挂载是否配置成功！

```
[root@local sysconfig]# mount -a 
mount: /dev/sr0 写保护，将以只读方式挂载
[root@local sysconfig]# ls /mnt
addons  EULA  images    LiveOS      Packages       repodata                 RPM-GPG-KEY-redhat-release
EFI     GPL   isolinux  media.repo  release-notes  RPM-GPG-KEY-redhat-beta  TRANS.TBL
```

卸载挂载

```
[root@local sysconfig]# umount /mnt
[root@local sysconfig]# ls /mnt
```

可以挂到别的目录下，只要是空的都行。

```
[root@local sysconfig]# ls /dev/cdrom
/dev/cdrom
```

直接访问硬件系统，是啥都看不到的。

--------------------

先死后活，先记住，再灵活运用。

拍个快照，方便系统坏了，找回。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103150623815-842296457.png)



![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103150756878-262917312.png)

硬件知识，cpu，内存，i/o总线，电源，机箱。

需求：公司需要做一个内容发布网站，展示公司的信息，你需要选择符合公司要求的Web服务器，做成公司的Web服务器。目前的预算是2-3万元，希望公司的网站能够正常运行。

评估访问量。搜索主流服务器，对比大致的价格。

（主板，硬盘，内存，机箱，电源，风扇等）。

服务器上的显卡都是集成的，因为不需要显示东西。

一般RDIMM带寄存器的，一般用于服务器。UDIMM，无缓冲双通道内存模块，一般用于家用。

**大型机、小型机、x86服务器的区别**

首先来讲x86服务器，与平常人们所接触的台式机笔记本类似，采用CISC架构处理器。随着英特尔至强处理器的性能不断提升，业内有种说法是x86服务器有抢占小型机市场的趋势。

小型机，是一种介于PC服务器和大型机之间的高性能计算机，一般认为，传统小型机是指采用RISC、MIPS等专用处理器，主要支持UNIX操作系统的封闭、专用的计算机系统，所以又称RISC服务器或Unix服务器。

大型机，又名大型主机，使用专用的处理器指令集、操作系统和应用软件。故此，大型机不仅仅是一个硬件上的概念，更是一个硬件和专属软件的有机整体。大型机是上世纪六十年代发展起来的计算机系统。经过四十年的不断更新，其稳定性和安全性在所有计算机系统中是首屈一指的。

现在的大型机的性能，并不能用单一的每秒并行浮点计算能力来体现，大型机相比于其他计算机系统，其主要特点在于其RAS(Reliability, Availability, Serviceability 高可靠性、高可用性、高服务性）。对于一些企业，其关键业务往往需要不间断服务，亚马逊网站宕机一分钟的损失就超过5万美元。力求零宕机的大型机正好符合要求。

Red Hat下载一个小型机的版本，内核跟其他版本不一样。可以跑在小型机上面。因为CPU的指令是不一样的。

------------------------------

tty控制台终端。

pts虚拟终端。

tty1 图形界面。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103162702596-1465458272.png)

tty2 字符界面。

```
Ctrl+Alt+F2-6
```



![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103163217628-1119817247.png)



在字符界面下，通过```Alt+F2``` 切换回来。或者切换到其他的字符界面。

```
Alt+F2 
```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103163511706-566273204.png)

pts虚拟终端。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180103163802846-1974267951.png)

```
Ctrl+Shift+加号
```

放大字体

```
Ctrl+Shift+T 
```

新建新的终端，这个在shell链接中无效。只在系统中操作有效。

```
Alt+数字
```

在虚拟终端之间切换。

```
who am i
```

查看当前登录的用户所在终端。

ssh的作用，是远程链接Linux服务器。连上之后，也算是一个终端。

```
[root@local ~]# who am i
root     pts/2        2018-01-03 16:22 (192.168.0.33)
[root@local ~]# ssh root@192.168.0.66
The authenticity of host '192.168.0.66 (192.168.0.66)' can't be established.
RSA key fingerprint is 45:33:b7:09:a9:a0:c0:77:f4:e5:12:80:9d:0d:14:f2.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.66' (RSA) to the list of known hosts.
root@192.168.0.66's password: 
Last login: Mon Jan  1 18:32:22 2018 from 192.168.0.33
[root@localhost ~]# who am i
root     pts/0        2018-01-03 00:59 (192.168.0.77)

```

33的机器，访问77的终端，再在77的终端中链接66。

```
[root@localhost local]# exit
logout
Connection to 192.168.0.66 closed.

```

exit退出。

```
ls -a 
```

显示隐藏文件，linux隐藏的文件前面都有一个点。

man ls 查看详细执行操作。

```
空格键（Space）：代表向下翻一页。
Enter：代表向下滚动一行。
/字符串：代表在当前显示的内容中，向下查找“字符串”这个关键字。
q：代表立即退出，不予显示。
b或[ctrl]-b：往回翻，不过该操作只对文件有用。
```

Linux学习是一个聚沙成塔的过程。

Linux下不同的颜色代表不同的文件类型：

```
蓝色 文件夹

黑色 文件

浅蓝色 链接

红色 压缩包

绿色 可执行文件

黑底黄字 设备文件

```



