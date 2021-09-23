

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

code runner：

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

### win10玩红警

下载ddraw.all插件，适用于几乎所有红警

禁用3d加速，注册表法

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
