硬链接，软链接。

```
文件名1->inode1->blockA

文件名2->inode1->blockA
```

硬链接。

例子：

```
[root@local ~]# ln a.txt a2.txt
[root@local ~]# cat a2.txt
hello
[root@local ~]# cat a.txt
hello
[root@local ~]# ls -i a.txt a2.txt
39098831 a2.txt  39098831 a.txt
```

点评：两个文件的inode值相同。

```
[root@local ~]# rm a2.txt 
rm：是否删除普通文件 "a2.txt"？y
[root@local ~]# cat a.txt
hello
```

点评：删除其中一个后，另一个不受影响。



软连接相当于快捷方式。

```
[root@local lab]# ln -s a.txt as.txt
[root@local lab]# ll
总用量 4
lrwxrwxrwx 1 root root 5 1月  26 16:15 as.txt -> a.txt
-rw-r--r-- 1 root root 6 1月  26 16:15 a.txt

```

为a.txt文件创建一个软连接。

```
[root@local lab]# rm a.txt
rm：是否删除普通文件 "a.txt"？y
[root@local lab]# ll
总用量 0
lrwxrwxrwx 1 root root 5 1月  26 16:18 as.txt -> a.txt
[root@local lab]# cat as.txt 
cat: as.txt: 没有那个文件或目录
```

软连接，如果删除了源文件，软连接就失效了。

软连接支持目录和跨目录创建。硬链接不支持。

-----

物质的饥饿感

安全感

成长的愿望和野心

成就感

使命主义