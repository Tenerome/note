1.vscode默认是utf-8，但最好再打开自动检测

2.在vscode设置里搜 auto guess，启用auto guess encoding

3.windows默认的是gbk，在windows设置-语言-管理语言设置-更改区域-启用utf-8（用这个法改的是全局的编码方式，可能会导致某些文件乱码）

4.java默认也是gbk，修改方法：
  win键+s键，搜编辑环境变量，在系统变量中添加一个条目
    变量名：JAVA_TOOL_OPTIONS
    值:-Dfile.encoding=UTF-8

5.如果需要调用cmd，cmd默认也是gbk，直接用chcp 650001 指令可以修改，但是只能一次有效，重启cmd恢复。永久修改方法：
  win+s，搜注册表项
    位置HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor
    新建字符串
    名：autorun
    值：chcp 650001