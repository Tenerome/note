

### 环境变量

#### 环境变量配置路径

##### path

mysql:  xxxx/bin

mingw:xxx/bin

git:xxx/cmd

jdk:xxx/bin

##### 注意

Java，可以直接在path中配置，但是想tomcat不能识别，只能配置java_home或者jre_home

##### jdk和tomcat

tomcat 8 不能用太高的jdk,用jdk 8就行

##### jdk改完没有作用

c-program file和 x86-common files-oracle

删掉，这里默认配置jdk路径

### 插件

#### vscode

vscode自带shift+alt+f格式化

code runner：设置 run in terminal

Open in default browser

Tomcat for java

c/c++

c++ Intelllisense

chinese

html snippets

intellisense for css in html

java server page

jstl snippets:jsp intellisense

language support for java by red hat

masm







默认输出在  输出 中，不能输入，需要设置code runner   run  in  terminal，在终端运行

### 刷系统

security boot：disable

cms：enable

F10开启boot

### git

git config --global user.name ''

git config --global user.email ''

git clone

### 挂完vpn浏览器断网

1.关代理

自动检测打开

设置脚本关闭

脚本地址空

手动设置代理关闭

地址端口空

关闭  请勿将代理服务器用于本地

2.如果是google扩展，添加的解压后的扩展，不能直接删，要在edge善2

### 万能

网页前加wn.run/

### win10-red2

下载ddraw.all插件，适用于几乎所有红警

禁用3d加速，注册表

红警黑边

### 解决某些软件删除不了或者不能初始化

右键-属性-详细信息-删除属性及个人信息

### vscode分级文件夹

首选项-设置-功能-资源管理器-compack folders

### vscode -java package机制，找不到主类

code runner 设置，coderunner.excutormap

java

"java": "cd $dir && javac -d. $fileName && java app.$fileNameWithoutExt",

### dosbox

下载，安装

挂载：mount   C（dosbox的c盘） xxx（自己的路径）

环境变量：set PATH =$PATH$;xxx

### vscode中文乱码

vscode 默认utf-8，最好再打开自动检测

-设置-搜auto guess -启用

-windows默认为gbk，设置-语言-管理语言设置 -更改区域-启用utf-8

-最后java默认gbk，添加一个环境变量，名：JAVA_TOOL_OPTIONS

值-Dfile.encoding=UTF-8

-注册表-计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor-

新建字符串autorun，值设为chcp 65001

### vscode 开发javaee

1.jdk，jdk-utf-8

2.tomcat

3.在tomcat上运行的web工程

​		需要的文件结构

​		webapp

​		--WEB-INF      必须的配置文件

​		---classes       编译好的class

​      --html和jsp

5.直接run on tomcat





### cmd管理员

直接搜索栏输入CMD后（不要立即回车进入），按住CTRL+SHIFT+ENTER键可直接进入管理员模式命令行。

### servlet包找不到，webservlet注解无效

把tomcat-lib-annotations-api.jar和servlet-api.jar复制到jdk-jre-lib-ext中就行了

### vscode自定义snippet

新建-用户片段

json文件格式  

 // "片段名": {

  // "prefix": "log",

  // "body": [

  //   "console.log('$1');",

  //   "$2"

  // ],

  // "description": "Log output to console"

  // }

转义:\"输出"

$2光标移动到这

### vscode中package问题

runcode 改为javac -d ./  

生成的class包含包名

如果没有写package，可以直接运行

如果有包，运行时用java   包名.class

### c scoket编译问题

需要外链lib

gcc   -L/库文件夹-l库文件名   

gcc filename   -lwsock32  需要外链wsock32 

### vscode runner  code

code runner可以在文件夹中设置不同的run，相当于不同的调试任务



### assmbly

编译asm

masm  

link

运行/debug

debug xx.exe 全称！！



| Debug-R | 查看、改变CPU寄存器的内容                |
| ------- | ---------------------------------------- |
| Debug-D | 查看内存中的内容                         |
| Debug-E | 改写内存中的内容                         |
| Debug-U | 将内存中的机器指令翻译成汇编指令         |
| Debug-T | 执行一条机器指令                         |
| Debug-A | 以汇编指令的格式在内存中写入一条机器指令 |
