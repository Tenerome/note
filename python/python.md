### pre

~~下载配置python3.9.0~~

~~安装版的python自带Scripts文件夹,集成好了pip~~

~~解压版的没有,很清爽只有15M,需手动建文件夹,安装pip~~

~~pip依赖于setuptool,先安装setuptools~~

<mark>一堆依赖,搞乱了,直接用安装版</mark>



直接在cmd或者powershell中输入python.exe进去交互模式，输入文件结束符 结束输入，win下:Ctrl +z ,linux 下Ctrl + d。推出状态码为0。

设置编码方式

```python
# -*- coding: utf-8 -*-
```

注释:用#

支持四则等运算，+，-，\*，\*\*,/,//,%

其中 / 返回浮点数，//返回整数

\*\*表示乘方，如2 \*\*3=8

用=表示赋值，同时也会对变量定义类型

### python基础

#### 变量

python 内部是有类型的,int ,float,str等,但编程时不需要关注变量的类型.所有变量无需声明,赋值后直接使用.

```python
#int i=0
i=0
```

另外可以给一个变量赋不同类型的值

```python
i=0
print(i)
i="Hello"
print(i)
```

可以使用type加变量名来查看变量类型

#### 分支结构

python中的if分支结构

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

python的if语句,条件不用括号

#### 循环结构

while

while 判断条件(condition)：
        执行语句(statements)

for

```python
for <variable> in <sequence>:
      <statements>
```

eg: for i in range

很像bash语言的for语法

#### 组合类型

##### 列表

列表用[],表示,里面的元素用逗号隔开,列表中的元素可以是不同的数据类型.

```python
list1 = ['百度','nanjing',1997,20.57]
```

列表支持修改元素

```python
print ("第三个元素为 : ", list1[2])
list1[1] = '南京'#更新第二个元素
list1.append('中国')#增加一个新的元素
```

##### 元组

元组用()表示,相较于列表,它不能修改里面的元素

元组不能修改,但可以连接,类似字符串连接的效果

##### 组合类型

列表和元组可以互相嵌套使用

##### 字典

字典是一种可变容器模型,可以存储任意类型的对象.它是由键值对构成的列表.字典的每个键值key=>value对  用冒号 : 分割,每个键值对之间用逗号分割,整个字典用{}表示.

```python
dict = {'张海': ['男',18,'南京'],'李慧':[ '女',21,'武汉'],'王霞':[ '女',19,'苏州']}
```

在字典中,key值必须是唯一的

搜索键

```python
dict['张海']
```

即字典名+key值

键值可以修改,可以添加,但是键不允许修改

key可以是数字,字符串或者元组,不能是列表(可变的)

#### 字符串

单引号和双引号处理字符串，用\转义字符，单引号可以转义双引号，双引号也可以转义单引号，但引号内的相同引号要用\转义

字符串可以用+连接，用\*重复

字符串支持索引，如

```python
>>>word="Hello"
>>>word[1]
'e'
```

且可以使用负索引从右向左计数,但是word[-0]=word[0]=‘H’，word[-1]='o'。即负索引从-1开始，正索引从0开始

字符串还支持切片,切片提取子字符串。使用[i,j]提取从第i个到第j-1个字符。缺省时表示从头到j，或从i到尾

```python
>>>word[1:3]
'el'
>>>word[2:]
'llo'
>>>word[:3]
'Hel'
```

大致可以这样理解

![](python/2022-08-23-19-38-34-image.png)

字符串不能修改子串，字符串是immutable(不可变的)。

不能word[2]='J'

但是可以整个赋值，word="Hi"

内置的len()函数可以返回字符串的长度



### 第三方库

#### numpy

numpy :Numberical python,支持大量维度数组与矩阵运算.另外针对数组提供大量的数学函数库,与pandas ,matplotlib齐称数据分析三剑客

下载

```bash
pip install numpy
```

#### matplotlib

是一个python 2D绘图库,常用来生成图表,直方图,功率谱,条形图,误差图,散点图等.

安装

```bash
pip install matplotlib
```

#### pandas

一个用来从文件中读取大量数据的库

#### seaborn

  用来绘制图像的库,relplot函数用于可视化统计  量间的关系.

relplot常用参数

参数名含义
x:x轴数据
y:y轴数据
hue:在某一维度上，用颜色区分
style:在某一维度上, 用线的不同形式区分, 如点线、虚线等
size:控制数据点大小或者线条粗细
col:列上的子图
row:行上的子图
kind:kind= ‘scatter’(默认)，图形样式如点图、折线图等
data数据源
