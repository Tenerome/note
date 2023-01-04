### 关键字

| <mark>asm</mark>          | else                  | new                           | this                  |
| ------------------------- | --------------------- | ----------------------------- | --------------------- |
| auto                      | enum                  | <mark>operator</mark>         | throw                 |
| bool                      | <mark>explicit</mark> | private                       | true                  |
| break                     | <mark>export</mark>   | protected                     | try                   |
| case                      | extern                | public                        | typedef               |
| catch                     | false                 | register                      | <mark>typeid</mark>   |
| char                      | float                 | <mark>reinterpret_cast</mark> | <mark>typename</mark> |
| class                     | for                   | return                        | union                 |
| const                     | <mark>friend</mark>   | short                         | unsigned              |
| <mark>const_cast</mark>   | goto                  | signed                        | using                 |
| continue                  | if                    | sizeof                        | <mark>virtual</mark>  |
| default                   | <mark>inline</mark>   | static                        | void                  |
| delete                    | int                   | <mark>static_cast</mark>      | volatile              |
| do                        | long                  | struct                        | <mark>wchar</mark>_t  |
| double                    | <mark>mutable</mark>  | switch                        | while                 |
| <mark>dynamic_cast</mark> | namespace             | <mark>template</mark>         |                       |

### 新增类型:布尔型和宽字符型

#### 布尔型

c语言中表示布尔型一般用0/1,或者flag,c++把布尔型内置了,布尔型的变量只有true和false 两个值

**和0/1的关系**:

true和false不是0/1,c++编译器会把非0处理成true,把0处理成false

#### 宽字符型

char型只有一个字节的长度,如果要在c中表示汉字,则需要使用字符串数组

c++添加的宽字符型就是专门用来存储汉字,日文,韩文等占两个字节字符的.

wchar_t的本质:

```c
typedef short int wchar_t;
```

是的,它和short int有相同的2个字节空间.

使用前需要导入头文件\<locale\>,并需要用`setlocale(LC_ALL,"chs");`指定中文

如:

```c
wchar_t c[]=L"你好";
wcout<<c;
```

L:是常量的前缀,L表示宽字符

wcout也是针对wchar_t的输出

### 常量的前缀和后缀

常量的前缀像上面说的L,用来表示宽字符,这是字符型的常量,除此之外,还有:

整型前缀:0x表示十六进制

                0表示八进制

整型后缀:U表示无符号数

                L表示长整数(long)

### restrict

restrict关键字,规定被其修饰的指针所指的对象不能被其他指针引用

在C++中用`__restrict来修饰指针`

```c
int a;
int* __restrict p=&a;
```

这样,变量a就只能被指针p所指,不能被其他指针指

作用:有些时候可以优化性能,见[知乎](https://zhuanlan.zhihu.com/p/349726808)

### 存储类

和C相同都有auto,extern,static,register存储类,并新增mutable和thread_local(C++11)

**auto**:C语言中auto用来声明函数内的变量,C++98标准中和C相同.C++11后,auto用来定义自动推导的类型,且必须在定义时赋初值.

```c
int a=1;
float b=1.2;
auto c=a;
auto c=b;
```

编译器会根据给赋初值的类型推导auto变量的类型,常用于lambda表达式,这样lambda的返回类型就可以省略

**mutable**用于类中,用mutable修饰的成员变量可以被const函数修改

**thread_local**:

thread_local说明符声明的变量仅可以在创建其的线程上访问.变量在创建线程时创建,在销毁线程时销毁.

与其他几个存储类不同的是,thread_local只能用于修饰变量,不能修饰函数

### 杂项运算符

| 运算符               | 描述                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------------- |
| sizeof            | [sizeof 运算符](https://www.runoob.com/cplusplus/cpp-sizeof-operator.html)返回变量的大小。例如，sizeof(a) 将返回 4，其中 a 是整数。   |
| Condition ? X : Y | [条件运算符](https://www.runoob.com/cplusplus/cpp-conditional-operator.html)。如果 Condition 为真 ? 则值为 X : 否则值为 Y。     |
| ,                 | [逗号运算符](https://www.runoob.com/cplusplus/cpp-comma-operator.html)会顺序执行一系列运算。整个逗号表达式的值是以逗号分隔的列表中的最后一个表达式的值。    |
| .（点）和 ->（箭头）      | [成员运算符](https://www.runoob.com/cplusplus/cpp-member-operators.html)用于引用类、结构和共用体的成员。                           |
| Cast              | [强制转换运算符](https://www.runoob.com/cplusplus/cpp-casting-operators.html)把一种数据类型转换为另一种数据类型。例如，int(2.2000) 将返回 2。 |
| &                 | [指针运算符 &](https://www.runoob.com/cplusplus/cpp-pointer-operators.html) 返回变量的地址。例如 &a; 将给出变量的实际地址。             |
| *                 | [指针运算符 *](https://www.runoob.com/cplusplus/cpp-pointer-operators.html) 指向一个变量。例如，*var; 将指向变量 var。             |

其中,逗号运算符例子:

```c
#include<iostream>
using namespace std;
int main(){
    int a=0;
    int j;
    j=(a++,a-99,a+2);
    cout<<j;
}
```

逗号运算符必须在括号中,它的意义是先从左到右运算,最后把最右边的值返回

这个例子输出:3

先运算a++ =>a=0,然后运算a-99,a-99并不会对a做影响,所以无效,最后返回a+2,也就是3

最终a的值为1,j的值为3

### 引用类型

c++增加引用类型的概念,定义方法`int &b=a;`表示引用类型,引用类型相当于变量的别名,地位和被引用的变量相同,`int &b=a;`,执行后,变量a和b有相同的值和地址,相当于一个地址的内容有两个标签

必须在定义时用,如果在定义后,`int b;&b=a`就不是引用了,而是取地址

类似于指针的定义和取内容,`int *p;`定义指针,`*p`取指针p的内容

### 缺省的参数

在定义函数时可以在形参中为其赋值,表示这个参数可缺省

```c
void f(int x,int y=1){
    cout<<x+y;
}
int main(){
    f(3);
}
```

缺省的参数必须放在其他的参数后面

### Lambda函数

参考:[CSDN](https://blog.csdn.net/qq_37085158/article/details/124626913)

C++11开始,提供了对匿名函数的支持,成为Lambda函数(表达式)

通常,lambda函数用于封装传递给算法或异步方法的几行代码,对应不需要复用,且短小的函数,使用lambda函数可以增加代码的可读性

格式:

`auto function=[capture list](parameters) mutable throw()->return-type {statement}`

一般用一个auto变量来接收,然后通过这个变量名function(paramenters)调用,也可以直接附上参数,不需要auto变量名

`[capture list](paramenters) mutable throw()->return-type {statement}(real paramenters) `

例如:

```cpp
auto function=[a,&b](int x) mutable ->int {return a+b+x;};
int m=function(20);
//another
int m=[a,&b](int x) mutable ->int {return a+b+x;}(20);
```

- 捕获列表:在C++规范中也称Lambda导入器,`[]`就是lambda引出符,编译器根据该引出符判断接下来的代码是否lambda函数,捕捉列表能捕捉上下文中的变量,供Lambda函数使用,也就相当于在函数中调用函数外的变量.
- 参数列表:和普通函数的参数列表一致,如果不需要传递参数,则可以连同`()`一同省略
- 可变规格:`mutable`修饰符,默认情况下**lambda函数总是一个const函数**,mutable可以取消其常量性,如果使用了mutable,则参数列表不可省略
- 异常说明:用来抛出异常
- 返回类型:声明函数的返回类型,如果不需要返回值,则可以连同符号`->`一起省略,在返回类型明确的情况下,也可以省略该部分,让编译器对返回类型进行推到
  - 如`int a; return a+2;`编译器就能自动推导返回值类型为int
- lambda函数体:和普通函数别无二致,除了传入的参数,还可以使用捕获的变量

#### 捕获列表

捕获列表就是lambda以值传递或引用传递的方式调用上下文的变量

- []表示不捕获任何变量

```c
auto function=[]{std::cout<<"Hello";};
function();
```

这是一个简单的lambda例子,它的功能是输出"hello"

- [var]表示**值传递**的方式捕获变量var

```cpp
int num=100;
auto function=[num]{std::cout<<num;};
function();
```

捕获就是在lambda表达式内部调用外面的变量,值传递相当于普通函数的值传递形式

- [=]表示值传递方式捕获父作用域的所有变量,包括this

```cpp
int a=100;
float b=1.2;
auto function=[]{cout<<a<<endl<<b;};
function();
```

- [&var]表示**引用传递**捕捉变量var

```cpp
int a=100;
auto function=[]{a++;cout<<a;};
function();
```

也就是能在lambda表达式中改变变量的值

- [&]表示引用传递捕捉父作用域的所有变量

```cpp
int a=100;
float b=1.2;
auto fnction=[]{a++;
                b+=2.3;
                cout<<a<<endl<<b;};
function();
```

- [this]表示值传递方式捕捉当前的this指针

```cpp
#include<iostream>
using namespace std;

class test{
    public:
        void sayHello(){
            cout<<"hello"<<endl;
        }
        void lambda(){
            auto function=[this]{this->sayHello();};
            function();
        }
};
int main(){
    test t1;
    t1.lambda();
}
```

- [=,&]拷贝和引用混合
  
  - \[=,&a,&b\]:以值传递的方式捕捉其他所有变量,以引用方式捕捉a,b
  
  - \[&,a,this\]:以值传递捕捉a和this,其他用引用方式

- 捕捉列表不允许变量重复传递,如
  
  - \[=,a\]:已经捕捉了所有变量,重复捕捉a,会报错
  
  - \[&,&this\]:也是会报错

#### 参数列表

格式和使用都和普通函数无二致

```cpp
auto function=[](int x,int y){return x+y};
int a=function(100,200);
```

#### 可变规格mutable

通过值传递方式捕获的变量在lambda中默认是const类型,只能输出,不能改变,使用mutable可以使其可变,但是只能在lambda中短暂使用,并不能影响到父作用域的变量

```cpp
int a=1;
auto function=[a]() mutable {a++;};
function();
```

这时参数列表`()`不能省略,可以使空的参数列表,但`()`不能省

#### lambda的优缺点

**优点:**

- 可以直接在需要调用函数的位置定义短小精简的函数,不需要预先定义好函数

- 可以使代码结构更紧凑,因为调用的函数的定义就在旁边,不用向前后向后找,可读性更好

**缺点:**

- 增加了阅读代码的难度

- 无法复用

#### 工作原理

编译器会把一个Lambda表达式生成一个匿名类的匿名对象,并在类中**重载函数调用运算符**,实现了一个`operator()`方法

```cpp
auto print=[]{cout<<"hello"<<endl;};
```

编译器会把它翻译为下面的代码:

```cpp
class print_class{
    public:
        void operator()(void) const{
            cout<<"hello"<<endl;
        }
};
auto print=print_class();
```

### 基本输入输出

输出:cout<<

输入:cin>>

错误:cerr<<

日志:clog<<

在功能和调用上,cout,cerr和clog看上去无差别,cerr对象是**非缓冲的** ,每个流插入到cerr后会立即输出,而clog对象是缓冲的,每个流插入到clog会先存储在缓冲区,直到缓冲填满或缓冲刷新才输出

虽然看上去功能无差别,但最好还是用cerr输出错误信息,clog输出日志,不要全都用cout 

#### cout格式化输出

| 成员函数              | 说明                                                |
| ----------------- | ------------------------------------------------- |
| flags(fmtfl)      | 当前格式状态全部替换为 fmtfl。注意，fmtfl 可以表示一种格式，也可以表示多种格式。    |
| precision(n)      | 设置输出浮点数的精度为 n。                                    |
| width(w)          | 指定输出宽度为 w 个字符。                                    |
| fill(c)           | 在指定输出宽度的情况下，输出的宽度不足时用字符 c 填充（默认情况是用空格填充）。         |
| setf(fmtfl, mask) | 在当前格式的基础上，追加 fmtfl 格式，并删除 mask 格式。其中，mask 参数可以省略。 |
| unsetf(mask)      | 在当前格式的基础上，删除 mask 格式。                             |

| 标 志             | 作 用                                |
| --------------- | ---------------------------------- |
| ios::boolapha   | 把 true 和 false 输出为字符串              |
| ios::left       | 输出数据在本域宽范围内向左对齐                    |
| ios::right      | 输出数据在本域宽范围内向右对齐                    |
| ios::internal   | 数值的符号位在域宽内左对齐，数值右对齐，中间由填充字符填充      |
| ios::dec        | 设置整数的基数为 10                        |
| ios::oct        | 设置整数的基数为 8                         |
| ios::hex        | 设置整数的基数为 16                        |
| ios::showbase   | 强制输出整数的基数（八进制数以 0 开头，十六进制数以 0x 打头） |
| ios::showpoint  | 强制输出浮点数的小点和尾数 0                    |
| ios::uppercase  | 在以科学记数法格式 E 和以十六进制输出字母时以大写表示       |
| ios::showpos    | 对正数显示“+”号                          |
| ios::scientific | 浮点数以科学记数法格式输出                      |
| ios::fixed      | 浮点数以定点格式（小数形式）输出                   |
| ios::unitbuf    | 每次输出之后刷新所有的流                       |

### C++引用和指针

- 不存在空引用。引用必须连接到一块合法的内存。
- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。

### 类和对象

#### 构造函数初始化列表

对于需要传值的构造函数,如

```cpp
class box{
    protected:
        int X;
        int Y;
        int Z;
    public:
        box(int,int,int);
};
box::box(int x,int y,int z){
    X=x;
    Y=y;
    Z=z;
}
```

可以使用初始化列表

```cpp
box::box(int x,int y,int z):X(x),Y(y),Z(z){

}
```

在函数后加冒号,然后是`成员变量名(形参名)`的格式

#### 复制构造函数

复制构造函数是用已经实例化的对象来初始化新的对象的函数

如:`box b2(b1);`,格式:`classname (const classname &obj){}`

参数一般都是引用类型`&`,不能是不同传值,用指针也能但会出错

const也可以不加,还可以有两个复制构造函数,一个是const的,一个非const

即使没有定义复制构造函数,也可以使用对象初始化新对象,因为编译器会自动生成**默认的复制构造函数**,如果自己定义了,则会覆盖默认的

实例:

```cpp
class box{
    public:
        int a;
        int b;
        box(const box & c):a(c.a),b(c.b){}; 
};
```

**复制构造函数被调用的三种情况**:

1. 当用一个对象去初始化另一个同类对象,会调用复制构造函数

```cpp
box b2(b1);
box b2=b1;
```

注:第二条语句是初始化语句,不是赋值.赋值语句的左边是已经初始化的变量.

```cpp
box b1,b2;
b2=b1;
```

像上面这样就不会调用赋值构造函数,因为b2已经初始化过了

2. 作为函数的参数时,会调用复制构造函数

```cpp
class box{
    ...
};
void func(box b){
    ...    
}
int main(){
    box b1;
    func(b1);
}
```

3. 作为函数的返回值时也会调用复制构造函数

```cpp
class box{
    ...
};
box func(){
    box b;
    ...
    return b;
}
```

**关于为什么当类成员中含有指针类型成员且需要对其分配内存时,一定要有自定义的复制构造函数?**

默认的复制构造函数实现的只是**浅拷贝**,即直接将原对象的数据成员值依次复制给新的对象中对应的数据成员,并没有给新对象分配另外的内存空间.这样就导致,如果对象的数据成员 是指针的话,两个指针实际指向同一块内存空间

所以,这样就需要我们自己定义复制构造函数,为指针分配新的内存

例如:

```cpp
#include<iostream>
using namespace std;

typedef struct{
    int a;
}T,*TP;

class box{
    public:
        TP tp=(TP)malloc(sizeof(T));
        box(){};
};

int main(){
    box b1;
    b1.tp->a=21;
    box b2=b1;
    b2.tp->a=22;
    cout<<b1.tp->a;
}
```

类box中有一个TP指针,我们先初始化b1,并给b1的tp结构体中的变量a赋值21,然后复制一个b2,给b2中的结构体的变量a赋值22,再输出b1的变量值,就是看看对b2操作能否改变b1

结果:

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153902697-2142366034.png)

说明了两个tp指向同一个内存地址

**自定义复制构造函数深拷贝**:

```cpp
#include<iostream>
using namespace std;

typedef struct{
    int a;
}T,*TP;

class box{
    public:
        TP tp=(TP)malloc(sizeof(T));
        box(){};
        box(const box& b);
};

box::box(const box& b){
    free(tp);
    tp=(TP)malloc(sizeof(T));
    tp->a=b.tp->a;
}
int main(){
    box b1;
    b1.tp->a=21;
    box b2(b1);
    b2.tp->a=22;
    cout<<b1.tp->a;
}
```

重新给tp分配内存,再输出:

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153903099-615718379.png)

#### 友元函数

友元函数是定义在**类的外部**,但有权访问类的所有私有(private)和保护(protectd)成员.友元函数的原型在类的定义中出现,但它并不是类的成员函数

友元不止可以是函数,还可以是类,称为友元类

声明友元函数/类,用**friend**关键字

如:

```cpp
#include<iostream>
using namespace std;

class box{
    private:
        int lenght;
        int width;
        int height;
    public:
        friend void getter(box b);
        box(int l,int w,int h):lenght(l),width(w),height(h){};
};

void getter(box b){
    cout<<"length:"<<b.lenght<<endl;
    cout<<"width:"<<b.width<<endl;
    cout<<"height:"<<b.height;
}

int main(){
    box b1(2,3,5);
    getter(b1);
}
```

友元函数没有this指针,参数主要有三种情况:

- 非static成员,用对象做参数

- 访问static成员或全局变量时,不需要对象做参数

- 如果要访问的对象是一个全局对象,也不需要参数

友元函数的调用同普通函数,不需要通过类或对象

#### 内联函数

```cpp
inline void fun(){
    cout<<"hello";
}
int main(){
    fun();
}
```

内联函数使用关键字**inline**来声明,它和普通函数的区别是:

普通函数在**运行时被调用**,内联函数在**编译时嵌入**

也是空间换时间,增加了父作用域的空间使用,缩短了运行时的花销

使用内联函数的原则:

- 内联函数一般都是小于10行的小函数

- 不允许使用循环,递归和开关语句

**类中声明的函数,定义在类外,实际也是内联函数,只是省略了inline说明符**

#### this指针

this指针是指向对象本身的指针,在所有的成员函数的参数都隐含了this指针,可以通过this指针调用所有的成员

```cpp
class box{
    private:
        ...
    public:
        void print(this);
};
```

- 类似python的self参数

- 友元函数没有this指针,因为它不是类的成员函数

- this是一个const指针,不允许修改

#### 类的静态成员

类的静态成员用关键字`static`修饰,类似静态变量或静态函数,也是有共享的概念

**类的静态变量:**

静态变量在类的所有对象中共享,不能再类的定义中初始化,但可以在类外部通过作用域符`::`来初始化,或通过对象初始化

```cpp
class box{
    public:
        static int a;
};
int box::a=2;
int main(){
    box b1;
    cout<<b1.a;
}
```

静态变量也是有作用域的,需要`public`,调用时,只能**通过对象调用**,不能直接用类调用

**静态成员函数**:

类的静态成员函数可以直接被类调用,不需要初始化对象

```cpp
class box{
    public:
        static void print(){};
};
int main(){
    box::print();
}
```

和普通成员函数的区别:

- 静态成员函数没有this指针,只能访问静态成员

- 而普通成员函数可以访问所有的,包括静态和非静态的成员

**类中特殊成员变量的初始化:**

- const常量:必须通过构造函数参数列表初始化

- 引用变量:必须通过构造函数参数列表初始化

- 普通静态**变量**:要在类外通过`::`初始化

- 静态整型常量:就是`static const int`,可以在定义的时候直接初始化

- 静态非整型常量:要在类外通过`::`初始化

#### 访问控制和继承

访问范围:

| 访问   | public | protected | private |
| ---- | ------ | --------- | ------- |
| 同一个类 | yes    | yes       | yes     |
| 派生类  | yes    | yes       | no      |
| 外部的类 | yes    | no        | no      |

一个派生类继承所有基类的方法,除了:

- 基类的构造函数,析构函数和拷贝构造函数

- 基类的重载运算符

- 基类的友元函数

- **而且,派生类不能用初始化列表去初始化基类的成员,只能在函数体中初始化**

继承范围:

| 继承方式        | 基类的public成员   | 基类的protected成员 | 基类的private成员 |
| ----------- | ------------- | -------------- | ------------ |
| public继承    | 仍为public成员    | 仍为protected成员  | 不可见          |
| protected继承 | 变为protected成员 | 变为protected成员  | 不可见          |
| private继承   | 变为private成员   | 变为private成员    | 不可见          |

**c++支持多继承**:一个子类可以有多个父类

**环状继承**:A->D,B->D,C->A,B

这样的继承会使D创建两个对象,如:

```cpp
#include<iostream>
using namespace std;

class box{
    public:
        box(){cout<<"create object"<<endl;};
};

class A:public box{};
class B:public box{};
class C:public A,public B{};
int main(){
    C c1;
}
```

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153903449-347711993.png)

要解决上面的问题就要用虚拟继承

格式:`class 类名:virtual 继承方式 父类名`

```cpp
class A:virtual public box{};
class B:virtual public box{};
class C:public A,public B{};
```

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153903900-885059607.png)

**上面说了,派生类不继承基类的构造函数,但是可以通过初始化列表调用基类的构造函数来初始化**

```cpp
#include<iostream>
using namespace std;

class box{
    public:
        int a;
        box();
        box(int a){this->a=a;};
};

class square:public box{
    public:
        square(int a):box(a){};
};
int main(){
    square s(23);
    cout<<s.a;
}
```

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153904222-1871496332.png)

使用`square(int a):box(a){};`调用了基类的构造函数.

**派生类继承的成员和本身的成员重名的话,不会覆盖或冲突,因为继承过来变量和本身的变量在不同的内存空间**

如:

```cpp
#include<iostream>
using namespace std;

class box{
    public:
        int a;
        void setA(int a){this->a=a;};
};

class square:public box{
    public:
        int a;
        void setAA(int a){this->a=a;};
};
int main(){
    square s;
    s.setA(10);
    s.setAA(20);
    cout<<s.box::a<<endl;
    cout<<s.square::a;
}
```

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153904577-1225548546.png)

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153904888-834779619.png)

可以用作用域符`::`访问不同的同名变量

### 重载运算符和重载函数

重载是c++多态性的一大体现,重载运算符是给运算符添加新的定义,使之前不能运算的对象变得可运算,且一般和运算符的意义相似.

函数重载主要是同名函数参数类型不同,参数个数不同,实现不同的功能

#### 运算符重载

运算符重载一般作用于类的对象运算，因为它需要相同返回类型和参数，运算符重载依赖关键字`operator`,格式：

`返回类类型 operator<符号>(const 类&)`

如`Box operator+(const Box&)`

例：

```cpp
#include<iostream>
using namespace std;

class Box{
    public:
        int a;
        Box operator+(const Box& b){
            Box b1;
            b1.a=this->a+b.a;
        }
};
```

因为要用到this指针，所以运算符重载类中的，它的原理就是：

`obj3=obj1+obj2`,obj1是发生重载的对象本身，用this调用其成员；obj2是传入const obj&对象，用形参名来调用成员，obj3就是返回值。

##### 可重载的运算符和不可重载的运算符

- 可重载：

| 双目算术运算符 | + (加)，-(减)，*(乘)，/(除)，% (取模)                      |
| ------- | ------------------------------------------------ |
| 关系运算符   | ==(等于)，!= (不等于)，< (小于)，> (大于)，<=(小于等于)，>=(大于等于)  |
| 逻辑运算符   | \|(逻辑或)，&&(逻辑与)，!(逻辑非)                           |
| 单目运算符   | + (正)，-(负)，*(指针)，&(取地址)                          |
| 自增自减运算符 | ++(自增)，--(自减)                                    |
| 位运算符    | \| (按位或)，& (按位与)，~(按位取反)，^(按位异或),，<< (左移)，>>(右移) |
| 赋值运算符   | =, +=, -=, *=, /= , % = , &=, \|=, ^=, <<=, >>=  |
| 空间申请与释放 | new, delete, new[ ] , delete[]                   |
| 其他运算符   | ()(函数调用)，->(成员访问)，,(逗号)，[]\(下标\)                 |

- 不可重载     

    `.`：成员访问运算符

    `.*`,` ->*`：成员指针访问运算符

    `::`：域运算符

    `sizeof`：长度运算符

    `?:`：条件运算符

    `#`： 预处理符号

##### 运算符重载不止可以在类中实现,还可以在结构体中实现

```cpp
#include<iostream>
using namespace std;

typedef struct test{
    int a;
    test operator+(const test& t){
        test temp;
        temp.a=t.a+this->a;
        return temp;
    }
}T;


int main(){
    T t1,t2,t3;
    t1.a=12;
    t2.a=15;
    t3=t1+t2;
    cout<<t3.a;
}
```

![](https://img2022.cnblogs.com/blog/2629720/202211/2629720-20221121153905219-1136039009.png)

#### 函数重载

函数重载体现在相同的函数名和不同形参列表上，和java等都类似

如：

```cpp
#include<iostream>
using namespace std;

void print(int a){
    cout.precision(0);
    cout<<a<<endl;
}

void print(float a){
    cout.precision(2);
    cout<<a<<endl;
}

void print(double a){
    cout.precision(4);
    cout<<a<<endl;
}

int main(){
    float pi=3.1415926;
    print(pi);
}
```

### C++多态

#### 继承和派生

当类之间存在层次结构，并且类之间是通过继承关联时，就会用到多态

如：shape类被派生为两个类：Rectangle和Triangle

```cpp
#include<iostream>
using namespace std;

class Shape{
    protected:
        int width,height;
    public:
        Shape(int a=0,int b=0){width=a;height=b;}
        int area(){
            cout<<"parent class area";
            return 0;
        }
};

class Rectangle:public Shape{
    public:
        Rectangle(int a=0,int b=0):Shape(a,b){}
        int area(){
            return width*height;
        }
};
class Triangle:public Shape{
    public:
        Triangle(int a=0,int b=0):Shape(a,b){}
        int area(){
            return width*height/2;
        }
};
int main(){
    Rectangle rec(10,7);
    Triangle tri(10,5);
    cout<<tri.area()<<endl;
    cout<<rec.area()<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202211/2629720-20221129144624976-528361051.png)

#### 虚函数

虚函数是在基类中用关键字`virtual`声明的函数，在派生类中重新定义基类中定义过的虚函数时，会告诉编译器不要静态链接到该函数

如：上面的例子

```cpp
int main(){
    Shape *shape;
    Rectangle rec(10,7);
    Triangle tri(10,5);
    shape=&rec;
    cout<<shape->area()<<endl;
    shape=&tri;
    cout<<shape->area()<<endl;
}
```

输出

![](https://img2023.cnblogs.com/blog/2629720/202211/2629720-20221129144625415-1890809029.png)

并不是想象中的两个面积，这是因为调用shape->area()是基类中的area()函数，这就是`静态多态`、`静态链接`，函数调用在程序执行前就准备好了，也被称为`早绑定`，要解决这个问题，可以使用`virtual`修饰基类中的area()函数。

```cpp
class Shape{
    protected:
        int width,height;
    public:
        Shape(int a=0,int b=0){width=a;height=b;}
        virtual int area(){
            cout<<"parent class area";
            return 0;
        }
};
```

输出

![](https://img2023.cnblogs.com/blog/2629720/202211/2629720-20221129144625742-263409324.png)

这样程序中任意点可以根据所调用的对象类型来选择调用的函数，这种操作被称为动态链接

#### 纯虚函数

如果定义虚函数=0，如`virtual int area()=0;`，

那么这个函数就是一个纯虚函数，纯虚函数所在的类，只能被继承，不能用于实例化，类似java中的抽象类

如：

```cpp
#include<iostream>
using namespace std;

class Shape{
    protected:
        int width,height;
    public:
        Shape(int a=0,int b=0){width=a;height=b;}
        virtual int area()=0;
};

class Rectangle:public Shape{
    public:
        Rectangle(int a=0,int b=0):Shape(a,b){}
        int area(){
            return width*height;
        }
};

int main(){
    Rectangle rec(10,2);
    cout<<rec.area();
}
```

### 数据封装

封装性是面对对象编程语言的一大特点，在C++中也可以把类成员私有、保护，然后通过公有的setter()和getter()获取、设置数据成员，以起到保护作用

如：

```cpp
#include<iostream>
using namespace std;

class Shape{
    private:
        int width,height;
    public:
        Shape(){width=0;height=0;}
        int getWidth(){return width;}
        void setWidth(int w){width=w;}
        int getHeight(){return height;}
        void setHeight(int h){height=h;}
};

int main(){
    Shape shape;
    shape.setWidth(3);
    shape.setHeight(5);
    cout<<"area:"<<shape.getWidth()*shape.getHeight()<<endl;
}
```

### C++文件和流

C++文件的读写流用的是fstream库，它定义了三个新的数据类型：

| 数据类型     | 描述                                                                       |
| -------- | ------------------------------------------------------------------------ |
| ofstream | 该数据类型表示输出文件流，用于创建文件并向文件写入信息。                                             |
| ifstream | 该数据类型表示输入文件流，用于从文件读取信息。                                                  |
| fstream  | 该数据类型通常表示文件流，且同时具有 ofstream 和 ifstream 两种功能，这意味着它可以创建文件，向文件写入信息，从文件读取信息。 |

#### 打开文件

从文件读取信息或向文件写入信息之前，必须先打开文件，用到open()函数，open()函数是fstream,ifstream,ofsteam对象的一个成员

open()函数的第一参数是要打开的文件的名称，第二个参数是模式:`open(path,mode);`

| 模式标志        | 描述                      |
| ----------- | ----------------------- |
| ios::app    | 追加模式。所有写入都追加到文件末尾。      |
| ios::ate    | 文件打开后定位到文件末尾。           |
| ios::in     | 打开文件用于读取。               |
| ios::out    | 打开文件用于写入。               |
| ios::trunc  | 如果该文件已经存在，则先删除该文件，再重新创建 |
| ios::binary | 二进制方式                   |

且可以把多个模式结合起来用，如：

```cpp
ofstream outfile;
outfile.open("data.dat",ios::out|ios::trunc);
```

就是以写入模式打开文件，且如果文件已经存在，就把之前的内容截断

#### 关闭文件

虽然程序终止时，会自动关闭刷新所有的流，释放所有分配的内存，并关闭所有打开的文件，但最好还是在程序终止前用close()函数关闭文件

```cpp
void close();
```

#### 读写文件流

fstream也有类似cout,cin的流操作，`ofstream<<str;`一个ofstream对象可以和`<<`连接使用，将后面的内容写入ofstream对象打开的文件

如：

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    ofstream outfile("data.dat");
    int a=4321;
    outfile<<a<<"test";

}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173720967-480769850.png)

同样，ifstream对象可以和`>>`连用，将ifstream对象打开的文件的内容读到变量中。如：

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    ifstream infile("data.dat");
    string str;
    infile>>str;
    cout<<str;

}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173721510-398893291.png)

#### 逐行和逐个字符读文件

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173721928-586424248.png)

##### 逐个字符

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    fstream file;
    char c;
    file.open("data.dat",ios::in);
    while(!file.eof()){
        file>>c;
        cout<<c;
    }
    file.close();
    cout<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173722333-1514350201.png)

file.eof()是文件对象的成员，当读到文档的结尾时，会返回一个EOF标志，eof()函数当遇到EOF标志时，返回boolean的true

##### 逐行读取

需要用到getline()函数：`getline(char* str,int size,char delim);`

str:用来接收读文件流的字符串变量

size:字符数

delim:分隔符，一般为`'\n'`

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    fstream file;
    char buffer[256];
    file.open("data.dat",ios::in);
    while(!file.eof()){
        file.getline(buffer,256,'\n');
        cout<<buffer<<endl;
    }
    file.close();
    cout<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173722755-1612594297.png)

#### 流指针

ifstream 对象有一个get pointer指针，指向下一个被读取的元素

ofstream有一个put pointer指针，指向写入下一个元素的位置

fstream，同时继承了get和put指针

- 获取流指针的位置

tellg()和tellp(),返回一个整数，表示当前的get和put指针的位置

- 设置流指针的位置

seekg()和seekp(),他们有两种函数原型：

`seekg(pos_type position);`只有一个参数时，定义到第position的位置

`seekg(off_type offset,seekdir direction)`有两个参数时，用偏移量定位，direction是定位的初位置，offset是前后偏移量

| 参数       | 含义              |
| -------- | --------------- |
| ios::beg | 从流开始位置计算的位移     |
| ios::cur | 从流指针当前位置开始计算的位移 |
| ios::end | 从流末尾处开始计算的位移    |

如：

```cpp
file.seekg(-10,ios::cur)
```

就是从当前位置向前移动10个字节

例子：

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    fstream file;
    file.open("data.dat",ios::in|ios::out);
    char buffer[100];
    file<<"Hello,tom";

    file>>buffer;
    file.close();
    cout<<buffer;
}
```

对文件先写后读，输出：

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173723265-516358018.png)

因为写完指针移动到了末尾，然后读就什么都读不出来，需要移动get指针

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    fstream file;
    file.open("data.dat",ios::in|ios::out);
    char buffer[100];
    file<<"Hello,tom";
    file.seekg(0);
    file>>buffer;
    file.close();
    cout<<buffer;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173723767-904411858.png)

#### 二进制读写

二进制数据的读写用的是write和read函数：

`write/read(char* buffer,streamsize size);`

如：

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main(){
    fstream file;
    file.open("data.dat",ios::in|ios::out|ios::binary);
    char buffer[100];
    file.write("Hello,eva",9);
    file.seekg(0);
    file.read(buffer,9);
    file.close();
    cout<<buffer;
}
```

### 异常处理

参考：[cnblogs](https://www.cnblogs.com/nbk-zyc/p/12449331.html)

#### 异常和错误（bug）

异常：是程序开发过程中必须考虑的一些特殊情况，是程序运行时可以预料的执行分支。异常是不可以避免的，如0除问题，数组越界问题，文件不存在问题等。但是可以处理，通过抛出，捕获异常，**可以使程序继续运行**。

错误：是程序的缺陷，是程序运行时无法预料的运行方式，一旦发生错误，**程序将会被终止**。

如：

遇到错误时：

```cpp
#include<iostream>
using namespace std;

int main(){
    const int a=10;
    a++;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173724274-153741303.png)

程序会终止运行

而遇到异常时，可以抛出，捕获，程序不会因为异常而终止运行，而是在抛出异常后继续运行后续代码

```cpp
#include<iostream>
using namespace std;

void divide(int x,int y){
    if(y==0){
        throw -1;
    }
    cout<<x/y;
}

int main(){
    try{
        divide(20,0);
    }catch(int){
        cout<<"零除异常"<<endl;
    }
    cout<<"over"<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173724706-1784084505.png)

  如上，在遇到异常时，throw抛出一个表达式，可以是任意类型的，但是catch时要和throw抛出的表达式类型相同，如这里抛出-1，catch就要捕获int，如果抛出了"exception"这样的字符串，catch就要捕获const char*类型。

捕获完就可以处理异常，处理异常的过程是直接跳转到catch语句后，throw后面的语句便不再执行。

如：

```cpp
#include<iostream>
using namespace std;


int main(){
    try{
        cout<<"hello";
        throw -1;
        cout<<"Tom";
    }catch(int a){
        cout<<"异常:"<<a<<endl;
    }
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173725171-1793715005.png)

throw 出异常后，其后面的输出不再执行

且如上，catch捕获的不止throw表达式类型，同时可以赋给一个变量，然后在catch块中使用

#### 异常的基本原则

- 通常，异常的抛出和捕获并不是在同一个函数中进行的，假设在函数B()中遇到了异常，并不会直接在B中捕获处理异常，而是抛出给它的调用者假设为A(),

```cpp
B(){
    ...
    throw -1;
}
A(){
    try{
    B();
}catch(int){
    ...
}
}
```

如果A中没有捕获异常，程序将会自动继续向上抛出给A的调用者，一直到main()函数，如果都没有捕获异常，程序将终止执行

- 一个try语句后可以跟多个catch语句，捕获多种类型的异常，但至少有一个catch块

- 使用catch(...)可以捕获任意类型的异常

- 异常只能被一个catch捕获，一旦被捕获，其他的catch就没有捕获机会了

#### try..catch嵌套（在catch中重新抛出异常）

try...catch可以嵌套使用，也就是内层的catch捕获到异常后什么都不做，直接抛出，由上一层的catch来处理异常,如：

```cpp
#include<iostream>
using namespace std;

int main(){
    try{
        try{
            cout<<"内层抛出异常"<<endl;
            throw -1;
        }catch(int){
            throw 'a';
        }
    }catch(char){
        cout<<"外层处理异常"<<endl;
    }
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173725640-1543643672.png)

为什么要在catch语句中重新抛出异常？

![](https://img2020.cnblogs.com/i-beta/1438401/202003/1438401-20200310175802933-356066380.png)

第三方库的异常解释可读性很差，甚至需要查手册才能知道什么异常，比如直接抛出一些数值，像windows系统中常见的error:-1,error:#0x0081之类的，根本不可能通过这些信息知晓异常的详情

所以在引入第三方库后，如果遇到这些异常，就捕获了重新抛出，然后加入一些自定义的解释，来增加可读性

模拟：

```cpp
#include<iostream>
using namespace std;

void lib(){
    throw -1;
}

void myfunc(){
    try{
        lib();
    }catch(int a){
        if(a==-1){
            throw "参数错误";
        }
    }
}
int main(){
    try{
        myfunc();
    }catch(const char* str){
        cout<<"发生异常:"<<str<<endl;
    }
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173726121-1914156858.png)

#### 自定义异常类

 异常类是可以自定义的，用于整个大工程，将通用的异常集合起来管理。且异常类通常也会有派生类，一般也类似一个Exception父类，派生多种不同的异常类。在赋值兼容性原则中，一般将匹配子类异常的catch放在上部，匹配父类异常的catch放在下部。

例子：

```cpp
#include<iostream>
using namespace std;

class Exception{
    private:
        int Eid;
        string Edes;
    public:
        Exception(int id,string des){
            Eid=id;
            Edes=des;
        };

        int getEid(){return Eid;};
        string getEdes(){return Edes;};
};
void lib(){
    throw -1;
}

void myfunc(){
    try{
        lib();
    }catch(int a){
        if(a==-1){
            throw Exception(-1,"参数错误");
        }
    }
}
int main(){
    try{
        myfunc();
    }catch(Exception e){
        cout<<"发生异常:"<<e.getEid()<<e.getEdes()<<endl;
    }
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173726639-425562360.png)

#### C++标准库中的异常类

![](https://img2020.cnblogs.com/i-beta/1438401/202003/1438401-20200311010826333-201158844.png)

#### C++动态内存

同C，C++中也是有堆和栈的概念。栈是函数内部声明的所有变量都所占用空间，堆是程序中未使用的内存，在程序运行期间可用于动态分配。

同样也有alloc()分配内存，新增了new和delete运算符来分配释放内存

#### new和delete

new关键字用来分配一种类型的内存：`new type;`,并返回一个该类型的指针，`new type->type*`。如：

```cpp
int *p;
p=new int;
```

用完之后可以用delete关键字释放内存

```cpp
delete p;
```

除此之外，new还可以在给对象分配内存空间的同时创建对象。多用来创建对象数组，如：

```cpp
#include<iostream>
using namespace std;

class student{
    public:
        student(){
            cout<<"创建对象"<<endl;
        }
        ~student(){
            cout<<"销毁对象"<<endl;
        }
};

int main(){
    student* stpt=new student[3];
    delete [] stpt;

}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173727176-2070478766.png)

### C++模板

模板是泛型的基础，泛型编程就是一种独立于任何特殊类型的方式编写代码。模板就是创建**泛型类或泛型函数**的蓝图。STL库中的几个数据结构(vector,list,map等)以及算法都使用了泛型。

#### 函数模板

格式：`template <typename type> return-type function-name(parameter list){//函数体}`

模板用到的关键字是template,其后跟的就是后续可以指定的模板类型，return-type是返回值类型，后面是函数名和参数列表，和普通函数别无二致。

就是多了template关键字和一个可以后续修改的模板类型

例子：

```cpp
#include<iostream>
using namespace std;

template <typename T> T Max(T x,T y){
    return x<y?y:x;
}
int main(){
    int a=12,b=15;
    float a1=1.2,b1=1.5;
    cout<<Max(a,b)<<endl;
    cout<<Max(a1,b1)<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173727681-1587029110.png)

如上，Max函数可以作用于不同的类型的参数，它会根据参数的类型自动转换模板类型T的类型，T只是一个名字，用来标志模板的类型。

函数的参数以及返回值也是可以为T类型。

T的类型在传参时会自动确定，但也可以显式指定类型:`Max<int>()`

#### 类模板

格式：`template <class type> class class-name{};`

类似于函数模板，`<class type>`就是用来定义类模板的，后续可以指定为不同的类型

例子：

```cpp
#include<iostream>
#include<string.h>
using namespace std;

class people{
    protected:
        string name;
    public:
        people(){name="";}
        people(string name){this->name=name;}
};
class student:public people{
    protected:
        int sno;
    public:
        student(){sno=-1;}
        student(int no,string name):people(name){sno=no;}
        int getno(){return sno;}
        string getname(){return name;}
};
class teacher:public student{
    public:
        teacher(int no,string name):student(no,name){}
        int getno(){return sno;}
        string getname(){return name;}
};


template <class T> class Item{
    private:
        T* tp;
    public:
        Item(T* tp){
            this->tp=tp;
        }
        ~Item(){
            delete tp;
        }
        void getInformation(){
            if(typeid(T)==typeid(student)){
                cout<<"学号:"<<tp->getno()<<" ";
                cout<<"学生姓名:"<<tp->getname()<<endl;
            }else if(typeid(T)==typeid(teacher)){
                cout<<"工号:"<<tp->getno()<<" ";
                cout<<"教师姓名:"<<tp->getname()<<endl;
            }
        }

}; 
int main(){
    Item i(new student(2014114,"张璇"));
    i.getInformation();
    Item<teacher> i1(new teacher(2001401,"李朱强"));
    i1.getInformation();

}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173728172-172394403.png)

类模板中用到的类T的不同情况要有相同的字段，因为模板的解释是发生在编译阶段的，如果用了不同的字段，则会因为类和字段不对应找不到成员，导致编译不通过。

如上的例子中，teacher和student有相同的成员函数getno()和getname()，所以在模板类中调用两个函数可以自动识别，如果两个函数定义成不同的，如：

```cpp
class student:public people{
    protected:
        int sno;
    public:
        student(){sno=-1;}
        student(int no,string name):people(name){sno=no;}
        int getSno(){return sno;}
        string getSname(){return name;}
};
class teacher:public student{
    public:
        teacher(int no,string name):student(no,name){}
        int getTno(){return sno;}
        string getTname(){return name;}
};
template <class T> class Item{
    private:
        T* tp;
    public:
        Item(T* tp){
            this->tp=tp;
        }
        ~Item(){
            delete tp;
        }
        void getInformation(){
            if(typeid(T)==typeid(student)){
                cout<<"学号:"<<tp->getSno()<<" ";
                cout<<"学生姓名:"<<tp->getSname()<<endl;
            }else if(typeid(T)==typeid(teacher)){
                cout<<"工号:"<<tp->getTno()<<" ";
                cout<<"教师姓名:"<<tp->getTname()<<endl;
            }
        }

};
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173728679-1334697340.png)

那么在模板中，确定模板类型后，假设为student，就会因为student没有getTno()和getTname()字段而无法通过编译，因为模板T识别为student是发生在<mark>编译阶段</mark>的，一旦确定为student，模板类中所有的T都会被替换成student，所以就出现"student类无getTno()和getTname()成员"的错误。

### 信号处理

信号是由操作系统传给进程的中断，能够提前终止一个程序。在Unix,Linux,Mac OS 或Windows系统上，都可以通过Ctrl+C产生中断。

下面是可以在程序中被捕获的信号，并且可以基于信号采取适当的动作，这些信号定义在C++头文件\<csignal\>中。

| 信号      | 描述                     |
| ------- | ---------------------- |
| SIGABRT | 程序的异常终止，如调用 **abort**。 |
| SIGFPE  | 错误的算术运算，比如除以零或导致溢出的操作。 |
| SIGILL  | 检测非法指令。                |
| SIGINT  | 程序终止(interrupt)信号。     |
| SIGSEGV | 非法访问内存。                |
| SIGTERM | 发送到程序的终止请求。            |

#### signal函数

signal函数用来捕获突发事件，signal语法：

```cpp
signal (registered signal,signal handler)
```

函数的第一个参数是一个整数，代表了信号的编号，第二个参数一个指向信号处理函数的指针，也就是要把一个函数传进去当参数。例子：

```cpp
#include<iostream>
#include<csignal>
#include<unistd.h>

using namespace std;

void signalHandler(int signum){
    cout<<"Interrupt signal:"<<signum<<endl;
    exit(signum);
}
int main(){
    signal(SIGINT,signalHandler);
    int x;
    cout<<"Press Ctrl C"<<endl;
    cin>>x;
}
```

signal()的第一个参数是定义好的可以捕获的信号，如上SIGINT就是用来捕获**交互注意信号**的。可以在VS中查看定义:

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173729278-583877295.png)

该头文件给出了这几个信号的宏定义以及解释，可以看到它们是一些整数

signal()的第二个参数是捕获到信号后用来执行动作的函数，其参数就是前面该信号的整型值。

运行：

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173729812-1447921357.png)

就捕获到了这个信号，并输出提示语句

*ps:捕捉信号不能用run and debug,只能先编译，然后在终端运行*

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173730317-453818310.png)

#### raise()函数

raise()函数用来<mark>主动</mark>生成信号，参数为一个整数

```cpp
int raise(signal sig);
```

例子：

```cpp
#include<iostream>
#include<csignal>
#include<unistd.h>

using namespace std;

void signalHandler(int signum){
    cout<<"Interrupt signal:"<<signum<<endl;
    exit(signum);
}
int main(){
    signal(SIGINT,signalHandler);
    int i=-1;
    if(i<0){
        raise(SIGINT);
    }

}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173730833-861537538.png)

### 多线程

参考:[CSDN](https://blog.csdn.net/QLeelq/article/details/115747717),[知乎](https://zhuanlan.zhihu.com/p/194198073?utm_source=com.google.android.gm)

传统C++(C++11之前)中并没有引入线程的概念，如果想要在C++中实现多线程，需要借助操作系统平台提供的API，如Linux的\<pthread.h\>,或windows下的\<windows.h\>

从C++11开始提供了语言层面的多线程,包含在头文件\<thread\>中，它解决了跨平台的问题，并提供了管理线程，保护共享数据，线程间同步操作，原子操作等类。

![](https://img-blog.csdnimg.cn/20210428113430200.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1FMZWVscQ==,size_16,color_FFFFFF,t_70#pic_center)

**何时使用并发？**

程序使用并发的原因有两种。一是为了关注点分离；程序中需要执行不同的功能，就使用不同的线程来执行。二是为了提高性能，同时处理多个任务或者充分利用cpu资源，节省时间。

#### 创建线程

创建线程用到thread类，用它来创建对象，其必须的参数是一个函数

```cpp
#include<thread>
void fun(){}
thread th1(fun);
```

启用线程有两种方式，join和detach。join会阻塞父线程，等待子线程执行完，父线程才结束。而detach不会等待，一旦父线程执行完，未执行完的子线程被释放掉。

例子：

```cpp
#include<iostream>
#include<thread>
#include<unistd.h>
using namespace std;
void func(){
    for(int i=0;i<3;i++){
        cout<<"func"<<endl;
        sleep(1);
    }
}

int main(){
    thread th1(func);
    th1.join();
    cout<<"main"<<endl;
    return 0;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173731342-2107583573.png)

join模式下，子现场把func()函数执行完，main线程才结束

修改成detach模式：

```cpp
int main(){
    thread th1(func);
    th1.detach();
    cout<<"main"<<endl;
    return 0;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173731855-930391889.png)

#### 多线程

采用多线程和单线程执行两个函数对比

```cpp
#include<iostream>
#include<thread>
#include<unistd.h>
#include<time.h>
using namespace std;
void func(){
    for(int i=0;i<3;i++){
        cout<<"func"<<" ";
        sleep(1);
    }
}
void func1(){
    for(int i=0;i<3;i++){
        cout<<"func1"<<" ";
        sleep(1);
    }
}

void Main(){
    thread th(func);
    thread th1(func1);
    th.join();
    th1.join();
}

void Main1(){
    func();
    func1();
}
int main(){
    time_t start=0,end=0;
    time(&start);
    Main();
    time(&end);
    cout<<"single thread exectime:"<<difftime(end,start)<<endl;
    time(&start);
    Main1();
    time(&end);
    cout<<"multi threads exectime:"<<difftime(end,start)<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202212/2629720-20221220173732372-1304746775.png)

多线程比单线程执行时间少了一半

# 

### STL库
