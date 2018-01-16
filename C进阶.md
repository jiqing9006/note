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

