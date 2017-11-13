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