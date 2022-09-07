### lesson 1

#### 1

创建一个包含10个整数的列表x = [11, 9, 11, 10, 5, 5, 5, 7, 4, 12]，去除列表中的重复项。

```python
x = [11, 9, 11, 10, 5, 5, 5, 7, 4, 12]
y = list(set(x))
print(y)
```

set() -> new empty set object set(iterable) -> new set object

Build an unordered collection of unique elements.

set():创建迭代器的未排序的唯一值

#### 2

引入random库，创建一个包含10个随机整数的列表，随机整数的取值范围为[1~50]。使用map()函数返回一个包含每个整数平方值的新列表，并使用列表推导式提取出新列表中所有大于等于1000的整数。

```python
from random import randint
x = [randint(1,50) for i in range(10)]
y = list(map(lambda x : x **2, x))
print(y)
z=([i for i in y if i >= 1e3])
print(z)
```

#元组[]的元素是randint()
#randint() 循环i次
#range(m,n) m≤i<n

#map:Make an iterator that computes the function using arguments from each of the iterables. Stops when the shortest iterable is exhausted.
#map(func, *iterables) --> map object
#map函数的两个参数,第一个是一个函数,用来返回值,第二个是迭代器,功能是把迭代器送进func()函数,运算后返回值返回给map()

#### 3

两个列表[1,2,3,4]、[5,6,7,8] 合并为[8, 7, 6, 5, 4, 3, 2, 1]

```python
x = [1, 2, 3, 4]
y = [5, 6, 7, 8]
x.extend(y)
x.reverse()
print(x)
```

extend():Extend list by appending elements from the iterable.

reverse():倒置

#### 4

s = 'sdaaerdaxxdfwsbhh'，去重并从⼩到⼤输出'abdefhrswx'

```python
s = 'sdaaerdaxxdfwsbhh'
s= list(set(s))
s = sorted(s)
res = ''.join(s)
print(res)
```

join:Concatenate any number of strings.

The string whose method is called is inserted in between each given string. The result is returned as a new string.

Example: '.'.join(['ab', 'pq', 'rs']) -> 'ab.pq.rs'

' '中设置分隔符,可为空

#### 5

 a = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]，⽤filter函数求出所有偶数，并创建新
的列表

```python
def oushu(x):
    if x % 2 == 0:
        return True
a = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
b = list(filter(oushu,a))
print(b)
```

def是python中自定义函数的形式,函数名(形参)

filter(function or None, iterable) --> filter object

Return an iterator yielding those items of iterable for which function(item) is true. If function is None, return the items that are true.
