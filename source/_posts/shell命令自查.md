---
title: shell命令自查
date: 2018-09-13 15:06:04
tags: 
- shell
categories:
- 学习
---

- getopts
- grep && egrep
- $读取命令行参数
- chmod
- sort
- uniq
- wc 
- cut

<!-- more -->

> ### getopts

```bash
#!/bin/bash
 
while getopts "a:b:cdef" opt; do
  case $opt in
    a)
      echo "this is -a the arg is ! $OPTARG" 
      ;;
    b)
      echo "this is -b the arg is ! $OPTARG" 
      ;;
    c)
      echo "this is -c the arg is ! $OPTARG" 
      ;;
    \?)
      echo "Invalid option: -$OPTARG" 
      ;;
  esac
```

getopts的使用形式是：`getopts option_string variable`

getopts一共有两个参数，` test.sh -a hello`第一个是`-a`这样的选项，第二个参数是 `hello`这样的参数。

option_string之间可以直接相连，把`:`加在某个选项后面表示这个选项必须带有参数

 例如：`getopts ahfvc: option`表明选项a、h、f、v可以不加实际值进行传递，而选项c必须取值。使用选项取值时，必须使用变量**OPTARG**保存该值。

> ### grep

 **grep命令使用正则表达式来搜索文本，并且把匹配的文本打印出来**。

grep [options]pattern [file]

option表示选项，pattern表示匹配的模式。file表示一系列文件名。

常用选项：

-c  只打印匹配的文本行的函数，不显示文本内容。

-i   匹配时忽略字母大小写

-h  当搜索多个文件，不显示匹配文件名前缀。

-l   只列出含义匹配的文本行的文件的文件名，不显示其具体匹配的内容。

-n  列出所有匹配的文本行，并显示行号

-s   不显示关于不存在或无法读取文件的错误信息

-v   只显示不匹配的文本行。

-w  匹配整个单词

-x   匹配整个文本行

-r   递归搜索，不仅搜索当前目录，还有各级子目录

**-q   用于if逻辑判断**

-q 参数，本意是 Quiet; do not write anything to standard output.  Exit immediately with zero status if any match is found, even if an error was detected.   中文意思为，安静模式，不打印任何标准输出。如果有匹配的内容则立即返回状态值0。

**<u>正则表达式</u>**

**1）行首定位符 "^"**

用来匹配行首的字符。表示行首的字符是^后面的那个字符。

行首定位符位于所作用的字符之前

例如：

```bash
#列出/etc目录中的以字母po开头的文件名
str=`ls /etc | grep "^po"`
echo"$str"
```

 **2）行尾定位符"$"**

作用：定位文本行的末尾。

行尾定位符位于所作用的字符之后。

```bash
#列出/etc目录中以conf结尾的文件名
str=`ls /etc | grep "conf$"`
echo"$str"
```

精确匹配一个文本行：`^cat$` 完全匹配cat的文本行

`^$`:匹配所有空行

单独的^和$没有任何意义，因为任何一个文本行都有开头和结尾。

 **3）单个字符匹配”.”**

圆点`.`用来匹配任意单个字符。包括空格，但不包括换行符\n。当使用`.`后，意味着该位置一定有一个字符，无论他是什么字符。

(可以连续使用..来匹配多个字符，如l..p，匹配含义字母l，然后是两个任意字符，再接着是字母p的字符串)   

**4） 限定符“\*”**

限定符本身不代表任何字符，用来指定其前面的一个字符必须重复出现多次才能满足匹配。而星号表示匹配其前导字符的任意次数，包括0次。

**5） 字符集匹配“[]”**

只要某个字符串在方括号所在的位置上出现了方括号中的任意一个字符，就满足匹配规则。

对于连续的数字或字母，可使用连字符-来表示一个范围。

如：[a-f]表示匹配a到f中的任意一个字母

[0-9]匹配任意单个数字

 **6）字符集不匹配“[^]”**

> ### egrep

(egrep命令默认使用扩展正则表达式)

**1 ）限定符“+”**

“+”限定前面的字符至少出现一次。

\#筛选以字符串“ss”开头，后面至少紧跟着1个字符“s”的文本行

```bash
#筛选以字符串“ss”开头，后面至少紧跟着1个字符“s”的文本行
str=ls /etc | egrep "^sss+"
echo"$str"
```

结果：sssd

 **2）限定符“？”**

限定前面的字符最多只出现一次。

```bash
#筛选以字符串“ss”开头，后面跟着0或者1个s的文本行
str=ls /etc |egrep "^sss?"
echo"$str"
```

结果：ssh,ssl,sssd

 **3）竖线“|”和圆括号“()”**

竖线|表示多个正则表达式之前或的关系

圆括号表示一组可选值得集合。

竖线和圆括号经常一起使用，表示一组可选值。

```bash
#筛选含有字符串“ssh”、“ssl”或者以字符串“yum”开头的文本行
str=ls /etc |egrep "(ssh|ssl|^yum)"
echo"$str"
```

> ### $读取命令行参数

```bash
#all params 全部参数
echo $@
#all params  全部参数
echo $*
#length of params 参数的长度
echo $#
#first param 第一个参数
echo $1
#last param 最后一个参数
echo ${@:${#@}}
#last 2 param 最后两个参数
echo ${@:${#@}-1}
#last 2nd param 倒数第二个参数
echo ${@:${#@}-1:1}
#from 2nd to last param 从第二个到最后一个参数
echo ${@:2}
#from 2nd, count 2 从第2个参数开始，连续2个参数
echo ${@:2:2}
```

> ### chmod

chmod [可选项]  <mode>  <file...>

```bash
可选项：
  -c, --changes          like verbose but report only when a change is made (若该档案权限确实已经更改，才显示其更改动作)
  -f, --silent, --quiet  suppress most error messages  （若该档案权限无法被更改也不要显示错误讯息）
  -v, --verbose          output a diagnostic for every file processed（显示权限变更的详细资料）
       --no-preserve-root  do not treat '/' specially (the default)
       --preserve-root    fail to operate recursively on '/'
       --reference=RFILE  use RFILE‘s mode instead of MODE values
  -R, --recursive        change files and directories recursively （以递归的方式对目前目录下的所有档案与子目录进行相同的权限变更)
       --help		显示此帮助信息
       --version		显示版本信息
mode ：
权限设定字串，详细格式如下 ：
[ugoa...][[+-=][rwxX]...][,...]，
 
其中
[ugoa...]
u 表示该档案的拥有者，g 表示与该档案的拥有者属于同一个群体(group)者，o 表示其他以外的人，a 表示所有（包含上面三者）。
[+-=]
+ 表示增加权限，- 表示取消权限，= 表示唯一设定权限。
[rwxX]
r 表示可读取，w 表示可写入，x 表示可执行，X 表示只有当该档案是个子目录或者该档案已经被设定过为可执行。
 	
file...
文件列表（单个或者多个文件、文件夹）

```

#### **数字权限使用格式**

在这种使用方式中，首先我们需要了解数字如何表示权限。 首先，我们规定 数字 4 、2 和 1表示读、写、执行权限（具体原因可见下节权限详解内容），即 r=4，w=2，x=1 。此时其他的权限组合也可以用其他的八进制数字表示出来，如： rwx = 4 + 2 + 1 = 7 rw = 4 + 2 = 6 rx = 4 +1 = 5 即

若要同时设置 rwx (可读写运行） 权限则将该权限位 设置 为 4 + 2 + 1 = 7 若要同时设置 rw- （可读写不可运行）权限则将该权限位 设置 为 4 + 2 = 6 若要同时设置 r-x （可读可运行不可写）权限则将该权限位 设置 为 4 +1 = 5

上面我们提到，每个文件都可以针对三个粒度，设置不同的rwx(读写执行)权限。即我们可以用用三个8进制数字分别表示 拥有者 、群组 、其它组( u、 g 、o)的权限详情，并用chmod直接加三个8进制数字的方式直接改变文件权限。语法格式为 ：`chmod <abc> file...`

```bash
其中
a,b,c各为一个数字，分别代表User、Group、及Other的权限。
相当于简化版的
chmod u=权限,g=权限,o=权限 file...
而此处的权限将用8进制的数字来表示User、Group、及Other的读、写、执行权限
```

范例：

- 设置所有人可以读写及执行

```bash
chmod 777 file  (等价于  chmod u=rwx,g=rwx,o=rwx file 或  chmod a=rwx file)
```

- 设置拥有者可读写，其他人不可读写执行

```bash
chmod 600 file (等价于  chmod u=rw,g=---,o=--- file 或 chmod u=rw,go-rwx file )
```

常见的权限表示形式有：

```bash
-rw------- (600)      只有拥有者有读写权限。
-rw-r--r-- (644)      只有拥有者有读写权限；而属组用户和其他用户只有读权限。
-rwx------ (700)     只有拥有者有读、写、执行权限。
-rwxr-xr-x (755)    拥有者有读、写、执行权限；而属组用户和其他用户只有读、执行权限。
-rwx--x--x (711)    拥有者有读、写、执行权限；而属组用户和其他用户只有执行权限。
-rw-rw-rw- (666)   所有用户都有文件读、写权限。
-rwxrwxrwx (777)  所有用户都有读、写、执行权限。

# 实际上，后九位每个位置的意义（代表某个属组的某个权限）都是固定的，如果我们将各个位置权限的有无用二进制数 1和 0来代替，则只读、只写、只执行权限，可以用三位二进制数表示为
r-- = 100
-w- = 010
--x = 001
--- = 000

# 实际上，我们可以将所有的权限用二进制形式表现出来，并进一步转变成八进制数字
rwx = 111 = 7
rw- = 110 = 6
r-x = 101 = 5
r-- = 100 = 4
-wx = 011 = 3
-w- = 010 = 2
--x = 001 = 1
--- = 000 = 0

-rw------- =  600
-rw-rw-rw- =  666
-rwxrwxrwx = 777
```

**关于第一位最高位的解释**： 上面我们说到了权限表示中后九位的含义，剩下的第一位代表的是文件的类型，类型可以是下面几个中的一个：

```bash
d代表的是目录(directroy)
-代表的是文件(regular file)
s代表的是套字文件(socket)
p代表的管道文件(pipe)或命名管道文件(named pipe)
l代表的是符号链接文件(symbolic link)
b代表的是该文件是面向块的设备文件(block-oriented device file)
c代表的是该文件是面向字符的设备文件(charcter-oriented device file)
```

> ### sort

**1) sort的工作原理**

sort将文件的每一行作为一个单位，相互比较，比较原则是从首字符向后，依次按ASCII码值进行比较，最后将他们按升序输出。

**2) sort的-u选项**

输出行中去除重复行。

**3) sort的-r选项** 

sort默认的排序方式是升序，如果想改成降序，就加个-r就搞定了。

**4) sort的-o选项**

由于sort默认是把结果输出到标准输出，所以需要用重定向才能将结果写入文件，形如sort filename > newfile。

但是，如果你想把排序结果输出到原文件中，用重定向可就不行了。

```bash
[rocrocket@rocrocket programming]$ sort -r number.txt > number.txt
[rocrocket@rocrocket programming]$ cat number.txt
[rocrocket@rocrocket programming]$
```

看，竟然将number清空了。

就在这个时候，-o选项出现了，它成功的解决了这个问题，让你放心的将结果写入原文件。这或许也是-o比重定向的唯一优势所在。

```bash
[rocrocket@rocrocket programming]$ sort -r number.txt -o number.txt
[rocrocket@rocrocket programming]$ cat number.txt
5
4
3
2
1
```

**5) sort的-n选项**

你有没有遇到过10比2小的情况。我反正遇到过。出现这种情况是由于排序程序将这些数字按字符来排序了，排序程序会先比较1和2，显然1小，所以就将10放在2前面喽。这也是sort的一贯作风。

我们如果想改变这种现状，就要使用-n选项，来告诉sort，“要以数值来排序”！

**6) sort的-t选项和-k选项**

如果有一个文件的内容是这样：

```bash
[rocrocket@rocrocket programming]$ cat facebook.txt
banana:30:5.5
apple:10:2.5
pear:90:2.3
orange:20:3.4
```

这个文件有三列，列与列之间用冒号隔开了，第一列表示水果类型，第二列表示水果数量，第三列表示水果价格。

那么我想以水果数量来排序，也就是以第二列来排序，如何利用sort实现？

幸好，sort提供了-t选项，后面可以设定间隔符。（是不是想起了cut和paste的-d选项，共鸣～～）

指定了间隔符之后，就可以用-k来指定列数了。

```bash
[rocrocket@rocrocket programming]$ sort -n -k 2 -t : facebook.txt
apple:10:2.5
orange:20:3.4
banana:30:5.5
pear:90:2.3
```

我们使用冒号作为间隔符，并针对第二列来进行数值升序排序，结果很令人满意。

> ### uniq

```bash
用法：uniq [选项]... [文件]  
从输入文件或者标准输入中筛选相邻的匹配行并写入到输出文件或标准输出。  
不附加任何选项时匹配行将在首次出现处被合并。   
长选项必须使用的参数对于短选项时也是必需使用的。  
 -c, --count              //在每行前加上表示相应行目出现次数的前缀编号  
 -d, --repeated          //只输出重复的行  
 -D, --all-repeated      //只输出重复的行，不过有几行输出几行  
 -f, --skip-fields=N     //-f 忽略的段数，-f 1 忽略第一段  
 -i, --ignore-case       //不区分大小写  
 -s, --skip-chars=N      //根-f有点像，不过-s是忽略，后面多少个字符 -s 5就忽略后面5个字符  
 -u, --unique            //去除重复的后，全部显示出来，根mysql的distinct功能上有点像  
 -z, --zero-terminated   end lines with 0 byte, not newline  
 -w, --check-chars=N      //对每行第N 个字符以后的内容不作对照  
 --help              //显示此帮助信息并退出  
 --version              //显示版本信息并退出 
```

> ### wc

```bash
wc [-clw][--help][--version][文件...]
```

- -c或--bytes或--chars 只显示Bytes数。
- -l或--lines 只显示行数。
- -w或--words 只显示字数。
- --help 在线帮助。
- --version 显示版本信息。

> ### cut

```bash
cut -c -b -f -d -s
```

- -c character

- -b byte

- -f field

- -d delimiter分隔符

- 　-c 和 -f 参数可以跟以下子参数：

  　　**N 第N个字符或字段**

  　　**N- 从第一个字符或字段到文件结束**

  　　**N-M 从第N个到第M个字符或字段**

  　　**-M 从第一个到第N个字符或字段** 

----------

### 参考资料

[shell getopts 用法](https://blog.csdn.net/xluren/article/details/17489667)

[《sort帮你排序》-linux命令五分钟系列之二十六 作者 roc)](http://roclinux.cn/?p=1350)

[Linux权限详解（chmod、600、644、666、700、711、755、777、4755、6755、7755）](https://blog.csdn.net/u013197629/article/details/73608613)

[shell之正则表达式](https://blog.csdn.net/qq504196282/article/details/52995198)

