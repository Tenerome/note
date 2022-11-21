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

### cout格式化输出

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

运算符重载依赖关键字`operator`,

**运算符重载不止可以在类中实现,还可以在结构体中实现**

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
