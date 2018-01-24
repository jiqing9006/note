是什么？

能干嘛？

怎么用？

小巧灵活、语法简单、适合做小工具。

如何搭建C语言的开发环境和运行环境。


头文件的好处，一次编译，多次使用。
只需要引入声明就可以了。
```
root@jiqing-virtual-machine:~/cspace/les2# gcc max.o min.o main.c
main.c: In function ‘main’:
main.c:8:18: warning: implicit declaration of function ‘max’ [-Wimplicit-function-declaration]
     int maxNum = max(a1,a2);
                  ^
main.c:9:18: warning: implicit declaration of function ‘min’ [-Wimplicit-function-declaration]
     int minNum = min(a1,a2);
                  ^

```

没有声明，会报错。

```
#include <stdio.h>
//#include "max.h"
//#include "min.h"
int main()
{
    int a1 = 22;
    int a2 = 33;
    int maxNum = max(a1,a2);
    int minNum = min(a1,a2);
    printf("the max value is %d\n",maxNum);
    printf("the min value is %d\n",minNum);
    return 0;
}

```

将注释的去掉就可以了。

单个编译max.c,min.c

```
root@jiqing-virtual-machine:~/cspace/les2# gcc -c max.c -o max.o
root@jiqing-virtual-machine:~/cspace/les2# gcc -c min.c -o min.o

```

编译成max.o和min.o之后，计算机就能够识别了。

以后可以在多个c文件中使用。只需要引入头文件h就可以了。

```
root@jiqing-virtual-machine:~/cspace/les2# gcc max.o min.o main.c -o main.out

```

```
root@jiqing-virtual-machine:~/cspace/les2# ./main.out
the max value is 33
the min value is 22
```



-------------------------------

Makefile完成项目的管理。

```
root@jiqing-virtual-machine:~/cspace/les2# ls
main.c  Makefile  max.c  max.h  min.c  min.h
```

```
root@jiqing-virtual-machine:~/cspace/les2# gcc max.c min.c main.c -o main.out
```

这才两个模块，就要写这么多。如果很多的话，岂不是累死。

这个时候就通过```Makefile``` 进行管理。

```
root@jiqing-virtual-machine:~/cspace/les2# make -v
GNU Make 4.1
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2014 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

查看是否安装了make。

撰写Makefile文件，

```makefile
# this is make file
main.out:max.o min.o main.c
    gcc max.o min.o main.c -o main.out
max.o:max.c
    gcc -c max.c
min.o:min.c
    gcc -c min.c

```

注意了，这里的gcc命令前一定是tab6位。

不可以是4个空格或者6个空格。

可以通过

```
set ts=6
```

来设置。

```bash
root@jiqing-virtual-machine:~/cspace/les2# make
gcc -c max.c
gcc -c min.c
gcc max.o min.o main.c -o main.out

```

执行完，会发现多了一些文件。

```bash
root@jiqing-virtual-machine:~/cspace/les2# ls
main.c  main.out  Makefile  max.c  max.h  max.o  min.c  min.h  min.o

```

```bash
root@jiqing-virtual-machine:~/cspace/les2# ./main.out 
the max value is 33
the min value is 22

```

-------------------------------------

两条指令同时执行，前提是第一条指令返回0。否则不执行第二条指令。

```
root@jiqing-virtual-machine:~/cspace/les3# gcc main.c -o main.out && ./main.out
./main.out
hello world!
```

可以通过

```
echo $?
```

来查看指令是否成功，返回0则成功，返回其他则不成功。

```
root@jiqing-virtual-machine:~/cspace/les3# gcc main.c -o main.out
root@jiqing-virtual-machine:~/cspace/les3# echo $?
0
```

我们继续进入main.c文件。修改return的返回值。

```c

#include <stdio.h>

int main(int argc,char *argv[])
{
    printf("%s\n",argv[0]);//读取可执行程序（包括路径）

    /*读取参数*/
    int i = 1;
    while(i < argc)
    {
        printf("%s\n",argv[i]);
        i++;
    }
    printf("hello world!\n");
    return 1;
}

```

这个时候，执行

```bash
root@jiqing-virtual-machine:~/cspace/les3# gcc main.c -o main2.out && ./main2.out && ls
./main2.out
hello world!

```

ls 指令将不会执行，因为之前的返回值不是0。

重新改为0，再次执行

```bash
root@jiqing-virtual-machine:~/cspace/les3# gcc main.c -o main.out && ./main.out && ls
./main.out
hello world!
main2.out  main.c  main.out

```

----------------------------

输入流stdin默认是键盘，输出流stdout默认是显示器，错误流stderr

```c
#include <stdio.h>

int main()
{
    printf("请输入选择的数字:\n"); // 标准输出流
    int choice;
    scanf("%d",&choice); // 标准输入流
    printf("您输入的数字是:%d\n",choice);
}
```
```c
root@jiqing:~/cspace/les4# ./cio.out
请输入选择的数字:
10
您输入的数字是:10

```

```c
#include <stdio.h>

int main()
{
    // printf("please input the value a: \n");
    fprintf(stdout,"please input the value a: \n"); // 非标准输出流

    int a;

    // scanf("%d",&a);
    fscanf(stdin,"%d",&a); // 非标准输入流
    if (a<0) {
        fprintf(stderr,"the value must > 0 \n");
        return 1;
    }
    return 0;
}

```

```
root@jiqing:~/cspace/les4# ./cio.out 
please input the value a: 
-1
the value must > 0 

```

重定向

```c
#include <stdio.h>
int main()
{
    printf("please input value of i:\n");
    int i;
    scanf("%d",&i);

    printf("please input value of j:\n");
    int j;
    scanf("%d",&j);

    printf("i+j=%d\n",i+j);
    return 0;
}

```

```
root@jiqing:~/cspace/les5# cc main.c -o main.out && ./main.out
please input value of i:
10
please input value of j:
20
i+j=30

```

管道重定向处理

```
root@jiqing:~/cspace/les5# ./main.out  1>> a.txt
10
20
root@jiqing:~/cspace/les5# cat a.txt
please input value of i:
please input value of j:
i+j=30

```

这个时候会将所有的标准输出流都写入到a.txt中。

```
root@jiqing:~/cspace/les5# ./main.out  1> a.txt
10
20
root@jiqing:~/cspace/les5# cat a.txt
please input value of i:
please input value of j:
i+j=30

```

单箭头不会累计数据，每次都是最新的数据。

重定向输入流。

新建一个input.txt

```
10
30
```

```
root@jiqing:~/cspace/les5# ./main.out < input.txt
please input value of i:
please input value of j:
i+j=40

```

直接就输出了结果，键盘都没有敲。

标准错误流，

```c
#include <stdio.h>
int main()
{
    printf("please input value of i:\n");
    int i;
    scanf("%d",&i);

    printf("please input value of j:\n");
    int j;
    scanf("%d",&j);
    if (0!=j) {
        printf("%d/%d=%d\n",i,j,i/j);
    } else {
        fprintf(stderr,"j must > 0\n");
        return 1;
    }
    return 0;
}

```



```
root@jiqing:~/cspace/les5# ./main.out 1>t.txt 2>f.txt
10
0
root@jiqing:~/cspace/les5# cat t.txt
please input value of i:
please input value of j:
root@jiqing:~/cspace/les5# cat f.txt
j must > 0

```

错误流会重定向到f.txt中，正确流会到t.txt中。



三者结合使用，

```
root@jiqing:~/cspace/les5# vim input.txt
```

```
10
0
```

```
root@jiqing:~/cspace/les5# ./main.out 1>t.txt 2>f.txt <input.txt
root@jiqing:~/cspace/les5# cat t.txt
please input value of i:
please input value of j:
root@jiqing:~/cspace/les5# cat f.txt
j must > 0
```

------------------------------------------

通过管道，让小程序更有活力

```
root@jiqing:~/cspace/les6# ls
avg.c  avg.out  input.c  input.out

```

一个负责输入，一个负责统计平均值

avg.c

```c
#include <stdio.h>

int main()
{
    int s,n;
    scanf("%d,%d",&s,&n);

    float v = s/n;

    printf("v=%0.2f\n",v);
    return 0;
}

```

input.c

```c
#include <stdio.h>
int main()
{
    int flag = 1;
    int i;
    int count = 0;
    int s = 0;
    while(flag) {
        scanf("%d",&i);
        if (0==i) break;
        count++;
        s += i;
    }
    printf("%d,%d",s,count);
    return 0;
}

```

分开用！

```
root@jiqing:~/cspace/les6# ./input.out
1000
2000
3000
0
6000,3
```

```
root@jiqing:~/cspace/les6# ./avg.out
6000,3
v=2000.00
```

结合起来用！

```
root@jiqing:~/cspace/les6# ./input.out | ./avg.out
1000
2000
3000
0
v=2000.00

```

---------------------------------------------------------

指针

```c
#include <stdio.h>
void change(int *a,int *b) {
    int tmp = *a;
    *a = *b;// 将指针a所在地址的值，更换为b地址的值
    *b = tmp;
}

int main()
{
    int a=5;
    int b=3;

    change(&a,&b); // 指针a获取a的地址，指针b获取b的地址

    printf("num a=%d\nnum b=%d \n",a,b);
    return 0;
}

```

让我们用gdb工具来看看其中的奥妙。

```
root@jiqing:~/cspace/pointer# gcc -g main.c -o main.out
```

生成gdb调试版本的main.out文件。

```
root@jiqing:~/cspace/pointer# gdb main.out
```

进入调试模式

```
(gdb) l
1	#include <stdio.h>
2	void change(int *a,int *b) {
3		int tmp = *a;
4		*a = *b;// 将指针a所在地址的值，更换为b地址的值
5		*b = tmp;
6	}
7	
8	int main()
9	{
10		int a=5;

```

l 进行查看

```
(gdb) start
Temporary breakpoint 1 at 0x4005cb: file main.c, line 9.
Starting program: /root/cspace/pointer/main.out 

Temporary breakpoint 1, main () at main.c:9
9	{

```

start 开始执行

```
(gdb) n
10		int a=5;

```

n 下一步

```
(gdb) n
13		change(&a,&b); // 指针a获取a的地址，指针b获取b的地址
(gdb) s
change (a=0x7fffffffe4d0, b=0x7fffffffe4d4) at main.c:3
3		int tmp = *a;

```

s 进入子函数

```
(gdb) p a
$1 = (int *) 0x7fffffffe4d0
(gdb) p b
$2 = (int *) 0x7fffffffe4d4

```

```
(gdb) p *a
$5 = 3
(gdb) p *b
$6 = 5
```

p 打印值。经过交换之后，a变成了3 ，b变成了5。

```
(gdb) q
A debugging session is active.

	Inferior 1 [process 11754] will be killed.

Quit anyway? (y or n) y

```

q退出。

> 通过gdb可以一步一步的查看程序的执行情况，看到内存的值。

----------------------------------------

32位操作系统最多只支持4G内存。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180124102555365-780839868.png)

CPU能不能直接访问硬盘的数据呢， 不能。 只能通过把硬盘的数据先放到内存里， 然后再从内存里访问硬盘的数据。我们平时玩游戏碰上读图loading 进度条的这个过程， 就是把数据从硬盘读到内存的过程啊。  读完条后地图的数据就在内存中了。

内存是把8个8个bit排成1组， 每1组成为1个单位， 大小是1**byte**(字节）， CPU每一次只能访问1个byte， 而不能单独去访问具体的1个小格子(bit)。**1个byte字节就是内存的最小的IO单位**。

1千兆字节(gb)=1073741824字节(b)。

32位只支持2^32个寻址。也就是4294967296字节的大小。除以上面的1073741824得到4G。

2^32 = 4 * 1024(G) * 1024(M) * 1024(K) = 4294967296 , 就是**4G** 啊, 而每1个地址对应1个1个字节， 容量就是1byte， 所以2^32个地址就总共能对应应**4GB** 的内存容量啊， 这里的B指的是byte 字节啊。

既然32位系统里内存地址长度是32位的.  所以32位的地址范围就是从 0000 0000 0000 0000 0000 0000 0000 0000 到 1111 1111 1111 1111 1111 1111 1111 1111 啦（Ox00000000 ~ OxFFFFFFFF)， 这里有几个地址呢？ 明显是有 2^32 个啦。**每个地址对应一个8bit的的内存单位。**

![img](http://images2017.cnblogs.com/blog/422101/201801/422101-20180124103354522-1545929639.png)



64位操作系统，最高支持2^32*4G内存，非常大了。

------------------------------------------------------

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180124165919334-1969225904.png)

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180124172804506-522528917.png)

