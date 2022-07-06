## 杂知识

### struct和typedef struct

首先：**//注意在C和C++里不同**
　　　　在C中定义一个结构体类型要用typedef:
　　　　**typedef struct Student**
　　　　**{**
　　　　**int a;**
　　　　**}Stu;**
　　　　于是在声明变量的时候就可：Stu stu1;(如果没有typedef就必须用struct Student stu1;来声明)
　　　　这里的Stu实际上就是struct Student的别名。**Stu==struct Student**
　　　　另外这里也可以不写Student（于是也不能struct Student stu1;了，必须是Stu stu1;）
　　　　**typedef struct**
　　　　**{**
　　　　**int a;**
　　　　**}Stu;**
　　　　但在c++里很简单，直接
　　　　**struct Student**
　　　　**{**
　　　　**int a;**
　　　　**};**　　　　

　　　　于是就定义了结构体类型Student，声明变量时直接Student stu2；

　　2.其次：
　　　　在c++中如果用typedef的话，又会造成区别：
　　　　**struct  Student** 
　　　　**{** 
　　　　**int  a;** 
　　　　**}stu1;//**stu1是一个变量 

　　　　**typedef  struct  Student2** 
　　　　**{** 
　　　　**int  a;** 
　　　　**}stu2;**//stu2是一个结构体类型=struct Student 

　　　　使用时可以直接访问stu1.a
　　　　但是stu2则必须先  stu2 s2;

　　　　然后        s2.a=10;

### molloc

​    1.关于void *：

​     void * p1;

​     int *p2;

​     p1 = p2;         

就是说其他任意类型都可以直接赋值给它，无需进行强转，但是反过来不可以。

2.malloc和new

   new返回指定类型的指针，并且可以自动计算所需要的大小。

   int *p;

   p = new int;  //返回类型为int *类型，分配的大小为sizeof(int)

   p = new int[100];  //返回类型为int *类型，分配的大小为sizeof(int) * 100

   而malloc则必须由我们计算字节数，并且在返回的时候强转成实际指定类型的指针。

   int *p;

   p = (int *)malloc(sizeof(int));

​     1,malloc的返回是void *,如果我们写成了: p = malloc(sizeof(int));间接的说明了（将void *转化给了int *,这不合理）

   2，malloc的实参是sizeof(int),用于指明一个整形数据需要的大小，如果我们写成：

​      p = （int *）malloc(1),     那么可以看出：只是申请了一个字节的空间，如果向里面存放了一个整数的话，

​      将会占用额外的3个字节，可能会改变原有内存空间中的数据

   3，malloc只管分配内存，并不能对其进行初始化，所以得到的一片新内存中，其值将是随机的。一般意义上：我

​      们习惯性的将其初始化为NULL。      当然,也可以用memset函数的。

简单的说：

malloc 函数其实就是在内存中：找一片指定大小的空间，然后将这个空间的首地址给一个指针变量，这里的指针变量可以是一个单独的指针，也可以是一个数组的首地址， 这要看malloc函数中参数size的具体内容。我们这里malloc分配的内存空间在逻辑上是连续的，而在物理上可以不连续。我们作为程序员，关注的 是逻辑上的连续，其它的，操作系统会帮着我们处理的。

### 未赋值的变量的值

int a；

a的值直接输出，可能是随机数，也可能是固定的数

### gcc C语言编译

       （1）.预处理，生成预编译文件（.文件）：

        Gcc –E hello.c –o hello.i  
       （2）.编译，生成汇编代码（.s文件）：

        Gcc –S hello.i –o hello.s  
       （3）.汇编，生成目标文件（.o文件）：  
        Gcc –c hello.s –o hello.o  
       （4）.链接，生成可执行文件：  
        Gcc hello.o –o hello

10 目标文件反汇编objdump -S obj

## 从c到c++

### gcc和g++的区别

gcc和g++

g++对文件都处理成c++

gcc对.c文件处理成c，.cpp处理成c++

### 传参数的实质

```c
void swap(int a,int b){
int s=a;
a=b;
b=s;
}

int main(){
int x,y;
swap(x,y);     
}
```

不能实现函数，传参相当于 int a=x,int b=y.

所以相当于给局部变量a和b赋值了，交换了，但对x,y没有影响

而&和*可以的原因是

int &a=x,int &b=y;是别名

int *a=x,int *b=y;是指针

### c和c++

#### c++的const

const 用来定义变量，一旦定义不能再改变

int * const 定义常指针，只能指向一个变量

const float a=4.5，与c的define不同，define 预处理，不占内存，而const是实际的变量

#### c++变量检查能力加强

int a;

int a=1;   在c中可以，c++不能重复定义

#### c++增强struct，可以省略struct来实例化

#### c++所用的变量和函数都必须有类型

eg：f（）{

}在c中可以，c++不行

#### c++增强三目运算符

（a>b?a:b）=50；可以当左值

#### c++输出输入

输出：cout<<""<<endl;

输入：cin>>a>>b；

#### c++定义函数声明时必须和定义相同

#### c++增加引用变量

int &b=a；b是a的别名

不能引用数组

### c++函数重载

eg：

```c++
template<typename T>
T min(T a, Tb){
}
实现重载
int x=min();

float y=min();
```

### *和&

*前有类型时为定义指针

&前有类型时为引用变量

*p取内容

&p取地址

![](c++/pics/2022-07-06-11-28-20-image.png)

### c++内联函数

```c
#include <stdio.h>  

inline int prin(){
return "hhh";
}

int main(){
for(int i=0;i<100;i++){
prin();
}
}
```

### c语言静态变量

有static修饰，生命周期为整个程序，存在静态存储区，不能被外部文件访问和调用，即使用extern也不行，只能初始化一次，没有赋值自动赋值0或者null

不用内联的话，每次循环都会开辟空间运行prin()函数，而内联之后，相当于把return "hhh";临时复制在for循环中，每次循环不用开辟新空间，只需要运行return "hhh"

## c/c++连接库文件

库的分类：静态库和动态库

连接：静态连接和动态连接

linux：

​    静态库：libXXX.a

​    动态库：libXXX.so

window：

​    静态库：XXX.lib

​    动态库：XXX.dll

使用：

​    gcc     xx.c    -l库名     ；库路径放在环境变量

​    gcc     xx.c     -L静态库路径    -l库名    ；库路径

​    

动态库和静态库的特点
静态库的特点：
1、使用静态库的时候，会将静态库的信息直接编译到可执行文件中
2、优点:当静态库被删除，对可执行文件没有影响
3、缺点:浪费内存空间。如果静态库被修改，可执行程序要重新编译

动态库的特点：
加载器在加载动态库时，操作系统会先检查动态库是否因为其它程序已经将这个动态库信息加载到了内存中。如果没有加载到内存中，操作系统会将动态库载入内存，并将它的引用计数设置为1;如果已经加载到内存，仅将动态库的引用计数加

## c++

### 枚举类型

```cpp
enum color{red,yellow,blue}
color c;
enum:定义枚举关键字
color枚举类型名
red，blue枚举常量/元素
c：枚举变量
或者：ennum color {red,red ,blue},c,b;
```

注意：

1. 枚举元素都是常量，不是变量，不能为枚举元素赋值
2. 每个枚举元素都有一个确定的整数值，可以在枚举类型定义的时候显式地给出枚举元素的值，若缺省则默认0，1，2，...
3. 可以将一个整数强制转换类型后赋给枚举变量
4. 枚举常量可以直接赋给整型变量

### 运算

如果某个算术运算符的两个运算对象都是整数，那么，运算将按照整型数的运算规则来运算

只要其中有一个是浮点型数，则按照浮点数运算规则来进行

### 强制类型转换

c：(类型名)表达式

c++:类型名(表达式)

### goto

```c++
#include"iostream.h"
void main(){
    int i;
    float sum;
    sum=1;
    i=2;
  L1:sum+=1/(float)i;
    i+=2;
    goto L1;
    cout<<sum;
}
```

### 输入输出

cin：标准输入流

cout：标准输出流

cerr：非缓冲型的标准出错流

clog：缓冲型的标准出错流

#### 十六进制，八进制

默认：十进制

hex：十六进制

oct：八进制

dec:十进制

eg：

cin>>hex>>j;指定输入为十六进制

#### 占位

1. setw()
   
   需要头文件iomanip.h
   
   ```c++
   #include<iomanip>
   cout<<setw(6)<<i<<setw(10) //左右空格6和10位
   ```

2. width（）
   
   位于iostream
   
   ```c++
   #include"iostream"
   cout.width(10);
   ```

3. cout.fill()

填充自定义字符,配合width使用

```c++
#include"iostream"
cout.width(10);
cout.fill('#');
```

#### 精度控制

cout.pricision();

```c++
cout.precision(7);
cout<<1234.4558<<endl;
```

输出：1234.456

从左开始精确n位，第n位四舍五入

#### 刷新

cout.flush()

刷新

或者cin.tie(&cout)

#### 科学计数法

   cout.setf(ios::scientific,ios::floatfield);

#### get(),put()

cin只能输入字符，不能输入空格，回车等

cin.get()可以获取所有字符

cout.put()

#### getline()

cin.getline()

定义形式:istream&get/getline(char *ss,int count,char delim='\n')

ss:缓冲区指针，count最多向ss存入的字符数，delim：如果遇到此字符，输入结束

get( )和getline( )函数的功能基本相同，getline( )函数读入由delim标识的区分字符

### 文件

头文件：include<fstream>

ifstream：文件输入用流类

ofstream：输出

fstream：输入输出

#### 文件的打开和关闭

```cpp
//文件的输入输出
#include <iostream>
#include <fstream>
using namespace std; //ifstream,ofstream都是std中的
int main()
{
    char c;
    ifstream fin;  //获取打开的文件的内容，待写入变量，只能和>>匹配
    ofstream fout; //打开一个文件，将内容写入这个文件,只能和<<匹配
    fstream file;  //打开一个文件，用>>是读文件内容，用<<是写文件内容

    char aa[100], bb[100] = "HHALL", cc[100];

    fin.open("aa.txt");
    fout.open("bb.txt");
    file.open("cc.txt");

    fin >> aa;  //将aa.txt的内容写到aa   相当与aa.txt>>fin>>aa    从文件读
    fout << bb; //相当于bb.txt<<fout<<bb,将bb的内容写到bb.txt,也可以是直接的字符串      向文件写
    file >> cc;
    file << bb;
    //fout <<"Hello,world"<<endl;//将"Hello,world"写入bb.text
    fin.close();
    fout.close();
    cout << aa[1] << endl;
   cout << cc[0] << endl;
}
```

### 期末

全局变量，全局静态变量，局部变量，局部静态变量

: 有static的是静态变量，没有的不是

定义在main()外面的是全局变量，main和其他函数地位相同，里面的变量都是局部变量

在函数中可以直接调用全局变量，如果函数中定义了同名的变量，再调用全局变量就要用：：

Virtual继承和不继承：

用virtual修饰的虚函数，用来继承重写，没有virtual修饰的，取决于父类

定义 父类  *x=new 子类

首先父类不能调用子类的函数，自能调用本身的函数，所以，只有两种情况，1.无virtual修饰，调用本身函数。2.有virtual修饰，调用子类重写的函数

定义 子类  *y=new 子类

子类对父类的函数，如果没有同型函数，直接继承父类的函数，如果型名，有virtual修饰，则重写，无virtual修饰，则调用子类的。

特别的：如果子类和父类有同名但不同型，则不能调用父类的同名函数，不能继承或重写的同时还重载

总结：

 对于父类函数（virtual、非virtual），如果子类没有同名函数，则正常继承

对于父类函数（virtual、非virtual），如果子类有同名函数，无同型（形参不同）函数，则不能调用父类函数
  对于父类函数（virtual、非virtual），如果有同型函数：
 ----非virtual函数由指针类型决定调用哪个，既和父类一致，编译时确定
 ----virtual函数由指针指向的对象决定调用哪个（运行时决定）和子类一致，运行时确定

C++new和delete

New用来开辟新的地址空间，返回一个地址，需要用delete释放空间

用new创建的对象，delete后才能调用析构函数

New可以开启所有类型空间，返回地址，形式：类型  *指针名=new 类型；

对于对象指针：eg: class *p;

如果这样，p只有类型，没有指向，delete时，也能调用类class的析构函数，但是只能释放一次，如果时class *p=new class（）；那么，可以多次delete，多次析构

Const

const int *p: 定义指针，指向的变量的值不能修改(指向整型常量或普通整型，但值不能通过指针修改)

int const *p: 同上

int * const p=&a: 一直指向a，不能改变方向

const int * const p:一直指向不能修改的整型常量

int const * const p:同上

两个不常用的

int (* p )[3];指向数组的指针

int （*p） (形参 ):指向函数返回值为整型的函数指针

三种继承

​    继承优先级:private>protect>public

​       变量或函数函数本身的类型和继承方式，比较，取小的就是继承的访问性

​           eg: protected x,通过private继承，继承后就是private的

​    可见性

​       继承后为public和protected的可以被派生类访问，private不能

​       继承后为public的可以被对象访问，protected和private不能

类外指向类成员和成员函数的指针

​    指向类成员

​       eg：class base{ x; }

​           int base::*p=&base::x;

​           调用：base b;

​               b.*p≌b.x

​    指向成员函数

​       eg：class base{ int fun(int x); }

​           int (base::*p)(int x)=&base::fun;

​           调用：base b;

​               (b.*p)(6);

虚函数：

​    只能是：非静态成员函数

​           析构函数

​           成员运算符重载函数
