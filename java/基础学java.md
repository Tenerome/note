## 第二章java开发工具

### jdk常用工具

javac:把.java文件编译成.class文件

java:执行.class文件

javadoc：生成java的说明文档

javap:java反编译器，.class可访问的成员，方法

jdb:java调试工具

### java应用程序发布工具

#### jar包的结构

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

#### 操作指令

打包同时指定主类

jar cvfe  xx.jar   主类名   *(表示所有class)

-c：创建jar

-v：输出打包详情

-f：指定包名xx.jar

-e:指定程序入口  ：主类

执行：

java -jar  xx.jar

#### 图形化操作

可以手动编译好class，创建META-INF和MANIFEST.MF,并指定主类

添加压缩文件

更改后缀名为.jar

## 第三章java数据类型和运算符

java中的常量用final 修饰

## 第五章数组

java也支持对象数组

## 第六章字符串处理

### String类和StringBuffer类的比较

String：一旦实例化，其长度内容固定不可改变，所有对其改变的操作不改变本身，而是生成新的实例

StringBuffer：处理可变长字符串，直接对对象本身操作，实例化时除分配本身所占空间，系统额外提供16个字符大小的缓冲区

String适合短字符串，StringBuffer适合长

### String构造器

string():默认构造器，空字符串

String(byte[] byte):参数为字节数组，将其初始化为字符串

String(byte[] byte,int offset,int length):将字节数组byte从offset位置开始到length长度结束，初始化为字符串

String(byte[] byte,int offset,int length,String charsetName):charsetName指定编码方式

String (char[] value):将字符数组连接成字符串

String (char[] value,int offset,int count):截取
