c语言中可以选择的数据类型太少了。
Java中有一些高级的数据结构。
结构中能够存放基本的数据类型以及其他的结构。
结构定义，一般放在程序的开头部分。
一般放在include之后。
```
#include <stdio.h>
#include <string.h>
struct Hero {
    int id;
    char name[50]; // 英雄名称
    int level;     // 英雄的等级
    int hp;        // 英雄的血量
    int mp;        // 英雄的魔法值
    char skill[50];  // 英雄的技能

};
int main()
{
    // 使用结构体
    struct Hero hero1;
    hero1.id = 1;
    strcpy(hero1.name ,"张三");
    hero1.level = 5;
    hero1.hp = 500;
    hero1.mp = 100;
    strcpy(hero1.skill,"大保健");
    printf("%d\t%s\t%d\t%d\t%s\n",hero1.id,hero1.name,hero1.level,hero1.hp,hero1.skill);

    return 0;
}

```

```
#include <stdio.h>
#include <string.h>
typedef struct Hero {
    int id;
    char name[50]; // 英雄名称
    int level;     // 英雄的等级
    int hp;        // 英雄的血量
    int mp;        // 英雄的魔法值
    char skill[50];  // 英雄的技能

} Hero1;
int main()
{
    // 使用结构体
    Hero1 hero1;
    hero1.id = 1;
    strcpy(hero1.name ,"张三");
    hero1.level = 5;
    hero1.hp = 500;
    hero1.mp = 100;
    strcpy(hero1.skill,"大保健");
    printf("%d\t%s\t%d\t%d\t%s\n",hero1.id,hero1.name,hero1.level,hero1.hp,hero1.skill);

    return 0;
}
```
----------------------------------------

源代码分门别类管理，通过头文件。

放置一些函数声明，变量声明，常量定义，宏定义。

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180116143632943-217232907.png)

hotel.h

```c
#ifndef HOTEL_H_INCLUDED
#define HOTEL_H_INCLUDED

#define HOTEL1 872.0 // 各家酒店的默认房费
#define HOTEL2 1838.0 // 各家酒店的默认房费
#define HOTEL3 789.0 // 各家酒店的默认房费
#define HOTEL4 1658.0 // 各家酒店的默认房费
#define DISCOUNT 0.95 // 折扣率


// 菜单函数：显示菜单选项，接收并返回用户的输入
int Menu(void);

// 返回用户预订的天数
int GetNights(void);

// 根据入住的天数显示最终需要支付的金额
double ShowPrice(int choice,int nights);
#endif // HOTEL_H_INCLUDED

```



hotel.c

```c
#include <stdio.h>
// 自定义的头文件用双引号
#include "hotel.h"

char hotelNames[4][50] = {
    "贝罗酒店","香榭丽舍酒店","阿斯图里亚斯酒店","斯克里布酒店"
};

int Menu(void) {
    int choice; // 用户的选择
    int i;
    printf("请选择入住的酒店：\n");
    for (i = 0; i< 4;i++) {
        printf("%d、%s\n",i+1,hotelNames[i]); // 写完就去main中测试一下
    }

    printf("5、退出程序\n");

    printf("请输入您的选择：");

    int result = scanf("%d",&choice);

    // 判断是否合法
    while ( result !=1 || choice < 1 || choice >5 ) {
        if (result != 1) {
            scanf("%*s"); // 消除错误的输入
            // fflush(stdin);
        }

        printf("必须输入1-5之间的整数:");
        result = scanf("%d",&choice);
    }



    return choice;
}

int GetNights(void) {
    int nights;

    printf("先生、女士，请输入要入住的天数：");

    int result = scanf("%d",&nights);

    // 判断是否合法
    while ( result !=1 || nights < 1) {
        if (result != 1) {
            scanf("%*s"); // 消除错误的输入
            // fflush(stdin);
        }

        printf("必须输入大于1的整数！\n");
        printf("先生、女士，请输入要入住的天数：");
        result = scanf("%d",&nights);
    }

    return nights;
}

double ShowPrice(int choice,int nights) {
    double hotelPrice;
    double totalPrice = 0;
    if (choice == 1) {
        hotelPrice = HOTEL1;
    }

    if (choice == 2) {
        hotelPrice = HOTEL2;
    }

    if (choice == 3) {
        hotelPrice = HOTEL3;
    }

    if (choice == 4) {
        hotelPrice = HOTEL4;
    }

    int i;
    for (i = 0 ;i<nights ;i ++ ) {
        if (i == 0) {
            totalPrice = hotelPrice * DISCOUNT;
        } else {
            totalPrice += hotelPrice * DISCOUNT;
        }

        hotelPrice = hotelPrice * DISCOUNT;
    }

    return totalPrice;

}

```

main.c

```c
#include <stdio.h>
#include <stdlib.h>
#include "hotel.h"  // 最好引入一下头文件
extern char hotelNames[4][50]; // 声明为外部变量

int main()
{
    int choice;
    int nights;
    double totalPrice;
    // 用户输入入住的酒店和天数，程序计算出对应的金额
    // 1.显示菜单 - 封装成函数
    choice = Menu();

    if (choice > 0 && choice <5) {
        printf("当前用户选择的是：%s\n",hotelNames[choice-1]); // 多遇到一些错误，在错误中成长。将顺序思维，改为模块思维。
    }

    if (choice == 5) {
        printf("欢迎使用本系统,再见。\n");
        exit(0);
    }


    nights = GetNights();
    if (nights > 0) {
        printf("当前用户选择入住%d天\n",nights); // 多遇到一些错误，在错误中成长。将顺序思维，改为模块思维。
    }

    // 2.计算过程
    totalPrice = ShowPrice(choice,nights);
    printf("您入住的酒店是:%s \t 入住天数： %d \t 总费用： %0.2f \n",hotelNames[choice-1],nights,totalPrice);

    printf("欢迎使用本系统,再见。\n");
    return 0;
}

```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180116143856099-668380070.png)



--------------------------

结构体中定义结构体

```c
#include <stdio.h>
#include <string.h>

/* 门派 */
struct Martial {
    int id;
    char name[50];
    int count;
    int type; // 门派的类型 1 正派 2 中立 3 邪派
};

struct Player {
    int id;
    char name[50];
    char pass[50];
    char sex;
    struct Martial martial; // 玩家所属门派
};


int main()
{
    struct Martial martial1 = {1,"人族",500,1};
    struct Martial martial2 = {2,"兽族",500,3};

    struct Player player1 = {1,"小强","123456",'f',martial1};

    printf("玩家%s \t 所属帮派%s \t",player1.name,player1.martial.name);

    return 0;
}


```

结构体与类的区别在于，结构体中只有属性。类中，有属性也有方法。

指针，指向结构。

结构指针变量指向的地址就是结构的首地址。

struct 结构名称 * 结构指针变量名。

访问的方式：

（*结构指针变量）.成员变量名

结构指针变量->成员变量名

```c
#include <stdio.h>
#include <string.h>

/* 门派 */
struct Martial {
    int id;
    char name[50];
    int count;
    int type; // 门派的类型 1 正派 2 中立 3 邪派
};

struct Player {
    int id;
    char name[50];
    char pass[50];
    char sex;
    struct Martial martial; // 玩家所属门派
};


int main()
{
    struct Martial martial1 = {1,"人族",500,1};
    struct Martial martial2 = {2,"兽族",500,3};

    struct Player player1 = {1,"小强","123456",'f',martial1};

    // 定义结构体指针，指向结构体
    struct Player * ptr_player1 = &player1;

    printf("玩家%s \t 所属帮派%s \n",player1.name,player1.martial.name);
    printf("玩家%s \t 所属帮派%s \n",ptr_player1->name,ptr_player1->martial.name); // -> 指针访问
    printf("玩家%s \t 所属帮派%s \n",(*ptr_player1).name,(*ptr_player1).martial.name);

    return 0;
}

```

