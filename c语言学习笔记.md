 数值类型

分为数值类型，非数值类型。

数值类型包括，整形int，短整形short int，长整形long int，单精度浮点型float，双精度浮点型double。

其他的，比如数组，结构体，枚举。

非数值类型包括，char字符型。

字符串，封装了的字符数组。

整型，*int*，32位。

11111111 8 bit (比特)  = 1 byte(字节)

11111111

11111111

11111111

几进制就没有几，二进制没有二，十进制没有十，八进制没有八，都变成10了。

8bit的最大值是2的8次方-1。也就是255。



短整型，short int，16位。

长整型，long int，32位。

float 32。

 *double* 64。

字符型 *char* 8位。

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{
    int salary = 2500;
    printf("小明的月薪是 %d\n",salary);
    return 0;
}

```



float小例子：

```c
#include <stdio.h>
#include <stdlib.h>

// 已知长方形宽和高，求长方形的面积
int main()
{
    float width = 2.5f;
    float height= 3.5f;
    float s = width*height;
    printf("长方形的面积:%f\n",s);
    return 0;
}

```

double小例子：

```c
#include <stdio.h>
#include <stdlib.h>

// 已知圆的半径，求圆的面积
int main()
{
    double radius = 3.0;
    double area = 3.141592653*radius*radius;
    printf("圆的面积:%lf\n",area);
    return 0;
}

```

微调一下，小数显示两位数。

```c
#include <stdio.h>
#include <stdlib.h>

// 已知圆的半径，求圆的面积
int main()
{
    double radius = 3.0;
    double area = 3.141592653*radius*radius;
    printf("圆的面积:%.2lf\n",area); // .2lf表示保留两位小数
    return 0;
}

```

char小例子：

```c
#include <stdio.h>
#include <stdlib.h>

// 打印字符对应的ASCII码
int main()
{
    char a = 'a';
    char A = 'A';
    printf("字符的ASCII码:\n");
    printf("%c\t%d\n",a,a);
    printf("%c\t%d\n",A,A);
    printf("%c\t%d\n",a-32,a-32);
    return 0;
}

// 结果
字符的ASCII码:

a       97

A       65

A       65

```



调整：

```c
#include <stdio.h>
#include <stdlib.h>

// 打印字符对应的ASCII码
int main()
{
    char a = 'a';
    char ch = 97;
    printf("字符的ASCII码:\n");
    printf("%c\t%d\n",a,a);
    printf("%c\t%d\n",ch,ch);
    return 0;
}

结果：
字符的ASCII码:
a       97
a       97
```



从上面可以看出，用'a',97效果都是一样的。

有符号的char类型指向-128到127之间，无符号的char类型指向0到255之间。

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171113223953281-700657028.png)

转换练习

```c
#include <stdio.h>
#include <stdlib.h>

// 接收用户输入的小写字母，输出大写字母
int main()
{
    char ch = 'a';

    printf("小写字母%c对应的大写字母位%c",ch,ch-32);

    return 0;
}
```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171113224908921-632660731.png)

> 九老师语录，不要钻牛角尖。有些东西一时半会理解不了正常，因为你还没到那个程序。等学到那个程度，回头会发现原来如此简单。



-----------------------------------------

scanf接收输入

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171113232930968-1229447417.png)

```c
#include <stdio.h>
#include <stdlib.h>

// 接收用户输入的小写字母，输出大写字母
int main()
{
    char ch;

    // 接收输入的内容
    printf("请输入小写字母:\n");
    scanf("%c",&ch); // scan扫描，f某种格式


    while (ch < 97 || ch > 122 ) {
        fflush(stdin); // 清空缓存
        printf("输入有误，请重新输入:\n");
        scanf("%c",&ch);
    }

    printf("小写字母%c对应的大写字母位%c",ch,ch-32);



    return 0;
}

```

小练习，计算英雄伤害：

```c
#include <stdio.h>
#include <stdlib.h>

// 游戏中根据英雄的生命值，计算英雄的真是伤害
int main()
{
    // 思考1、 需要定义几个变量？ -- 武器的最终真实伤害，最大生命值，武器的伤害
    //     2、 对应什么数据类型？ -- double                int         double

    double factPower;
    int    strength;
    double power = 256;

    printf("请输入玩家的力量:\n");
    scanf("%d",&strength);

    factPower = power * (strength + 100) / 100;

    printf("英雄的真实伤害为:%.2lf\n",factPower);

    return 0;
}

```

算术运算符与表达式

一元运算符：++、--

二元运算符：+、-、*、/、%



取模

%

5%2 取余数 得 1

5%3 取余数 得 2

5%-3 得?

-5%3 得?

-5%-3得?



```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    printf("%d\n",5%-3);

    printf("%d\n",-5%-3);

    printf("%d\n",-5%3);
    return 0;
}

// 结果
2
-2
-2
```



取模符号跟第一个数字的符号相关。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int num = 5 / 2;

    printf("%d\n",num); // 2

    double d = 5 / 2; // 整型 除以 整型 还是 整型

    printf("%f\n",d); // 2.000000

    double dd = 5.0 / 2; // 整型 除以 整型 还是 整型

    printf("%f\n",dd); // 2.500000

    return 0;
}

```

细细分析也对，否则会把你掰弯。



> 老九老师说，代码要敲三遍！第一遍，可以照着敲；第二遍，可以写注释，按照注释再写一遍；第三遍，独立的写出来。

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{
    int num = 10;
    num++;
    printf("%d\n",num); // 11

    return 0;
}


```

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{
    int num = 10;
    num++;
    printf("%d\n",num); // 11

    int num2 = 10;
    printf("%d\n",num2++); // 10

    int num3 = 10;
    printf("%d\n",++num3); // 11

    return 0;
}



```

由案例可以看出，num++ 是先输出，再加一。++num是先加一，再输出。



-------------------------------------

类型转换

自动转换

小范围的类型能够自动转换成大范围的类型。short->int->long->float->double



强制类型转换

（类型名）变量或数值



```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{
    // 大类型就相当于把一瓶酒中的水，倒入酒盅里，会洒

    double num = 6; // 小类型转大类型 - 自动类型转换
    int    num1=(int)num;// 大类型转小类型，损失精度 - 强制类型转换

    return 0;
}



```



运算符和条件结构

赋值运算符、算术运算符、关系运算符、逻辑运算符

表达式是由一系列[**操作符**]（operators）和[**操作数**]（operands）组成的。

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171115153604015-736701847.png)

赋值运算符

=、+=、-=、*=、/=、%=

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{

    // 复合运算符
    int num = 8;
    num %= 5;  // num = 8 % 5;
    printf("%d",num); // 3

    return 0;
}

```



算术运算符

一元：++、--

二元：+、-、*、/、%





关系运算符

\> 、<

\>=、<=

== 、 !=



```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{

    // 关系运算符
    int num1 = 5;
    int num2 = 8;
    int result = num1>num2;
    printf("%d\n",result); // 0

    return 0;
}

```



> 老九语录，在高级语言中才有true、false。c语言中没有这玩意。学习C语言能够增加大家的内功。



逻辑运算符

||   &&   ！

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{

    // 逻辑运算符
    int hasHouse; // 有房吗
    int hasCar;   // 有车吗

    printf("是否有房?\n");
    scanf("%d",&hasHouse);

    printf("是否有车?\n");
    scanf("%d",&hasCar);

    if (hasHouse && hasCar) {
        printf("可以结婚");
    } else {
        printf("不可以结婚");
    }

    return 0;
}

```



位运算符(转换为二进制进行计算)

& 

|

~

^

<<

\>>

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171115162047421-344193623.png)

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{

    // 逻辑运算符，位运算符
    printf("%d\n",4 && 2); // 1

    printf("%d\n",4 & 2); // 0 换算成二进制 0000-0100 0000-0010 与运算之后得到 0000-0110

    printf("%d\n",4 | 2); // 6 换算成二进制 0000-0100 0000-0010 或运算之后得到 0000-0110

    printf("%d\n",4 ^ 2); // 6 换算成二进制 0000-0100 0000-0010 位异或运算之后得到 0000-0110

    printf("%d\n",~4); // -5 换算成二进制 0000-0100 非运算之后得到 1111-1011(补码 -5) 原码10000101 反码11111010 补码11111011


    return 0;
}
```

原码(原码就是符号位加上真值的绝对值, 即用第一位表示符号，其余位表示值)、反码(正数的反码是其本身,负数的反码是在其原码的基础上，符号位不变，其余各个位取反)、补码(正数的补码就是其本身，负数的补码是在其原码的基础上，符号位不变， 其余各位取反，最后+1。【即在反码的基础上+1】)。

```
[+1] = [00000001]原 = [00000001]反 = [00000001]补
```

```
[-1] = [10000001]原 = [11111110]反 = [11111111]补
```

既然原码才是被人脑直接识别并用于计算表示方式，为何还会有反码和补码呢？

因为人脑可以知道第一位是符号位， 在计算的时候我们会根据符号位， 选择对真值区域的加减。 但是对于计算机， 加减乘数已经是最基础的运算， 要设计的尽量简单。计算机辨别"符号位"显然会让计算机的基础电路设计变得十分复杂！于是人们想出了将符号位也参与运算的方法。 我们知道，根据运算法则减去一个正数等于加上一个负数。即: 1-1 = 1 + (-1) = 0 ， 所以机器可以只有加法而没有减法，这样计算机运算的设计就更简单了。



原码计算: 1-1=0

```
1 - 1 = 1 + (-1) = [00000001]原 + [10000001]原 = [10000010]原 = -2
```

得到的结果是不正确的。



反码计算: 1-1=0

```
1 - 1 = 1 + (-1) = [0000 0001]原 + [1000 0001]原= [0000 0001]反 + [1111 1110]反 = [1111 1111]反 = [1000 0000]原 = -0
```

发现用反码计算减法，结果的真值部分是正确的。而唯一的问题其实就出现在"0"这个特殊的数值上。 虽然人们理解上+0和-0是一样的，但是0带符号是没有任何意义的。而且会有[0000 0000]原和[1000 0000]原两个编码表示0。

补码计算: 1-1=0

```
1-1 = 1 + (-1) = [0000 0001]原 + [1000 0001]原 = [0000 0001]补 + [1111 1111]补 = [0000 0000]补=[0000 0000]原 = 0
```

补码的出现解决了0的符号以及两个编码的问题。

-------------------------------------------------

#### sizeof可以获取数据类型的内存中的大小（字节）

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{

    // 逻辑运算符，位运算符
    int num = 8;
    int sizeOfNum = sizeof(num);
    printf("num的内容空间%d\n",sizeOfNum); // 4

    double num2 = 8;
    int sizeOfNum2 = sizeof(num2);
    printf("num的内容空间%d\n",sizeOfNum2); // 8

    return 0;
}


```

#### 运算符优先级

```c
#include <stdio.h>
#include <stdlib.h>

// standared 标准
// input output 输入/输出
// header 头 .h头文件

int main() // 返回int，如果是void表示没有返回
{
    // 算术运算符 + - * / %
    // 关系运算符 > < >= <= == !=
    // 逻辑运算符 && || !
    // 位运算符 & | ^ ~

    int num = 10;
    int result = num++ == 10 && --num == 10;

    /** 等同于
    int result1 = (num++ == 10);
    int result2 = (--num == 10);
    int result = result1 && result2;
    **/

    printf("%d\n",result); // 1

    return 0;
}

```

> 老九语录，这道题的思路是这样的，你看对不对？自己在讲解的时候，就渐渐的清晰了。学会问问题，学会讲解问题。

() sizeof ++ --

！



算术运算符 + - * / %

关系运算符 > < >= <= == !=



&&

||



赋值运算符

#### while循环

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    // while循环
    int i = 0;
    while (i<10) {
        printf("第%d遍\n",i);
        i++;
    }

    return 0;
}

```

while循环

循环三要素，循环变量的初值、判断、更新。也就是i的初值，判断，更新。



```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 计算1-100的和
    int sum;
    sum = 0;
    //    sum = (1+100) * 50;
    //    printf("1到100的和为:%d\n",sum);

    int i;
    i = 1;
    while (i <= 100) {
        sum = sum + i;
        i++;
    }
    printf("1到100的和为:%d\n",sum);

    return 0;
}

```

密码输错案例

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 使用循环实现三次密码错误，推出系统
    int i = 0;
    int password = 123456;
    int inPassword;


    while (i < 3) {
        printf("请输入密码:\n");
        scanf("%d",&inPassword);
        if (inPassword != password) {
            i++;
            printf("您输错了%d次\n",i);
        }
    }

    return 0;
}

```



```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 某宝15年交易额是800亿，按照每年递增25%，哪一年超过2000
    double trade_money = 800;
    int year = 2015;
    while (trade_money <= 2000) {
        trade_money *= 1.25;
        year++;
        printf("%d年交易额.2%lf\n",year,trade_money);
    }

    printf("某宝在%d年,交易额将超过2000亿，交易额为%.2lf\n",year,trade_money);

    return 0;
}

/*
2016年交易额1000.000000
2017年交易额1250.000000
2018年交易额1562.500000
2019年交易额1953.125000
2020年交易额2441.406250
某宝在2020年,交易额将超过2000亿，交易额为2441.406250
*/
```

小练习挺有意思的。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <windows.h>

int main() {
    // 这个很有用，否则rand()会一直41
    srand((unsigned) time(NULL));

    // 使用循环模拟实现玩家对战
    // 双方初始值HP均为100
    // 每次攻击5~15
    // HP最先到0或者以下的被KO
    int liubeiHP = 100;
    int sunquanHP = 100;

    int attack;

    int i = 0;
    while(1) {

        printf("************************************\n");
        i++;
        attack = (5 + rand()%11); // %11取值0-10

        if (attack == 15) {
            // 暴击
            attack *= 2;
        }

        sunquanHP -= attack;
        printf("孙权在第%d回合,受到伤害%d,剩余生命值%d\n",i,attack,sunquanHP);
        if (sunquanHP <= 0) {
            printf("孙权败了\n");
            break;
        }

        attack = (5 + rand()%11);
        if (attack == 15) {
            // 暴击
            attack *= 2;
        }
        liubeiHP -= attack;

        printf("刘备在第%d回合,受到伤害%d,剩余生命值%d\n",i,attack,liubeiHP);
        if (liubeiHP <= 0) {
            printf("刘备败了\n");
            break;
        }

        Sleep(500); // 需要引入<windows.h>


    }



    return 0;
}

/*
************************************
孙权在第1回合,受到伤害8,剩余生命值92
刘备在第1回合,受到伤害5,剩余生命值95
************************************
孙权在第2回合,受到伤害11,剩余生命值81
刘备在第2回合,受到伤害13,剩余生命值82
************************************
孙权在第3回合,受到伤害9,剩余生命值72
刘备在第3回合,受到伤害12,剩余生命值70
************************************
孙权在第4回合,受到伤害14,剩余生命值58
刘备在第4回合,受到伤害8,剩余生命值62
************************************
孙权在第5回合,受到伤害14,剩余生命值44
刘备在第5回合,受到伤害30,剩余生命值32
************************************
孙权在第6回合,受到伤害10,剩余生命值34
刘备在第6回合,受到伤害12,剩余生命值20
************************************
孙权在第7回合,受到伤害6,剩余生命值28
刘备在第7回合,受到伤害13,剩余生命值7
************************************
孙权在第8回合,受到伤害13,剩余生命值15
刘备在第8回合,受到伤害8,剩余生命值-1
刘备败了

*/

```



#### 调试

设置断点。

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171117004119046-323030734.png)

单步调试。

---------------------------------------------------------------------------------

do while



```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int a = 1,b = 10;
    do {
        b -= a;
        a++;
    } while (b-- < 0);

    printf("%d\n",b); // 8

    return 0;
}


```



不管条件是否满足都执行一次。

模拟dos游戏。

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int choice; // 用户的选择

    // 打印游戏菜单
    printf("性格测试:\n");
    printf("如果您是一位君王，对于身旁的伴侣，你希望十什么样的？\n");
    printf("1.只要有一位真爱的妻子\n");
    printf("2.可以有两位以上的爱人\n");
    printf("3.拥有三千佳丽\n");

    do { // 如果输入错误，将会一直输入
        printf("请选择:");
        scanf("%d",&choice);

        if (choice < 1 || choice >3) {
            printf("只能输入1-3之间的数字！请重新输入！\n");
        }
    } while(choice <1 || choice > 3);

    switch (choice) {
        case 1 :
            printf("你是好人");
            break;
        case 2:
            printf("贪得无厌");
            break;
        case 3:
            printf("大胆放肆");
            break;
    }

    return 0;
}

```

循环实现数字反转

```c
#include <stdio.h>
#include <stdlib.h>

int main() {

    // 使用循环实现数字反转
    int value,right_num;
    value = 0;
    do {
        printf("\n请输入一个数:");
        scanf("%d",&value);

        if (value <= 0) {
            printf("必须是正数!\n");
        }

    } while (value <= 0);


    printf ("\n反转后的数为:");

    do {
        right_num = value % 10;
        printf("%d",right_num);
        value = value / 10;
    } while (value != 0);
    printf("\n");
    return 0;
}


```

打印加法表

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int num;
    // 打印简单加法表
    printf("请输入一个数字：");

    scanf("%d",&num);

    int i ;
    for (i = 0 ;i <num; i++) {
        printf("%d + %d = %d",i,num-i,num);


        if (i % 2 == 1) {
            printf("\n");
        } else {
            printf("\t");
        }
    }


    return 0;
}


```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171121230209477-1581996604.png)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int age;

    // for (;;)

    while (1) {
        printf("请输入玩家年龄:\n");
        scanf("%d",&age);
        // 判断年龄是否大于0
        if (age<0) {
            break;
        }
    }
    printf("游戏结束！");

    return 0;
}


```

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 设定一个商品价格
    // 用户输入猜测的价格后，系统给出大小提示
    // 如果在5轮内就猜到，就给于奖励提示
    int price = 1000;
    int count = 0;

    int guessPrice;

    while (1) {
        printf("请输入商品价格:\n");
        scanf("%d",&guessPrice);

        count++;

        if (guessPrice > price) {
            printf("大了\n");
        }

        if (guessPrice < price) {
            printf("小了\n");
        }

        if (guessPrice == price) {
            if (count <=5 ) {
                printf("5轮之内就猜对了，你真棒！");
            } else {
                printf("猜对了!");
            }

            break;
        }
    }

    return 0;
}


```

![](http://images2017.cnblogs.com/blog/422101/201711/422101-20171121235256727-875879476.png)



```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 循环输入5个玩家的年龄，统计年龄为负数的次数
    int i;
    int age;
    int wrongCount = 0;

    for (i = 0 ; i< 5 ;i ++) {
        printf("请输入玩家年龄：\n");
        scanf("%d",&age);
        if (age > 0)
            continue;

        wrongCount++;
    }

    printf("错误的次数为%d",wrongCount);



    return 0;
}


```



```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // c语言算法题很有意思
    // 求1-100之间的偶数和
    int i = 1;

    int sum = 0;

    for (i ; i<= 100 ; i++) {
        if (i % 2 == 0) {
            sum += i;
        }
    }

    printf("1到100之间的偶数和为%d",sum);


    return 0;
}


```

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 用 "*" 输出一个菱形图案

    /*

         *
        ***
       *****
      *******
       *****
        ***
         *

      ###*
      ##***
      #*****
      *******
      #*****
      ##***
      ###*

    */


    // 设置双循环
    // 外层循环控制行，内层循环控制列
    int i,j;
    for (i = 0;i < 7;i ++) {

        int starNum;
        int spaceNum;
        if (i < 4) {
            starNum = i * 2 + 1;
            spaceNum = 3 - i;
        } else {
            starNum = (6 - i) * 2 + 1;
            spaceNum = (3 - (6 - i));
        }


        for (j = 0;j < spaceNum; j++) {
            printf(" ");
        }

        for (j = 0;j < starNum; j++) {
            printf("*");
        }
        printf("\n");
    }


    return 0;
}


```

太难了

-----

![](https://images2018.cnblogs.com/blog/422101/201711/422101-20171123231456140-1131558490.png)

![](https://images2018.cnblogs.com/blog/422101/201711/422101-20171123231851453-1765951930.png)



```c
#include <stdio.h>
#include <stdlib.h>

#define N 5
int main() {
    double score[5];
    int i;
    for (i = 0; i< N ;i++)
    {
        printf("请输入第%d门课的成绩:",i+1);
        scanf("%lf",&score[i]);
    }

    printf("---------------------\n");

    int j;
    for (j = 0; j< N ;j++)
    {
        printf("第%d门课的成绩为%.2lf\n",j+1,score[j]);
    }

    return 0;
}


```

综合的小练习

```c
#include <stdio.h>
#include <stdlib.h>

//宏定义布尔类型
#define BOOL int
#define TRUE 1
#define FALSE 0

int main() {
    int arr[] = {8,4,2,1,23,344,12};

    // 循环输出数组的值
    int length;

    length = sizeof(arr)/sizeof(arr[0]);

    int i;
    for (i=0;i<length;i++) {
        printf("数组第%d个元素值为%d\n",i+1,arr[i]);
    }

    // 求数组中所有元素的和与平均值
    double sum = 0;
    double average;
    for (i=0;i<length;i++) {
        sum += arr[i];
    }

    average = sum / length;

    printf("数组元素的和为：%.2lf\n",sum);
    printf("数组元素的平均值为：%.2lf\n",average);

    // 输入数值判断是否存在数组中，循环五次
    int guessNum;
    int count = 0;
    BOOL isInArray;
    while (count < 5) {
        printf("请输入数值：");
        scanf("%d",&guessNum);

        isInArray = FALSE;
        for (i=0;i<length;i++) {
            if (guessNum == arr[i]) {
                isInArray = TRUE;
                break;
            }
        }

        if (isInArray) {
            printf("输入的数值在数组中\n");
        } else {
            printf("输入的数值不在数组中\n");
        }

        count++;
    }





    return 0;
}



```

冒泡排序

```c
#include <stdio.h>
#include <stdlib.h>

//宏定义布尔类型
#define SIZE 5

int main() {
    // 循环录入5个整型数字，进行降序排列后输出

    // 冒泡排序

    int arr[SIZE] = {};
    int i;
    printf("请输入5个数字:\n");
    for (i = 0;i<SIZE;i++) {
        scanf("%d",&arr[i]);
    }

    for (i=0;i<SIZE;i++) {
        printf("输入第%d个数字为:%d\n",i,arr[i]);
    }

    // 进行冒泡排序，降序排列，大的排在前面，小的排在后面
    bubble_sort(arr,SIZE);
    printf("降序排序后的顺序为:\n");

    for (i=0;i<SIZE;i++) {
        printf("输入第%d个数字为:%d\n",i,arr[i]);
    }



    return 0;
}

// 冒泡函数
void bubble_sort(int a[],int n) {
    int i,j,temp;
    for (i=0;i<n-1;i++) { // 只需要n-1轮

        // 每一轮的比较
        for (j=0;j<n-1-i;j++) { // 每一轮比较的次数都会越来越少
            // 核心的判断
            if (a[j] < a[j+1]) {
                // 交换位置，大的排在前面
                temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
            }
        }
    }
}


```

删除真心费劲，感觉还是php操作数组更加便捷。

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 数组删除元素
    int count = 5;
    double powers[] = {42322,25771,40907,41234,40767};
    double deletePower; // 用户要删除的战力值
    int deleteIndex = -1; // 要删除的战力值的下标
    int i;

    printf("请输入要删除的战力值:\n");
    scanf("%lf",&deletePower);

    for (i= 0;i<count;i++) {
        if (deletePower == powers[i]) {
            // 记录下标
            deleteIndex = i;
            break;
        }
    }

    // 判断是否找到
    if (deleteIndex >=0) {
        // 从下标开始，后面一个覆盖前面一个数字
        for (i = deleteIndex ; i <count -1;i++) {
            powers[i] = powers[i+1];
        }
    } else {
        printf("很遗憾，没有找到要删除的战力值");
    }

    for (i=0;i<count-1;i++) {
        printf("第%d个元素为:%.2lf\n",i,powers[i]);
    }



    return 0;
}

```



二维数组

![](https://images2018.cnblogs.com/blog/422101/201711/422101-20171127200353565-583612307.png)

![](https://images2018.cnblogs.com/blog/422101/201711/422101-20171127200955784-972888749.png)

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // 使用二维数组表示学生的成绩，并展示
    double scores[4][3] = {
        {98,67,93},
        {88,87,93},
        {98,65,93},
        {68,67,93}
    };

    int i,j;
    // 使用双循环输出
    for (i = 0;i<4;i++) {
        for (j=0;j<3;j++) {
            printf("%.2lf\t",scores[i][j]);
        }

        printf("\n");
    }

    return 0;
}


```

不如php灵活。



-----------------------------------------------------------

一个综合的游戏，对所学知识进行整合！

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h> // 支持字符串操作
#include <windows.h>
#include <mmsystem.h>
#pragma comment(lib,"winmm.lib")

#define MAX 6 // 最大的妃子数量
int main()
{
    // 项请目实践之陛下翻牌
    // 播放音乐
    PlaySound(TEXT("sounds\\背景音乐.wav"),NULL,SND_FILENAME | SND_ASYNC | SND_LOOP);


    // 8个字符能存放4个汉字
    char tempName[20];
    // 定义二维数组来存放妃子
    char names[MAX][20] = {"西施","貂蝉","王昭君","杨玉环","赵飞燕"};

    // 定义二维数组来存放妃子等级
    char levelNames[5][8] = {"贵人","嫔妃","贵妃","皇贵妃","皇后"};

    // 存放每个妃子的等级
    int levels[MAX] = {0,0,2,0,0,-1};

    // 用来存放每个妃子的好感度
    int loves[MAX] = {100,100,100,100,100,-1};

    int i,j,temp; // 用于冒泡排序
    int count = 5; // 当前未被打入冷宫的妃子数量
    int day = 1; // 第几天

    /*
    printf("测试代码：查看当前嫔妃的状态\n");
    printf("%-12s级别\t好感度\n","姓名");
    for (i = 0;i <count;i++) {
        printf("%-12s%s\t%d\n",names[i],levelNames[levels[i]],loves[i]);
    }
    */

    // 皇帝的名号
    char emperorName[50];
    // 皇帝的选择
    int choice;

    int selectIndex; // 选择的妃子的index

    // 使用字符数组表示字符串
    printf("请输入当前登基的皇帝名号:");

    scanf("%s",emperorName); // 录入字符串
    printf("当前皇帝是【%s】,万岁万岁万万岁!\n",emperorName);


    while (day <= 10) {
        printf("******************************************************\n");
        printf("第%d天\n",day);
        day++;

        // 做出菜单
        printf("1.皇帝下旨选妃\t\t (增加)\n");

        printf("2.翻牌宠幸 \t\t (修改状态)\n");

        printf("3.打入冷宫 \t\t (删除)\n");

        printf("4.召见爱妃去谈心 \n");

        printf("陛下请选择： \n");


        scanf("%d",&choice);

        switch(choice) {
            case 1: // 1.皇帝下旨选妃\t\t (增加)\n
                PlaySound(TEXT("sounds\\选妃.wav"),NULL,SND_FILENAME | SND_ASYNC);

                if (count < MAX) {
                    // 执行添加操作
                    printf("请输入娘娘的名讳:");
                    scanf("%s",names[count]);
                    // 初始化状态
                    levels[count] = 0;
                    loves[count]  = 100;

                    count++;

                } else {
                    printf("陛下要注意龙体啊，后宫已经人满为患！\n");
                }


                break;

            case 2: // 2.翻牌宠幸 \t\t (修改状态)\n
                PlaySound(TEXT("sounds\\翻牌.wav"),NULL,SND_FILENAME | SND_ASYNC);
                // 1. 找到妃子
                // 2. 修改妃子状态 好感度+10 级别升1级 最高级不再升
                // 3. 修改其他妃子的状态 其他妃子 好感度 -10
                printf("陛下请输入今天要翻牌的妃子：");
                scanf("%s",tempName);

                selectIndex = -1;

                // strcmp(tempName,"abc") 0表示两个字符串相等，1表示前一个大于后一个，-1表示前一个小于后一个
                for (i = 0;i<count ;i++) {
                    if (strcmp(tempName,names[i]) == 0) {
                        selectIndex = i;
                        break;
                    }
                }

                if (selectIndex == -1) {
                    printf("皇上，这个妃子不存在啊！\n");
                    break;
                }

                // 更改选中人的状态
                if (levels[selectIndex] < 4) {
                    levels[selectIndex] += 1;
                }
                loves[selectIndex]  += 10;

                // 更改其他妃子的状态
                for (i = 0;i<count ;i++) {
                    if (i != selectIndex) {
                        loves[i]  -= 10;
                    }
                }


                break;


            case 3: // 3.打入冷宫 \t\t (删除)\n
                PlaySound(TEXT("sounds\\冷宫.wav"),NULL,SND_FILENAME | SND_ASYNC);
                // 1.查找
                // 2.后面一个赋给前面一个
                // 3.总数--
                printf("请输入需要打入冷宫的妃子姓名：");
                scanf("%s",tempName);

                selectIndex = -1;

                // strcmp(tempName,"abc") 0表示两个字符串相等，1表示前一个大于后一个，-1表示前一个小于后一个
                for (i = 0;i<count ;i++) {
                    if (strcmp(tempName,names[i]) == 0) {
                        selectIndex = i;
                        break;
                    }
                }

                if (selectIndex == -1) {
                    printf("皇上，这个妃子不存在啊！\n");
                    break;
                }

                for (i = selectIndex ; i<count - 1;i++) {
                    // names[i] = names[i + 1]; C语言中不支持数组的直接赋值，字符串在C语言中就是数组
                    strcpy(names[i],names[i+1]);
                    loves[i] = loves[i + 1];
                    levels[i] = levels[i + 1];
                }
                count-- ;

                break;


            case 4: // 4.召见爱妃去谈心 \n
                PlaySound(TEXT("sounds\\一笑倾城.wav"),NULL,SND_FILENAME | SND_ASYNC);

                printf("请输入需要单独约见的妃子姓名：");
                scanf("%s",tempName);

                selectIndex = -1;

                // strcmp(tempName,"abc") 0表示两个字符串相等，1表示前一个大于后一个，-1表示前一个小于后一个
                for (i = 0;i<count ;i++) {
                    if (strcmp(tempName,names[i]) == 0) {
                        selectIndex = i;
                        loves[i] += 10;
                        break;
                    }
                }

                if (selectIndex == -1) {
                    printf("皇上，这个妃子不存在啊！\n");
                    break;
                }

                break;

            default:
                printf("君无戏言，陛下请再次确认！\n");
                break;

        }

        // 播放背景音乐
        PlaySound(TEXT("sounds\\背景音乐.wav"),NULL,SND_FILENAME | SND_ASYNC | SND_LOOP);

        // 按照级别进行排序，使用冒泡排序
        for (i = 0;i<count-1;i++) {
            for ( j = 0;j< count - i - 1;j++) {
                if (levels[j] < levels[j+1]) { // 交换
                    temp = levels[j];
                    levels[j] = levels[j+1];
                    levels[j+1] = temp;

                    temp = loves[j];
                    loves[j] = loves[j+1];
                    loves[j+1] = temp;

                    strcpy(tempName,names[j]);
                    strcpy(names[j],names[j+1]);
                    strcpy(names[j+1],tempName);
                }
            }
        }

        printf("当前后宫人员状态\n");
        printf("%-12s级别\t好感度\n","姓名");
        for (i = 0;i <count;i++) {
            printf("%-12s%s\t%d\n",names[i],levelNames[levels[i]],loves[i]);
        }

        for (i = 0;i <count ;i++) {
            if (loves[i] < 60) {
                printf("皇上，有妃子被冷落了，生了杀意。游戏失败。\n");

                // 跳转到over的位置
                goto over;
            }
        }


    }


    printf("恭喜你，赢了!\n");

    over:


    return 0;
}

```

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171201223928714-292179589.png)



------------------------

指针，c语言的灵魂

指针是一个值为内存地址的变量。

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171201234925995-380852705.png)

变量是一块内存空间，指针是变量，是用来存储内存地址的变量。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int num = 9;
    printf("num变量的地址为:%p\n",&num); // p表示指针占位符
    return 0;
}

```

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171202001653933-779517732.png)

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int num = 9;
    int * ptr_num = &num;
    printf("num变量的地址为:%p\n",ptr_num); // p表示指针占位符
    return 0;
}

```

![](http://images2017.cnblogs.com/blog/422101/201712/422101-20171202002223120-68238159.png)



根据地址，找到空间！然后操作空间！

**变量地址也占用空间，只不过占用的不是内存空间，而是寄存器的存储空间。**

**内存地址实际上是一种偏移量，存储于段寄存器中。内存地址只是一种抽象，不是真正的物理内存地址，而是逻辑地址。由逻辑地址寻找到物理地址需要经过 逻辑地址->线性地址->物理地址 转换过程，而这些过程都是基于寄存器完成的。**

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int num = 9;
    int * ptr_num = &num;
    * ptr_num = 10;
    printf("* ptr_num的值为:%d\n",* ptr_num);
    printf("num的值为:%d\n",num); // p表示指针占位符
    return 0;
}

```



**指针的类型，跟他所指向的数据结构有关。**
**基本类型的指针指向基本类型的数据结构。**
比如：char * p; int *p; float *p; double *p;
**分别指向的是char， int ，float,  double 类型的变量。**