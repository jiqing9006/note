
![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180126110322365-1037792584.png)


c语言面向过程

c++支持面向过程+支持面向对象

```cpp
#include <iostream>

using namespace std;

int main()
{
    int a;
    cout << "请输入a的值:" << endl;
    cin  >> a;
    cout << "a的值为:" << a << endl;
    return 0;
}

```

挺方便的。不用关注占位符。不用关注数据类型。

endl 相当于回车。

或者下面这样使用，

```cpp
#include <iostream>

// using namespace std; // 张家-小强 李家-小强
int main()
{
    int a;
    std::cout << "请输入a的值:" << std::endl;
    std::cin  >> a;
    std::cout << "a的值为:" << a << std::endl;
    return 0;
}

```

或者

```c
#include <iostream>

using std::cout;
using std::cin;
using std::endl;

int main()
{
    int a;
    cout << "请输入a的值:" << endl;
    cin  >> a;
    cout << "a的值为:" << a << endl;
    return 0;
}

```

------------------------------------

预处理

```
E:\CppSpace\hello>g++ -o main.i -E main.cpp

E:\CppSpace\hello>dir /p
 驱动器 E 中的卷是 固盘-项目
 卷的序列号是 0000-5D89

 E:\CppSpace\hello 的目录

2018/01/27/周六  09:52    <DIR>          .
2018/01/27/周六  09:52    <DIR>          ..
2018/01/26/周五  11:18    <DIR>          bin
2018/01/26/周五  11:18             1,065 hello.cbp
2018/01/26/周五  17:42                93 hello.depend
2018/01/26/周五  17:39               358 hello.layout
2018/01/27/周六  09:35               214 main.cpp
2018/01/27/周六  09:52           447,921 main.i
```

```
# 2 "main.cpp" 2

using std::cout;
using std::cin;
using std::endl;

int main()
{
    int a;
    cout << "xxx:" << endl;
    cin >> a;
    cout << "xxx:" << a << endl;
    return 0;
}

```





将预处理文件转为汇编文件

```
E:\CppSpace\hello>g++ -o main.s -S main.i

E:\CppSpace\hello>dir /p
 驱动器 E 中的卷是 固盘-项目
 卷的序列号是 0000-5D89

 E:\CppSpace\hello 的目录

2018/01/27/周六  10:11    <DIR>          .
2018/01/27/周六  10:11    <DIR>          ..
2018/01/26/周五  11:18    <DIR>          bin
2018/01/26/周五  11:18             1,065 hello.cbp
2018/01/26/周五  17:42                93 hello.depend
2018/01/26/周五  17:39               358 hello.layout
2018/01/27/周六  09:35               214 main.cpp
2018/01/27/周六  09:52           447,921 main.i
2018/01/27/周六  10:11             2,574 main.s
2018/01/26/周五  11:18    <DIR>          obj
               6 个文件        452,225 字节
               4 个目录  7,373,844,480 可用字节
```

```
	.file	"main.cpp"
.lcomm __ZStL8__ioinit,1,1
	.def	___main;	.scl	2;	.type	32;	.endef
	.section .rdata,"dr"
LC0:
	.ascii "\307\353\312\344\310\353a\265\304\326\265:\0"
LC1:
	.ascii "a\265\304\326\265\316\252:\0"
	.text
	.globl	_main
	.def	_main;	.scl	2;	.type	32;	.endef
_main:
	leal	4(%esp), %ecx
	andl	$-16, %esp
	pushl	-4(%ecx)
	pushl	%ebp
	movl	%esp, %ebp
	pushl	%ebx
	pushl	%ecx
	subl	$32, %esp
	call	___main
	movl	$LC0, 4(%esp)
	movl	$__ZSt4cout, (%esp)
	call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
	movl	$__ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_, (%esp)
	movl	%eax, %ecx
	call	__ZNSolsEPFRSoS_E
	subl	$4, %esp
	leal	-12(%ebp), %eax
	movl	%eax, (%esp)
	movl	$__ZSt3cin, %ecx
	call	__ZNSirsERi
	subl	$4, %esp
	movl	-12(%ebp), %ebx
	movl	$LC1, 4(%esp)
	movl	$__ZSt4cout, (%esp)
	call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
	movl	%ebx, (%esp)
	movl	%eax, %ecx
	call	__ZNSolsEi
	subl	$4, %esp
	movl	$__ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_, (%esp)
	movl	%eax, %ecx
	call	__ZNSolsEPFRSoS_E
	subl	$4, %esp
	movl	$0, %eax
	leal	-8(%ebp), %esp
	popl	%ecx
	popl	%ebx
	popl	%ebp
	leal	-4(%ecx), %esp
	ret
	.def	___tcf_0;	.scl	3;	.type	32;	.endef
___tcf_0:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	movl	$__ZStL8__ioinit, %ecx
	call	__ZNSt8ios_base4InitD1Ev
	leave
	ret
	.def	__Z41__static_initialization_and_destruction_0ii;	.scl	3;	.type	32;	.endef
__Z41__static_initialization_and_destruction_0ii:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$24, %esp
	cmpl	$1, 8(%ebp)
	jne	L4
	cmpl	$65535, 12(%ebp)
	jne	L4
	movl	$__ZStL8__ioinit, %ecx
	call	__ZNSt8ios_base4InitC1Ev
	movl	$___tcf_0, (%esp)
	call	_atexit
L4:
	leave
	ret
	.def	__GLOBAL__sub_I_main;	.scl	3;	.type	32;	.endef
__GLOBAL__sub_I_main:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$24, %esp
	movl	$65535, 4(%esp)
	movl	$1, (%esp)
	call	__Z41__static_initialization_and_destruction_0ii
	leave
	ret
	.section	.ctors,"w"
	.align 4
	.long	__GLOBAL__sub_I_main
	.ident	"GCC: (tdm-1) 4.9.2"
	.def	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc;	.scl	2;	.type	32;	.endef
	.def	__ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_;	.scl	2;	.type	32;	.endef
	.def	__ZNSolsEPFRSoS_E;	.scl	2;	.type	32;	.endef
	.def	__ZNSirsERi;	.scl	2;	.type	32;	.endef
	.def	__ZNSolsEi;	.scl	2;	.type	32;	.endef
	.def	__ZNSt8ios_base4InitD1Ev;	.scl	2;	.type	32;	.endef
	.def	__ZNSt8ios_base4InitC1Ev;	.scl	2;	.type	32;	.endef
	.def	_atexit;	.scl	2;	.type	32;	.endef

```



把汇编文件转为二进制文件

```
E:\CppSpace\hello>g++ -o main.o -c main.s
```

```
4c01 0600 0000 0000 f602 0000 1f00 0000
0000 0401 2e74 6578 7400 0000 0000 0000
0000 0000 f000 0000 0401 0000 2402 0000
0000 0000 1400 0000 2000 3060 2e64 6174
6100 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
4000 30c0 2e62 7373 0000 0000 0000 0000
0000 0000 0400 0000 0000 0000 0000 0000
0000 0000 0000 0000 8000 30c0 2e72 6461
7461 0000 0000 0000 0000 0000 1800 0000
f401 0000 0000 0000 0000 0000 0000 0000
4000 3040 2e63 746f 7273 0000 0000 0000
0000 0000 0400 0000 0c02 0000 ec02 0000
0000 0000 0100 0000 4000 30c0 2f34 0000
0000 0000 0000 0000 0000 0000 1400 0000
1002 0000 0000 0000 0000 0000 0000 0000
4000 3040 8d4c 2404 83e4 f0ff 71fc 5589
e553 5183 ec20 e800 0000 00c7 4424 0400
0000 00c7 0424 0000 0000 e800 0000 00c7
0424 0000 0000 89c1 e800 0000 0083 ec04
8d45 f489 0424 b900 0000 00e8 0000 0000
83ec 048b 5df4 c744 2404 0d00 0000 c704
2400 0000 00e8 0000 0000 891c 2489 c1e8
0000 0000 83ec 04c7 0424 0000 0000 89c1
e800 0000 0083 ec04 b800 0000 008d 65f8
595b 5d8d 61fc c355 89e5 83ec 08b9 0000
0000 e800 0000 00c9 c355 89e5 83ec 1883
7d08 0175 1f81 7d0c ffff 0000 7516 b900
0000 00e8 0000 0000 c704 2493 0000 00e8
0000 0000 c9c3 5589 e583 ec18 c744 2404
ffff 0000 c704 2401 0000 00e8 b9ff ffff
c9c3 9090 c7eb cae4 c8eb 61b5 c4d6 b53a
0061 b5c4 d6b5 ceaa 3a00 0000 d200 0000
4743 433a 2028 7464 6d2d 3129 2034 2e39
2e32 0000 1300 0000 1400 0000 1400 1b00
0000 0e00 0000 0600 2200 0000 1500 0000
0600 2700 0000 1700 0000 1400 2e00 0000
1800 0000 0600 3500 0000 1900 0000 1400
4300 0000 1600 0000 0600 4800 0000 1a00
0000 1400 5600 0000 0e00 0000 0600 5d00
0000 1500 0000 0600 6200 0000 1700 0000
1400 6c00 0000 1b00 0000 1400 7600 0000
1800 0000 0600 7d00 0000 1900 0000 1400
9a00 0000 0c00 0000 0600 9f00 0000 1c00
0000 1400 bb00 0000 0c00 0000 0600 c000
0000 1d00 0000 1400 c700 0000 0800 0000
0600 cc00 0000 1e00 0000 1400 0000 0000
0800 0000 0600 2e66 696c 6500 0000 0000
0000 feff 0000 6701 6d61 696e 2e63 7070
0000 0000 0000 0000 0000 0000 0000 0f00
0000 0000 0000 0300 0000 0300 5f6d 6169
6e00 0000 0000 0000 0100 2000 0201 0000
0000 0000 0000 0000 0000 0000 0000 0000
5f5f 5f74 6366 5f30 9300 0000 0100 2000
0300 0000 0000 1f00 0000 a500 0000 0100
2000 0300 0000 0000 5000 0000 d200 0000
0100 2000 0300 2e74 6578 7400 0000 0000
0000 0100 0000 0301 ee00 0000 1400 0000
0000 0000 0000 0000 0000 2e64 6174 6100
0000 0000 0000 0200 0000 0301 0000 0000
0000 0000 0000 0000 0000 0000 0000 2e62
7373 0000 0000 0000 0000 0300 0000 0301
0100 0000 0000 0000 0000 0000 0000 0000
0000 2e72 6461 7461 0000 0000 0000 0400
0000 0301 1600 0000 0000 0000 0000 0000
0000 0000 0000 2e63 746f 7273 0000 0000
0000 0500 0000 0301 0400 0000 0100 0000
0000 0000 0000 0000 0000 0000 0000 6500
0000 0000 0000 0600 0000 0301 1300 0000
0000 0000 0000 0000 0000 0000 0000 5f5f
5f6d 6169 6e00 0000 0000 0000 2000 0200
0000 0000 7000 0000 0000 0000 0000 0000
0200 0000 0000 7b00 0000 0000 0000 0000
0000 0200 0000 0000 8500 0000 0000 0000
0000 2000 0200 0000 0000 be00 0000 0000
0000 0000 2000 0200 0000 0000 fa00 0000
0000 0000 0000 2000 0200 0000 0000 0c01
0000 0000 0000 0000 2000 0200 0000 0000
1801 0000 0000 0000 0000 2000 0200 0000
0000 2301 0000 0000 0000 0000 2000 0200
0000 0000 3c01 0000 0000 0000 0000 2000
0200 5f61 7465 7869 7400 0000 0000 0000
2000 0200 5501 0000 2e72 6461 7461 247a
7a7a 005f 5f5a 5374 4c38 5f5f 696f 696e
6974 005f 5f5a 3431 5f5f 7374 6174 6963
5f69 6e69 7469 616c 697a 6174 696f 6e5f
616e 645f 6465 7374 7275 6374 696f 6e5f
3069 6900 5f5f 474c 4f42 414c 5f5f 7375
625f 495f 6d61 696e 002e 7264 6174 6124
7a7a 7a00 5f5f 5a53 7434 636f 7574 005f
5f5a 5374 3363 696e 005f 5f5a 5374 6c73
4953 7431 3163 6861 725f 7472 6169 7473
4963 4545 5253 7431 3362 6173 6963 5f6f
7374 7265 616d 4963 545f 4553 355f 504b
6300 5f5f 5a53 7434 656e 646c 4963 5374
3131 6368 6172 5f74 7261 6974 7349 6345
4552 5374 3133 6261 7369 635f 6f73 7472
6561 6d49 545f 5430 5f45 5336 5f00 5f5f
5a4e 536f 6c73 4550 4652 536f 535f 4500
5f5f 5a4e 5369 7273 4552 6900 5f5f 5a4e
536f 6c73 4569 005f 5f5a 4e53 7438 696f
735f 6261 7365 3449 6e69 7444 3145 7600
5f5f 5a4e 5374 3869 6f73 5f62 6173 6534
496e 6974 4331 4576 00
```

连接执行，

```
E:\CppSpace\hello>g++ -o main.exe main.o

E:\CppSpace\hello>main.exe
请输入a的值:
100
a的值为:100
```

![](http://images2017.cnblogs.com/blog/422101/201801/422101-20180127102353397-2141021222.png)



---------------------------------

指令 - 命令，操控计算机去做一些事情。

```cpp
#include <iostream>
#include <cmath>
#include <iomanip>

using namespace std;

int main()
{
    cout << fixed;
    cout << setprecision(2);

    double num = 100.0 / 3.0;
    cout << num << endl;
    return 0;
}

```

