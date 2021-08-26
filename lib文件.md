## lib文件

本词条由[“科普中国”科学百科词条编写与应用工作项目](https://baike.baidu.com/science) 审核 。

.lib是一种[文件名后缀](https://baike.baidu.com/item/文件名后缀/8299429)，代表的是[静态数据](https://baike.baidu.com/item/静态数据/10528956)连接库，在[windows操作系统](https://baike.baidu.com/item/windows操作系统/852149)中起到链接程序和函数（或子过程）的作用，相当于[Linux](https://baike.baidu.com/item/Linux)中的.a或.o、.so文件。

- 中文名

  lib文件

- 外文名

  lib File

- 选  择

  通过vc自带的depends查看dll接口

- 分  类

  静态与动态之分

## 目录

1. 1 [意义](https://baike.baidu.com/item/lib文件/2108657#1)
2. ▪ [静态编译](https://baike.baidu.com/item/lib文件/2108657#1_1)
3. ▪ [动态编译](https://baike.baidu.com/item/lib文件/2108657#1_2)
4. 2 [详细说明](https://baike.baidu.com/item/lib文件/2108657#2)
5. ▪ [内容](https://baike.baidu.com/item/lib文件/2108657#2_1)

1. 3 [与dll区别](https://baike.baidu.com/item/lib文件/2108657#3)
2. 4 [加载方法](https://baike.baidu.com/item/lib文件/2108657#4)
3. ▪ [直接加入](https://baike.baidu.com/item/lib文件/2108657#4_1)
4. ▪ [设置](https://baike.baidu.com/item/lib文件/2108657#4_2)
5. ▪ [程序代码](https://baike.baidu.com/item/lib文件/2108657#4_3)

1. 5 [生成工具](https://baike.baidu.com/item/lib文件/2108657#5)
2. 6 [生成步骤](https://baike.baidu.com/item/lib文件/2108657#6)
3. 7 [lib文件的使用](https://baike.baidu.com/item/lib文件/2108657#7)

## 意义

[编辑](javascript:;)[ 语音](javascript:;)

LIB文件中存放的是函数调用的信息，值得一提的是数据库有静态数据库（.lib文件）和动态数据库（.dll文件）。

### 静态编译

静态编译将导出声明和实现都放在lib中。编译后所有代码都嵌入到[宿主程序](https://baike.baidu.com/item/宿主程序)。

静态编译的优点是编写出来的程序不需要调用DLL和载入函数，直接可以当成程序的一部分来使用。

静态编译的缺点也是显而易见的，使用静态编译的程序体积会比动态编译大，原因是函数的实现被嵌入为程序代码的一部分。

### 动态编译

动态LIB文件相当于一个C语言中的h文件，是函数导出部分的声明，而不将实现过程嵌入到程序本身中，编译后只是将函数地址存在宿主程序中，运行到调用函数是调用DLL并载入函数来实现函数的具体操作。

## 详细说明

[编辑](javascript:;)[ 语音](javascript:;)

LIB文件是不对外公开的，除非有专门的LIB查看工具，否则不能查看LIB文件中对函数的具体实现过程

有几个选择：

1、如果你查看有同名的dll文件，可以通过vc自带的depends查看dll接口

2、通过msdn看你使用的该lib包含的函数名，来查找其对应的头文件，头文件里面有整个lib的函数声明（可能不全）

3、查看vc或者其他工具[安装目录](https://baike.baidu.com/item/安装目录)下的src目录，查看函数的[代码](https://baike.baidu.com/item/代码)

4、使用lib文件的方法：

1-在object/library modules使用全路径名；

2-把*.lib放在VC的Lib目录中

3-修改project setting的Link->Input中的Addtional library path，加入你的目录。

LIB文件是库文件（与DLL文件相类似），供其它程序调用的，直接打不开。

5、查看LIB和DLL文件都可以通过OLLYDBG中LOADDLL插件来反汇编查看各个函数的过程。

### 内容

一个lib文件是obj文件的集合。当然，其中还夹杂着其他一些[辅助信息](https://baike.baidu.com/item/辅助信息)，目的是为了让[编译器](https://baike.baidu.com/item/编译器)能够准确找到对应的obj文件。我们可以通过tlib.exe（在tc2.0下的根目录）来对lib文件进行操作，你可以把自己生成的obj文件通过tlib命令加入到一个lib文件中，也可以把lib文件内的obj文件进行删除操作，还可以把内部的obj文件给提取出来。明白了lib文件的大致结构以及对它的具体操作，在学习C语言的过程中，就会又多了一个切入点对C语言具体实现进行研究。

## 与dll区别

[编辑](javascript:;)[ 语音](javascript:;)

(1)lib是编译时需要的，dll是运行时需要的。

如果要完成[源代码](https://baike.baidu.com/item/源代码)的编译，有lib就够了。

如果要使动态连接的程序运行起来，有dll就够了。

在开发和调试阶段，当然最好都有。

(2)一般的动态库程序有lib文件和dll文件。lib文件是必须在编译期就连接到应用程序中的，而dll文件是运行期才会被调用的。如果有dll文件，那么对应的lib文件一般是一些索引信息，具体的实现在dll文件中。如果只有lib文件，那么这个lib文件是[静态编译](https://baike.baidu.com/item/静态编译)出来的，索引和实现都在其中。静态编译的lib文件有好处：给用户安装时就不需要再挂动态库了。但也有缺点，就是导致应用程序比较大，而且失去了动态库的灵活性，在[版本升级](https://baike.baidu.com/item/版本升级)时，同时要发布新的应用程序才行。

(3)在动态库的情况下，有两个文件，一个是引入库（.LIB）文件，一个是DLL文件，引入库文件包含被DLL导出的函数的名称和位置，DLL包含实际的函数和数据，应用程序使用LIB文件链接到所需要使用的DLL文件，库中的函数和数据并不复制到[可执行文件](https://baike.baidu.com/item/可执行文件)中，因此在应用程序的可执行文件中，存放的不是被调用的函数代码，而是DLL中所要调用的函数的[内存地址](https://baike.baidu.com/item/内存地址)，这样当一个或多个应用程序运行时再把程序代码和被调用的函数代码链接起来，从而节省了内存资源。从上面的说明可以看出，DLL文件必须随应用程序一起发行，否则应用程序将会产生错误。

## 加载方法

[编辑](javascript:;)[ 语音](javascript:;)

### 直接加入

在VC中打开File View一页，选中工程名，单击鼠标右键，然后选中"Add Files to Project"菜单，在弹出的文件对话框中选中要加入DLL的LIB文件即可。

### 设置

打开工程的 Project Settings菜单，选中Link，然后在Object/library modules下的文本框中输入DLL的LIB文件。

### 程序代码

加入[预编译](https://baike.baidu.com/item/预编译)指令#pragma comment (lib,"*.lib")，这种方法优点是可以利用条件预编译指令链接不同版本的LIB文件。因为，在Debug方式下，产生的LIB文件是Debug版本，如Regd.lib；在Release方式下，产生的LIB文件是[Release版本](https://baike.baidu.com/item/Release版本/6497294)，如Regr.lib。

当应用程序对DLL的LIB文件加载后，还需要把DLL对应的头文件（*.h）包含到其中，在这个头文件中给出了DLL中定义的函数原型，然后声明。

## 生成工具

[编辑](javascript:;)[ 语音](javascript:;)

操作系统：Win7。

开发软件：VS2010。

## 生成步骤

[编辑](javascript:;)[ 语音](javascript:;)

1. 建立win32控制台工程MyLib（或者win32项目中下的静态库），添加mySub.h文件以及mySub.cpp文件。
2. 编写mySub.h文件代码，#ifndef _MYSUB_H。
3. 编写mySub.cpp文件代码。
4. 由于在工程中，没有main()函数，所以编译可能会出错。这时，点击工程，并选择工程属性，出现下图，选择静态链接库即可。
5. 这时候再按快捷键 F7，build solution即可产生lib文件。在Debug中只生成.lib文件 [1] 。

## lib文件的使用

[编辑](javascript:;)[ 语音](javascript:;)

1. 新建一个.cpp文件myLibTest.cpp（用于测试）。
2. 点击工程，并选择工程属性，将附加库目录新增包含刚才生成.lib的目录。
3. 将工程项目属性中的配置类型改回至原来默认的应用程序（.exe），并执行myLibTest.cpp。
