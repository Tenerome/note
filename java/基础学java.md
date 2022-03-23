### 第二章java开发工具

#### jdk常用工具

javac:把.java文件编译成.class文件

java:执行.class文件

javadoc：生成java的说明文档

javap:java反编译器，.class可访问的成员，方法

jdb:java调试工具

#### java应用程序发布工具

##### jar包的结构

---jar

​    --META-INF    

​            --MANIFEST.MF    //配置文件，说明程序入口类main class等

​    --xx.class        //假设xx.class为主类

​    --xx1.class

​    --xx2.clss

-MANIFEST.MF-

Manifest-Version: 1.0
Created-By: 1.8.0_301 (Oracle Corporation)
Main-Class: xx    //程序入口主类

Class-Path:xxx.jar   导入的jar包

eg:

```markdown
Manifest-Version: 1.0
Main-Class: com.hejing.paserTsp.ShowResultFrame
Class-Path: lib/commons-beanutils-1.8.0.jar
 lib/byte-buddy-1.7.5.jar
 lib/client-combined-3.8.1.jar
 lib/client-combined-3.8.1-sources.jar
 lib/commons-codec-1.10.jar
 lib/commons-collections-3.2.1.jar
 lib/commons-exec-1.3.jar
 lib/commons-lang-2.5.jar
 lib/commons-logging-1.1.1.jar
```

规则

1. 第一行不能空，行与行之间不能有空行，每一行的最后一个字符不能是空格。
2. 最后一行一定是空行。
3. 每个属性的名称和值之间（冒号后面）一定要有空格。
4. 文件的每一行都不能超过72个字节（一般是70个ASCII字母加上回车换行符）；如果72个字节不够用，则另起一行并以空格开头：以空格开头的行都被视为前一行的续行，不要使用TAB键，否则会报错：invalid header。
5. Class-Path属性指定的类或jar包是本地的文件，不可以是远程访问的类或者JAR包文件中的JAR包，即不能是jar in jar，当然也就不能是本jar包中包含的jar包。要实现对jar in jar的引用，需要自定义相关代码来读取它们。上面提到的RunnableJAR file之所以能够运行，就是因为Eclipse为我们提供了jarinjarloader，来帮助我们读取jar in jar。

路漫漫其修远兮，吾将上下而求索！

-end-

##### 操作指令

打包同时指定主类

jar cvfe  xx.jar   主类名   *(表示所有class)

-c：创建jar

-v：输出打包详情

-f：指定包名xx.jar

-e:指定程序入口  ：主类

执行：

java -jar  xx.jar

##### 图形化操作

可以手动编译好class，创建META-INF和MANIFEST.MF,并指定主类

添加压缩文件

更改后缀名为.jar

### 第三章java数据类型和运算符

java中的常量用final 修饰

### 第五章数组

java也支持对象数组

### 第六章字符串处理

#### String类和StringBuffer类的比较

String：一旦实例化，其长度内容固定不可改变，所有对其改变的操作不改变本身，而是生成新的实例

StringBuffer：处理可变长字符串，直接对对象本身操作，实例化时除分配本身所占空间，系统额外提供16个字符大小的缓冲区

String适合短字符串，StringBuffer适合长

#### String构造器

```java
string()//默认构造器，空字符串

String(byte[] byte)//参数为字节数组，将其初始化为字符串

String(byte[] byte,int offset,int length)
                //将字节数组byte从offset位置开始到length长度结束，初始化为字符串

String(byte[] byte,int offset,int length,String charsetName)
                                    //charsetName指定编码方式

String (char[] value)//将字符数组连接成字符串

String (char[] value,int offset,int count)//从offset开始截取count个字符
```

#### 字符串处理方法

##### 字符串连接

    1.直接用 “+”

    2.String.concat(String   str)方法

```java
String str1="China";
String str2="Yes";
str1.concat(str2);
```

##### 提取字符串

    1.从index提取到字符串末尾

```java
String.substring(int index)
```

    2.从beginindex开始提取到end

```java
String substring(int beginIndex,int endIndex)
```

##### 从字符串中分解字符

返回第index个字符

```java
char String.charAt(int index)
```

##### 获取字符串长度

```java
int String.length()
```

和数组length的区别，数组的length是属性，调用的时候是arr.length,而字符串的length()是方法

##### 测试字符串是否相等

判断字符串是否相等，不能直接用==

判断字符串相等

```java
boolean String.equals(String str)
```

忽略大小写，用来做验证码判断

```java
boolean String.equalsIgnoreCase(String str)
```

##### 查找字符串（串的模式匹配）

1.返回子串在主串的位置；首字母起始位置。如果无子串，返回-1

```java
int String.indexOf(String str)
```

2.若主串以子串开头，返回true

```java
boolean String.startsWith(String str)
```

3.以子串结尾，返回true

```java
boolean String.endWith(String str)
```

##### 基本类型转换称字符串

```java
String Object.valueOf()
```

##### toString()

```java
String str="How are you feeling now？";

System.out.printf(str);
```

str是一个对象，但是可以输出，因为它自动调用了str.toString()

java中所有的类对象都可以输出,他们都有toString()方法

#### 缓冲字符处理类StringBuffer

##### StringBuffer构造器

1.默认构造器

```java
StringBuffer sb=new StringBuffer();
```

默认分配16个字节

```java
System.out.printf(sb.capacity());
System.out.printf(sb.length();
```

```bash
16
0
```

capacity()方法是他的容量，length()方法是长度

2.设定容量构造器

```java
StringBuffer sb=new StringBuffer(int x);
```

x,分配的容量大小，单位：字节



```java
sb.ensureCapacity(100);
```

ensureCapacity(int x)将容量扩充到x个字节

##### 缓冲字符串的处理

1.用String 初始化StringBuffer

```java
StringBuffer sb=new StringBuffer(String str);
```

2.字符串连接方法

```java
sb.append(String str);
```

将str和sb连接在一块

3.设置长度,setLength()方法

```java
StringBuffer sb=new StringBuffer("How are you?");
sb.setLength(3);
System.out.println(sb);
```

输出结果

```bash
How
```

如果设置的长度小于原字符串的长度，超出部分会被截断

然而如果

```java
StringBuffer sb=new StringBuffer("How");
sb.setLength(10);
System.out.println(sb);
System.out.println(sb.length());
```

输出

```bash
How
10
```

如果设置的长度大于字符串字符个数，则输出长度时会改变，但并不会追加什么

源码

```java
If the newLength argument is greater than or equal to the current length,
 sufficient null characters ('\u005Cu0000') are appended so that
 length becomes the newLength argument.
```

4，取单个字符

```java
char StringBuffer.charAt(int x);
```

返回第x个字符(从0开始)



5.设置单个字符

```java
StringBuffer.setCharAt(int x,char ch);
```

将第x为设置为ch

6.插入字符串

```java
StringBuffer.insert(int x,String str);
```

在第x处插入字符串str

7.返回子串

```java
StringBuffer.substring(int index);
StringBuffer.substring(int beginx,int endx);
```

同String的

8.倒置字符串

```java
String StringBuffer.reverse();
```

返回倒置的字符串

#### 常见疑难解答

##### equals和==

如果操作的两边都是对象句柄，则比较两个句柄是否指向同一个对象。

如果两边是基本类型，比较的就是值。



equals比较的是两个对象的内容，如果不重载equals，自动调用object的equals，和==一样。

eg：

```java
public class test{
    int x;
    public test(){
        this.x=0;
    }
    public test(int x){
        this.x=x;
    }
}
```

1.

```java
public static void main(String[] args) {
        test t1=new test();
        test t2=t1;
        System.out.println(t1.equals(t2));
}
```

输出

```bash
true
```

2.

```java
public static void main(String[] args) {
        test t1=new test(3);
        test t2=new test(3);
        System.out.println(t1.equals(t2));
    }
```

输出

```bash
false
```

##### String为什么被定义为final

为了系统的效率和安全性，不允许String被继承

##### char和int转换，int转换为String

```java
char c='A';
int i=c;//直接转换
c=(char)i;//需要强制转换
```

```java
int i;
String s=String.valueOf(i);
String s=Integer.toString(i);//两种方法
```

### 句柄

### 类和对象
