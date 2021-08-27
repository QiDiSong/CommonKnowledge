# 一. 简介

## 1.1 C++两种库文件

1. lib包含了函数所在的dll文件和文件中函数位置的信息（入口），代码由运行时加载在进程空间中的dll提供，称为动态链接库dynamic link library。**（这种方式更灵活，写的程序体积小，但是需要.exe和dll同时发布）**
2. lib包含函数代码本身，在编译时直接将代码加入程序当中，称为静态链接库static link library。**（这种方式不是很灵活，因为lib被编译到.exe中，写出的程序体积大，但是只需要发布exe即可，不需要dll文件）**

## 1.2 C++两种链接方式

1. 动态链接使用动态链接库，允许可执行模块（.dll文件或.exe文件）仅包含在运行时定位 dll 函数的可执行代码所需的信息。
2. 静态链接使用静态链接库，链接器从静态链接库 lib 获取所有被引用函数，并将库同代码一起放到可执行文件中。

## 1.3 lib与dll的区别

### 1. 功能区别

- lib是编译时用到的，dll是运行时用到的。如果要完成源代码的编译，只需要lib；如果要使动态链接的程序运行起来，只需要dll。
- 如果有dll文件，那么lib一般是一些索引信息，记录了dll中函数的入口和位置，dll中是函数的具体内容；如果只有lib文件，那么这个lib文件是静态编译出来的，索引和实现都在其中。使用静态编译的lib文件，在运行程序时不需要再挂动态库，缺点是导致应用程序比较大，而且失去了动态库的灵活性，发布新版本时要发布新的应用程序才行。
- 动态链接的情况下，有两个文件：一个是LIB文件，一个是DLL文件。LIB包含被DLL导出的函数名称和位置，DLL包含实际的函数和数据，应用程序使用LIB文件链接到DLL文件。**在应用程序的可执行文件中，存放的不是被调用的函数代码，而是DLL中相应函数代码的地址**，从而节省了内存资源。DLL和LIB文件必须随应用程序一起发行，否则应用程序会产生错误。如果不想用lib文件或者没有lib文件，可以用WIN32 API函数LoadLibrary、GetProcAddress装载。

### 2. 文件数量的区别

1. **（静态连接）**使用lib需注意两个文件:

- .h头文件，包含lib中说明输出的类或符号原型或数据结构。应用程序调用lib时，需要将该文件包含入应用程序的源文件中。
- .LIB文件，略。

1. **（动态连接）**使用dll需注意三个文件：

- .h头文件，包含dll中说明输出的类或符号原型或数据结构的.h文件。应用程序调用dll时，需要将该文件包含入应用程序的源文件中。
- .LIB文件，是dll在编译、链接成功之后生成的文件，作用是当其他应用程序调用dll时，需要将该文件引入应用程序，否则产生错误。如果不想用lib文件或者没有lib文件，可以用WIN32API函数LoadLibrary、GetProcAddress装载。
- .dll文件，真正的可执行文件，开发成功后的应用程序在发布时，只需要有.exe文件和.dll文件，并不需要.lib文件和.h头文件。

# 二. lib文件

## 2.1 生成工具

操作系统： Win7

开发软件： VS2010

## 2.2 生成步骤

1. 建立win32控制台工程MyLib（或者win32项目中下的静态库）, 添加mySub.h文件以及mySub.cpp文件。

2. 编写mySub.h文件代码

   

   ```c
   #ifndef _MYSUB_H               // 这里的#ifndef可以避免头文件重复包含
   #define _MYSUB_H  
   void mySub(int a,int b);       // 这一行代码不能够写在上一行，只能另起一行写
   #endif
   ```

3. 编写mySub.cpp文件代码

   

   ```c
     #include "mySub.h"                   //包含头文件
     #include <iostream>                  
                                      
     void mySub(int a,int b)              //自定义的函数 
     {
        std::cout<<(a-b)<<std::endl;
     }
   ```

4. 由于在工程中，没有main()函数，所以编译可能会出错。这时，点击工程，并选择工程属性，出现下图，选择静态链接库即可。

   ![img](https://upload-images.jianshu.io/upload_images/2909277-defa63e77cdc30a4.png?imageMogr2/auto-orient/strip|imageView2/2/w/919/format/webp)

   012302.png

1. 这时候再按快捷键 F7，build solution即可产生lib文件。在Debug中只生成.lib文件。

## 2.3 lib文件的使用

1. 新建一个.cpp文件myLibTest.cpp(用于测试)

   

   ```c
   #include <iostream>
   #include "mySub.h"                       // 引用头文件
   using namespace std;
   
   #pragma comment(lib,"MyLib.lib")         // 导入上一步生成的lib文件
   
   int main()
   {
     mySub(5,4);                            // 调用lib中的自定义函数mySub()
   
     return 0;
   }
   ```

2. 点击工程，并选择工程属性，出现下图，将附加库目录新增包含刚才生成.lib的目录。

   ![img](https://upload-images.jianshu.io/upload_images/2909277-30e2e9d8c74374fd.png?imageMogr2/auto-orient/strip|imageView2/2/w/917/format/webp)

   012303.png

1. 将工程项目属性中的**配置类型**改回至原来默认的**应用程序（.exe）**,并执行myLibTest.cpp。

# 三. dll文件

## 3.1 生成.dll文件

1. 新建win32项目，项目名称为SubDLL，解决方案名称为DLLTest，下一步。

2. 选择应用程序类型为DLL，将附加选项的“导出符号”勾选上，完成。

3. 修改SubDLL.h中的内容（将原来代码中，除预处理部分的代码外全部删除），并在后面新增你要实现的函数声明（见代码第21行）。注意：项目名为SubDLL，但此时生成的名字为 SUBDLL。

   

   ```c
   #ifdef SUBDLL_EXPORTS
   #define SUBDLL_API __declspec(dllexport)
   #else
   #define SUBDLL_API __declspec(dllimport)
   #endif
   
   /*
   // 此类是从 SubDLL.dll 导出的
   class SUBDLL_API CSubDLL {
   public:
    CSubDLL(void);
    // TODO: 在此添加您的方法。
   };
   
   extern SUBDLL_API int nSubDLL;
   
   SUBDLL_API int fnSubDLL(void);
   */
   
   //这边是新增的内容
   SUBDLL_API void mySub(); 
   ```

4. 修改SubDLL.cpp中的内容（将原来代码中，除头文件引入部分的代码外全部删除），并在后面新增你要实现的函数声明（见代码第26行）。

   

   ```c
   // SubDLL.cpp : 定义 DLL 应用程序的导出函数。
   //
   
   #include "stdafx.h"
   #include "SubDLL.h"
   
   #include<stdio.h>
   /*
   // 这是导出变量的一个示例
   SUBDLL_API int nSubDLL=0;
   
   // 这是导出函数的一个示例。
   SUBDLL_API int fnSubDLL(void)
   {
    return 42;
   }
   
   // 这是已导出类的构造函数。
   // 有关类定义的信息，请参阅 SubDLL.h
   CSubDLL::CSubDLL()
   {
    return;
   }
   */
   //这边为SUM（）的内容，很简易
   SUBDLL_API void mySub(int a,int b)
   {
    printf("the result is %d",a-b);
   }
   ```

5. 点击“项目”，选择“属性”，进行如下图的配置（粗体字显示部分）。

   ![img](https://upload-images.jianshu.io/upload_images/2909277-f9dd1a8a96108bfe.png?imageMogr2/auto-orient/strip|imageView2/2/w/923/format/webp)

   012306.png

1. 构建项目（build）/生成解决方案，在项目的debug目录下面会生成很多的文件，其中包括有.dll和.lib。

## 3.2 dll文件的使用

### 3.2.1 显示调用方式

1. 在之前“解决方案”中新建项目（选中解决方案 -> 增加 -> 新建项目），这次选择“win32控制台应用程序”，生成向导中选择“空项目”即可。取名为MyTest。

2. 在新建项目的源文件下新建一个UseDLL.cpp文件，下面是其中的代码。

   

   ```c
   #include <iostream>
   #include <Windows.h>          //使用函数和某些特殊变量
   
   using namespace std;
   typedef void (*FUN)(int,int); //定义一个函数指针，确定调用函数的形参
   
   int main()
   {
    const char* dllname = "SUBDLL.dll"; // 加载.dll
    const char* funname = "mySub";      //SUMDLL.cpp中函数名称
   
    HMODULE hDLL = LoadLibrary(dllname); //不要问，跟着做
   
    if (hDLL != NULL)
    {
        FUN fp = FUN(GetProcAddress(hDLL,funname)); //继续做，不要问
        if(fp != NULL)
           {
             fp(5,4);
           }
        else 
           {
             cout << "Can not Find: " << funname << endl;
           }    
        FreeLibrary(hDLL);
    }
    else 
        cout << "Can not find: " << dllname;
     
    return 0;
   }
   ```

3. 点击**解决方案名**，选择**设置启动项目 -> 通用属性 -> 启动项目 -> 单启动项目**（选中UseDLL）。

4. 运行项目，出现了错误：`Can not find:mySub`。造成这种错误的原因正是**导出函数的修饰名称**。在dll二进制文件中，经过编译器的“加工”，实际上有了不同的名称。这也是函数重载机制得以实现的一个技术支持。怎么办呢？我们可以通过vs2010附带工具dumpbin，找到加工以后的名称。详见[dumpbin工具的使用](https://link.jianshu.com/?t=http%3A%2F%2Fblog.csdn.net%2Ffengbingchun%2Farticle%2Fdetails%2F43956673)

   - 在C:\Program Files(x86)\Microsoft Visual Studio 10.0\VC\bin目录下，按住shift键，鼠标右键在空白处单击，选择**在此处打开命令窗口**
   - 输入命令: dumpbin /export 文件全名
   - 将“加工”后的真是函数名复制后，粘贴。赋值给UseDLL.cpp文件中的变量funname。
   - 经过上一步后，重新执行UseDLL.cpp，成功运行。详见[VS2010 C++ 调用 DLL （C++编写）](https://link.jianshu.com/?t=http%3A%2F%2Fwww.cnblogs.com%2Fshenchao%2Fp%2F3201249.html)

5. 为了能够使原来的UseDLL.cpp（上面第2步所示代码）成功运行，可以进行下列操作：

   - 在**生成DLL文件的SubDLL项目的源文件中新建模块定义文件createDLL.def**，其中的代码如下：

     

     ```c
     LIBRARY createDLL  
     EXPORTS  
     mySub = ?mySub@@YAXHH@Z          //?mySub@@YAXHH@Z 即为dumpbin工具找到的真实名。
     ```

   - 修改SubDLL.h中的代码（去掉这些不太规范的修饰名称），修改之后重新编译生成CreateDLL.dll。

     

     ```c
     #ifdef SUBDLL_EXPORTS
     #define SUBDLL_API        //去掉了原来的 __declspec(dllexport) 
     #else              //或改为 #define SUBDLL_API  extern "C" __declspec(dllexport)
     #define  SUBDLL_API           //同上  
     #endif
     ```

6. 重新运行UseDLL.cpp程序，成功执行。

### 3.2.2 隐式调用方式

1. 在之前“解决方案”中新建项目（选中解决方案 -> 增加 -> 新建项目），这次选择“win32控制台应用程序”，生成向导中选择“空项目”即可。取名为MyTest。

2. 在新建项目的源文件下新建一个UseDLL.cpp文件，下面是其中的代码。

   

   ```c
   #include <iostream>
   
   extern void mySub(int,int);
   
   int main()
   {
    mySub(5,4);
    return 0;
   }
   ```

3. **右键工程–>Linker–>General–>Additional Library Directories（附加库目录） –>找到那个SubDLL.lib所在的目录**

4. 右键UseDLL工程–>Linker->input写下lib的名称。如SubDLL.lib和你DEBUG文件下的对应（这步没有也可以，因为会在上一步的路径下寻找）。

5. 点击**解决方案名**，选择**设置启动项目 -> 通用属性 -> 启动项目 -> 单启动项目**（选中UseDLL）

6. 运行UseDLL.cpp程序，成功执行。

[参考资料](https://link.jianshu.com/?t=http%3A%2F%2Fblog.csdn.net%2Faidem_brown%2Farticle%2Fdetails%2F38712705)

# 四. 小结

## 4.1 程序中的问题

1. error C2664: “LoadLibraryW”: 不能将参数 1 从“const char [10]”转换为“LPCWSTR”与指向的类型无关；转换要求 reinterpret_cast、C 样式转换或函数样式转换
   解决方法：

   选中项目，然后点击属性——>配置属性——>常规——>项目默认值——>字符集，选为“使用多字节字符集"

   ![img](https://upload-images.jianshu.io/upload_images/2909277-7361f5796e2db5a3.png?imageMogr2/auto-orient/strip|imageView2/2/w/920/format/webp)

   012304.png

1. fatal error LNK1104: 无法打开文件：×××.lib的解决办法
   一般情况是因为没有导入相应的.lib文件，或者是导入的路径有误。给项目添加库文件路径。

   在VS中右击项目点属性：

   配置属性-->链接器-->常规-->附加目录 。在里面填上库文件所在的路径即可。

2. fatal error LNK1104: 无法打开文件“x x x.def”
   如果不想使用xxx.def文件，可以在**项目-属性-配置属性-链接器-输入** 选项中，将右侧的模块定义文件删掉，这样就不会提示了。

## 4.2 vs的常用操作

1. 添加头文件：

   配置属性-->C/C++-->常规-->附加包含目录 加上头文件存放的目录。

2. 添加lib文件：

   - 配置属性-->链接器-->输入-->附加依赖项加入库名（×××.lib）；或者是在cpp源文件中用#pragma comment(lib,"×××.lib")来代替。
   - 将xxx.lib拷入工程所在目录，或者执行文件生成的目录，或者系统Lib目录中（如果lib文件是自己生成的，可以跳过这一步）。
   - 给项目添加库文件路径：
     在VS中右击项目点属性。配置属性-->链接器-->常规-->附加目录 。在里面填上库文件所在的路径即可。

## 4.3 windows小常识

1. 在当前目录下运行命令：shift键 + 鼠标右键
2. 首先将命令窗体属性中的**快速编辑模式**选中打勾，这样就可以一复制粘贴了。复制dos窗体中的内容：右键->标记->选择复制内容->回车键或者鼠标右击，粘贴的时候：鼠标右键粘贴。
   dos中不能使用快捷键。
