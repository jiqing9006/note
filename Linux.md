

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



-------------------------------

### 系统时间与开关机

* 查看系统时间

  ```
  date
  ```


* 查看硬件日期

  ```
  hwclock
  ```

学习Linux不必全部指令都会，只要记住主要常用的几个就可以了。--MK



* 关机命令

  ```
  shutdown init reboot poweroff
  ```

  ```
  [root@local ~]# shutdown -h +10
  Shutdown scheduled for 四 2018-01-04 23:34:56 CST, use 'shutdown -c' to cancel.
  [root@local ~]# 
  Broadcast message from root@local.rhel77.com (Thu 2018-01-04 23:24:56 CST):

  The system is going down for power-off at Thu 2018-01-04 23:34:56 CST!

  ```

  十分钟之后关机。

  ```
  shutdown -c
  ```

  取消关机。


### Linux下端口号的分配

  TCP和UDP采用16位的端口号来识别应用程序。

  2^16 = 65536 一个有0到65535。

  TCP端口分配：

  ```
  21 ftp 文件传输服务
  22 ssh 安全远程连接服务
  23 telnet 远程连接服务
  25 smtp 电子邮件服务
  80 http web服务
  443 https 安全web服务
  ```

  UDP端口分配：

  ```
  69 tftp 简单文件传输协议
  123 ntp 时间同步服务
  ```

  可以通过

  ```
  vi /etc/services
  ```

  进入查看详细的端口使用情况。


### 查看端口的监听状态

```
netstat
```

tcp anpt

udp anpu

全部 anput

```
[root@local ~]# netstat -anput | grep sshd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1227/sshd           
tcp        0     52 192.168.0.77:22         192.168.0.101:49390     ESTABLISHED 2713/sshd: root@pts 
tcp6       0      0 :::22                   :::*                    LISTEN      1227/sshd   
```



```
[root@local ~]# netstat -anput | grep :22
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1227/sshd           
tcp        0     52 192.168.0.77:22         192.168.0.101:49390     ESTABLISHED 2713/sshd: root@pts 
tcp6       0      0 :::22                   :::*                    LISTEN      1227/sshd     
```

```
[root@local ~]# vi /etc/hostname
```

修改主机名。

配置hosts文件，DNS解析的时候，先看hosts，再看DNS。

```
vi /etc/hosts
```

查看网关情况。

```
route -n
```

ping 指令。

```
[root@local ~]# ping -c 4 www.baidu.com
PING www.a.shifen.com (180.97.33.108) 56(84) bytes of data.
64 bytes from 180.97.33.108: icmp_seq=1 ttl=55 time=11.8 ms
64 bytes from 180.97.33.108: icmp_seq=2 ttl=55 time=12.7 ms
64 bytes from 180.97.33.108: icmp_seq=3 ttl=55 time=12.5 ms
64 bytes from 180.97.33.108: icmp_seq=4 ttl=55 time=12.1 ms

--- www.a.shifen.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 11.824/12.310/12.732/0.376 ms
```



-----------------------------------------

Linux当中，一切皆文件。

### Linux目录结构

```/```  根分区，只有root用户对此目录拥有写权限。

```/etc``` 配置文件

``` /boot``` 启动文件

``` /var ``` 可增长的目录 。日志，文件等。

``` /root ``` 管理员所有数据 root用户的家目录。

``` /tmp ``` 临时文件 （大概15天清空一次。）

``` /usr ``` unix software source  /usr/src 源代码目录。/usr/local 自己的软件安装位置。

``` /bin``` 命令 二进制可执行文件。

``` /sbin ``` 系统命令。

``` /mnt``` 挂载目录。

```/dev``` 设备文件。 一切皆文件，终端，磁盘等。键盘，鼠标等。

```/home ``` 普通用户文件存放位置。

``` /proc ``` 虚拟目录。可以查看每个进程的情况。

``` /lib``` 存放系统的库文件（动态库，静态库。 .a静态库，.so动态库）。类似于.dll文件。



### 绝对路径与相对路径

绝对路径是从```/``` 开始的。

相对路径是以```.``` ```..``` 开始的。



### 创建，删除复制文件

```
touch a.txt
```

创建一个文件

```
mkdir test
```

创建一个目录

```
[root@local ~]# cat a.txt
hello linux
```

查看文件

```
[root@local ~]# less /var/log/messages
```

less 可以上下左右查看。enter，空格都是下一页。q退出查看。

```
[root@local ~]# more /var/log/messages 
```

more只能向下翻页查看。

```
[root@local ~]# cat /var/log/messages 
```

cat一次性展示所有内容。

```
[root@local ~]# tail -n 10 /var/log/messages 
Jan  5 15:30:01 local systemd: Started Session 14 of user root.
Jan  5 15:30:01 local systemd: Starting Session 14 of user root.
Jan  5 15:40:01 local systemd: Started Session 15 of user root.
Jan  5 15:40:01 local systemd: Starting Session 15 of user root.
Jan  5 15:50:01 local systemd: Started Session 16 of user root.
Jan  5 15:50:01 local systemd: Starting Session 16 of user root.
Jan  5 16:00:01 local systemd: Started Session 17 of user root.
Jan  5 16:00:01 local systemd: Starting Session 17 of user root.
Jan  5 16:01:01 local systemd: Started Session 18 of user root.
Jan  5 16:01:01 local systemd: Starting Session 18 of user root.

```

tail 最后多少行。

```
[root@local ~]# head -n 10 /var/log/messages 
Jan  2 16:17:58 local rsyslogd: [origin software="rsyslogd" swVersion="7.4.7" x-pid="887" x-info="http://www.rsyslog.com"] start
Jan  2 16:17:47 local journal: Runtime journal is using 8.0M (max allowed 99.2M, trying to leave 148.9M free of 984.9M available → current limit 99.2M).
Jan  2 16:17:47 local journal: Runtime journal is using 8.0M (max allowed 99.2M, trying to leave 148.9M free of 984.9M available → current limit 99.2M).
Jan  2 16:17:47 local kernel: Initializing cgroup subsys cpuset
Jan  2 16:17:47 local kernel: Initializing cgroup subsys cpu
Jan  2 16:17:47 local kernel: Initializing cgroup subsys cpuacct
Jan  2 16:17:47 local kernel: Linux version 3.10.0-327.el7.x86_64 (mockbuild@x86-034.build.eng.bos.redhat.com) (gcc version 4.8.3 20140911 (Red Hat 4.8.3-9) (GCC) ) #1 SMP Thu Oct 29 17:29:29 EDT 2015
Jan  2 16:17:47 local kernel: Command line: BOOT_IMAGE=/vmlinuz-3.10.0-327.el7.x86_64 root=UUID=87b51ffa-2f57-4ac2-99e7-e491bb257520 ro rhgb quiet LANG=zh_CN.UTF-8
Jan  2 16:17:47 local kernel: Disabled fast string operations
Jan  2 16:17:47 local kernel: e820: BIOS-provided physical RAM map:

```

head 开头多少行。

```
[root@local ~]# tail -f -n 10 /var/log/messages 
Jan  5 15:30:01 local systemd: Started Session 14 of user root.
Jan  5 15:30:01 local systemd: Starting Session 14 of user root.
Jan  5 15:40:01 local systemd: Started Session 15 of user root.
Jan  5 15:40:01 local systemd: Starting Session 15 of user root.
Jan  5 15:50:01 local systemd: Started Session 16 of user root.
Jan  5 15:50:01 local systemd: Starting Session 16 of user root.
Jan  5 16:00:01 local systemd: Started Session 17 of user root.
Jan  5 16:00:01 local systemd: Starting Session 17 of user root.
Jan  5 16:01:01 local systemd: Started Session 18 of user root.
Jan  5 16:01:01 local systemd: Starting Session 18 of user root.
Jan  5 16:03:51 local systemd-logind: New session 19 of user root.
Jan  5 16:03:51 local systemd: Started Session 19 of user root.
Jan  5 16:03:51 local systemd: Starting Session 19 of user root.
Jan  5 16:03:51 local dbus[887]: [system] Activating service name='org.freedesktop.problems' (using servicehelper)
Jan  5 16:03:51 local dbus-daemon: dbus[887]: [system] Activating service name='org.freedesktop.problems' (using servicehelper)
Jan  5 16:03:51 local dbus[887]: [system] Successfully activated service 'org.freedesktop.problems'
Jan  5 16:03:51 local dbus-daemon: dbus[887]: [system] Successfully activated service 'org.freedesktop.problems'

```

tail -f 动态的查看数据。这个很实用。

```
[root@local ~]# rm -r test2
rm：是否删除目录 "test2"？y
```

```
[root@local ~]# rm -rf test
```

rm -r 包括子目录，-f 强制删除。

cp  复制。

```
[root@local ~]# cp b.txt a.txt
```



mv 重命名。剪切。

```
[root@local ~]# mv a.txt b.txt
```

-------------------------------------------

vi 使用！

通过which指令来查看文件位置！

```
[root@local ~]# which vim
/usr/bin/vim
[root@local ~]# which vi
/usr/bin/vi
```

```
[root@local ~]# rpm -qf /usr/bin/vi
vim-minimal-7.4.160-1.el7.x86_64
[root@local ~]# rpm -qf /usr/bin/vim
vim-enhanced-7.4.160-1.el7.x86_64
```

查看版本！

整体使用，查看系统是否安装了vim。

```
[root@local ~]# rpm -qf `which vim`
vim-enhanced-7.4.160-1.el7.x86_64
```

``` !$``` 表示上一个命令的最后一个参数。

```
[root@local ~]# vim /etc/passwd
[root@local ~]# vi !$
vi /etc/passwd
```

### 命令模式

**```i``` 光标前插入**

```I ```行首插入

```a ``` 光标后插入

``` A``` 行尾插入

```o``` 下一行插入

```O``` 上一行插入



```x``` 向后删除一个字符，

```X``` 向前删除一个字符。

```u``` 撤销一步。



**行首与行尾**

```home``` 或者 ```^ ``` 行首

```$```  或者 ```end ``` 行尾



**删除复制粘贴**

```dd ``` 删除一行 ```数字+dd``` 删除多行

```yy``` 复制一行 ```数字+yy``` 复制多行

```p``` 粘贴



**删除到行尾**

```shift+d ``` 或者 ```d+end```

**单词操作**

``` w```  单词之间切换

``` dw```  删除一个单词



###  命令行模式

```w``` 保存

```q``` 退出

```q!``` 强制退出不保存

```wq``` 保存退出

```wq!``` 强制保存并退出

```ZZ``` 也可以保存退出



**vim中定位**

```gg ``` 定位到行首

```G``` 定位到最后一行，行首

```数字+G``` 定位到某一行，行首

```：数字``` 定位到某一行

```数字+gg```定位到某一行



-------------------------------

Linux 用户与组

```
root超级用户，UID 0

系统用户(伪用户，不登录)，UID 1~999

普通用户，UID 1000+

```

用户组就是具有相同特征的用户的集合。一个组可以包含多个用户，每个用户也可以属于不同的组。用户组在Linux中扮演着重要的角色，方便管理员对用户进行集中管理。等你有了成百上千个用户的时候，你就知道组有多么方便了。

linux 先死后活！ 先死记住！ 再讲原理。

### 用户的相关命令

语法：useradd 用户名（区分大小写）

常用参数：

-u UID

-d 宿主目录

-g 起始组

-G 附加组

-s 登录shell

-m 自动建立用户的登入目录

```
[root@local ~]# adduser san
[root@local ~]# tail -n 1 /etc/passwd
san:x:1001:1001::/home/san:/bin/bash
[root@local ~]# tail -1 /etc/passwd
san:x:1001:1001::/home/san:/bin/bash
[root@local ~]# adduser SAN
[root@local ~]# tail -2 /etc/passwd
san:x:1001:1001::/home/san:/bin/bash
SAN:x:1002:1002::/home/SAN:/bin/bash
```

```/etc/passwd``` 文件，保存系统账户信息。

```
[root@local www]# which adduser
/usr/sbin/adduser
[root@local www]# which useradd
/usr/sbin/useradd
[root@local www]# ll /usr/sbin/adduser
lrwxrwxrwx. 1 root root 7 1月   2 15:56 /usr/sbin/adduser -> useradd
```

useradd 跟 adduser是一样的效果。

开源思维，一切都可以修改。跟老司机，学习的是经验和思维。

```
[root@local www]# chsh -l
/bin/sh
/bin/bash
/sbin/nologin
/usr/bin/sh
/usr/bin/bash
/usr/sbin/nologin
/bin/tcsh
/bin/csh
```

查看系统中的壳。

```
[root@local www]# useradd -u 2018 zhubajie
[root@local www]# id zhubajie
uid=2018(zhubajie) gid=2018(zhubajie) 组=2018(zhubajie)
[root@local www]# useradd -g 2018 sunwukong 
[root@local www]# useradd -g 2018 niumowang
[root@local www]# id sunwukong
uid=2019(sunwukong) gid=2018(zhubajie) 组=2018(zhubajie)
[root@local www]# id niumowang
uid=2020(niumowang) gid=2018(zhubajie) 组=2018(zhubajie)

```

指定用户组

```
[root@local www]# ll /home
总用量 4
drwx------. 14 jiqing    jiqing   4096 1月   2 16:38 jiqing
drwx------   3 niumowang zhubajie   74 1月   9 09:36 niumowang
drwx------   3 sunwukong zhubajie   74 1月   9 09:36 sunwukong
drwx------   3 zhubajie  zhubajie   74 1月   9 09:35 zhubajie
[root@local www]# userdel sunwukong
[root@local www]# ll /home
总用量 4
drwx------. 14 jiqing    jiqing   4096 1月   2 16:38 jiqing
drwx------   3 niumowang zhubajie   74 1月   9 09:36 niumowang
drwx------   3      2019 zhubajie   74 1月   9 09:36 sunwukong
drwx------   3 zhubajie  zhubajie   74 1月   9 09:35 zhubajie
[root@local www]# userdel -r niumowang
[root@local www]# ll /home
总用量 4
drwx------. 14 jiqing   jiqing   4096 1月   2 16:38 jiqing
drwx------   3     2019 zhubajie   74 1月   9 09:36 sunwukong
drwx------   3 zhubajie zhubajie   74 1月   9 09:35 zhubajie

```

userdel 删除 -r 彻底删除。



### 密码文件 /etc/shadow

```
vim /etc/shadow
```

```
root:$6$SAbdjDh6vas5CQXF$atWNnFJ5XlKKJuPQpP1SqOBb5K3QjtrFFCR.MMF3pAGEk6SB6giV0pgvhXj4qF2IbG3SqnrTQN3Kru6VCWVMQ1::0:99999:7:::
...
jiqing:$6$VSgx2Ag/$bqF3.5GGPiUzNiVN02dExyGUxzLqNuuju/Q0WNHjr2vROKP1LAv0hDSh.rAnmQ98WGgcRu1BNoKkNZWhksNth0:17533:0:99999:7:::
www:$6$GH90pCSs$Dm/V2.X5nSsO/5YiPtE/9iZmU3iVJrZFXjKQAsCJ/zQdZ5eq2pB84h.oxlomg0dGYlU.piXpN4CRJHDzyzHma/:17539:0:99999:7:::
zhubajie:!!:17540:0:99999:7:::
```

修改密码的两种方式

```
[root@local www]# passwd zhubajie
更改用户 zhubajie 的密码 。
新的 密码：
无效的密码： 密码少于 8 个字符
重新输入新的 密码：
passwd：所有的身份验证令牌已经成功更新。

```

通过passwd进行修改。

```
[root@local www]# echo 123456 | passwd --stdin zhubajie
更改用户 zhubajie 的密码 。
passwd：所有的身份验证令牌已经成功更新。

```

通过管道模式修改用户密码。

两个用户密码一样，加密后的内容不一样。

```
[root@local www]# echo 123456|sha1sum 
c4f9375f9834b4e7f0a528cc65c055702bf5f24a  -

```

hash 123456。



### 组管理

本地组，远程组（域）

超级用户组root GID 0

普通用户组

​	系统用户组 GID 1-999

​	本地用户组 GID 1000+

注：每一个用户都有一个同名的组。除非你额外指定它。

```
vim /etc/group
```

查看组。

-------------------------------------

环境变量

```
[root@local ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
```

注：只有自己执行的命令在PATH变量包括的目录下，才可以直接使用。否则只能通过绝对路径或者相对路径来使用。

```
[root@local ~]# vim /etc/profile  
[root@local ~]# source /etc/profile
```

修改环境变量。

```
PATH="$PATH:/root"
export PATH
```



位置变量

利用位置变量写一个加法的脚本。

```

#! /bin/bash
SUM=$(expr $1 + $2)
echo "$1 + $2 = $SUM"

```

```
[root@local ~]# vim add.sh
[root@local ~]# chmod +x add.sh
[root@local ~]# add.sh 100 200
100 + 200 = 300

```



---------------------------------------------------

文件查找方法

1.which

查找可执行文件的位置

```
[root@local /]# which passwd
/usr/bin/passwd
```



2.whereis 

查找可执行文件的位置与相关的文件

```
[root@local /]# whereis passwd
passwd: /usr/bin/passwd /etc/passwd /usr/share/man/man1/passwd.1.gz /usr/share/man/man5/passwd.5.gz

```



3.grep

过滤

```
[root@local /]# grep home /etc/passwd
jiqing:x:1000:1000:jiqing:/home/jiqing:/bin/bash
www:x:1001:1001::/home/www:/sbin/nologin
zhubajie:x:2018:2018::/home/zhubajie:/bin/bash
sunwukong:x:2019:2018::/home/sunwukong:/bin/bash
niumowang:x:2020:2018::/home/niumowang:/bin/bash
```

```
[root@local /]# netstat -anpo | grep :22
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      5711/sshd            off (0.00/0/0)
tcp        0     52 192.168.70.77:22        192.168.70.33:59072     ESTABLISHED 9414/sshd: root@pts  on (0.23/0/0)
tcp        0      0 192.168.70.77:22        192.168.70.33:56269     ESTABLISHED 5732/sshd: www [pri  keepalive (1019.14/0/0)
tcp6       0      0 :::22                   :::*                    LISTEN      5711/sshd            off (0.00/0/0)
```

```
-a (all)显示所有选项，默认不显示LISTEN相关。
-n 拒绝显示别名，能显示数字的全部转化成数字。
-p 显示建立相关链接的程序名。
```

4.find

找文件 ```.``` 当前目```/``` 根目录。

```
-type 
b 设备文件
d 目录
c 字符设备文件
p 管道文件
l 符号链接文件
f 普通文件
```

```
[root@local /]# find  / -name  passwd -type f
/etc/passwd
/etc/pam.d/passwd
/usr/bin/passwd
/usr/share/bash-completion/completions/passwd
```

```
[root@local /]# find  /etc/ -name  "host*"
/etc/selinux/targeted/modules/active/modules/hostname.pp
/etc/host.conf
/etc/hosts
/etc/hosts.allow
/etc/hosts.deny
/etc/avahi/hosts
/etc/hostname
```

搜索以host开头的文件

--------------------------------------------

Nginx安装

1.复制解压。

```
[root@localhost ~]# mv /opt/nginx-1.13.8.tar.gz /usr/local/src
[root@localhost ~]# cd /usr/local/src
[root@localhost src]# tar -zxvf nginx-1.13.8.tar.gz 
```

2.编译安装

```
[root@localhost src]# cd nginx-1.13.8
[root@localhost nginx-1.13.8]# ./configure --prefix=/usr/local/nginx 
```

如果没有安装pcre、pcre-devel、openssl、zlib都安装一下。

提示

```
Configuration summary
  + using system PCRE library
  + OpenSSL library is not used
  + using system zlib library
```



```
[root@localhost nginx-1.13.8]# ./configure --prefix=/usr/local/nginx  --with-openssl=/usr/local/openssl
```

调整，增加openssl位置绑定。

3.安装

```
make && make install
```

4.检测是否安装成功

```
ps -ef |grep nginx
```

ps 查看进程。
-e 显示所有进程。
-f 全格式。

```
[root@localhost sbin]# ./nginx
[root@localhost sbin]# ps -ef |grep nginx
root       9334      1  0 18:38 ?        00:00:00 nginx: master process ./nginx
nobody     9335   9334  0 18:38 ?        00:00:00 nginx: worker process
root       9341   4092  0 18:38 pts/1    00:00:00 grep nginx
```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180110104343863-547950507.png)

5.配置环境变量

```
[root@localhost sbin]# vim /etc/profile
```

```
PATH=$PATH:/usr/local/nginx/sbin
export PATH
```

```
[root@localhost sbin]# source /etc/profile
```

这个时候就可以在任何地方操作nginx了。

```
[root@localhost local]# nginx -s stop
[root@localhost local]# ps -ef |grep nginx
root       9370   4092  0 18:46 pts/1    00:00:00 grep nginx
```

6.nginx关闭

```
[root@localhost local]# nginx -s stop
```

其他的方式

```
kill -quit 主进程号
kill -term 主进程号
pkill -9 nginx
```
-----------------------

### 配置php-fpm

```
[root@localhost php7]# which php-fpm
/usr/local/php7/sbin/php-fpm
[root@localhost php7]# php-fpm
[09-Jan-2018 19:52:28] ERROR: failed to open configuration file '/usr/local/php7/etc/php-fpm.conf': No such file or directory (2)
[09-Jan-2018 19:52:28] ERROR: failed to load configuration file '/usr/local/php7/etc/php-fpm.conf'
[09-Jan-2018 19:52:28] ERROR: FPM initialization failed
[root@localhost php7]# find / -name 'php-fpm.conf.default'
/usr/local/php7/etc/php-fpm.conf.default
[root@localhost php7]# cp /usr/local/php7/etc/php-fpm.conf.default /usr/local/php7/etc/php-fpm.conf
[root@localhost php7]# php-fpm
[09-Jan-2018 19:58:27] WARNING: Nothing matches the include pattern '/usr/local/php7/etc/php-fpm.d/*.conf' from /usr/local/php7/etc/php-fpm.conf at line 125.
[09-Jan-2018 19:58:27] ERROR: No pool defined. at least one pool section must be specified in config file
[09-Jan-2018 19:58:27] ERROR: failed to post process the configuration
[09-Jan-2018 19:58:27] ERROR: FPM initialization failed
[root@localhost php7]# ll /usr/local/php7/etc/php-fpm.d/
total 20
-rw-r--r--. 1 root root 18521 Dec 28 22:13 www.conf.default
[root@localhost php7]# cp /usr/local/php7/etc/php-fpm.d/www.conf.default /usr/local/php7/etc/php-fpm.d/www.conf
[root@localhost php7]# php-fpm

```

启动php-fpm成功！

```
[root@localhost php7]# ps -ef | grep php-fpm
root       9677      1  0 20:00 ?        00:00:00 php-fpm: master process (/usr/local/php7/etc/php-fpm.conf)
nobody     9678   9677  0 20:00 ?        00:00:00 php-fpm: pool www
nobody     9679   9677  0 20:00 ?        00:00:00 php-fpm: pool www
root       9681   4092  0 20:01 pts/1    00:00:00 grep php-fpm

```

或者通过netstat查看

```
[root@localhost php7]# netstat -anpo | grep 9000
tcp        0      0 127.0.0.1:9000              0.0.0.0:*                   LISTEN      9677/php-fpm        off (0.00/0/0)
[root@localhost php7]# netstat -anpo | grep php-fpm
tcp        0      0 127.0.0.1:9000              0.0.0.0:*                   LISTEN      9677/php-fpm        off (0.00/0/0)
unix  3      [ ]         STREAM     CONNECTED     232696 9677/php-fpm        
unix  3      [ ]         STREAM     CONNECTED     232695 9677/php-fpm      
```

配置 php-fpm 服务

```
[root@localhost php7]# cp /usr/local/src/php-7.1.2/sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
[root@localhost php7]# chmod a+x /etc/init.d/php-fpm 
```

```
[root@localhost php7]# service php-fpm start
Starting php-fpm  done
[root@localhost php7]# service php-fpm stop
Gracefully shutting down php-fpm . done
[root@localhost php7]# service php-fpm restart
Gracefully shutting down php-fpm warning, no pid file found - php-fpm is not running ?
Starting php-fpm  done
[root@localhost php7]# ps -ef | grep php-fpm
root       9825      1  0 21:33 ?        00:00:00 php-fpm: master process (/usr/local/php7/etc/php-fpm.conf)                                                                      
nobody     9826   9825  0 21:33 ?        00:00:00 php-fpm: pool www                                                                                                               
nobody     9827   9825  0 21:33 ?        00:00:00 php-fpm: pool www                                                                                                               
root       9829   4092  0 21:33 pts/1    00:00:00 grep php-fpm
```

### 配置nginx支持php

```
[root@localhost ~]# useradd nginx -s /sbin/nologin -M
```

```
[root@localhost php7]# vim /usr/local/nginx/conf/nginx.conf
```

```
user nginx nginx;           # 指定Nginx服务的用户和用户组
```

```
[root@localhost php7]# nginx -s reload
```

```
[root@localhost php7]# ps -ef | grep nginx
root       9583      1  0 19:24 ?        00:00:00 nginx: master process /usr/local/nginx/sbin/nginx
nginx      9862   9583  0 21:49 ?        00:00:00 nginx: worker process      
root       9866   4092  0 21:50 pts/1    00:00:00 grep nginx
```

这个时候用户就编程nginx了。

继续修改其他配置。

```
#user  nobody;
user nginx nginx;           # 指定Nginx服务的用户和用户组
worker_processes auto;

error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;
    server_tokens off;
    sendfile        on;
    #tcp_nopush     on;
    tcp_nodelay on;
    #keepalive_timeout  0;
    keepalive_timeout  65;
    send_timeout 30;
    gzip  on;

    server {
        listen       80;
        server_name  localhost;

        charset UTF-8;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   /var/webroot;
            index  index.php index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /var/webroot;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
            root           /var/webroot;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /var/webroot/$fastcgi_script_name;
            include        fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

```
[root@localhost php7]# mkdir /var/webroot
[root@localhost php7]# vim /var/webroot/index.php
[root@localhost php7]# nginx -s reload
```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180110140524519-39279248.png)

```
[root@localhost php7]# service php-fpm stop
Gracefully shutting down php-fpm . done
```

关闭了php-fpm就会出现错误了。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180110140710832-2059556628.png)

-----

