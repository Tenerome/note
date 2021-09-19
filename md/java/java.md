## java课程

### 基础

### 对象，类和方法

对象：对客观世界里的任何实体的抽象

属性：表示实体的静态特征，所有属性的组合反映实体的状态

行为：表示实体的动态特征，一个行为的过程可能会影响或改变实体的状态

### 对象的创建

new运算符用于创建对象，完成3个工作：

在堆中为对象分配内存

调用构造方法

返回该对象在堆中的地址



concat：用于连接数组

````java
arrayObject.concat(arrx,arry);
````

substring

substring() 方法用于提取字符串中介于两个指定下标之间的字符。

````java
stringObject.substring(start,stop)
````

### 类的定义

格式：

修饰符(public等) class <类名>{

成员变量；

构造方法；

成员方法；

}

#### 成员变量

修饰符：

public，protected，private：定义变量可见性

final：定义变量有名常量

static：定义静态变量，也叫类变量

#### 成员方法

#### this，return，do，get

````java
 protected int a,b;
    public int getA(){
        return a;
    }
    public void setA(int a){
        this.a=a;
    }
    public int getB(){
        return this.b;//return 的是这个类的变量，就算是protected，也可以直接return，也可以用this
    }
    public void setB(int b){
        this.b=b;       //this.b是类的变量，b是方法setB()的形参
    }
````





