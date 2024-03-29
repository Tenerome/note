### 杂记

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

#### 常量的前缀和后缀

常量的前缀像上面说的L,用来表示宽字符,这是字符型的常量,除此之外,还有:

整型前缀:0x表示十六进制

                0表示八进制

整型后缀:U表示无符号数

                L表示长整数(long)

#### 缺省的参数

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

#### restrict

restrict关键字,规定被其修饰的指针所指的对象不能被其他指针引用

在C++中用`__restrict来修饰指针`

```c
int a;
int* __restrict p=&a;
```

这样,变量a就只能被指针p所指,不能被其他指针指

作用:有些时候可以优化性能,见[知乎](https://zhuanlan.zhihu.com/p/349726808)

#### 存储类

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

#### 杂项运算符

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

#### explicit

在 C++ 中，explicit 是一个关键字，用于修饰类的构造函数，其作用是禁止编译器将一个参数构造函数用于隐式类型转换。具体来说，当一个构造函数被 explicit 修饰时，只能通过显式调用来创建该类的对象，而不能通过隐式类型转换来创建对象。

下面通过一个例子来说明 explicit 关键字的作用：

```cpp
class A {
public:
    explicit A(int x) : m_x(x) {}
    int getX() const {
        return m_x;
    }

private:
    int m_x;
};

void foo(A a) {
    cout << a.getX() << endl;
}

int main() {
    A a1{1}; // 正确，使用显式调用构造函数创建对象
    A a2 = 2; // 错误，隐式类型转换被禁止了
    foo(3); // 错误，隐式类型转换被禁止了
    foo(A{4}); // 正确，使用显式调用构造函数创建对象
    return 0;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202306/2629720-20230601154313609-115389541.png)

在上面的代码中，我们定义了一个类 A，其中构造函数被 explicit 修饰。我们在函数 foo 中使用了 A 类型的参数，然后在 main 函数中分别使用了显式调用构造函数和隐式类型转换来创建 A 类型的对象，并尝试将这些对象作为参数传递给函数 foo。

由于构造函数被 explicit 修饰，因此我们无法直接使用隐式类型转换来创建 A 类型的对象，也无法将一个整数隐式转换为 A 类型并作为参数传递给函数 foo。只有通过显式调用构造函数来创建对象，才能正常进行编译。

使用 explicit 关键字可以显式地指定哪些构造函数可以被用于隐式类型转换，从而避免了一些潜在的类型转换错误。使用 explicit 关键字还可以提高代码的可读性，使得代码更加易于理解和维护。

#### export

`export`关键字是C++20中引入的新特性，用于向编译器声明和导出模块接口。它用于定义模块的接口，可以将声明的标识符（函数、变量、类等）导出到模块外部，供其他模块使用。同时，它还可以限定一个模块内的标识符只能被本模块内的其他代码使用，而不能被导出到外部。

`export`关键字通常与`import`关键字一起使用，`import`用于导入其他模块的接口。

下面是一个使用`export`的示例：

```cpp
// module1.cpp 
export module module1;

export int add(int a, int b) {
    return a + b;
}

export int value = 42;

// main.cpp
import module1;

int main() {
    int result = add(2, 3);
    std::cout << "result: " << result << std::endl;
    std::cout << "value: " << value << std::endl;
    return 0;
}
```

在上面的示例中，`module1`模块中导出了`add`函数和`value`变量，并在`main.cpp`中使用了这两个标识符。当编译`main.cpp`时，编译器会自动将`module1`模块编译成一个单独的文件，并将其链接到`main`程序中。

需要注意的是，`export`关键字目前还不是所有编译器都支持，具体情况需要查看编译器的文档。

#### typeid和decltype

C++中的`typeid`关键字用于获取一个表达式的类型信息，可以用来判断两个对象是否为同一种类型。具体来说，`typeid`可以返回一个`type_info`类型的对象，该对象包含了表达式的类型信息，可以通过`type_info`对象的`name()`方法获取类型名。`typeid`一般用于运行时类型识别（RTTI）。

> RTTI运行时类型识别（Runtime Type Identification，RTTI）是一种在程序运行时确定对象类型的机制。RTTI通常用于C++中，可以使用typeid运算符来获得对象的类型信息。在程序中，通过将对象转换为其基类或接口类型来使用RTTI。RTTI可以用于在程序运行时进行类型安全的转换和异常处理，但过度使用RTTI可能会导致代码的性能下降。
> 
> 与之相关的还有编译时类型识别（Compile-time type checking）

例如，下面的代码可以获取一个变量的类型信息，并输出其类型名：

```cpp
#include <iostream>
#include <typeinfo>

int main() {
    int x = 42;
    const std::type_info& type = typeid(x);
    std::cout << type.name() << std::endl;
    return 0;
}
```

输出结果为：

```
i
```

这里的`i`表示整数类型。另外，char型的类型值为c,long型的类型值为l,float型为f。简单类型是用的单个字符表示，类或函数用字符串表示，其中会包括返回值类型、参数类型等字符，如：

```cpp
int fun(long x=0,char y='1'){
    return 0;
}
int main(){
    const std::type_info& type = typeid(fun);
    std::cout << type.name() << std::endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202306/2629720-20230601154316511-550059457.png)

第二个i是函数返回值类型，l是第一个参数类型值，c是第二个参数类型值。

另外，C++11中引入了`decltype`关键字，可以用来获取一个表达式的类型，也可以用于函数返回类型的推导等。

C++11中引入了`decltype`关键字，用于获取一个表达式的类型，也可以用于函数返回类型的推导等。`decltype`的基本语法如下：

```cpp
decltype(expression)
```

其中，`expression`可以是任意一个表达式，`decltype`会返回该表达式的类型，包括const、引用等修饰符。

下面是几个使用`decltype`的例子：

```cpp
int x = 42;
const int& y = x;
decltype(x) z1 = 0;  // z1的类型为int
decltype(y) z2 = x;  // z2的类型为const int&
decltype(x+y) z3 = 0;  // z3的类型为int
```

在上面的代码中，`z1`的类型为`int`，因为`decltype(x)`的结果是`int`；`z2`的类型为`const int&`，因为`decltype(y)`的结果是`const int&`；`z3`的类型为`int`，因为`decltype(x+y)`的结果是`int`。

另外，`decltype`还可以用于函数返回类型的推导。例如：

```cpp
template <typename T, typename U>
auto add(T t, U u) -> decltype(t+u) {
    return t + u;
}
```

在上面的代码中，`decltype(t+u)`用于推导函数返回类型，即`t`和`u`相加的结果类型。

需要注意的是，`decltype`并不会对表达式进行求值，而是仅仅返回表达式的类型。因此，如果表达式中包含了函数调用或运算符重载等操作，`decltype`会返回对应的函数返回类型或运算符重载结果类型，而不是表达式的值。

#### typename

`typename`关键字则用于指明一个名称是类型名称。在C++中，有时需要使用嵌套的类型名称，如类模板中的类型别名或嵌套类的名称等。在这种情况下，需要使用`typename`关键字来指明名称是类型名称而非成员名称。例如：

```cpp
template <typename T>
struct my_template {
    typename T::value_type* ptr;
};
```

在上面的代码中，`typename T::value_type`表示T类型中的value_type类型，而不是T类型中的名为value_type的成员变量。如果省略了`typename`关键字，则编译器会将`T::value_type`解释为成员变量名，从而导致编译错误。

#### 四种cast

在C++中，有四种类型转换的方式，它们分别是static_cast、dynamic_cast、const_cast和reinterpret_cast。

1. static_cast：用于基本数据类型的转换，以及非多态类型的转换。例如，将int类型转换为double类型，或将指针类型转换为void*类型。
   
   如：
   
   ```cpp
   int a = 10;
   double b = static_cast<double>(a);  // 将int类型的a转换为double类型的b
   
   class Base {};
   class Derived : public Base {};
   Base* base = new Derived;
   Derived* derived = static_cast<Derived*>(base);  // 将基类指针转换为派生类指针
   ```

2. dynamic_cast：用于多态类型的转换，即具有虚函数的类型。它会在运行时检查是否能够安全地将一个指针或引用转换为目标类型，如果不能则返回NULL。例如，将基类指针转换为派生类指针，或将派生类指针转换为基类指针。
   
   ```cpp
   class Base {
   public:
       virtual void print() { cout << "Base" << endl; }
   };
   class Derived : public Base {
   public:
       void print() { cout << "Derived" << endl; }
   };
   
   Base* base = new Derived;
   Derived* derived = dynamic_cast<Derived*>(base);  // 将基类指针转换为派生类指针
   if (derived) {
       cout<<"derived"<<endl;  // 输出"Derived"
   }else{
       cout<<"error deriving";
   }
   ```

3. const_cast：用于去除const属性。例如，将const int*类型指针转换为int*类型指针，或将const对象转换为非const对象。
   
   ```cpp
   const int a = 10;
   int& b = const_cast<int&>(a);  // 将const int类型的a转换为int类型的b的引用
   b = 20;
   cout << a << endl;  // 输出10，因为a依然是const类型
   ```

4. reinterpret_cast：用于进行二进制的低层次转换，不考虑类型之间的关系。例如，将一个指针转换为一个整数，或将一个整数转换为一个指针。
   
   ```cpp
   int a = 10;
   int* p = &a;
   long long b = reinterpret_cast<long long>(p);  // 将int类型的指针p转换为long long类型的b
   cout << b << endl;  // 输出p的地址的十进制表示
   ```

需要注意的是，这些类型转换都具有一定的风险，需要谨慎使用。特别是reinterpret_cast，容易导致不可预测的错误，应该尽量避免使用。

#### memset

C++ 中的 memset 是一个用于填充内存块的函数，其定义在头文件 `<cstring>` 中。memset 可以将一段内存块的值都设置为指定的值，常用于清空数组或结构体等操作。

memset 函数的语法如下：

```cpp
void* memset(void* ptr, int value, size_t num);
```

其中，第一个参数 ptr 是指向内存块的指针，第二个参数 value 是要设置的值（通常是 0 或 -1），第三个参数 num 是要设置的字节数。函数会将 ptr 指向的内存块中的前 num 个字节都设置为 value。

例如，下面的代码使用 memset 函数将一个数组清空：

```cpp
int arr[10];
memset(arr, 0, sizeof(arr));
```

在上面的代码中，我们将 arr 数组中的所有元素都设置为 0。由于数组中有 10 个元素，因此我们传递给 memset 函数的第三个参数是 sizeof(arr)，表示要设置的字节数。

需要注意的是，memset 函数并不会检查数组越界等错误，因此使用时需要确保不会访问到不属于自己的内存区域。此外，对于非 POD 类型（即含有构造函数、析构函数或虚函数的类型），使用 memset 函数可能会导致不可预期的行为，因此需要谨慎使用。

#### assert

assert断言，是C++\<assert.h\>库的函数，用来找出程序的错误的。格式:`assert(exp);`

assert的第一个参数是一个表达式，就是用来找错的表达式，如果为真则程序继续执行，若为假则引起abort中断信号，程序终止执行。

如:

```cpp
#include<assert.h>
#include<iostream>
int main(){
    int a=0;
    assert(a);

}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223012216-1574175905.png)

##### 为什么不用if

assert是用来排除错误的，而if是用来找异常的，错误是可以通过修改去掉的，而异常是无法避免的。

##### 为什么不直接cout

因为在一些大项目中，可以不止一个输出，所以如果找到错误，后续的程序便不需要继续执行。如：

```cpp
#include<assert.h>
#include<iostream>
int main(){
    int a=0;
    int b=0;
    int c=0;
    //...
    assert(a);

    std::cout<<a<<" ";
    std::cout<<b<<" ";
    std::cout<<c<<" ";
    //...
}
```

##### 使用规则

- 根据上一条，所以assert一般用于程序输出的开始

- 每个assert只检查一个条件，不然找到错误不知道是哪个

- 不能改变环境的表达式
  
  如:`assert(a++);`这样会改变环境的表达式要用，只能用`assert(a),assert(a<100)`这样对原环境无影响的表达式

- 一般assert()语句下一行空着，用来标注断言语句

### 引用类型

c++增加引用类型的概念,定义方法`int &b=a;`表示引用类型,引用类型相当于变量的别名,地位和被引用的变量相同,`int &b=a;`,执行后,变量a和b有相同的值和地址,相当于一个地址的内容有两个标签

必须在定义时用,如果在定义后,`int b;&b=a`就不是引用了,而是取地址

类似于指针的定义和取内容,`int *p;`定义指针,`*p`取指针p的内容

#### C++引用和指针

- 不存在空引用。引用必须连接到一块合法的内存。
- 一旦引用被初始化为一个对象，就不能被指向到另一个对象。指针可以在任何时候指向到另一个对象。
- 引用必须在创建时被初始化。指针可以在任何时间被初始化。

#### 左值、右值与引用

参考:[C语言中文网](http://c.biancheng.net/view/7829.html).

C++的左值和右值是从C语言继承过来的，左值的英文简写是"lvalue",右值是"rvalue"。但是他们并不是"left"和"right"。左值的本意是"loactor value",即"可定位的值"，也就是存储在内存中、有明确的存储地址的数据，或者说可寻址的数据。而右值"read value"，指仅提供数值的数据，不一定可以寻址，如存储在寄存器中的数据。

通常，简单区分左值右值就看赋值号(=)的左右侧，能放在左侧的就是左值，<mark>只</mark>能放在右侧的是右值。所以就有既能做左值又能做右值的。

如：

```cpp
int a=1;
int b=a;
```

变量a仅能放在左边，也能放右边，而数值1只能放右边，就是右值。

另外一个例子：const修饰的类型不能再修改值，本质就是不能做左值了。

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214821918-715843583.png)

#### 右值引用[C++ 11新增]

在C++98/03中，就有引用，用‘&’表示，但是不能对数值引用只能引用定义好的变量。

```cpp
int a=10;
int &b=a;
//int &c=10;  不能这么用
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214822770-1097300467.png)

但是可以给常量左值引用赋数值

```cpp
const int &a=10;
```

因为const关键字把locator value变成read value，所以可以将数值赋给常量左值引用

C++ 11中添加新的引用方式：右值引用，用“&&”表示

右值引用也必须定义时初始化，但右值引用初始化不能是左值，只能是右值。

```cpp
int &&a=10;
//int b=1; int &&a=b;  是不行的
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214823694-225617273.png)

右值引用，用别名更容易理解，`int &&a=10;`,是给数值10起个别名叫做a。而且，a的值是可以修改的。

意义：主要用于<mark>移动构造函数</mark>，避免不必要的深拷贝，提高程序运行效率。

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

### 构造函数和复制构造函数

#### 构造函数

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

### 移动构造函数[C11新增]

参考:[知乎:C++11右值引用和移动构造函数详解](https://zhuanlan.zhihu.com/p/365412262#:~:text=%E7%A7%BB%E5%8A%A8%E8%AF%AD%E4%B9%89%E7%9A%84%E5%85%B7%E4%BD%93%E5%AE%9E%E7%8E%B0%E5%B0%B1%E6%98%AFC%2B%2B%E7%A7%BB%E5%8A%A8%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%E3%80%82%20class%20A%20%7B%20public%3A%20int%20x%3B%20%2F%2F%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0,cout%20%3C%3C%20%22Move%20Constructor%22%20%3C%3C%20endl%3B%20%7D%20%7D%3B).[知乎:什么是POD数据类型](https://zhuanlan.zhihu.com/p/45545035?utm_id=0).

C++ 11之前，对象的拷贝由三个函数决定：拷贝构造函数，拷贝赋值运算符和析构函数。

C++ 11新增两个函数:移动构造函数和移动赋值运算符。

首先介绍移动语义（move），指以移动的方式而非深拷贝的方式初始化含有指针成员的类对象。也就是剥夺了用于初始化的对象的资源。

如：使用std::move()函数来初始化对象

```cpp
#include<iostream>
using namespace std;

int main(){
   string str="hello";
   string ss=move(str);
   cout<<"str:"<<str<<endl<<"ss:"<<ss<<endl;

}
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214824383-94194771.png)

可以看到str字符串变为空了，也就是移动而非拷贝的方式初始化ss。

#### move

move在Cplusplus中的解释是：

> `std::move` is used to *indicate* that an object `t` may be "moved from", i.e. allowing the efficient transfer of resources from `t` to another object.
> 
> In particular, `std::move` produces an [xvalue expression](https://en.cppreference.com/w/cpp/language/value_category "cpp/language/value category") that identifies its argument `t`. It is exactly equivalent to a `static_cast` to an rvalue reference type.

move函数是用于对象之间高效地转移资源的。也就是前面说的move语义，剥夺而非拷贝的方式获取资源。特别，move函数可以生成一个和它的参数t有关联的xvalue(指资源可以再利用的对象)表达式。也就是move会返回和参数类型相同的类型的表达式。完全等同于static_cast强制转换右值引用类型。

对于no-pod类型，move是以移动的方式获取资源，而pod类型，则是直接复制。并不会有参数的资源销毁。

> pod类型是plain old data的缩写，指没有构造/析枸函数、复制/移动构造函数、复制/移动运算符的的数据类型。如int,char,float等。
> 
> 而no-pod就是有这些东西的，如string，以及自定义的类

如：直接move()一个int

```cpp
#include<iostream>
using namespace std;

int main(){
    int a=10;
    int b=move(a);
    cout<<"a:"<<a<<"  b:"<<b;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214825102-572906.png),move就并不会销毁a中的资源

再比如：没有定义移动构造函数的类的对象用move初始化

```cpp
#include<iostream>
using namespace std;

class A{
   public:
   char *c;
   A(string s){
      this->c=&s[0];
   }

};
int main(){
   A a1("hello");
   A a2=move(a1);
   cout<<a2.c<<endl;
   cout<<a1.c;

}
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214825768-1429578651.png),move也没有销毁参数的资源

所以是需要我们自己定义销毁行为的

```cpp
#include<iostream>
using namespace std;

class A{
   public:
   char *c;
   A(string s){
      this->c=&s[0];
   }
   A(A &&temp){
      this->c=temp.c;
      temp.c=nullptr;
   }

};
int main(){
   A a1("hello");
   A a2=move(a1);
   cout<<a2.c<<endl;
   cout<<a1.c;

}
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214826490-2106290296.png),这样就实现了移动。

**为什么要销毁？**

一般认为，移动资源后，原来的参数就不会再被访问到，为了保证这一点，需要手动置零/置空/释放内存，这也是对前面"高效"的解释。

### 友元函数、内联函数和this指针

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

### 类的访问控制和继承

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

#### 访问控制范围和继承范围

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

### 运算符重载和函数重载

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
    func();
    func1();
}

void Main1(){
    thread th(func);
    thread th1(func1);
    th.join();
    th1.join();
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

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223012872-512799918.png)

多线程比单线程执行时间少了一半

#### this_thread类

this_thread是一个类，有4个功能函数：

##### get_id()

获取当前线程id

```cpp
#include<iostream>
#include<thread>
using namespace std;

void fun(){
    cout<<"hello"<<endl;
}
int main(){
    thread th1(fun);
    cout<<th1.get_id()<<endl;
    th1.join();
}
```

##### yield

放弃当前线程占用的时间片，使CPU重新调度以便其他线程执行。

为了展示yield的效果，把程序绑定到一个cpu上处理。使用以下代码，把cpp程序绑定在指定的cpu上：

```cpp
int your_fixed_cpu_kernl=3;
cpu_set_t cpuset;
CPU_ZERO(&cpuset);
CPU_SET(your_fixed_cpu_kernl,&cpuset);
int rc =pthread_setaffinity_np(pthread_self(),sizeof(cpu_set_t), &cpuset);
if (rc != 0) {
  std::cerr << "Error calling pthread_setaffinity_np: " << rc << "\n";
}
```

并且在编译时需要链接pthread库

代码：

```cpp
#include<iostream>
#include<thread>
using namespace std;

void fun(){
    cout<<"th1"<<endl;
    this_thread::yield();
    cout<<"th1.1"<<endl;
}

void fun1(){
    cout<<"th2"<<endl;
    this_thread::yield();
    cout<<"th2.1"<<endl;
}
int main(){
    //绑定到0号CPU
    int cpu_kernl=0;
    cpu_set_t cpuset;
    CPU_ZERO(&cpuset);
    CPU_SET(cpu_kernl,&cpuset);
    int rc=pthread_setaffinity_np(pthread_self(),sizeof(cpu_set_t),&cpuset);
    if(rc!=0){
        cerr<<"Error calling pthread_setaffinity_np"<<rc<<endl;
    }
    //end
    thread th1(fun);
    thread th2(fun1);
    th1.join();
    th2.join();
}
```

本来该并行执行的多线程任务，被指定到单个CPU上并发执行，当运行到yield暂停当前线程，执行其他线程，之后再返回继续执行。

编译：

```bash
g++ test.cpp -o test -lpthread
```

结果：

![](https://img2023.cnblogs.com/blog/2629720/202301/2629720-20230110143054365-1289103664.png)

##### sleep_for和sleep_until

都是延时线程的函数

sleep_for()要和std:\:chrono::seconds，minutes,hours连用，设定暂停的时间。

sleep_until和chrono::system_clock连用，设定暂停到一个时间点。

#### mutex类

mutex类是C++中最基本的互斥量。它提供了基本的上锁与解锁函数，lock(),unlock()以及try_lock()。

###### lock()与unlock()：

下面模拟之前说过的打印机的情况，就是多线程访问打印机，其中A线程在装入信息后被阻塞，打印机中的数据就会被线程B覆盖，当A恢复执行时，打印机中的数据仍然是B的数据。

```cpp
#include<iostream>
#include<thread>
using namespace std;

string printstr;//模拟打印机装入信息
void printer(string str){
    printstr=str;
    this_thread::sleep_for(chrono::seconds(1));//模拟线程被阻塞
    for(int i=0;i<3;i++)
        cout<<printstr<<endl;
}

int main(){
    thread th1(printer,"Hello");
    thread th2(printer,"world");
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202301/2629720-20230110143054901-1290540751.png)

可以看到打印机打印了6次th2线程的数据。想要获取正确的信息，就要用互斥锁，在打印前加锁，打印后解锁。

```cpp
#include<iostream>
#include<thread>
#include<mutex>
using namespace std;

mutex plocker;//打印机锁
string printstr;//模拟打印机装入信息
void printer(string str){
    plocker.lock();//加锁
    printstr=str;
    this_thread::sleep_for(chrono::seconds(1));//模拟线程被阻塞
    for(int i=0;i<3;i++)
        cout<<printstr<<endl;
    plocker.unlock();//解锁
}

int main(){
    thread th1(printer,"Hello");
    thread th2(printer,"world");
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202301/2629720-20230110143055296-1211884803.png)

就获得了正确的打印结果

###### try_lock()

- try_lock()是尝试上锁，有两种情况：
1. 锁空闲，返回true，并加锁

2. 锁已经其他线程获取，返回false

模拟apt安装包时，另外一个线程等待的情况：

```cpp
#include<iostream>
#include<thread>
#include<mutex>
#include<unistd.h>//sleep函数

using namespace std;

mutex aptlocker;//模拟apt锁

void installer(string str){
    while(!aptlocker.try_lock()){
        cout<<"waitting for other installing thread"<<endl;
    }
    cout<<"installing package:"<<str<<endl;
    sleep(0.5);
    aptlocker.unlock();

}

int main(){
    thread th1(installer,"vim");
    thread th2(installer,"stacer");
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202301/2629720-20230110143055690-1514237332.png)

- 另外try_lock()还可以给多个互斥量加锁，格式：

```cpp
int try_lock(mutex1,mutex2,mutex3...);
```

如果所有互斥量都加锁成功，则返回-1。当首次遇到加锁失败的互斥量时，停止对后续互斥量的加锁，并解锁前面的互斥量，返回首个加锁失败的互斥量的序号。 （Attempts to lock all the objects  passed as arguments using their [try_lock](https://cplusplus.com/mutex::try_lock) member functions (non-blocking).  

The function calls the [try_lock](https://cplusplus.com/mutex::try_lock) member function for each argument (first a, then b, and eventually the others in cde, in the same order), until either all calls are successful, or as soon as one of the calls fails (either by returning `false` or throwing an exception).  

If the function ends because a call fails, [unlock](https://cplusplus.com/mutex::unlock) is called on all objects for which the call to [try_lock](https://cplusplus.com/mutex::try_lock) was successful, and the function returns the argument order number of the object whose lock failed. No further calls are performed for the remaining objects in the argument list.）from [cplusplus](https://cplusplus.com/reference/mutex/try_lock/).

如：

```cpp
mutex locker1,locer2,locker3;
locker2.lock();
try_lock(locker1,locker2,locker3);
```

- lock()和try_lock()的区别

lock()是以阻塞的方式获取锁，而try_lock()是非阻塞式的。当线程请求被占用的锁时，用lock方式请求，会阻塞当前线程，无限时间，直到锁被释放。这就是<mark>死锁</mark>产生的直接原因,如果被占用的锁没有释放，那么请求的线程会永久地阻塞。

try_lock()方式请求锁时，会有一个设定好的最大时间，当在这个时间内没有获取到锁，线程会放弃请求锁，直接继续执行后续的代码。

了解更多：[wait for single object函数](https://blog.csdn.net/zx3517288/article/details/52743011).

- 所以有时候try_lock()并不能同步，如果是严格的同步程序，最好用lock();

如：之前打印机的模拟例子，使用互斥锁得到了正确的结果，如果是try_lock():

```cpp
#include<iostream>
#include<thread>
#include<mutex>
using namespace std;

mutex plocker;//打印机锁
string printstr;//模拟打印机装入信息
void printer(string str){
    plocker.try_lock();//加锁
    printstr=str;
    this_thread::sleep_for(chrono::seconds(1));//模拟线程被阻塞
    for(int i=0;i<3;i++)
        cout<<printstr<<endl;
    plocker.unlock();//解锁
}

int main(){
    thread th1(printer,"Hello");
    thread th2(printer,"world");
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202301/2629720-20230113212233394-1765595.png)

##### try_lock_for和try_lock_until

类似this_thread_for/until，参数也是时间

#### lock类

##### 简单说明三个参数

lock_guard和unique_lock的第二个参数，是一个常数，一个标记tag。

| Type          | Effect(s)                                                    |
| ------------- | ------------------------------------------------------------ |
| defer_lock_t  | do not acquire ownership of the mutex                        |
| try_to_lock_t | try to acquire ownership of the mutex without blocking       |
| adopt_lock_t  | assume the calling thread already has ownership of the mutex |

其中，lock_guard只能使用adopt_lock,而unique_lock三个都可以用。

defer_lock是一个标记，用来阻止对象在构造时获取mutex的所有权，也就是在构造时先不加锁，后面可以手动用lock加锁

> Passing [defer_lock](https://cplusplus.com/defer_lock) to [unique_lock](https://cplusplus.com/unique_lock)'s constructor, makes it not to lock the *mutex object* automatically on construction, initializing the object as not *[owning a lock](https://cplusplus.com/unique_lock::owns_lock)*.

try_to_lock类似try_lock都是非阻塞式地尝试获取锁，而adopt则是假设调用的线程已经对互斥量上锁，实际mutex对象并没有上锁，只是thread获取了mutex对象的所有权。

##### lock_guard

lock_guard是mutex的封装类，它提供了一种方便的RAII-style机制来获取一个mutex互斥量，到达持续加锁的目的。

(RAII-style是C++的一种资源管理机制，用其管理的对象，在对象构造时获取该对象的资源，在对象生命周期间控制对象资源的访问，最后在对象析构后释放对象资源。)

lock_guard完整格式：`template <class Mutex> class lock_guard;`

其中的Mutex不是mutex类，而是一个Basiclockable的类型，C++中有这几个类：

| type                                                                 |
| -------------------------------------------------------------------- |
| [mutex](https://cplusplus.com/mutex)                                 |
| [recursive_mutex](https://cplusplus.com/recursive_mutex)             |
| [timed_mutex](https://cplusplus.com/timed_mutex)                     |
| [recursive_timed_mutex](https://cplusplus.com/recursive_timed_mutex) |
| [unique_lock](https://cplusplus.com/unique_lock)                     |

例子：将之前的打印机模拟改成lock_guard同步

```cpp
#include<iostream>
#include<thread>
#include<mutex>
using namespace std;

mutex l;//打印机锁
string printstr;//模拟打印机装入信息
void printer(string str){
    lock_guard<mutex> locker(l);//用lock_guard改写
    printstr=str;
    this_thread::sleep_for(chrono::seconds(1));//模拟线程被阻塞
    for(int i=0;i<3;i++)
        cout<<printstr<<endl;

}

int main(){
    thread th1(printer,"Hello");
    thread th2(printer,"world");
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230209214826994-910588005.png)

lock_guard不能中途解锁，不能复制/移动，但是效率高。

可以使用的参数:adopt_lock

```cpp
lock_guard<mutex> locker(l,adopt_lock);
```

但是不能后续手动lock

##### unique_lock

参考：[cplusplus](https://cplusplus.com/reference/mutex/unique_lock/)

unique_lock也是一个模板类，拥有lock_guard的所有功能，但比lock_guard更强大。相比lock_guard构造时自动加锁析、构时解锁，unique_lock提供了加锁和解锁的接口，可以根据需求加锁解锁。

比如，在使用defer_lock参数后，unique_lock对象还可以后续手动上锁。如：

```cpp
#include<iostream>
#include<thread>
#include<mutex>
using namespace std;

mutex l;//打印机锁
string printstr;//模拟打印机装入信息
void printer(string str){
    unique_lock<mutex> locker(l,defer_lock);//用unique_lock改写
    locker.lock();//手动上锁
    printstr=str;
    this_thread::sleep_for(chrono::seconds(1));//模拟线程被阻塞
    for(int i=0;i<3;i++)
        cout<<printstr<<endl;

}

int main(){
    thread th1(printer,"Hello");
    thread th2(printer,"world");
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230213220916294-88427910.png)

##### defer_lock和adopt_lock的区别

defer_lock是暂时先不加锁，和未上锁的状态是一致的，而adopt_lock假设线程已经获取了锁，在mutex对象中，有个m_owns参数，也就是前面说的ownership，被谁获取了，这个值表示是否被调用的线程获取mutex对象的所有资源。但是并不是上锁的意思，上锁的参数是mutex对象的数据域的_lock值控制的，defer_lock和未上锁的状态一致，m_owns为false,data域的_lock值为0。当使用lock()手动上锁时，m_owns为true，data域的_lock值为1。

而adopt_lock,会使m_owns为true,但是_lock却是0,也就是线程拥有了mutex对象，但是并没有上锁，后续如果上锁的话，会导致死锁，因为上锁首先要获取锁，而锁已经被拥有了，也就导致死锁了。

实际操作：初始用defer_lock，后面手动上锁

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230213220917118-1959553518.png)

可以看到_m_owns为false，__lock为0。接着step over

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230213220918019-576218349.png)

而adopt_lock：

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230213220918707-2098652302.png)

_m_owns为true，所以说假设线程获取了资源，就是mutex的owns为true，但是__lock是0,也就是并没有上锁，如果此时继续调试，将会产生死锁：

![](https://img2023.cnblogs.com/blog/2629720/202302/2629720-20230213220919662-1621846472.png)

#### atomic

参考:[c++11 多线程（3）atomic 总结 - 简书](https://www.jianshu.com/p/8c1bb012d5f8).[c++11 atomic Npgw的博客](https://blog.csdn.net/wanxuexiang/article/details/104280021).[C++11 并发指南系列 - Haippy - 博客园](https://www.cnblogs.com/haippy/p/3284540.html).

##### atomic_flag

atomic_flag看名字就能知道是一种flag类型，它是一种简单的原子布尔类型，只支持两种操作：test-and-set和clear。

创建atomic_flag对象时，如果不初始化，那么该对象的状态就是unspecified，未指定的。(C++11的，C++20后未初始化时为clear)

```cpp
atomic_flag flag;
```

可以使用ATOMIC_FLAG_INIT标志初始化对象， 表示对象处于clear状态。转到定义，可以看到该tag的值为0

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102537693-1849910439.png)

atomic_flag对象只有两种操作，test_and_set就是把atomic_flag的\_M\_i域置为1,clear则是置零。

###### 功能

test_and_set()的作用是先test测试返回atomic_flag对象的状态，接着set，把对象设置为true。

clear()是直接设置为false,返回类型为void。

##### 原子类型

原子类型需要引用头文件\<atomic\>，一个原子类型就是原有类型加上atomic_表示。如int对应的原子类型atomic_int,也可以使用原始格式,是类模板实现的：atomic\<int\> 。

其他原子类型还有:

| Typedefs                   |                                 |
| -------------------------- | ------------------------------- |
| std::atomic_bool           | std::atomic<bool>               |
| std::atomic_char           | std::atomic<char>               |
| std::atomic_schar          | std::atomic<signed char>        |
| std::atomic_uchar          | std::atomic<unsigned char>      |
| std::atomic_short          | std::atomic<short>              |
| std::atomic_ushort         | std::atomic<unsigned short>     |
| std::atomic_int            | std::atomic<int>                |
| std::atomic_uint           | std::atomic<unsigned int>       |
| std::atomic_long           | std::atomic<long>               |
| std::atomic_ulong          | std::atomic<unsigned long>      |
| std::atomic_llong          | std::atomic<long long>          |
| std::atomic_ullong         | std::atomic<unsigned long long> |
| std::atomic_char16_t       | std::atomic<char16_t>           |
| std::atomic_char32_t       | std::atomic<char32_t>           |
| std::atomic_wchar_t        | std::atomic<wchar_t>            |
| std::atomic_int_least8_t   | std::atomic<int_least8_t>       |
| std::atomic_uint_least8_t  | std::atomic<uint_least8_t>      |
| std::atomic_int_least16_t  | std::atomic<int_least16_t>      |
| std::atomic_uint_least16_t | std::atomic<uint_least16_t>     |
| std::atomic_int_least32_t  | std::atomic<int_least32_t>      |
| std::atomic_uint_least32_t | std::atomic<uint_least32_t>     |
| std::atomic_int_least64_t  | std::atomic<int_least64_t>      |
| std::atomic_int_fast8_t    | std::atomic<int_fast8_t>        |
| std::atomic_uint_fast8_t   | std::atomic<uint_fast8_t>       |
| std::atomic_int_fast16_t   | std::atomic<int_fast16_t>       |
| std::atomic_uint_fast16_t  | std::atomic<uint_fast16_t>      |
| std::atomic_int_fast32_t   | std::atomic<int_fast32_t>       |
| std::atomic_uint_fast32_t  | std::atomic<uint_fast32_t>      |
| std::atomic_int_fast64_t   | std::atomic<int_fast64_t>       |
| std::atomic_uint_fast64_t  | std::atomic<uint_fast64_t>      |
| std::atomic_intptr_t       | std::atomic<intptr_t>           |
| std::atomic_uintptr_t      | std::atomic<uintptr_t>          |
| std::atomic_size_t         | std::atomic<size_t>             |
| std::atomic_ptrdiff_t      | std::atomic<ptrdiff_t>          |
| std::atomic_intmax_t       | std::atomic<intmax_t>           |
| std::atomic_uintmax_t      | std::atomic<uintmax_t>          |

可以看到主要是一些关于int,short,long,char等在内存中以整数存储的类型，没有float,double等浮点型的。

- 原子类型实现同步的例子：

多线程做累加，如果没有做同步，得到的结果可能是正确的，也可能小于预测值。

1. 无同步，直接++计算

```cpp
#include<iostream>
#include<thread>
#include<atomic>

using namespace std;

int count;
void counter(){
    for(int i=1;i<200000;i++)
        count++;

}

int main(){
    thread th1(counter);
    thread th2(counter);
    thread th3(counter);
    thread th4(counter);
    thread th5(counter);
    th1.join();
    th2.join();
    th3.join();
    th4.join();
    th5.join();
    cout<<count<<endl;
}
```

得到的结果：

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102538247-1179066802.png)![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102538731-1875944999.png)![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102539232-1855331548.png)

每次结果都不同。

2. 使用锁进行同步：

```cpp
#include<iostream>
#include<thread>
#include<atomic>
#include<mutex>
using namespace std;

int count;
mutex l;
void counter(){
    lock_guard<mutex> locker(l);
    for(int i=0;i<200000;i++)
        count++;
}

int main(){
    thread th1(counter);
    thread th2(counter);
    thread th3(counter);
    thread th4(counter);
    thread th5(counter);
    th1.join();
    th2.join();
    th3.join();
    th4.join();
    th5.join();
    cout<<count<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102539770-11278304.png)

3. 使用原子类型:

```cpp
#include<iostream>
#include<thread>
#include<atomic>
#include<mutex>
using namespace std;

atomic_int count;

void counter(){
    for(int i=0;i<200000;i++)
        count++;
}

int main(){
    thread th1(counter);
    thread th2(counter);
    thread th3(counter);
    thread th4(counter);
    thread th5(counter);
    th1.join();
    th2.join();
    th3.join();
    th4.join();
    th5.join();
    cout<<count<<endl;
}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102540384-868197017.png)

##### 原子类型的实现原理

原子类型实现的原理是直接翻译成CPU指令，而对原子类型的操作，像+，-，*，\,++等直接重载了运算符，编译时也直接翻译成CPU指令。每一个原子操作都是<mark>一条独立</mark>的CPU指令来完成，在其指令周期内，其他CPU无法对原子类型操作。

举例：

```cpp
#include<iostream>
#include<thread>
#include<atomic>
#include<mutex>
using namespace std;

atomic_int count;

void counter(){
    for(int i=0;i<200000;i++)
        count++;
}

int main(){
    thread th1(counter);
    th1.join();
    cout<<count<<endl;
}
```

调试该程序，断点打在count++，

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102540956-674625611.png)

首先可以看到调用栈有两个test，也就是两个线程，main和th1。

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102541632-127336604.png)

接着进入counter()的反汇编视图，open disassembly view:

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102542091-1642152223.png)

`call atomic_baseIiEppEi`就是这条CPU指令用来给count++，它是原子性的，保证了不会被其他CPU操作。

并且在step into中也能看到跳转到了运算符重载的头文件：

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102542597-894530707.png)

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102543149-630967364.png)

这就是atomic的实现机制

第二条`add  [rbp-0x4],0x1`就是i++对应的CPU指令，i就存在bp基址寄存器的前面四个字节的位置。我们step over几次让i的值有变化，看寄存器相对寻址的值：就是0x7

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102543731-1192801979.png)

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102544274-917426523.png)

第三条指令是CPU优化了for循环，本来应该先把i mov到寄存器，现在优化后直接比较i和19999的值，0x30d3f就是十进制的19999,也就是循环结束的条件。

如果给i加上volatile，就可以防止cpu优化

```cpp
....
volatile int i;
for(i=0;i<200000;i++)
    count++;
....
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230309102544909-1284024957.png)

##### 原子类型的操作

上面的count++例子中，step into 跳转到了atomic类型的运算符重载定义中，实际上所有能够对原子类型的操作，都是重载了普通的意思，或添加了新的函数。

所有的原子操作：atomic\<\>  a;

- 纵列 triv :针对std::atomic以及“其他普通类型之atomic”提供的操作

- 纵列 int type ：针对std::atomic<> 且使用整型类型而提供的操作；

- 纵列 ptr type ：针对std::atomic<> 且使用pointer类型 而提供的操作

| 操作                                 | triv  | int type | ptr type | 效果                                                                               |
| ---------------------------------- | ----- | -------- | -------- | -------------------------------------------------------------------------------- |
| atomic a = val                     | yes   | yes      | yes      | 以val为a的初值（这个不是atomic 的操作）                                                        |
| atomic a; atomic_init(&a,val)      | yes   | yes      | yes      | 同上 （若无后面的atomic_init(),则a的初始化不完整）                                                |
| a.is_lock_free()                   | yes   | yes      | yes      | 如果内部不使用lock则返回true 用来检测atomic类型内部是否由于使用lock才成为atomic。如果不是，则硬件本身就拥有对atomic操作的固有支持 |
| a.store(val)                       | yes   | yes      | yes      | 赋值 val （返回void）                                                                  |
| a.load()                           | yes   | yes      | yes      | 返回数值a的copy                                                                       |
| a.exchange(val)                    | yes   | yes      | yes      | 赋值val并返回旧值a的拷贝                                                                   |
| a.compare_exchange_strong(exp,des) | yes   | yes      | yes      | cas操作                                                                            |
| a.compare_exchange_weak(exp,des)   | yes   | yes      | yes      | weak cas操作                                                                       |
| a = val                            | yes   | yes      | yes      | 赋值并返回val的拷贝（copy）                                                                |
| a.operator atomic()                | yes   | yes      | yes      | 返回数值a的拷贝                                                                         |
|                                    |       |          |          |                                                                                  |
| a.fetch_sub(val)                   | no    | yes      | yes      | 不可切割值 a -= val 并返回新值得拷贝                                                          |
| a += val                           | no    | yes      | yes      | 等同于 t.fetch_add(val)                                                             |
| a -= val                           | no    | yes      | yes      | 等同于 t.fetch_sub(val)                                                             |
| ++a a++                            | no    | yes      | yes      | 等同于 t.fetch_add(1) 并返回 a 或者a+1的拷贝                                                |
| –a a–                              | no    | yes      | yes      | 等同于 t.fetch_sub(1) 并返回 a 或者a+1的拷贝                                                |
| a.fetch_and(val)                   | no    | yes      | no       | 不可切割值 a &= val 并返回新值得拷贝                                                          |
| a.fetch_or(val)                    | no    | yes      | no       | 不可切割值 a                                                                          |
| a.fetch_and(val)                   | no    | yes      | no       | 不可切割值 a ^= val 并返回新值得拷贝                                                          |
| a &= val                           | no    | yes      | no       | 等同于 t.fetch_and(val)                                                             |
| a                                  | = val | no       | yes      | no                                                                               |
| a                                  | = val | no       | yes      | no                                                                               |

atomic<>中的模板除了整型，还可以是其他如浮点型,指针，但是他们可能没有+,-,*,/等运算符的重载或位运算重载。

###### CAS操作

a.compare_exchange_strong/weak是CAS操作（compare and swap）,CPU提供这个操作用来比较“某内存的值”和“某给定的值”，当他们相同时，则把“该内存值”更新为”另一个给定的值“。如果不相同，则更新“某给定的值”为“某内存值”。

伪代码：

```cpp
bool compare_exchange_strong(T & expected ,T desired)
{
 if(this->load() == expected )
 {
     this->strore(desired)
     return true;
 }
 else
 {
    expected = this->load();
    return false;
}
}
```

this就是内存值的指针，expected是第一个给定的值，desired是另一个给定的值。

##### memory_order和内存模型

参考：[C++11 内存模型](https://www.cnblogs.com/haippy/p/3412858.html)。[知乎:C++ memory_order](https://zhuanlan.zhihu.com/p/515382936).[详解c++ atomic原子编程中的Memory Order](https://www.jb51.net/article/214304.htm).

C++11 中的原子类型的API大都需要提供一个std::memory_order(内存序，访存顺序)的枚举类型作为参数，如atomic_store, atomic_load, atomic_exchange, atomic_compare_exchange, atomic_flag, 以及还有test_and_set和clear等API都可以设置一个std::memory_order参数。在没有指定时，默认的参数是std::memory_order_seq_cst（顺序一致性）。

**研究内存序，首先要研究C++的内存模型。**

C++的内存模型一般可以分为静态内存模型和动态内存模型。静态内存模型主要涉及类的对象的在内存中是如何存放的，即从结构上来看一个对象在内存中的布局。和之前研究的内存对齐和排序（[C温故补缺(九):字节对齐与排序](https://www.cnblogs.com/Tenerome/p/Creview9.html)）类似。

而动态内存模型，可以理解为存储一致性模型。主要是从行为上来看多个线程对同一个对象同时操作时所做的约束。和我们做线程同步的意义相似的：都是为了程序执行的正确性，避免未知结果。

> `std::memory_order` specifies how memory accesses, including regular, non-atomic memory accesses, are to be ordered around an atomic operation. Absent any constraints on a multi-core system, when multiple threads simultaneously read and write to several variables, one thread can observe the values change in an order different from the order another thread wrote them. Indeed, the apparent order of changes can even differ among multiple reader threads. Some similar effects can occur even on uniprocessor systems due to compiler transformations allowed by the memory model.
> 
> from [cppreference](https://en.cppreference.com/w/cpp/atomic/memory_order)

在cppreference.com中的简单解释中也说了:多核系统在没有任何约束的条件下，在多个线程同时读取和写入多个变量时，因为执行顺序的不同可能导致不同的值。在没有规定时，多线程并发执行时，指令是可能被CPU重排的，所以就有可能出现不同的结果。比如：

> a,b两个共享变量，初始值都是0,通过两个改变值
> 
> | 线程 1    | 线程 2    |
> | ------- | ------- |
> | a = 1;  | b = 2;  |
> | R1 = b; | R2 = a; |

虽然对于每个线程每一步都是原子的，但是两个线程之前并没有规定先后顺序。就有可能出现6种情况。

| **情况 1**         | **情况 2**         | **情况 3**         | **情况 4**         | **情况 5**         | **情况 6**         |
| ---------------- | ---------------- | ---------------- | ---------------- | ---------------- | ---------------- |
| a = 1;           | b = 2;           | a = 1;           | a = 1;           | b = 2;           | b = 2;           |
| R1 = b;          | R2 = a;          | b = 2;           | b = 2;           | a = 1;           | a = 1;           |
| b = 2;           | a = 1;           | R1 = b;          | R2 = a;          | R1 = b;          | R2 = b;          |
| R2 = a;          | R1 = b;          | R2 = a;          | R1 = b;          | R2 = a;          | R1 = b;          |
| R1 == 0, R2 == 1 | R1 == 2, R2 == 0 | R1 == 2, R2 == 1 | R1 == 2, R2 == 1 | R1 == 2, R2 == 1 | R1 == 2, R2 == 1 |

 

常见的存储一致性模型包括：顺序一致性模型、处理器一致性模型、弱一致性模型、释放一致性模型、急切更新一致性模型、懒惰更新释放一致性模型、域一致性模型以及单项一致性模型。

因为C++中只有一下6种，所以只研究这几种访存次序。

 

| memory order         | 作用                             |
| -------------------- | ------------------------------ |
| memory_order_relaxed | 无fencing 作用，cpu和编译器可以重排指令      |
| memory_order_consume | 后面依赖此原子变量的访存指令勿重排至此条指令前        |
| memory_order_acquire | 后面的访存指令勿重排至此指令前                |
| memory_order_release | 前面的访存指令勿重排到此指令后                |
| memory_order_acq_rel | acquire+release                |
| memory_order_seq_cst | acq_rel+所有使用seq_cst的指令有严格的全序关系 |

多线程编程时，通过这些标志位，来读写原子变量，可以组合成4种同步模型：

###### Relaxed ordering

在这种模型下，std::atomic的load和store都要带上memory_order_relaxed参数，Relaxed ordering仅仅保证load和store是原子的，除此之外无任何跨线程同步。

###### Release_Acquire ordering

这个模型下，store()使用memory_order_release,而load()使用memory_order_acquire。这个模型限制指令的重排：

- 在store()之前的读写操作，不允许重排到store()的后面。一般对应写操作

- 在load()之后的读写操作，不允许重排到load()前面，一般对应读操作

<mark>也就是store总是排在load前面，保证不会读到修改前的数据。</mark>

如一个打印机有两个模块，一个负责装载打印数据，一个用来打印。如果未装载新的数据，会直接打印上一次的信息：

如果没有规定线程之间的执行顺序，则可能会读到上一此的信息：

```cpp
#include<iostream>
#include<thread>
#include<atomic>
using namespace std;

string printstr="old data";//上一此的信息
void load(string str){//装载
    printstr=str;
}
void print(){//打印
    cout<<printstr<<endl;
}
int main(){
    thread th1(load,"Hello");
    thread th2(print);
    th1.join();
    th2.join();
}
```

因为程序会被cpu优化，所以手动编译取消优化-O0

`g++ test.cpp -O0 -o test;./test`

每次的运行都是随机排序的，所以可能会出现old data

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223013490-870198732.png)

使用Release_acquire模型来规定线程间的执行顺序：

```cpp
#include<iostream>
#include<thread>
#include<atomic>
using namespace std;

atomic<bool> ready{false};
string printstr="old data";//上一此的信息
void load(string str){//装载
    printstr=str;
    ready.store(true,memory_order_release);
}
void print(){//打印
    while(!ready.load(memory_order_acquire))
        ;//循环等待
    cout<<printstr<<endl;
}
int main(){
    thread th1(load,"Hello");
    thread th2(print);
    th1.join();
    th2.join();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223013983-214445830.png)就得到了准确的结果

###### Release_Consume ordering

这个模型下 store()使用memory_order_release,而load()使用memory_order_consume。

- 在store前的所有读写，不允许被移动到store()后面

- 在load之后所有依赖此原子变量的读写，不允许被移动到load前面。

和上面Release-acquire模型的差别是load前可以出现不依赖该原子变量的读写

#### future

\<future\>头文件包括一下类和函数：

- providers类：std::promise, std::package_task

- futures类：std::future, std::shared_future

- providers函数：std::async()

- 其他类型： std::future_error, std::future_errc, std::future_status, std::launch

##### std::promise

promise对象可以保存某一类型T的值，该值可以被future对象读取（可能在另一个线程中），因此promise也提供了一种线程同步手段。在promise对象构造时可以和一个共享状态(通常是std::future)相关联，并可以在相关联的共享状态(std::future)上保存一个类型为T的值。

格式:`std::promise<Class T> val;`

val的值只能用promise的set_value()函数设置，且每个promise只能设置一次，promise对象没有获取这个值的接口，可以将promise对象和future对象关联，通过future对象访问共享值。`std::future<Class T> fval=val.get_future();`

如:

```cpp
#include<iostream>
#include<future>

int main(){
  std::promise<int> val;
  val.set_value(10086);
  std::future<int> fval=val.get_future();
  std::cout<<fval.get();
}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223014777-2022677814.png)

std::promise被禁用了拷贝构造函数，但允许使用构造函数。另外，std::promise的operator=是没有拷贝语义的，只有move语义。所以只能连接一个promise对象。

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223015474-1395809582.png)

可以使用move：

```cpp
#include<iostream>
#include<future>

int main(){
  std::promise<int> val;
  val.set_value(10086);
  std::promise<int> val1=move(val);
  std::future<int> fval=val1.get_future();
  std::cout<<fval.get();
}
```

但是一个promise对象只能set_value一次，如果对已经set_value过的promise对象再次set_value，虽然编译能通过，但会报std::future_error异常：

```cpp
#include<iostream>
#include<future>

int main(){
  std::promise<int> val;
  val.set_value(10086);
  val.set_value(10087);
}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223016242-1628087802.png)

这里还有set的机制，是用atomic变量的store,并使用了memory_order_release内存序。

想要改变promise对象保存的值，可以调用移动构造函数，给promise对象一个空的promise:`val=std::promise<int>();`,接着就可以重新set_value

```cpp
#include<iostream>
#include<future>

int main(){
  std::promise<int> val;
  val.set_value(10086);
  val=std::promise<int>();
  val.set_value(10087);
  std::future<int> fval=val.get_future();
  std::cout<<fval.get();
}
```

同时,一个promise对象也只能被一个future关联，不能改动。否则报future_errec:future_already_retrieved

```cpp
#include<iostream>
#include<future>

int main(){
  std::promise<int> val;
  val.set_value(328);
  std::future<int> fval=val.get_future();
  std::future<int> fval1=val.get_future();

}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223016802-1512910261.png)

但是，future对象是可以修改绑定的promise的：

```cpp
#include<iostream>
#include<future>

int main(){
  std::promise<int> val;
  val.set_value(328);
  std::promise<int> val1;
  val1.set_value(329);
  std::future<int> fval=val.get_future();
  fval=val1.get_future();
  std::cout<<fval.get();

}
```

![](https://img2023.cnblogs.com/blog/2629720/202303/2629720-20230320223017491-1106992181.png)

###### std::promise\:\:set_exception

========sep===

#### condition_variable

### STL库
