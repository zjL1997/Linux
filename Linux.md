# Linux

## 1 基础指令篇

### 1.1 linux的目录结构

linux的文件系统采用层级式树状目录结构，最上层是根目录 ”\“ , 然后在此目录下在创建其他的目录。

**在Linux中一切皆为文件**

![image-20200626100901873](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626100901873.png)



- **bin**：常用的指令
- sbin：管理员使用的指令
- **home**：存放普通用户的主目录
- **ropt**：管理员的用户主目录
- lib：系统开机所需要的动态链接库，相当于windos中的dll文件
- **usr**：应用程序安装的目录，相当于window的program file目录
- **boot**：启动linux时使用的一些核心文件
- proc、srv、sys：内核相关目录。别动
- temp：临时目录
- dev：将硬件映射为文件来管理
- **media**：U盘、光驱等设别的挂载目录
- **etc**：存放配置文件
- **opt**：安装的软件的存放目录
- **usr/local**：软件安装的安装目录
- **var**：经常被修改的文件

![image-20200626201729663](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626201729663.png)

总结一下：

（1）linux有且只有一个根目录

（2）linux各个目录存放的内容是提前规定好的

（3）linux以文件形式管理设备，故而一切皆文件

（4）要形成linux的目录树结构

### 1.2 vi和vim编辑器

​		所有linux系统都会内置  vi文本编辑器。vim具有程序编辑能力，可以看做时vi的增强版本，可以主动以字体颜色辨别语法的正确性。

​	vi和vim的三种模式

- 正常模式

在正常模式下，可以使用快捷键。以vim打开一个档案就直接进入一般模式了。

该模式中，可以使用上下左右按键来移动光标，可以删除字符或整行来处理内容，可以复制粘贴。

- 插入（编辑）模式

在该模式下，程序员可以输入内容。

一般来说按下i即可进入。还可使用iI oO aA rR 中的任意一个即可进入。

- 命令行模式

该模式下，可以提供完成读取、存盘、替换、离开vim、显示行号等动作在此模式中完成。

如何进入：插入模式下，点击esc先退出进入一般模式，再输入:或/，即可进入命令行模式。

输入 :wq 保存文件



![image-20200626115047905](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626115047905.png)

> vim的快捷键（只有在正常模式下才能使用）
>
> （1）拷贝当前行：yy拷贝行，粘贴为p。 nyy表示赋值光标下的n行，按p进行粘贴。
>
> （2）删除当前行：dd删除行，ndd删除当前光标下的n行。
>
> （3）在文件中查找单词：进入命令行模式，/关键字，回车。即可查询，输入n，查找下一个
>
> （4）设置（取消）文件的行号：在命令行模式下输入set nu / set nonu
>
> ![image-20200626142402053](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626142402053.png)
>
> （5）快速回到文档末尾：G     快速回到文档首行：gg     均在正常模式下执行
>
> （6）撤销操作：正常模式下输入u
>
> （7）将光标移动到指定的行：打开set nu后，先输入n，再输入shift+g

### 1.3 关机重启以及用户登录注销

关机重启指令：

- shutdown -h now：表示立即关机
- shutdown -h 1：表示1分钟后关机
- shutdown -r now：立即重启计算机
- halt：关机
- reboot：重启计算机
- sync：把内存数据同步到磁盘

关机或重启时，应当先执行sync，将数据保存后再进行关机。

用户的登录和注销：

- 登录时尽量少使用root

- logout：退出当前用户

### 1.4 用户管理

**基本介绍**：

![image-20200626144513978](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626144513978.png)



- linux系统是一个多用户多任务的操作系统，任何要使用系统资源的用户都必须先向系统管理员申请一个账号，然后以这个账号的身份进入系统。
- 一个用户至少属于一个组，一个用户对应有一个home目录。

**用户操作**：

-  基本语法：

  (1)创建用户：```useradd 【选项】 用户名```

![image-20200626145119904](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626145119904.png)、

创建用户后会自动创建和用户同名的home目录

也可以通过 ```useradd -d 指定目录 新的用户名``` 给新创建的用户指定home目录

​	(2)设置用户密码：```passwd 用户名```

​	(3) 删除用户：```userdel 用户名```

​		删除用户但是保存home目录：```userdel 用户名```

​		删除用户以及其home目录：```userdel -r 用户名```

一般而言都要保留用户的home目录。

（4）查询用户信息：```id 用户名```

![image-20200626150538443](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626150538443.png)

（5）切换用户：```su - 要切换的用户名```

![image-20200626150839299](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626150839299.png)

返回到原来的用户：exit

![image-20200626151055799](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626151055799.png)



**用户组**：

​	类似于角色，用来管理具有共性的用户。

基本语法：

创建一个组：```groupadd 组名称```

删除组：```groupdel 组名称```

创建用户时，指定用户存放的组：```useradd -g 组名称 用户名```

修改用户组：```usermod -g 用户组 用户名```

**用户相关文件：**

- /etc/passwd：用户的配置文件，记录用户的各种信息

每行的含义：用户名：口令：用户标识号：组标识号：注释性描述：主目录：登录shell

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626152708783.png" alt="image-20200626152708783" style="zoom:150%;" />

> x为口令或密码

-  /etc/shadow：口令的配置文件

![image-20200626152906832](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626152906832.png)

- /etc/group：组的配置文件，记录linux包含的组的信息

每行含义：组名：口令：组标识号：组内用户列表

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626152937928.png" alt="image-20200626152937928" style="zoom:150%;" />

### 1.5 实用指令

**linux的运行级别：**

![image-20200626153355940](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626153355940.png)

**指定运行级别：**

init [0123456]

现阶段运行级别已经别target代替。主要有两个targets

 ==multi-user.target: analogous to runlevel 3==

 ==graphical.target: analogous to runlevel 5==

但是init指令还可使用。

**面试题：**如何找回丢失的root密码？

①进入单用户模式，然后修改root密码。

开机—>在引导时输入 enter键—>看到一个界面输入 e —>看到一个新的页面，选中第二行（编辑内核） 再输入 e—>在这行最后输入1 再输入回车键—>再次输入b，这时就会进到单用户模式。

该操作必须在linux机房中进行操作，不可远程操作。

**帮助指令：**想要了解一个不熟悉的指令时

**基本语法**：

man [命令或配置文件]

![image-20200626155346353](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626155346353.png)

help [要查看的指令]

![image-20200626155600386](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626155600386.png)

百度更直接。

### 1.6 文件目录类指令

- pwd指令：显示当前工作目录的绝对路径

![image-20200626160103390](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626160103390.png)

- ls指令：

![image-20200626160354256](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626160354256.png)

ls -a [目录]：显示当前目录所有的文件和目录，包括隐藏的

![image-20200626160408638](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626160408638.png)

ls -l [目录]：以列表的方式显示列表

![image-20200626160449067](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626160449067.png)



- cd指令：切换目录

cd ~: 回到自己的home目录 

cd..：回到当前目录的上一级目录

- mkdir：用于创建目录。基本语法：```mkdir [] 要创建的目录```

mkdir -p 要创建的目录：创建多级目录（创建多个不存在的目录）

- rmdir：删除空目录

rmdir [] 目录：删除空目录

rm -rf：删除非空目录

- touch：创建空文件

touch 空文件名

![image-20200626165027195](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626165027195.png)



- ###### ==cp指令==：拷贝文件到指定目录

基本语法：cp 【】 source dest

cp -r source dest：递归复制整个文件夹

![image-20200626165502088](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626165502088.png)

\cp：强制覆盖

- rm指令：移除文件或者目录

基本语法：rm 文件或目录名

![image-20200626170151492](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626170151492.png)

删除时无需提示：rm -f 文件或目录名

递归删除整个文件夹: rm -r 要删除的文件夹

![image-20200626170423313](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626170423313.png)

- mv：移动文件与目录或重命名

mv oldfilename newfilename：重命名文件

mv 要移动的文件 移动到的文件目录：移动文件

- cat指令：查看文件内容

基本语法：cat 【】要查看的文件

![image-20200626171247195](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626171247195.png)

cat -n 要查看的文件：显示行号

![image-20200626171223438](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626171223438.png)

cat只能浏览，不能修4改。为了浏览方便，在cat指令之后加上|more：进行分页显示。

- more：全屏分页显示

more 要查看的文件：

enter按行向下 空格键按页向下

ctrl+b：上一页  ctrl+f：下一页

- less ：全屏显示，边显示边读取

less 要查看的文件：查看多少读取多少，适用于大文件的查看

快捷键：

![image-20200626172529089](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626172529089.png)

- ```>指令和>>指令```

```>指令```：输出重定向，覆盖写

```>>指令```：追加

ls -l > 文件：将列表内容写入文件中，覆盖式写入

ls -al >> 文件：将列表内容追加到文件末尾

- echo：输出内容到控制台

echo 【】输出内容

![image-20200626173933228](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626173933228.png)

- head：用于显示文件的开头部分内容，默认显示前10行

head -n N 文件：显示文件的前N行数据

- tail：显示文件中的尾部内容

  tail 文件：查看文件后10行

  tail -n N 文件：查看文件后N行

  **tail -f 文件：实时追踪文件的所有更新**（使用ctrl+c退出）

- ln：软链接指令，存放了链接其他文件的路径

ln -s 源文件或目录 软链接名称

![image-20200626174853481](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626174853481.png)

pwd查看软链接目录时，查看的还是软链接所在的目录

- history：查看已经执行过的历史命令，也可以执行历史命令

！历史中的指令行数：执行该行指令

### 1.7 时间日期类指令

- **date指令-显示当前日期**

date：显示当前时间![image-20200626175737757](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626175737757.png)

date "+%Y"（M/D）：显示当前年份(月/日)![image-20200626175923243](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626175923243.png)

date "+%Y %m %d %H %M %S"：按拼接顺序显示![image-20200626180116511](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626180116511.png)

设置系统时间：date -s ”设置的时间（2020-10-10 11:22:22）“

- cal：查看日历的指令

cal ：![image-20200626180310280](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626180310280.png)

cal 年份：显示一整年的日历

![image-20200626180350313](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626180350313.png)

### 1.8 搜索查找类

- **find**指令：从指定目录向下递归地遍历其各个子目录，将满足条件的文件或者目录显示在终端。

基本语法：```find  搜索范围  选项 文件名```

![image-20200626180703624](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626180703624.png)

文件大小（+N：大于多少，-N：小于多少，=N：等于多少）

find 范围 *.txt：使用通配符查找

- **locate**指令：可以快速定位文件路径，利用事先建立的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件。locate指令无需遍历整个文件系统，所以其速度比较快，但是必须定期更新locate数据库

第一次运行前必须使用updatedb指令创建locate数据库。

- **grep**指令和管道符号

grep：过滤查找

基本语法：grep 【选项】 查找内容 源文件

![image-20200626181910324](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626181910324.png)

管道符 ‘|’：表示将前一个命令的处理结果输出传递给后面的命令处理。

### 1.9 压缩和解压缩指令

- gzip：用于压缩文件

基本语法：gzip 文件：将文件压缩为*.gz

![image-20200626182642021](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626182642021.png)

压缩后原文件消失。

- gunzip：用于解压缩文件

基本语法：gunzip *.gz：将 gz压缩文件解压

![image-20200626182656101](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626182656101.png)

解压缩后源文件消失。

- zip 用于压缩文件

基本语法：zip 【】 XXX.zip 将要压缩的内容：压缩文件和目录的命令

常用选项：-r：递归压缩，即压缩目录

- unzip：解压文件

基本语法：unzip 【】 XXX.zip ：解压缩文件

常用选项：-d 目录：指定解压缩后的文件存放目录

- **tar**：打包指令，最后打包的是 .tar.gz

基本语法：tar 【选项】 XXX.tar.gz  打包的内容：打包目录

选项说明：![image-20200626184028119](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626184028119.png)

压缩（-zcvf）：

![image-20200626184425601](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626184425601.png)

解压缩（-zxvf）：

![image-20200626184751189](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626184751189.png)

## 2 实操管理篇

### 2.1 组管理（重点难点）

linux组的基本介绍：每个用户必须属于一个组，不能独立于组外。

linux中的文件必须有四个属性：所有者，所在组，其他组

- 所有者：一般为文件的创建者，谁创建了这个文件，就自然成为了该文件的所有者。

（1）查看文件的所有者：指令**ls -ahl**

基本语法：ls -ahl  要查看的文件

![image-20200626191420445](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626191420445.png)

（2）修改文件所有者：指令**chown**（ch：change，own）

基本语法：chown 用户名 文件名

![image-20200626192527857](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626192527857.png)

注意：该文件的组并未变化

- 所在组

当一个用户创建了一个文件后，默认这个文件的所在组就是该用户所在的组。

（1）查看文件所在组的指令和查看所有者的指令一致
（2）修改文件所在组：指令**chgrp**

基本语法：chgrp 组名 文件名

![image-20200626193330728](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626193330728.png)

- 其他组

除文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组。

- 改变用户所在组

改变用户所在组：

① usermod -g 组名 用户名：

![image-20200626194012055](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626194012055.png)

② usermod -d 目录名 用户名 改变该用户登录的初始目录

### 2.2 权限管理

#### **基本介绍**

这里的权限主要是指文件和目录的权限，以一个文件为例，介绍权限：

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200626195859055.png" alt="image-20200626195859055" style="zoom:150%;" />

- 三种权限（rwx）

对于文件而言

​	r：表示可读

​	w：表示可写，即可以修改，但是不一定可以删除。要删除一个文件的前提条件是对于==该文件的目录有写权限才可以删除==。

​	x：表示可执行

对于目录而言：

​	r：表示可以查看该目录，可以使用ls查看

​	w：表示可以修改目录，在目录内创建+删除+重命名目录

​	x：表示可执行，可以进入该目录

#### **修改权限**

修改权限所使用的基本命令是```chmod``。

- 第一种方式：+、-、=变更权限

u：所有者	g：所有组	o：其他人 	a：所有人

（1）chmod u=rwx,g=rx,o=x 文件目录名：赋予权限

![image-20200627095042106](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627095042106.png)

（2）chmod o+w 文件目录名：添加权限

![image-20200627095221040](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627095221040.png)

（3）chmod a-x 文件目录名：删除权限

![image-20200627095307957](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627095307957.png)

- 第二种方式：通过数字变更权限

规则：r=4（100） w=2（010） x=1（001）   ==> rwx=7

chmod u=rwx,g=rx,o=x 文件目录名     ==》

chmod 751 文件目录名

![image-20200627095813259](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627095813259.png)

#### 修改文件所有者-chown

chown newowner file：改变一个文件的所有者

chown newowner:newgroup file：改变用户的所有者和所有组

chown newowner -R  file/dir： 如果是目录，则使其下所有子文件或目录递归生效

#### 修改文件所在组-chgrp

chgrp newgroup file：改变一个文件的所在组

chown newgroup  -R  file/dir： 如果是目录，则使其下所有子文件或目录递归生效

### 2.3 定时任务调度

**任务调度**：是指系统在某一个时间执行的特定命令或程序。

![image-20200627104435687](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627104435687.png)

**任务调度分类**：

​		①系统工作：有些重要的工作必须周而复始的进行。

​		②个别用户工作：个别用户可能希望执行某些程序进行备份。

**基本语法**：

​	crontab 【选项】

**常用选项**:
	-e：编辑crontab的定时任务

​	-l：查询crontab任务

​	-r：删除当前用户所有的crontab任务

service crond restart：重启任务调度

**如何使用**：

​	**（1）**如果只是简单的任务，可以不用写脚本，直接在crontab中加入任务即可。、

创建crontab：

![image-20200627105205095](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627105205095.png)

写入命令：

![image-20200627104947417](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627104947417.png)

![image-20200627105221817](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627105221817.png)

命令说明：

​	![image-20200627105643395](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627105643395.png)

![image-20200627105828773](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627105828773.png)

效果：

![image-20200627105338009](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627105338009.png)

​	**（2）**如果是比较复杂的任务，需要写好脚本（shell编程）

使用shell脚本：

① 先编写一个文件(.sh),，在其中写入命令（linux执行命令）。

② 给编写的sh文件一个可执行权限

③ crontab -e

④ 在crontab的编译器中指定每隔多长时间执行一次sh脚本文件。

⑤ 查看效果

### 2.4 linux磁盘分区和挂载

#### 分区基础

分区有两种方式：

（1）mbr分区：最多四个

（2）gpt分区：支持无限个分区，且容量较大

**windows下的磁盘分区**

![image-20200627111628143](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627111628143.png)



#### Linux分区

**介绍**：

（1）linux无论有几个分区，分给哪一个目录使用，它归根接地只有一个根目录，一个独立且唯一的文件结构，linux中每个分区都是用来组成整个文件系统的一部分。

（2）Linux采用了一种叫载入的处理方式，他的整个文件系统中包含了一整套的文件和目录，且将一个分区和一个目录联系起来，这时要载入的一个分区将使它的存储空间在一个目录下获得。

（3）示意图：![image-20200627112625694](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627112625694.png)



硬盘说明：

（1）Linux硬盘分为IDE和SCSI硬盘，目前基本上时SCSI硬盘，

（2）对于IDE硬盘，驱动器表示为hdx~。其中hd表示分区所在设备的类型，x为盘号。

~代表分区，前四个分区用数字1-4表示它们是主分区或扩展分区，从5开始就是逻辑分区。

（3）对于SCSI硬盘则标识为sdx~。其中sd表示分区所在设备的类型.

![image-20200627115248069](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627115248069.png)

查看分区情况：lsblk（老师不离开）

#### 如何增加一块硬盘

详细步骤可以上网查。

（1）虚拟机添加硬盘

（2）分区

（3）格式化

（4）挂载

（5）设置可以自动挂载，实现永久挂载

#### 磁盘情况查询

- 查询系统整体磁盘使用情况

基本语法：df -h

![image-20200627144918222](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627144918222.png)



 

- 查询指定目录的磁盘占用情况

基本语法：du -h /目录

查询指定目录的磁盘占用情况，默认为当前目录。

-s 指定目录占用大小汇总

-h 带计量单位

-a 含文件

--max-depth=1 子目录深度

-c 列出明细的同时，增加汇总值

![image-20200627145759127](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627145759127.png)

- 对于一个文件夹中进行查询

![image-20200627151506155](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627151506155.png)

统计文件夹中的文件数目： ls -l 文件位置 |grep "^-"|wc -l

![image-20200627151405720](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627151405720.png)

统计文件夹中的目录数目： ls -l 文件位置 |grep "^d"|wc -l

![image-20200627151447334](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627151447334.png)

统计文件夹下文件的个数，包括子文件夹中的： ls -lR 文件位置 |grep "^-"|wc -l

![image-20200627151747761](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627151747761.png)

统计文件夹下目录的个数，包含子文件夹的： ls -lR 文件位置 |grep "^d"|wc -l

![image-20200627152029642](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627152029642.png)

### 2.5 网络配置

原理图：

![image-20200627152529993](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627152529993.png)



- 查看网络ip和网关：在有界面的形式下做查看。

- 自动获取：在有界面的情况下操作，自动获取的ip地址每次都不一样。
- 修改配置文件更改ip：可以指定固定的ip地址

① 编辑 vi /etc/sysconfig/network-scripts/ifcfg-eth0

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627155041782.png" alt="image-20200627155041782" style="zoom:150%;" />

② 重启网络服务：service network restart

### 2.6 进程管理（重点）

#### 基本介绍

（1）Linux中，每个执行的程序都称为一个进程·。每个进程都分配一个id号。

（2）每一个进程，都会对应一个父进程，这个父进程可以复制多个子进程

（3）每个进程都可能以两种方式存在。前台和后台，所谓前台进程就是用户目前屏幕上可以进行操作的。后台进程则是实际在操作，但由于屏幕上无法看到的进程，通常使用后台方式执行。

（4）一般系统的服务都是以后台进程的方式存在，而且都会常驻在系统中。直到关机才结束。

- 显示系统执行的进程

ps指令：查看进程使用的指令

ps  -a：显示当前终端的所有进程

ps -u：以用户的格式显示进程信息

ps -x：显示后台进程的运行参数

综合指令：ps -aux

ps指令详解：

![image-20200627162754627](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627162754627.png)

ps -ef：查看进程的父进程

![image-20200627163154886](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627163154886.png)

pstree：查看进程树

基本语法：pstree 【】：可以更直观的查看进程信息

![image-20200627164348629](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627164348629.png)

常用选项：

-p：显示进程的PID

![image-20200627164434507](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627164434507.png)

-u：显示进程的所属用户·

![image-20200627164502285](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627164502285.png)

- 终止进程

kill 【】 进程号： 通过进程号杀死进程

常用选项：-9：表示强迫进程立即停止

killall 进程名称：通过进程名称杀死进程，也支持通配符，这在系统因负载过大而变得很慢时很有用。

#### 服务管理

**介绍**：==服务==（service）本质就是进程，但是是运行在后台的，通常都会监听某个端口，等待其他程序的请求。比如（mysql，sshd，防火墙等），因此，又将服务称为==守护进程==，这是Linux中非常重要的知识点。

![image-20200627165157554](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627165157554.png)

**service管理的指令：**

centOS7.0之前使用：service 服务名 【start|stop|restart|reload|status】

centOS7.0之后使用：systemctl  【start|stop|restart|reload|status】服务名

**示例：**

查看、关闭、重启防火墙？

查看：

![image-20200627170014867](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627170014867.png)

关闭：

![image-20200627170140387](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627170140387.png)

重启：

![image-20200627170224380](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627170224380.png)

细节：

①关闭或启用防火墙后，立即生效。

②这种方式只是临时生效，当重启系统后，还是要回归以前对服务的设置。如果希望设置某个服务自启动或关闭永久生效，要使用chkconfig

**查看服务名**：

方式1：使用setup -->系统服务就可以看到

> centos7之后有变化

方式2：/etc/init.d/服务名称

![image-20200627171036704](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627171036704.png)

**服务的运行级别：**

![image-20200627171225970](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627171225970.png)

centos7之后：

![image-20200627171314969](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627171314969.png)

运行级别由targets代替。

**指令**：chkconfig，可以给每个服务的各个运行级别设置自启动/关闭

基本语法：查看服务状态：

chkconfig --list|grep xxx

![image-20200627171815924](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627171815924.png)

> centos7中如果想要查看系统级别的服务状态，需要使用```systemctl list-unit-files```
>
> ![image-20200627172047453](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627172047453.png)

chkconfig 服务名 --list：查看一个服务的运行状态

chkconfig 【 --level n(0-6的数字，表示运行级别)】 服务名 on/off：设置某个服务在某个运行级别下是否自启动。不写level，所有状态都关闭或开启。

#### 动态监控进程

**介绍**：top，与ps很类似。top在执行一段时间后可以更新正在运行的进程。

**基本语法**：top 【】

![image-20200627173529202](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627173529202.png)

**常用选项**：

-u：查看特定用户的运行进程（top -u 用户名）

![image-20200627173650190](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627173650190.png)

-k：杀死特定的用户的进程（top -k 进程名）

-d：指定自动刷新的时间（默认是3秒）：top -d 10（10s刷新一次）

**互动指令**：先执行top，再直接点击以下指令

P：对于监控的进程使用PID大小排序

M：以内存的使用率排序

N：以PID排序

q：退出top

#### 监控系统网络情况

基本语法：netstat 【】

选项说明：

-an 按一定顺序排列输出

-p 显示哪个进程在调用

综合：netstat -anp

![image-20200627174620238](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627174620238.png)

监听特定服务的网络情况：netstat -anp|grep 服务名

![image-20200627174748990](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627174748990.png)

### 2.7 rpm包管理

**介绍**：rpm是一种用于互联网下载的打包和安装工具，他包含在某些Linux系统中，生成 .RPM扩展名的文件。类似于windows中的setup.exe，全称为RedHat软件包管理工具。、

**rpm**包的查询：rpm -qa|grep xx

![image-20200627180005489](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627180005489.png)



**查询**rpm软件的安装目录：rpm -ql 软件名

**卸载**rpm包：rpm -e rpm包的名称

**强制删除**：rpm -e --nodeps foo rpm包的名称

**安装rpm包**：

（1）先找到要安装的rpm包：到/media/ 目录下去查看，使用cp指令将rpm包拷贝到/opt/

目录下。

（2）切换到/opt/目录下，执行 rpm -ivh rpm包名称，即可安装。

### 2.8 yum

**介绍**：yum与rpm类似都是一种包管理器，yum基于rpm，是一个shell前端软件包管理器，能够从指定的服务器自动下载rpm包并且安装，可以自动处理依赖关系，并且一次安装所有依赖的软件包。

**基本指令：**

- 查询yum服务器是否有需要安装的软件

基本语法：yum  list |grep xx软件列表

![image-20200627181824314](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627181824314.png)

- 安装指定的yum包

基本语法：yun install xxx

> 使用yum的前提是需要联网。



## 3 JavaEE定制篇

### 3.1 概述

​	要使用linux进行JavaEE的开发，首先搭建好环境，包含jdk1.8、mysql数据库、tomcat以及idea或eclipse。

### 3.2 安装软件

- 第一种方式：

（1）在windows上下载linux版的软件，通过xftp将tar.gz文件传输到 /opt/ 目录下。

（2）解压缩文件（tar -zxvf xxx.tar.gz）

（3）进入解压后文件的bin目录，执行stratup.sh脚本文件，启动软件。

（4）有些软件需要配置环境变量（jdk）：vim  /etc/profile

（5）linux中的tomcat如果需要别外部访问，需要将防火墙的8080端口放行。

vim /etc/sysconfig/firewalld —>开放8080端口

![image-20200627185947702](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200627185947702.png)

然后重启防火墙。

> centos有很多改变，上网查询资料。

- 第二种方式：yum直接安装（受服务器资源限制，但是自动安装，较为方便）
- 第三种方式：在linux上使用docker安装镜像。



