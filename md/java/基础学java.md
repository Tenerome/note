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

​	--META-INF	

​			--MANIFEST.MF	//配置文件，说明程序入口类main class等

​	--xx.class		//假设xx.class为主类

​	--xx1.class

​	--xx2.clss

-MANIFEST.MF-

Manifest-Version: 1.0
Created-By: 1.8.0_301 (Oracle Corporation)
Main-Class: xx	//程序入口主类

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

















