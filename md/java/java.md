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

#### 构造方法

1.构造方法名字和类名相同

2.构造方法没有返回值

3.构造方法一般用于对成员变量的初始化，重载

4.构造方法在创建对象时自动创建



·可以在一个构造方法中调用其他重载的构造方法 

eg:

````java

public class Car {
    int id;
    String brand;
    String color;
    int weight;

    public Car() {
    }
    public Car(int id,String brand){
        this(id, brand, null);
    }
    //（2）在构造方法中做调用，调用另一个重载的构造方法，让重复的代码只写一次，也便于以后的时候修改变量。
    public Car(int id,String brand,String color){

        //this.id = id;
        //this.brand = brand;
        //this.color = color;
        //重复的代码只写一次做调用
        //一个构造方法，调用另一个重载的构造方法
        this(id, brand, color, 0);//0位重量的默认值
    }

    //（1）我们在构造方法中集中的处理所有参数
    public Car(int id,String brand,String color,int weight){
        this.id = id;
        this.brand = brand;
        this.color = color;
        this.weight = weight;
    }

    public void go(){
        System.out.println(
            id+"号"+color+"的汽车启动");
    }
    public void stop(){
        System.out.println(
            id+"号"+color+"的汽车停止");
    }
    public void turnLeft(){
        System.out.println(
            id+"号"+color+"的汽车左转");
    }
    public void turnRight(){
        System.out.println(
            id+"号"+color+"的汽车右转");
    }
}

````

#### 实例成员和类成员

·类成员（静态成员）：

用static修饰

属于类，也属于该类创建的对象

在类外，可以用类名访问也可以用对象名访问

·实例成员：

不用static修饰

只属于对象

在类外只能用对象名访问



·在类内，实例方法可以访问实例成员和类成员，类方法只能访问类成员（不用static修饰的方法可以访问static修饰的变量和不用static修饰的，用static修饰的方法只能访问static修饰的变量）



eg：

````java
public class InstanceStatic {

    int x = 3;// 类的实例变量，初始化值为3
    static int y = 4;// 类的静态变量，初始化值为4

    public static void staticmethod()// 静态方法
    {
        //System.out.println(x);  X  静态方法不能直接调用实例成员
        System.out.println("实例变量x = " + new InstanceStatic().x);// 在静态方法中访问类的实例变量需首先进行类的实例化
        System.out.println("静态变量y = " + y);// 在静态方法中可直接访问类的静态变量
        staticmethod1();//静态方法可以调用其他静态方法
        // instancemethod();  X 静态方法不能访问实例方法
        new InstanceStatic().instancemathod1();
    }

    public static void  staticmethod1(){  //静态方法2
        System.out.println("另一个静态方法");
    }
    public void instancemathod(){
        System.out.println(x);//实力访问可以直接访问实例变量，类变量，实例方法，类方法
        System.out.println(y);
        staticmethod1();
        instancemathod1();
    }
    public void instancemathod1(){
        System.out.println("另一个实例方法");
    }
    public static void main(String[] args) {
        System.out.println("====类方法====");
        InstanceStatic.staticmethod();
        System.out.println("====实例方法===");
        InstanceStatic cc=new InstanceStatic();
        cc.instancemathod();
    }
}

结果：
====类方法====
实例变量x = 3
静态变量y = 4
另一个静态方法
另一个实例方法
====实例方法===
3
4
另一个静态方法
另一个实例方法
````





