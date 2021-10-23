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

### 类

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



|可以在一个构造方法中调用其他重载的构造方法 

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

|类成员（静态成员）：

用static修饰

属于类，也属于该类创建的对象

在类外，可以用类名访问也可以用对象名访问

|实例成员：

不用static修饰

只属于对象

在类外只能用对象名访问



|在类内，实例方法可以访问实例成员和类成员，类方法只能访问类成员（不用static修饰的方法可以访问static修饰的变量和不用static修饰的，用static修饰的方法只能访问static修饰的变量）



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



### 包

导包：

````java
import 包名1.包名2. ...  类名；

import 包名1.包名2.*;//   .*表示导入该包下所有类

````



### 类和类成员的可见性：

#### 类的可见性：

public修饰：任何位置可见

不用public 修饰：仅在当前包可见

|一个类文件，只能有一个public修饰的class，且和文件名字相同



#### 成员可见性：

public：任何位置可见

protected：当前包和当前类的子类

private：只能在当前类可见

无修饰符：默认，当前包可见

### 包装类和字符串类

常用包装类：

Boolean(boolean)

Character(char)

Byte(byte)

Integer(int)

Short(short)

Long(long)

Float(float)

Double(double)



Integer的方法：

````java
byte  byteValue();//把字符串转化成byte型
static int compare(int x,int y);//比较两个整数的大小
static int max(int x,int y);//取较小值
static int min(int x,int y);
static int parseInt(String s);//把字符串转换成整型
static Integer valueOf(String s);//把字符串转换成Integer
````



字符串类：

String静态字符串:

````java
char charAt(int index);//获取字符串的第n位
boolean equals(Object anObject);//判断两个字符串是否相等
int length();//获取字符串长度
String subString(int x,int y);//截取字符串x到y位
````

StringButtfer动态字符串

````java
StringBuffer append();//末尾插入
StringBuffer insert();//中间插入
````

### Array类

方法：

````java
static int binarySearch(int[] a,int k);查找数组元素	
static int compare(boolean[] a,boolean[] b);比较两个数组
static int[] copyOf(int[] original,int newlength)复制数组
static boolean equals(boolean[] a,boolean[] b)比较是否相等
static void fill(int[] a,int val)添加元素
static void sort(int[] a)对数组排序
static String toString(int[] a)数组字符串化
````

### 链表和动态数组

#### LinkedList<E>泛型

方法

````java
boolean	add(E e)
          将指定元素添加到此列表的结尾。
 void	add(int index, E element)
          在此列表中指定的位置插入指定的元素。
 void	addFirst(E e)
          将指定元素插入此列表的开头。
 void	addLast(E e)
          将指定元素添加到此列表的结尾。
 void	clear()
          从此列表中移除所有元素。
 boolean	contains(Object o)
          如果此列表包含指定元素，则返回 true。
 E	element()
          获取但不移除此列表的头（第一个元素）。
 E	get(int index)
          返回此列表中指定位置处的元素。
 E	getFirst()
          返回此列表的第一个元素。
 E	getLast()
          返回此列表的最后一个元素。
 boolean	offer(E e)
          将指定元素添加到此列表的末尾（最后一个元素）。
 boolean	offerFirst(E e)
          在此列表的开头插入指定的元素。
 boolean	offerLast(E e)
          在此列表末尾插入指定的元素。
 E	pop()
          从此列表所表示的堆栈处弹出一个元素。
 void	push(E e)
          将元素推入此列表所表示的堆栈。
 E	remove()
          获取并移除此列表的头（第一个元素）。
 E	remove(int index)
          移除此列表中指定位置处的元素。
          从此列表中移除最后一次出现的指定元素（从头部到尾部遍历列表时）。
 E	set(int index, E element)
          将此列表中指定位置的元素替换为指定的元素。
 int	size()
          返回此列表的元素数。
 Object[]	toArray()
          返回以适当顺序（从第一个元素到最后一个元素）包含此列表中所有元素的数组。
<T> T[]
toArray(T[] a)
          返回以适当顺序（从第一个元素到最后一个元素）包含此列表中所有元素的数组；返回数组的运行时类型为指定数组的类型。
````

#### Vector<E>动态数组

方法

````java
boolean	add(E e)
          将指定元素添加到此向量的末尾。
 void	add(int index, E element)
          在此向量的指定位置插入指定的元素。
 int	capacity()
          返回此向量的当前容量。
 void	clear()
          从此向量中移除所有元素。
 boolean	contains(Object o)
          如果此向量包含指定的元素，则返回 true。
 void	copyInto(Object[] anArray)
          将此向量的组件复制到指定的数组中。
 Enumeration<E>	elements()
          返回此向量的组件的枚举。
 void	ensureCapacity(int minCapacity)
          增加此向量的容量（如有必要），以确保其至少能够保存最小容量参数指定的组件数。
 boolean	equals(Object o)
          比较指定对象与此向量的相等性。
 E	firstElement()
          返回此向量的第一个组件（位于索引 0) 处的项）。
 E	get(int index)
          返回向量中指定位置的元素。
 int	hashCode()
          返回此向量的哈希码值。
 int	indexOf(Object o)
          返回此向量中第一次出现的指定元素的索引，如果此向量不包含该元素，则返回 -1。
 int	indexOf(Object o, int index)
          返回此向量中第一次出现的指定元素的索引，从 index 处正向搜索，如果未找到该元素，则返回 -1。
 void	insertElementAt(E obj, int index)
          将指定对象作为此向量中的组件插入到指定的 index 处。
 boolean	isEmpty()
          测试此向量是否不包含组件。
 E	lastElement()
          返回此向量的最后一个组件。
 int	lastIndexOf(Object o)
          返回此向量中最后一次出现的指定元素的索引；如果此向量不包含该元素，则返回 -1。
 int	lastIndexOf(Object o, int index)
          返回此向量中最后一次出现的指定元素的索引，从 index 处逆向搜索，如果未找到该元素，则返回 -1。
 E	remove(int index)
          移除此向量中指定位置的元素。
 boolean	remove(Object o)
          移除此向量中指定元素的第一个匹配项，如果向量不包含该元素，则元素保持不变。
 boolean	removeAll(Collection<?> c)
          从此向量中移除包含在指定 Collection 中的所有元素。
 void	removeAllElements()
          从此向量中移除全部组件，并将其大小设置为零。
 boolean	removeElement(Object obj)
          从此向量中移除变量的第一个（索引最小的）匹配项。
 void	removeElementAt(int index)
          删除指定索引处的组件。
protected  void	removeRange(int fromIndex, int toIndex)
          从此 List 中移除其索引位于 fromIndex（包括）与 toIndex（不包括）之间的所有元素。
 boolean	retainAll(Collection<?> c)
          在此向量中仅保留包含在指定 Collection 中的元素。
 E	set(int index, E element)
          用指定的元素替换此向量中指定位置处的元素。
 void	setElementAt(E obj, int index)
          将此向量指定 index 处的组件设置为指定的对象。
 void	setSize(int newSize)
          设置此向量的大小。
 int	size()
          返回此向量中的组件数。
 List<E>	subList(int fromIndex, int toIndex)
          返回此 List 的部分视图，元素范围为从 fromIndex（包括）到 toIndex（不包括）。
 Object[]	toArray()
          返回一个数组，包含此向量中以恰当顺序存放的所有元素。
<T> T[]
toArray(T[] a)
          返回一个数组，包含此向量中以恰当顺序存放的所有元素；返回数组的运行时类型为指定数组的类型。
 String	toString()
          返回此向量的字符串表示形式，其中包含每个元素的 String 表示形式。
 void	trimToSize()
          对此向量的容量进行微调，使其等于向量的当前大小。
````

### 类的继承

类的层次关系：一般性类和特殊性类，比如动物和人，政府机构和检察院

继承：描述一般类和特殊类之间的关系的机制

​	父类：一般类

​	子类：特殊类

​	子类拥有父类成员，实现程序复用

传递性：A是B的子类，B是C的子类，那么A是C的子类

定义格式：

修饰符  class  子类  extends  父类{

成员变量；

构造方法；

成员方法；

}

修饰符为public，用于控制子类的可见性

除了object类，所有的类都是子类，都有父类，父类可以指定，默认是object

#### 继承和构造方法：

构造方法不是类的成员

父类的构造方法不能被子类继承

在子类构造方法中可以访问父类中的构造方法，用super来指定父类成员

在子类创建对象时，先调用父类构造方法，再调用子类构造方法

在子类构造方法中第一行必须是super(),如果不是，系统自动添加

#### 继承和变量隐藏

如果子类和父类有相同名称的成员变量

用super.变量名访问父类的成员

用this.变量名访问子类成员

如果不加this，super，按就近原则确定被访问的变量

#### 继承与方法覆盖

如果子类和f父类有相同名称的方法

this.方法 访问子类方法

super.方法访问父类方法

如果没有this，super，按就近原则，如果当前类有，访问当前类，没有就访问父类

#### 继承和类型转换

格式

类型1    变量名=	new	类型2(实参)

当类型1和2不同时，1和2需要有父子关系

自动转换：1的范围比2大，即1是2的父类

````java
AA aa=new BB(5);
````



强制转换：1的范围比2小，1是2的子类

````java
BB bb=(bb)new AA(5);
````

变量的类外访问取决于引用变量的类型，上述，aa.x访问的是AA中的x，bb.x访问的是BB中的x，和前面的类型相关

#### 抽象类和抽象方法

抽象方法：

定义：用abstract 修饰，只有方法声明，没有方法体

格式：public    abstract 	返回值类型	方法名(形参)；

eg:   public abstract    void    show(int x);

抽象类：

定义：用abstract修饰，。含有抽象方法的类

格式：

修饰符	abstract 	class{

抽象方法

}

继承抽象方法的类，如果没有完全继承抽象类的所有方法，本身还是个抽象类，还需要abstract修饰

说明：

抽象类不能用来创建对象，只能被继承

### 接口

接口是一种抽象类

类和类的关系叫继承

接口和接口的关系也叫继承

类和接口的关系叫实现

一个类只有一个父类，但可以实现多个接口



接口定义：

修饰符	interface	接口名{

公共类常量；//用public  static  final修饰

公共抽象方法；//public static  final

}

接口的实现：

修饰符	class  	类名	implement	接口名{

方法体；

}

### 多态

重载多态，静态多态性：通过方法实现重载，一个类中的多个方法名相同，形参不同，