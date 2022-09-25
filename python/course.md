### course

#### 模块管理

##### 内置模块

```python
import math
dir(math)
```

```
['__doc__',
 '__loader__',
 '__name__',
 '__package__',
 '__spec__',
 'acos',
 'acosh',
 'asin',
 'asinh',
 'atan',
 'atan2',
 'atanh',
 'ceil',
 'comb',
 'copysign',
 'cos',
 'cosh',
 'degrees',
 'dist',
 'e',
 'erf',
 'erfc',
 'exp',
 'expm1',
 'fabs',
 'factorial',
 'floor',
 'fmod',
 'frexp',
 'fsum',
 'gamma',
 'gcd',
 'hypot',
 'inf'
```

```python
print(math.e)
```

```
2.718281828459045
```

```python
#用type()查看类型
print(type(math.e))
```

```
<class 'float'>
```

```python
#使用help()查看帮助文档
help(math)
```

```
Help on built-in module math:

NAME
    math

DESCRIPTION
    This module provides access to the mathematical functions
    defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.

        The result is between 0 and pi.

    acosh(x, /)
        Return the inverse hyperbolic cosine of x.

    asin(x, /)
        Return the arc sine (measured in radians) of x.

        The result is between -pi/2 and pi/2.

    asinh(x, /)
        Return the inverse hyperbolic sine of x.

    atan(x, /)
        Return the arc tangent (measured in radians) of x.

        The result is between -pi/2 and pi/2.

    atan2(y, x, /)
        Return the arc tangent (measured in radians) of y/x.

        Unlike atan(y/x), the signs of both x and y are considered.

    atanh(x, /)
        Return the inverse hyperbolic tangent of x.

    ceil(x, /)
        Return the ceiling of x as an Integral.

        This is the smallest integer >= x.

    comb(n, k, /)
        Number of ways to choose k items from n items without repetition and without order.

        Evaluates to n! / (k! * (n - k)!) when k <= n and evaluates
        to zero when k > n.

        Also called the binomial coefficient because it is equivalent
        to the coefficient of k-th term in polynomial expansion of the
        expression (1 + x)**n.

        Raises TypeError if either of the arguments are not integers.
        Raises ValueError if either of the arguments are negative.

    copysign(x, y, /)
        Return a float with the magnitude (absolute value) of x but the sign of y.

        On platforms that support signed zeros, copysign(1.0, -0.0)
        returns -1.0.

    cos(x, /)
        Return the cosine of x (measured in radians).

    cosh(x, /)
        Return the hyperbolic cosine of x.

    degrees(x, /)
        Convert angle x from radians to degrees.

    dist(p, q, /)
        Return the Euclidean distance between two points p and q.

        The points should be specified as sequences (or iterables) of
        coordinates.  Both inputs must have the same dimension.

        Roughly equivalent to:
            sqrt(sum((px - qx) ** 2.0 for px, qx in zip(p, q)))

    erf(x, /)
        Error function at x.

    erfc(x, /)
        Complementary error function at x.

    exp(x, /)
        Return e raised to the power of x.

    expm1(x, /)
        Return exp(x)-1.

        This function avoids the loss of precision involved in the direct evaluation of exp(x)-1 for small x.

    fabs(x, /)
        Return the absolute value of the float x.

    factorial(x, /)
        Find x!.

        Raise a ValueError if x is negative or non-integral.

    floor(x, /)
        Return the floor of x as an Integral.

        This is the largest integer <= x.

    fmod(x, y, /)
        Return fmod(x, y), according to platform C.

        x % y may differ.

    frexp(x, /)
        Return the mantissa and exponent of x, as pair (m, e).

        m is a float and e is an int, such that x = m * 2.**e.
        If x is 0, m and e are both 0.  Else 0.5 <= abs(m) < 1.0.

    fsum(seq, /)
        Return an accurate floating point sum of values in the iterable seq.

        Assumes IEEE-754 floating point arithmetic.

    gamma(x, /)
        Gamma function at x.

    gcd(*integers)
        Greatest Common Divisor.

    hypot(...)
        hypot(*coordinates) -> value

        Multidimensional Euclidean distance from the origin to a point.

        Roughly equivalent to:
            sqrt(sum(x**2 for x in coordinates))

        For a two dimensional point (x, y), gives the hypotenuse
        using the Pythagorean theorem:  sqrt(x*x + y*y).

        For example, the hypotenuse of a 3/4/5 right triangle is:

            >>> hypot(3.0, 4.0)
            5.0

    isclose(a, b, *, rel_tol=1e-09, abs_tol=0.0)
        Determine whether two floating point numbers are close in value.

          rel_tol
            maximum difference for being considered "close", relative to the
            magnitude of the input values
          abs_tol
            maximum difference for being considered "close", regardless of the
            magnitude of the input values

        Return True if a is close in value to b, and False otherwise.

        For the values to be considered close, the difference between them
        must be smaller than at least one of the tolerances.

        -inf, inf and NaN behave similarly to the IEEE 754 Standard.  That
        is, NaN is not close to anything, even itself.  inf and -inf are
        only close to themselves.

    isfinite(x, /)
        Return True if x is neither an infinity nor a NaN, and False otherwise.

    isinf(x, /)
        Return True if x is a positive or negative infinity, and False otherwise.

    isnan(x, /)
        Return True if x is a NaN (not a number), and False otherwise.

    isqrt(n, /)
        Return the integer part of the square root of the input.

    lcm(*integers)
        Least Common Multiple.

    ldexp(x, i, /)
        Return x * (2**i).

        This is essentially the inverse of frexp().

    lgamma(x, /)
        Natural logarithm of absolute value of Gamma function at x.

    log(...)
        log(x, [base=math.e])
        Return the logarithm of x to the given base.

        If the base not specified, returns the natural logarithm (base e) of x.

    log10(x, /)
        Return the base 10 logarithm of x.

    log1p(x, /)
        Return the natural logarithm of 1+x (base e).

        The result is computed in a way which is accurate for x near zero.

    log2(x, /)
        Return the base 2 logarithm of x.

    modf(x, /)
        Return the fractional and integer parts of x.

        Both results carry the sign of x and are floats.

    nextafter(x, y, /)
        Return the next floating-point value after x towards y.

    perm(n, k=None, /)
        Number of ways to choose k items from n items without repetition and with order.

        Evaluates to n! / (n - k)! when k <= n and evaluates
        to zero when k > n.

        If k is not specified or is None, then k defaults to n
        and the function returns n!.

        Raises TypeError if either of the arguments are not integers.
        Raises ValueError if either of the arguments are negative.

    pow(x, y, /)
        Return x**y (x to the power of y).

    prod(iterable, /, *, start=1)
        Calculate the product of all the elements in the input iterable.

        The default start value for the product is 1.

        When the iterable is empty, return the start value.  This function is
        intended specifically for use with numeric values and may reject
        non-numeric types.

    radians(x, /)
        Convert angle x from degrees to radians.

    remainder(x, y, /)
        Difference between x and the closest integer multiple of y.

        Return x - n*y where n*y is the closest integer multiple of y.
        In the case where x is exactly halfway between two multiples of
        y, the nearest even value of n is used. The result is always exact.

    sin(x, /)
        Return the sine of x (measured in radians).

    sinh(x, /)
        Return the hyperbolic sine of x.

    sqrt(x, /)
        Return the square root of x.

    tan(x, /)
        Return the tangent of x (measured in radians).

    tanh(x, /)
        Return the hyperbolic tangent of x.

    trunc(x, /)
        Truncates the Real x to the nearest Integral toward 0.

        Uses the __trunc__ magic method.

    ulp(x, /)
        Return the value of the least significant bit of the float x.

DATA
    e = 2.718281828459045
    inf = inf
    nan = nan
    pi = 3.141592653589793
    tau = 6.283185307179586

FILE
    (built-in)
```

```python
#也可以查看函数
help(math.pow)
```

```
Help on built-in function pow in module math:

pow(x, y, /)
    Return x**y (x to the power of y).
```

```python
math.pow(2,5)
```

```
32.0
```

```python
help(math.floor)
```

```
Help on built-in function floor in module math:

floor(x, /)
    Return the floor of x as an Integral.

    This is the largest integer <= x.
```

```python
math.floor(5.9)
```

```
5
```

##### 自定义模块

###### 导入其他文件

```python
#fun.py
def shout():
    print("hello")
shout()
```

在另一个py文件中定义函数,导入文件可以调用另一个文件的函数

```python
#test.py
import fun
fun.shout()
```

输出的结果是:
hello
hello
因为导入的时候会先执行一遍,为了避免fun中主函数的执行,可以添加判断条件

```python
if __name__=='_main_':
    shout()
```

函数执行时有个参数__name__,指代函数名,在本身里面它的值是__main__,其他文件调用时不是,用这个来区分.

另外一种导入方法:直接导入库函数,调用的时候不需文件名.库函数,可以直接用函数名

```python
from fun import shout
shout()
```

```
hello
```

还可以给导入库函数命名,然后用新命名调用

```python
from fun import shout as f
f()
```

```
hello
```

还可以用*导入,调用时也时直接用函数名

```python
from fun import *
shout()
```

```
hello
```

###### 包的概念

python中的包,就是一个文件夹,但是需要一个__init__.py文件来标志成包,且需要将包放在sys.path路径中

```python
import sys
sys.path
```

```
['c:\\Users\\Tenerome\\Desktop\\python',
 'c:\\environment\\python\\python39.zip',
 'c:\\environment\\python\\DLLs',
 'c:\\environment\\python\\lib',
 'c:\\environment\\python',
 '',
 'C:\\Users\\Tenerome\\AppData\\Roaming\\Python\\Python39\\site-packages',
 'C:\\Users\\Tenerome\\AppData\\Roaming\\Python\\Python39\\site-packages\\win32',
 'C:\\Users\\Tenerome\\AppData\\Roaming\\Python\\Python39\\site-packages\\win32\\lib',
 'C:\\Users\\Tenerome\\AppData\\Roaming\\Python\\Python39\\site-packages\\Pythonwin',
 'c:\\environment\\python\\lib\\site-packages']
```

sys.path路径就是拥有__pycache__文件夹的路径

```python
#导入调用
from bao import fun
fun.shout()
```

```
Moximoxi
```

#### 快速入门

![](course/2022-09-17-17-23-02-image.png)

##### 1.Python标识符

在 Python 里，标识符有字母、数字、下划线组成。

在 Python 中，所有标识符可以包括英文、数字以及下划线(_)，但不能以数字开头。

Python 中的标识符是区分大小写的。

以下划线开头的标识符是有特殊意义的。以单下划线开头 _foo 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 from xxx import * 而导入；

以双下划线开头的 foo 代表类的私有成员；以双下划线开头和结尾的 foo 代表 Python 里特殊方法专用的标识，如 init__() 代表类的构造函数。

##### 2.Python有五个标准的数据类型

Numbers（数字）  
String（字符串）  
List（列表）  
Tuple（元组）  
Dictionary（字典）  

Python支持四种不同的数字类型：

int（有符号整型）  
long（长整型[也可以代表八进制和十六进制]）  
float（浮点型）  
complex（复数）  

python的字串列表有2种取值顺序:

从左到右索引默认0开始的，最大范围是字符串长度少1  
从右到左索引默认-1开始的，最大范围是字符串开头  

List（列表） 是 Python 中使用最频繁的数据类型。

列表可以完成大多数集合类的数据结构实现。它支持字符，数字，字符串甚至可以包含列表（即嵌套）。  

列表用 [ ] 标识，是 python 最通用的复合数据类型。  

列表中值的切割也可以用到变量 [头下标:尾下标] ，就可以截取相应的列表，从左到右索引默认 0 开始，从右到左索引默认 -1 开始，下标可以为空表示取到头或尾。  

加号 + 是列表连接运算符，星号 * 是重复操作。  

元组是另一个数据类型，类似于List（列表）

。

元组用”()”标识。内部元素用逗号隔开。但是元组不能二次赋值，相当于只读列表。  

字典(dictionary)是除列表以外python之中最灵活的内置数据结构类型。

列表是有序的对象结合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。  

字典用”{ }”标识。字典由索引(key)和它对应的值value组成。

##### 3.Python数据类型转换

有时候，我们需要对数据内置的类型进行转换，数据类型的转换，你只需要将数据类型作为函数名即可。

以下几个内置的函数可以执行数据类型之间的转换。这些函数返回一个新的对象，表示转换的值。

int(x [,base]): 将x转换为一个整数

long(x [,base] ): 将x转换为一个长整数

float(x): 将x转换到一个浮点数

complex(real [,imag]): 创建一个复数

str(x):将对象 x 转换为字符串

repr(x): 将对象 x 转换为表达式字符串

eval(str): 用来计算在字符串中的有效Python表达式,并返回一个对象

tuple(s): 将序列 s 转换为一个元组

list(s): 将序列 s 转换为一个列表

set(s): 转换为可变集合

dict(d): 创建一个字典。d 必须是一个序列 (key,value)元组。

frozenset(s): 转换为不可变集合

chr(x) :将一个整数转换为一个字符

unichr(x): 将一个整数转换为Unicode字符

ord(x): 将一个字符转换为它的整数值

hex(x): 将一个整数转换为一个十六进制字符串

oct(x): 将一个整数转换为一个八进制字符串

##### 4.Python 运算符

算术运算符  
比较（关系）运算符  
赋值运算符  
逻辑运算符  
位运算符  
成员运算符  
身份运算符  
运算符优先级  

#### 序列

##### 列表

列表,类似某些语言的Arraylist,但不是数组.用[]表示

定义列表

```python
x=[1,2,3,4,5]
x2=list(range(1,9))
print(x)
print(x2)
```

```
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 6, 7, 8]
```

output:
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 6, 7, 8]

列表可以像数组一样按下标取值,自左向右从0开始,逆序从-1开始

```python
print(x[2])
print(x2[-3])
```

output:
3
6

列表支持切片操作,[a:b],取x,a≤x＜b

```python
x[1:4]
```

output:
[2, 3, 4]

列表元素可以是不同类型,还可以嵌套子列表

```python
x3=[1,'a',True,[1,2,3]]
x3[3]
```

output:[1, 2, 3]

访问子列表的元素

```python
x3[3][1]
```

output:2

追加列表的几种方式

```python
a=[1,2,3]+[4,5]
print(a)
a.append(6)
print(a)
a.extend([100,200])
print(a)
```

output:[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 6]
[1, 2, 3, 4, 5, 6, 100, 200]

插入列表:可以按下表插入,也可以逆序

```python
a.insert(0,'c')
print(a)
a.insert(-2,'mc')
print(a)
```

output:
['c', 1, 2, 3, 4, 5, 6, 100, 200]
['c', 1, 2, 3, 4, 5, 6, 'mc', 100, 200]

列表可以直接修改某个元素,按下标

```python
a[0]=300
print(a)
```

output:[300, 1, 2, 3, 4, 5, 6, 'mc', 100, 200]

如果想切片修改,比如把a0,a1修改成4,不能直接赋值4,会报错:can only assign an iterable,只能分配一个迭代器.所以要用列表赋值

```python
# a[0:2]=4  会报错
a[0:2]=[4]
print(a)
```

output: [4, 2, 3, 4, 5, 6, 'mc', 100, 200]

删除操作
del :支持删除指定下标元素,支持切片,删除是真正删除了这个元素

```python
a1=[1,2,3,4,'a','c']
del a1[2]
print(a1)
del a1[0:2]
print(a1)
```

output: [1, 2, 4, 'a', 'c']
[4, 'a', 'c']

pop():出栈,没有参数时,默认出栈栈顶元素,可以加参数指定位置,但不支持切片.相比于del,它有返回值,出栈时返回出栈元素

```python
a2=[1,2,3,4,5,6,7]
a2.pop()
print(a2)
b=a2.pop(0)
print(b,a2)
```

output:[1, 2, 3, 4, 5, 6]
1 [2, 3, 4, 5, 6]

列表支持*操作,重复元素

```python
a2=a2 * 3
print(a2)
```

output: [2, 3, 4, 5, 6, 2, 3, 4, 5, 6, 2, 3, 4, 5, 6]

按值删除,remove(value)函数,参数value会在列表中查找等于value的第一个值,并删除之

```python
a2.remove(3)
print(a2)
```

output:[2, 4, 5, 6, 2, 3, 4, 5, 6, 2, 3, 4, 5, 6]

清空列表:clear()

```python
a2.clear()
print(a2)
```

output: []

列表排序

```python
x=[2,5,3,100,45,77]
sorted(x)
```

output: [2, 3, 5, 45, 77, 100]

sorted()只是排序一下并输出,列表x本身次序并未改变,可以用列表排序函数

```python
x.sort()
print(x)
```

output: [2, 3, 5, 45, 77, 100]

列表推导式/列表解析式

①x=[1,2,3,4,5,6,7,8,9,10],求每个元素平方后输出

```python
#如果使用for循环<br>
x=[1,2,3,4,5,6,7,8,9,10]
for i in x: 
    print(i**2)
```

使用列表推导式

```python
[i ** 2 for i in x]
```

output: [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

还可以继续添加条件,循环嵌套

```python
[i ** 2 for i in x if i%2 ==0]
[(i,j) for i in range(2) for j in range(3)]
```

output: [4, 16, 36, 64, 100]
[(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2)]

②求两个列表对应位置元素的和,x从1到100,y为100个1

```python
#不用列表推导式
x=range(1,101)
y=[1]*100
z=list()
for i in range(100):
    z.append(x[i]+y[i])
print(z)
```

列表推导式

```python
[x[i] + y[i] for i in range(100)]
#或者
print([i+j for i,j in zip(x,y)],end=" ")
```

output: [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17,  
18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,  
34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50,  
51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66,  
67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83,  
84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101]

class zip(object)
 | zip(*iterables) --> A zip object yielding tuples until an input is exhausted.

| >>> list(zip('abcdefg', range(3), range(4)))
 | [('a', 0, 0), ('b', 1, 1), ('c', 2, 2)]
 | The zip object yields n-length tuples, where n is the number of iterables passed as positional arguments to zip(). The i-th element in every tuple comes from the i-th iterable argument to zip(). This continues until the shortest argument is exhausted.

使用向量表达式

```python
import numpy as np
x=np.array(x)
y=np.array(y)
z=x+y
print(z)
```

使用映射map()

```python
list(map(lambda x:x[0]+x[1],zip(x,y)))
```

##### 元组tuple

元组是不可变类型,比支持删除和添加操作

元组用()表示,可以用来作为函数多返回值类型

```python
def f():
    a=1
    b=2
    return a, b
x,y=f()
print(x,y)
```

```
1 2
```

查看返回值类型

```python
t=f()
print(type(t))
```

```
<class 'tuple'>
```

python 支持同时多赋值

```python
x,y,z=1,2,3
```

也可以使用元组

```python
x,y,z=(1,2,3)
```

如果元组中只有一个元素,要用','标志

```python
x=(1)
print(type(x))
x=(1,)
print(type(x))
```

```
<class 'int'>
<class 'tuple'>
```

元组也支持按下标取值还有切片

```python
x=(1,2,3,4,5)
print(x[1])
print(x[0:2])
```

```
2
(1, 2)
```

##### 集合set

用{}表示,不支持按下标取值,不支持切片

集合最大的特点:集合中的元素不能重复,类似数学中的集合的概念,也有交集,并集等性质

```python
x={1,2,2,3,4,4,5,5,5,6}
print(x)
```

```
{1, 2, 3, 4, 5, 6}
```

所以可以利用集合去重其他类型

```python
l=[1,2,3,4,4,4,5,5,6,6]
s=set(l)
print(s)
```

```
{1, 2, 3, 4, 5, 6}
```

交集

```python
a={1,2,3,4}
b={3,4,5}
a & b
```

```
{3, 4}
```

并集

```python
a | b
```

```
{1, 2, 3, 4, 5}
```

异或

```python
a ^ b
```

```
{1, 2, 5}
```

##### 字典dict

字典也用{}表示,区别于集合,它在初始化时,用键值对表示

```python
dic={'a':100,'b':200,'c':300}
```

添加update,添加的键值对用{}

```python
dic.update({'d':400})
print(dic)
```

```
{'a': 100, 'b': 200, 'c': 300, 'd': 400}
```

python中的字典类似与其他语言的hash表,按键取值

```python
dic['d']
```

```
400
```

如果无对应键,会报异常

```python
dic['e']
```

```
---------------------------------------------------------------------------

KeyError                                  Traceback (most recent call last)

c:\Users\Tenerome\Desktop\python\lesson.ipynb Cell 35 in <cell line: 1>()
----> <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y220sZmlsZQ%3D%3D?line=0'>1</a> dic['e']


KeyError: 'e'
```

可以用get()方法try to get value

```python
dic.get('e','none')
```

```
'none'
```

get()有两个参数,第一个参数为键,若字典有对应键,返回键值.若无对用键,返回第二个参数

遍历

```python
for i in dic:
    print(i,end=" ")
```

```
a b c d 
```

直接对dic遍历返回的是键(还可以用dic.keys()),遍历键值,使用dic.values()

```python
for i in dic.values():
    print(i,end=" ")
```

```
100 200 300 400 
```

输出键值对

```python
print(dic)
print(dic.items())
```

```
{'a': 100, 'b': 200, 'c': 300, 'd': 400}
dict_items([('a', 100), ('b', 200), ('c', 300), ('d', 400)])
```

区别:dic是字符串,dic.items()是元组

```python
for i in dic:
    print(type(i),end=" ")
print()
for i in dic.items():
    print(type(i),end=" ")
```

```
<class 'str'> <class 'str'> <class 'str'> <class 'str'> 
<class 'tuple'> <class 'tuple'> <class 'tuple'> <class 'tuple'> 
```

字典的键必须是不可变类型:数字(numbers),字符串(string),元组(tuple)

```python
dic1={(1,2):'苹果','a':'橘子',3:'香蕉'}
print(dic1)
```

```
{(1, 2): '苹果', 'a': '橘子', 3: '香蕉'}
```

字典的键不能重复,其他语言中hash键重复会报异常,python虽然不报异常,但重复的键会覆盖之前的键

```python
dic2={'a':100,'b':200,'a':300}
print(dic2)
```

```
{'a': 300, 'b': 200}
```

#### 程序流程控制

选择结构

①编写程序,判断某个日期是该年的第几天

```python
import time
def demo(year,month,day):
    day_month=[31,28,30,31,30,31,31,30,31,30,31]#十二个月的天数
    pass#pass关键字用来做占位符,表示待实现
print((demo(2021,1,15)))
print(demo(2021,3,26))
```

```python
import time
def demo(year,month,day):
    day_month=[31,28,30,31,30,31,31,30,31,30,31]
    if year % 400 ==0 or (year %4==0 and year%100!=0):
        day_month[1]=29
    # if month==1:
    #     return day
    # else:
    return sum(day_month[:month-1],day)
```

```python
print(demo(2021,3,26))
```

```
85
```

获取现在的时间,并调用demo()

```python
date=time.localtime()
print(type(date))
print(date)
print(date[:3])
```

```
<class 'time.struct_time'>
time.struct_time(tm_year=2022, tm_mon=9, tm_mday=22, tm_hour=14, tm_min=45, tm_sec=39, tm_wday=3, tm_yday=265, tm_isdst=0)
(2022, 9, 22)
```

time.localtime()获取当前的时间,返回值为一个struct

struct切片后返回的是一个元组

第一种调用方法:赋值给三个变量

```python
year,month,day=date[:3]
demo(year,month,day)
```

```
264
```

第二种:使用序列解包方式传参

```python
demo(*date[:3])
```

```
264
```

year % 100 !=0 可以简写为year % 100.因为在python条件判断时,只要表达式不为0,False,None,空(序列)时判断结果都是True

三元表达式

```python
w=100
h=1 if w>=100 else 2
print(h)
```

```
1
```

python中没有Switch结构,C语言中的Switch其实使用hash表实现跳转的,在python中可以用字典代替

```python
def func1():
    pass
def func2():
    pass
def func3():
    pass
d={'key1':func1(),'key2':func2(),'key3':fun3()}
```

##### 循环结构

编写程序,打印100以内的所有素数

仿C结构

```python
for i in range(2,101):
    flag=True
    for j in range(2,int(i**0.5)+1):
        if i%j ==0:
            flag=False
            break
    if flag:
        print(i,end=" ")
```

```
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97 
```

python提供了for...else结构.若内循环正常结束(而不是遇到break跳出)或没有执行for循环,则执行else语句.如果是由break语句跳出的,则不执行else语句

用for...esle结构

```python
for i in range(2,101):
    for j in range(2,int(i**0.5)+1):
        if i%j ==0:
            break
    else:
        print(i,end=" ")
```

```
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97 
```

使用列表推导式

```python
print([i for i in range(2,101) if 0 not in [i%j for j in range(2,int(i**0.5)+1)]])
```

```
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
```

##### 异常处理

③创建txt文本文件,内容三行文字

```python
f=open('2.txt',encoding='utf-8')
```

```
---------------------------------------------------------------------------

FileNotFoundError                         Traceback (most recent call last)

c:\Users\Tenerome\Desktop\python\lesson.ipynb Cell 31 in <cell line: 1>()
----> <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#X42sZmlsZQ%3D%3D?line=0'>1</a> f=open('2.txt',encoding='utf-8')


FileNotFoundError: [Errno 2] No such file or directory: '2.txt'
```

如果没有创建,就会报出异常

对可能产生异常的程序,可以用try...except Exception...else...finally

```python
try:
    f=open('test.txt',encoding='utf-8')
except Exception:
    print('文件不存在')
else:
    print(f.read())
finally:
    f.close()
```

```
Hi
Hello
CCVV
```

try:尝试运行后面的程序
如果有异常,except Exception捕获,并做个性化处理
若无异常,esle
不管有没有异常,finally

④断言语句assert,用户输入一个数字,判断是否在20-120之间,否则产生异常,并提示用户重新输入

```python
while True:
    x=int(input('请输入一个在20-120之间的数字'))
    try:
        assert x>=20 and x<=120
    except AssertionError:
        print('输入数字不合法')
    else:
        print('OK')
        break
```

```
输入数字不合法
输入数字不合法
OK
```

#### 函数与函数式编程

##### 函数的定义与调用

返回斐波那契数列中小于整数n的所有值

```python
def fib(n):
    pass
fib(1000)
```

python中的函数,用def关键字定义.函数不需要返回值类型,不需要参数类型

##### 函数的参数

函数参数的集中类型:  
位置参数(positional arguments):形参和实参数量相同,位置一致.  
缺省参数(default arguments):形参有默认值,有缺省参数的形参要在位置参数之后.  
关键字参数(keyword arguments):实参顺序可以和形参顺序不一致,避免了用户需要牢记位置参数顺序的麻烦  
可变参数(variable-length arguments):*parameter用来接受多个实参并将其放在元组中.**parameter接收多个关键参数并存放到字典中

位置参数:

```python
def func(a,b,c):
    print(a,b,c)
func(1,2)
```

```
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

c:\Users\Tenerome\Desktop\python\lesson.ipynb Cell 45 in <cell line: 3>()
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#X63sZmlsZQ%3D%3D?line=0'>1</a> def func(a,b,c):
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#X63sZmlsZQ%3D%3D?line=1'>2</a>     print(a,b,c)
----> <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#X63sZmlsZQ%3D%3D?line=2'>3</a> func(1,2)


TypeError: func() missing 1 required positional argument: 'c'
```

这个就是positional 参数,缺少时报错

缺省参数:

```python
def func1(a,b,c=1):
    print(a,b,c)
func1(2,3)
```

```
2 3 1
```

定义函数时就对形参赋值,就是缺省参数,后面传实参会覆盖

关键字参数:

```python
def func2(a,b,c):
    print(a,b,c)
func2(c=3,a=1,b=2)
```

```
1 2 3
```

可以看到调用的时候没有按形参顺序来,但是用关键字(形参名)来调用的,就可以忽略顺序

```python
def stu(country='中国',name):
    print("%s,%s" %(name,country))
stu('美国','Tom')
```

```
  Input In [7]
    def stu(country='中国',name):
                             ^
SyntaxError: non-default argument follows default argument
```

有缺省值的参数必须放位置参数后面

```python
def stu(name,country='中国'):
    print("%s ,%s" %(name,country))
stu('美国','Tom')
```

```
美国 ,Tom
```

可变参数:

##### 变量的作用域

函数体外部的变量:全局变量  
内部:局部变量

函数内可以调用全局变量

```python
x=100
def f():
    print(x)
f()
```

```
100
```

在函数内部的变量赋值操作,该变量就是局部变量.

```python
x=100
def f():
    print(x)
    x=200
    print(x)
f()
```

```
---------------------------------------------------------------------------

UnboundLocalError                         Traceback (most recent call last)

c:\Users\Tenerome\Desktop\python\lesson.ipynb Cell 63 in <cell line: 6>()
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=3'>4</a>     x=200
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=4'>5</a>     print(x)
----> <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=5'>6</a> f()


c:\Users\Tenerome\Desktop\python\lesson.ipynb Cell 63 in f()
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=1'>2</a> def f():
----> <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=2'>3</a>     print(x)
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=3'>4</a>     x=200
      <a href='vscode-notebook-cell:/c%3A/Users/Tenerome/Desktop/python/lesson.ipynb#Y116sZmlsZQ%3D%3D?line=4'>5</a>     print(x)


UnboundLocalError: local variable 'x' referenced before assignment
```

也就是说,在函数内,一旦引用了全局变量,就不能在函数内对全局变量赋值

但是可以先赋值再引用,这时两个x并不是同一个,相当于两个变量,一个全局,一个局部,但是有相同的变量名

```python
x=100
def f():
    x=200
    print(id(x))
f()
id(x)
```

```
2413391733392
2413391730128
```

想要在函数内真正调用全局变量,可以用global声明

```python
x=100
def f():
    global x
    x=200
    print(id(x))
f()
id(x)
```

```
2413391733392
2413391733392
```

python支持使用nonlocal关键字定义一宗介于全局和局部之间的变量,成为闭包作用域变量.关键字nonlocal声明的变量会引用距离最近的非全局作用域的变量(闭包变量或局部变量).要求声明的变量已经存在.关键字nonlocal不会创建新变量

##### lambda表达式

```python
def fsum(x,y):
    return x+y
```

像上面的函数,只是很简单的功能,就定义了函数.lambda表达式就是用来代替简单的函数的

基本结构lambda left : right.其中left是参数,right是返回值.

```python
f=lambda x,y : x+y
f(3,5)
```

```
8
```

lambda表达式就是把简单的函数改成无函数体的形式,只有参数和返回值.返回值用表达式的形式.只要能改成这样的结构的函数,都可以写成lambda表达式的形式

##### 函数式编程

函数式编程就是把函数作用于一个或多个序列,来实现一些功能

① 内置函数map()可以将一个函数作用到一个或多个序列或迭代器对象上,返回可迭代的map对象

![](course/fdae431e299d0e376654d103f6001e58b7fcab7e.png)

map()会把seq中的元素一个个作用在func()上,并将返回值组成一个新的可迭代对象mapped_seq

结构:map(func, *iterables) --> map object
第一个参数是函数名,也可以是lambda表达式,第二个参数是一个可迭代的对象,返回值为map object

```python
import math
map(lambda x:math.pow(x,2),[1,2,3,4,5,6,7])
```

```
<map at 0x231ffcec3a0>
```

返回结果是map object 是可迭代的

```python
list(map(lambda x:math.pow(x,2),[1,2,3,4,5,6,7]))
```

```
[1.0, 4.0, 9.0, 16.0, 25.0, 36.0, 49.0]
```

②标准库functools中的reduce(function,sequence)函数可以接收一个有两个参数的函数function(),以迭代的方式从左到右依次作用到一个序列sequence上实现类huffman树的聚集操作(求和,求连乘积等)

Huffman树聚集 

![pic](course/2893e4946d48616a8a44b066f74abe471b5851b7.png)

```python
from functools import reduce
reduce(lambda i,j:i+j,range(1,101))
```

```
5050
```

③内置函数filter将一个函数作用到一个序列上,返回该序列中式函数返回值为True的元素组成的filter对象,filter对象也是可迭代的 

![](course/070ea291b9e902da71d898c334c955799d89a3bb.png)

如:输出从1到1000所有的素数

```python
import math
def is_prime(n):
    if n<2:
        return False
    if n==2:
        return True
    if n%2==0:
        return False
    sqrt_n=math.floor(math.sqrt(n))
    for i in range(3,sqrt_n+1,2):
        if n%i==0:
            return False
    return True
```

```python
print(list(filter(is_prime,range(1,101))),end=" ")
```

```
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97] 
```

④内置函数zip

zip函数像一个拉链,把两个序列连接返回一个zip对象,可迭代.其元素是两个序列元素组成的元组 

![](course/8d8e77c1bea77d5f77e9dffa772e8923594a676a.png)

```python
list(zip(range(10),'abcdefghij'))
```

```
[(0, 'a'),
 (1, 'b'),
 (2, 'c'),
 (3, 'd'),
 (4, 'e'),
 (5, 'f'),
 (6, 'g'),
 (7, 'h'),
 (8, 'i'),
 (9, 'j')]
```



### tips

#### python的可变类型和不可变类型

可变类型:

- 列表[]

- 集合

- 字典

不可变类型

- 数字(整型,浮点型等)

- 字符串

- 元组:()

<mark>可变和不可变的实质:</mark> 可变数据和不可变数据是相对于**引用地址**来说的，不可变数据类型不允许变量的值发生变化，<u>如果改变了的变量的值，相当于新建了一个对象</u>，而对于相同的值的对象，内部会有一个引用计数来记录有多少个变量引用了这个对象。可变数据类型允许变量的值发生变化。对变量进行修改操作只会改变变量的值，不会新建对象，变量引用的地址也不会发生变化，不过对于相同的值的不同对象，在内存中则会存在不同的对象，即每个对象都有自己的地址，相当于内存中对于同值的对象保存了多份，这里不存在引用计数，是实实在在的对象。

简单地讲，可变数据和不可变数据的“变”是相对于引用地址来说的，不是不能改变其数据，而是改变数据的时候会不会改变变量的引用地址。

比如:

python中可以使用id()函数查看变量的引用地址

![](course/2022-09-20-11-16-24-image.png)

可以看到,字符串虽然值改变了,但它的引用地址也发生了变化,在内存中实际是

```python
a='China'
a->str1->'China'
a+='hello'
a->str2->'China hello'
```

而可变类型如列表不需要开辟新空间,还是曾经的引用地址

#### 深拷贝和浅拷贝

**浅拷贝** ：只复制指向某个对象的指针，而不复制对象本身，相当于是新建了一个对象，该对象复制了原对象的指针，新旧对象还是共用一个内存块

**深拷贝**：是新建一个一模一样的对象，该对象与原对象不共享内存，修改新对象也不会影响原对象
