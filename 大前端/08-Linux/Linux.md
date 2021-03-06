# 大纲

![image-20210919220750731](https://gitee.com/IU_czx/images/raw/master/img/Linux%E5%AD%A6%E4%B9%A0%E5%A4%A7%E7%BA%B2.png)

 # 网络连接的三种模式

## 桥接模式

虚拟系统可以和外部系统相互通信,但是容易造成IP冲突

## NAT模式(网络地址转换模式)

可以形成一个虚拟网卡,可以映射到本机的真实IP,可以和外部通讯,不造成IP冲突

## 主机模式

独立的系统

# Linux的目录结构

> Linux一切皆文件

1. root:(该目录为系统管理员,称为超级权限的用户主目录)
2. lib(系统开机所需要的最基本的动态连接共享库
3. bin(常用)(存放尝试用的命令)
4. sbin(系统管理员使用的系统管理程序)
5. lost+find:这个目录一般是空的,当系统非法关机后,这里存放的一些文件(老师那个版本有,我这个版本没有看见)
6. lib(系统开机所需要的最基本的动态连接共享库
7. etc(常用):所有系统管理所需要的配置文件和子目录,比如安装mysql数据库 my.conf
8. usr(常用):用户的很多应用程序和文件都放在这个目录下,类似于windows下的program files目录
9. boot(常用):存放的是启动Linux时使用的一些核心文件,包括一些连接文件和镜像文件
10. proc:是一个虚拟目录,他是系统内存的映射,访问这个目录来获取系统信息
11. srv:service的缩写,该目录存放一些服务启动之后需要提取的数据
12. sys:在linux 2.6内核之后出现的一个新的文件系统sysfs
13. tmp:存放一些临时文件的
14. dev:类似于windows的设备管理器,把所有硬件用文件的形式管理
15. mnt:(常用):系统提供该目录是为了让用户临时挂载别的文件系统的,我们可以把外部的存储挂载在mnt上,进入该目录就可以查看里面的内容了
16. media(常用):linux系统会自动识别一些设备,例如U盘,光驱等等,当识别过后,挂载到这个目录上
17. opt:给主机额外安装软件拜访的目录,就是放安装包的
18. usr/local(常用):放安装完成后的软件
19. var(常用):存放着不断扩充的东西,习惯将经常被修改的目录放在这个目录下,包括各种日志文件
20. selinux:是一种安全子系统,他能控制程序只能访问特定文件,有三种工作模式,可以自行设置

# fxtp和xshell

远程连接工具

1. fxtp:远程传输文件
2. xshell;远程连接工具

# vi和vim

## 常用的三种模式

1. 正常模式

2. 插入模式

   i,I,o,O,a,A,r 进入插入模式

3. 命令行模式

   : / 进入命令行模式

## 快速入门

```bash
vim hello.java  //vim代表使用 vim编辑器
i				//按下i,或者以上插入模式的字符 进入插入模式
				// 按下esc键退出插入模式 同时打入 :wq 表示 写入并退出  : 表示进入命令行模式
```

## 常见指令

1. `:wq`:写入并退出
2. `:q`退出
3. `:q!`:强制退出,不保存
4. 拷贝当前行 `yy`   拷贝当前行向下的5行 `5yy`  粘贴`p`
5. 删除当前行 `dd`  删除当前行向下的5行 `5dd` 
6. 在文件中查找某个单词 [命令行下` / `关键字,回车查找,输入`n`就是查找下一个]
7. 设置文件的行号,取消文件的行号.[命令行下 `:set nu` 和 `:set nonu`
8. 在一般模式下 使用快捷键到该文档的最末行 `G`  定位到最首行 `gg`
9. 撤销 `u`
10. 在一般模式下 快速定位行号  行号+gg 

==注意:拷贝和删除都是包括当前行的==

# 关机&重启命令

```bash
shutdown -h now      //立即进行关机
shutdown -h 1		//hello,1分钟后关机
shutdown -r now		//现在重新启动计算机
halt			   //关机
reboot			   //重新启动计算机
sync			   // 把内存的数据同步到数据盘
```

 不管是重启系统还是关闭系统,最好都执行一下sync命令,把内存写入到磁盘中

目前的shutdown,reboot和halt等命令前都在关机前执行了sync,但是最好还是手动的执行一下sync命令

# 用户管理

## 添加用户

每个用户会对应一个home 目录

1. `useadd` 用户名
   * 如果需要自定义用户存储目录
   * 使用 `useradd -d 目录名 用户名`
2. `passwd`用户名
3. 显示当前用户所在的目录 `pwd`

## 删除用户

1. `userdel 用户名`  会保留家目录
2. `userdel -r 用户名` 不保留家目录

## 切换用户

* `su 用户名`
* `id 用户名` :查询用户信息指令
* 从权限高的访问切换权限低的不需要密码
* `exit`退出当前用户 如果退出至刚登陆的用户 则会退出系统
* `who am i`:显示的是第一次登陆的用户的信息

## 用户组

> 类似于角色,系统可以对有共性的多个用户进行统一的管理

1. 新增组

   `groupadd 组名`

2. 删除组

   `groupdel 组名`

3. 增加用户时直接加上组

   `useradd -g 用户组 用户名`
   
4. 修改用户的组

   `usermod -g 用户组 用户名`

## 用户和组相关的文件

1. `/etc/passwd`文件

   用户(user)的配置文件,记录用户的各种信息

   每行的含义: `用户名:口令:用户标识符:组织识号:注释性描述:主目录:登录shell`

2. /etc/shadow 文件

   口令的配置文件

   每行的含义:`登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志`

3. /etc/group文件

   组的配置文件,记录Linux包含的组的信息

   每行含义:`组号:口令:组标识号:组内用户列表`

# 运行级别

* 0 :关机
*  1:单用户  [找回丢失密码]
*  2:多用户状态 没有网络服务
*  3:多用户状态有网络服务
*  4:系统未使用保留给用户
*  5:图形界面
*  6:系统重启

常用的运行级别是3(multi-user.target) 和 5(graphical.target),也可以指定默认运行级别

* 指令  `init [0,1,2,3,4,5,6]`

* 指令 `systemctl get-default` 可以拿到当前的默认级别

* 指令`systemctl set-default 想要修改的级别(multi-user.target)`

# 找回Root密码

看老韩的文档吧

操作太长了 记不住

# 帮助指令

* man 获得帮助信息

  man [命令或配置文件]

  eg:`man ls`

  在linux下,隐藏文件是以 `.`开头

* help指令

  help命令 (功能描述,获得shell内置命令的帮助信息)

# 文件目录类

* pwd : 显示当前路径,即你现在所处位置

* cd [参数] : 切换到指定目录

  `cd ~`回到当前用户的主页

  `cd..`回到当前目录的上一级

* mkdir:创建目录

  -p : 创建多级目录

  * `mkdir hello`  :创建一个目录
  * `mkdir -p hello/hello` :创建多级目录
  
* rmdir : 删除空目录

  删除的是**空目录**,如果目录下有内容,是无法删除的

  需要删除**非空目录**,需要使用 `rm -rf 要删除的目录`   

* touch:创建空文件

  `touch 文件名`
  
* cp 拷贝文件到指定目录

  `cp 文件 文件目录`
  
  `cp -r 递归复制整个文件夹`
  
  `\cp`:强制覆盖,不会提示
  
* rm :移除文件或目录
  
  rm 要删除的文件或者目录
  
  -r:递归删除整个文件
  
  -f:强制删除不提示
  
* mv  移动文件与目录 或者重命名
  
  mv oldnameFile newNameFile (功能描述:重命名)
  
  mv 如果是同文件夹下 移动文件 就是换名字
  
  如果在移动到不同文件夹下 就是移动功能
  
* cat 查看文件内容
  
  cat [选项] 要查看文件
  
  -n 显示行号
  
  为求方便 可以使用管道命令 `| more`这个命令
  
  eg: `cat -n /etc/profile | more`
  
  按下enter可以进入下一行 按空格 可以进入 下一页 直到显示完成
  
* 

  ![image-20210922081635480](https://gitee.com/IU_czx/images/raw/master/img/mroe%E6%8C%87%E4%BB%A4.png)


 * less 用来分屏查看文件内容，可以根据显示内容进行加载，相对于大文件来讲，效率会更高一点

   ![image-20210922082125622](https://gitee.com/IU_czx/images/raw/master/img/less%E6%8C%87%E4%BB%A4.png)

* echo 输出指定内容到控制台

  ​	echo 【选项】【输出内容】

  ​	eg：使用echo输出环境变量，比如echo $PATH $HOSTNAME.,echo $

* head 用于显示文件的开头部分内容 默认显示文件的前10行内容

  * 基本语法

    head 文件

    head -n 5 文件 （查看文件5行内容，5可以是任何行数）

* tail 用于输出文件中**尾部**的内容，默认是10行

  tail 文件

  tail -n 任意行数 文件

  tail -f 文件（实时追踪文档的所有更新）

* `>`和`>>`指令

  `>` 输出重定向 和 `>>`追加

  `>`会覆盖源文件内容 `>>`不会覆盖内容,而是追加内容

  基本语法

  * `ls -l >文件` (列表的内容写入文件,覆盖写)
  * `ls -al >>文件` (列表的内容追加到文件aa.txt内容)
  * `cat 文件1 > 文件2`(将文件1的内容覆盖到文件2) 

* ln 软链接 类似于windows内的快捷方式 主要存放了链接其他文件的路径

  `ln -s [源文件或目录] [软链接名]`(给源文件出创建一个软链接)

* history 查看已经执行的历史指令,也可以执行历史指令

  history 任意数量 查看最近执行的任意数量的指令

# 日期时间指令

* date 显示当前日期

  * date (显示当前日期)
  * date +%Y (显示当前年份)
  * date +%m (显示当前月份)
  * date +%d (显示当前是那一天)
  * date "+%Y-%m-%-d %H:%M:%S" (显示年月日时分秒)

* date -s 字符串时间

  设置系统当前时间 设置成2020-11-03 20:02:10

* cal 指令

  cal [选项]  (不加选项,显示本月月历)

# 搜索查找类

* find指令

  从指定目录向下递归的遍历其各个子目录,将满足的文件或者目录显示在终端

  基本语法

  * `find [搜索范围] [选项]`
  * -name<查询方式>  按照指定的文件名查找模式查找文件
  * -user <用户名> 查找指定用户名所有文件
  * -size <按照指定的文件大小查找文件>

  ![image-20210922093604184](https://gitee.com/IU_czx/images/raw/master/img/find%E6%8C%87%E4%BB%A4%E5%AE%9E%E4%BE%8B.png)

* locate指令

  ![image-20210922093827105](https://gitee.com/IU_czx/images/raw/master/img/locate%E6%8C%87%E4%BB%A4.png)

* which指令查看某个**指令**在哪个目录下

* grep 和管道符号 |

  grep过滤查找,管道符,"|"表示将前一个命令的处理结果输出传递给后面的命令处理

  基本语法

  * grep [选项] 查找内容 源文件

  * 常用选项

    -n :显示匹配及行号

    -i 忽略字母大小写

  * eg `grep -n Linux 课堂笔记.txt`

# 压缩和解压类

* gzip/gunzip 指令

  gzip用于压缩文件 gunzip 用于解压的

* zip/unzip

  * zip

    zip用于压缩文件 unzip用于解压的 在项目打包发布中很有用

    `zip [选项] xxx.zip 将要压缩的内容` (压缩文件和目录的命令)

    unzip [选项] xxx.zip (解压缩文件)

    -r 递归压缩,即压缩目录

  * unzip

    -d<目录>: 指定解压后文件的存放目录
  
* tar 指令

  打包指令 最后打包的是.tar.gz的文件

  基本语法

  `tar [选项] XXX.tar.gz 打包的内容`

  选项

  -c 产生.tar打包文件

  -v 显示详细信息

  -f 指定压缩后的文件名

  -z 打包同时压缩

  -x 解包.tar文件

  eg: tar -zcvf 1.tar.gz mytest

# shell编程

> shell是一个命令行解释器,他为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序
>
> 用户可以用shell来启动,挂起,停止甚至是编写一些程序

  ## 脚本格式要求

1. 脚本以 `#!/bin/bash` 开头
2. 脚本需要有可执行权限

## 脚本常用的执行方式

1. 输入脚本的绝对路径或相对路径

   首先赋予helloworld.sh脚本 `+x`权限,再执行脚本

   `chmod u+x hello.sh` 加权限

   `chmod u-x hello.sh` 取消权限

2. sh+脚本

   不需要赋予脚本+x权限,直接执行即可

## Shell变量介绍

1. shell变量分为 系统变量和用户自定义变量
2. 系统变量: $HOME $PWD $SHELL $USER等等
3. 显示shell中所有的变量:set

## shell变量的定义

基本语法

1. 定义变量: 变量=值 (==不要加空格==)
2. 撤销变量: unset 变量
3. 声明静态变量: readonly变量 注意不能unset

定义变量的规则

1. 变量名可以由字母,数字和下划线组成,但是不能以数字开头
2. 等号两侧不能有空格
3. 变量名称一般习惯为大写
4. "$A",\`date`,$(),可以传输变量

## 设置环境变量

1. export 变量名=变量值 (将shell变量输出为环境变量)
2. source 配置文件 (让修改后的配置信息立即生效)
3. echo $变量名 (查询环境变量的值)

## 注释

单行注释 #

多行注释 

```bash
:<<!
	内容
!
```

## 位置参数变量

基本语法

1. `$n`    10以上的参数需要加 ${n}
2. `$*`     这个变量代表命令行中的所有参数,`$*`把所有的参数看成一个整体
3. `$@`     这个变量代表命令行中的所有参数,不过`$@`把每个参数区分对待
4. `$#`     这个变量代表命令行中所有参数的的个数

```bash
#!/bin/bash
A=$(date)
echo $A
echo "$0 $1 $2"
echo "所有的参数 $*"
echo "$@"
echo "参数的个数:$#"
```

运行结果

```bash
sh test.sh 100 200 300
Wed Sep 22 19:19:07 CST 2021
test.sh 100 200
所有的参数 100 200 300
100 200 300
参数的个数:3
```

## 预定义变量

> shell设计者事先已经定义好的变量 可以直接shell脚本中使用

基本语法

1. `$$`  当前进程的进程号(PID)
2. `$!`  后台运行的最后一个进程的进程号(PID)
3. `$?`  最后一次执行的命令的返回状态,如果这个变量值为0,证明上一个命令正确执行,否则就是不正确

## 运算符

1. `$((运算式))`或`$[运算式]` 或 `expr m + n`
2. expr运算符之间要有空格
3. expr \\*,/,%   乘,除,取余
4. 如果要用expr,赋值需要使用  `` 进行括起来

## 条件判断

1. 基本语法

   [ condition ] (注意condition前后要有空格)

   非空返回true,可用 $? 验证 (0为true 1为false)

   实例:[ condition ] && echo ok || echo notbok

   ![Linux条件判断](https://gitee.com/IU_czx/images/raw/master/img/Linux%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD.png)

   ```bash
   #!/bin/bash
   if [ 5 -lt 7 ]
   then echo "你真棒"
   fi  #fi为结束
   ```

   ## 流程控制

### if判断

   ![image-20210925093456972](https://gitee.com/IU_czx/images/raw/master/img/Linux%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6.png)

   ```bash
   if [ $1 -gt 60 ]
   then echo "及格了"
   elif [ $1 -lt 60 ]
   then echo "对不起,请再接再厉"
   fi
   ```

### case分支

   ![image-20210925094307451](https://gitee.com/IU_czx/images/raw/master/img/if%E5%88%A4%E6%96%AD.png)

   ```bash
   #!/bin/bash
   
   case $1 in
   1)
   echo "今天星期一"
   ;;
   2)
   echo "今天星期二"
   ;;
   3)
   echo "今天星期三"
   ;;
   4)
   echo "今天星期四"
   ;;
   5)
   echo "今天星期五"
   ;;
   *)
   echo "其余时间都是周末"
   ;;
   esac
   
   ```

### for 循环

   ![image-20210925095524698](https://gitee.com/IU_czx/images/raw/master/img/for%E5%BE%AA%E7%8E%AF.png)

```bash
#!/bin/bash

#我们在使用$*的时候,加上"",这个时候所有参数都是一个整体,这个for循环只会执行一次
for i in "$*"
do
        echo $i
done

#如果是使用 $@ ,这时候,$@会将参数看成独立的个体 for循环会依照参数的个数执行相对应的次数
for i in "$@"
do
        echo $i
done
```

```bash
#!/bin/bash
SUM=0
for((i=0;i<=$1;i++))
do
        SUM=$[$SUM + $i]
done

echo $SUM
```

上述两个例子需要好好看看

## shell 命令行

1. 命令太长时,使用 `\` 可以切换到下一行输入

2. shift [N]  可以移走参数 [N] 代表移走参数的数量

3. 添加权限后的shell脚本和没添加shell脚本的区别

   ![image-20210926150229229](https://gitee.com/IU_czx/images/raw/master/img/%E6%B7%BB%E5%8A%A0%E6%9D%83%E9%99%90%E5%90%8E%E7%9A%84%E5%8C%BA%E5%88%AB.png)

4. declare [options] [name=value]  声明并初始化变量,设置他们的属性

   -a  声明为数组

   -f  声明为函数

   -i  声明一个整数

   -r 声明为只读的变量

   -x 表示变量可以被子进程访问,称为全局变量
   
5. 字符串比较

   ![image-20210926151356031](https://gitee.com/IU_czx/images/raw/master/img/%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%AF%94%E8%BE%83.png)
   

# LinuxC语言开发工具

## 函数介绍

### printf函数

![image-20211014082835813](https://gitee.com/IU_czx/images/raw/master/img/C%E8%AF%AD%E8%A8%80Printf%E5%87%BD%E6%95%B0.png)

### scanf函数说明

![image-20211014084005491](https://gitee.com/IU_czx/images/raw/master/img/scanf%E5%87%BD%E6%95%B0%E8%AF%B4%E6%98%8E.png)

### getchar参数

![image-20211014084455353](https://gitee.com/IU_czx/images/raw/master/img/getchar%E5%87%BD%E6%95%B0.png)

### putchar函数说明

![image-20211014084543302](https://gitee.com/IU_czx/images/raw/master/img/putchar%E5%87%BD%E6%95%B0%E8%AF%B4%E6%98%8E.png)

## 使用gcc

> 命令 `gcc [参数] 要编译的文件 [参数] [目标的文件]`

## gcc编译流程

### 00 支持编译的一些源文件

![image-20211014083356471](https://gitee.com/IU_czx/images/raw/master/img/gcc%E6%94%AF%E6%8C%81%E7%BC%96%E8%AF%91%E7%9A%84%E6%BA%90%E6%96%87%E4%BB%B6.png)



### 01-编写源代码

在这写入你的源代码

### 02-预处理阶段

使用 `-E`参数进行控制 使得在预处理阶段停止编译过程

### 03-编译阶段

1. 检查代码的规范性,是否有语法错误
2. 翻译成汇编语言
3. 可以使用  `-S`控制生成汇编代码

### 04-汇编阶段

* 将汇编代码转换为`.o`的二进制代码

### 05-链接阶段

将我们使用的库函数链接起来

![image-20211014083920555](https://gitee.com/IU_czx/images/raw/master/img/gcc%E9%93%BE%E6%8E%A5%E9%98%B6%E6%AE%B5.png)

## gcc编译器的主要参数

### 总体参数

![image-20211014084050366](https://gitee.com/IU_czx/images/raw/master/img/gcc%E7%BC%96%E8%AF%91%E5%99%A8%E7%9A%84%E4%B8%BB%E8%A6%81%E5%8F%82%E6%95%B0.png)

---

如果是引入自己定义的库 

需要 `#include "my.h"`这么写,这样就不需要添加`-L`参数了

### gcc的常用警告和出错参数

![image-20211014084649690](https://gitee.com/IU_czx/images/raw/master/img/gcc%E7%9A%84%E5%B8%B8%E7%94%A8%E8%AD%A6%E5%91%8A%E5%92%8C%E5%87%BA%E9%94%99%E5%8F%82%E6%95%B0.png)

---

eg:`gcc 3-6.c –o 3-6 –pedantic`

### 优化参数

![image-20211014085124129](https://gitee.com/IU_czx/images/raw/master/img/%E4%BC%98%E5%8C%96%E5%8F%82%E6%95%B0.png)

eg `gcc 3-8.c -o 3.8 -O2`

案例

设计一个程序，要求循环8亿次左右，每次都有一些可以优化的加减乘除运算。比较gcc的编译参数“-On”优化程序前后的运行速度

![image-20211014085459682](C:\Users\15461\AppData\Roaming\Typora\typora-user-images\image-20211014085459682.png)

以下场景不需要使用优化参数

1. 开发环境下
2. 资源受限下
3. 跟踪调试时

## 函数库

> 函数库是一组预先编译好的函数的集合，库文件的名字总是以lib开头.

### 静态库

![image-20211014085916390](https://gitee.com/IU_czx/images/raw/master/img/%E9%9D%99%E6%80%81%E5%BA%93.png)

