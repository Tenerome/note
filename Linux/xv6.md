## XV6

| 系统调用                      | 描述                                |
| ------------------------- | --------------------------------- |
| fork()                    | 创建进程                              |
| exit()                    | 结束当前进程                            |
| wait()                    | 等待子进程结束                           |
| kill(pid)                 | 结束 pid 所指进程                       |
| getpid()                  | 获得当前进程 pid                        |
| sleep(n)                  | 睡眠 n 秒                            |
| exec(filename, *argv)     | 加载并执行一个文件                         |
| sbrk(n)                   | 为进程内存空间增加 n 字节                    |
| open(filename, flags)     | 打开文件，flags 指定读/写模式                |
| read(fd, buf, n)          | 从文件中读 n 个字节到 buf                  |
| write(fd, buf, n)         | 从 buf 中写 n 个字节到文件                 |
| close(fd)                 | 关闭打开的 fd                          |
| dup(fd)                   | 复制 fd                             |
| pipe( p)                  | 创建管道，<mark> 并把读和写的 fd 返回到p</mark> |
| chdir(dirname)            | 改变当前目录                            |
| mkdir(dirname)            | 创建新的目录                            |
| mknod(name, major, minor) | 创建设备文件                            |
| fstat(fd)                 | 返回文件信息                            |
| link(f1, f2)              | 给 f1 创建一个新名字(f2)                  |
| unlink(filename)          | 删除文件                              |

### linux指令:

cat:用于连接文件并打印到标准输出设备上

echo:输出字符串

grep:查找字符串

ln:为某一个文件在另外一个位置建立一个同步的链接

mkdir:创建目录

rm:删除文件或目录

wc:用于计算字数，若不指定文件名称、或是所给予的文件名为"-"，则wc指令会从标准输入设备读取数据。！@#！

<mark>所有对文件的操作都是对文件描述符fd的操作</mark>

### 文件描述符fd

/dev/fd目录

![](../2022-03-05-09-40-19-image.png)

默认会有这四个项：  
0是标准输入，默认是键盘。 stdin  
1是标准输出，默认是屏幕/dev/tty stdout  
2是标准错误，默认也是屏幕 stderr  
255

### 重定向

命令>文件 和 命令>>文件，将命令执行的结果输出到文件中

命令<文件 和 命令<<文件，将文件的内容作为命令的输入，执行命令

前者是覆盖，后者是追加

- 输出

```c
echo "Hello,world">>sc.txt
```

字符串"Hello，world"就被输出到sc.txt

```c
ls data>>sc.txt
```

将`ls data`的结果输出到sc.txt

- 配合文件描述符，可以将不同的信息类型重定向：

描述符和< >之间不能有空格

```c
ls data 1>sc.txt
```

将`ls data`的执行结果输出到sc.txt

```c
ls date 2>sc.txt
```

因为`date`目录不存在，所有指令出错，将`ls date`的报错信息输出到sc.txt

```c
cat 0<sc.txt//sc.txt->hello,world
```

- 输入

```c
wc sc.txt
wc <sc.txt//sc.txt->hello
```

输出结果：

```c
0 1 5 sc.txt
0 1 5
```

第二个不会输出文件名，因为它读取了sc中的内容，并没有读取sc.txt

-     调用标准输入，在终端输入数据

```c
cat ->>sc.txt
```

cat 后面不接文件或者接着'-',是调用标准输入

在终端输入文本，按Ctrl D结束输入，然后重定向到sc.txt

-     组合使用

```c
wc <sc.txt >cc.txt
```

从sc.txt中获取输入，执行wc指令，再将执行的结果输出在cc

#### Here Document

Here Document 是shell中的一种特殊的重定向，用来将输入  重定向 到 一个交互式shell脚本或程序

```c
command << delimiter
    document
delimiter
```

将两个delimiter之间的内容(document)作为输入传递给command

结尾的delimiter必须顶格写

```c
wc <<eof
    hello,world
    hello,god
    how are you feeling today
eof
```

delimiter相当于开闭标签，可以随意定义(不冲突前提下)

#### /dev/null

如果希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null

```c
command >>/dev/null
```

/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃,将命令的输出重定向到它，会起到"禁止输出"的效果

#### exec

直接重定向只是一次输入输出的重定向，若想使重定向在一次终端中一直使用，就要用exec

```c
exec 1>sc.txt
```

将所有的输出都重定向到sc.txt

如果想回到标准输入输出可以这样做：

    实际文件描述符最多有9个

```c
exec 3>&1//描述符3重定向到标准输出
exec 1>sc.txt//1（=3）重定向到
ls//输出在sc.txt
exec 1>&3//标准输出重定向到monitor
ls//输出在屏幕
```
