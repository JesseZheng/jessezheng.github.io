---
title: Mac&Linux命令自查
date: 2018-07-15 17:29:42
tags:
- linux
- shell
categories:
- 学习
---

> ## Linux rm命令 删除文件夹

Linux删除目录很简单，很多人还是习惯用rmdir，不过一旦目录非空，就陷入深深的苦恼之中，现在使用rm -rf命令即可。

直接rm就可以了，不过要加两个参数-rf 即：`rm -rf 目录名字`

-r 就是向下递归，不管有多少级目录，一并删除

-f 就是直接强行删除，不作任何提示的意思

*注意事项：使用这个rm -rf的时候一定要格外小心，linux没有回收站的*

<!-- more -->

> ## Linux ls命令

**显示当前目录下非隐藏文件与目录:** `ls`

```
[root@localhost ~]# ls
anaconda-ks.cfg  install.log  install.log.syslog  satools
```

**显示当前目录下包括影藏文件在内的所有文件列表:**`ls -a`

```
[root@localhost ~]# ls -a
.   anaconda-ks.cfg  .bash_logout   .bashrc  install.log         .mysql_history  satools  .tcshrc   .vimrc
..  .bash_history    .bash_profile  .cshrc   install.log.syslog  .rnd            .ssh     .viminfo
```

**输出长格式列表:**`ls -l`

```
[root@localhost ~]# ls -1
anaconda-ks.cfg
install.log
install.log.syslog
satools
```

**水平输出文件列表:**`ls -m`

```
[root@localhost /]# ls -m

bin,boot, data, dev, etc, home, lib, lost+found, media, misc, mnt, opt, proc, root, sbin, selinux, srv, sys, tmp, usr, var
```

**最近修改的文件显示在最上面:**`ls -t`

```
[root@localhost /]# ls -t

tmp  root  etc  dev  lib  boot  sys  proc  data  home  bin  sbin  usr  var  lost+found  media  mnt  opt  selinux  srv  misc
```

**显示递归文件:**`ls -R`

```
[root@localhost ~]# ls -R
.:
anaconda-ks.cfg  install.log  install.log.syslog  satools

./satools:
black.txt  freemem.sh  iptables.sh  lnmp.sh  mysql  php502_check.sh  ssh_safe.sh
```

-a：显示所有档案及目录（ls内定将档案名或目录名称为“.”的视为影藏，不会列出）；
-A：显示除影藏文件“.”和“..”以外的所有文件列表；
-C：多列显示输出结果。这是默认选项；
-l：与“-C”选项功能相反，所有输出信息用单列格式输出，不输出为多列；
-F：在每个输出项后追加文件的类型标识符，具体含义：“*”表示具有可执行权限的普通文件，“/”表示目录，“@”表示符号链接，“|”表示命令管道FIFO，“=”表示sockets套接字。当文件为普通文件时，不输出任何标识符；
-b：将文件中的不可输出的字符以反斜线“”加字符编码的方式输出；
-c：与“-lt”选项连用时，按照文件状态时间排序输出目录内容，排序的依据是文件的索引节点中的ctime字段。与“-l”选项连用时，则排序的一句是文件的状态改变时间；
-d：仅显示目录名，而不显示目录下的内容列表。显示符号链接文件本身，而不显示其所指向的目录列表；
-f：此参数的效果和同时指定“aU”参数相同，并关闭“lst”参数的效果；
-i：显示文件索引节点号（inode）。一个索引节点代表一个文件；
--file-type：与“-F”选项的功能相同，但是不显示“*”；
-k：以KB（千字节）为单位显示文件大小；
-l：以长格式显示目录下的内容列表。输出的信息从左到右依次包括文件名，文件类型、权限模式、硬连接数、所有者、组、文件大小和文件的最后修改时间等；
-m：用“,”号区隔每个文件和目录的名称；
-n：以用户识别码和群组识别码替代其名称；
-r：以文件名反序排列并输出目录内容列表；
-s：显示文件和目录的大小，以区块为单位；
-t：用文件和目录的更改时间排序；
-L：如果遇到性质为符号链接的文件或目录，直接列出该链接所指向的原始文件或目录；
-R：递归处理，将指定目录下的所有文件及子目录一并处理；
--full-time：列出完整的日期与时间；
--color[=WHEN]：使用不同的颜色高亮显示不同类型的。

> ## Mac SSH命令

```
ssh root@ip -p 4567
```

用ssh连接服务器`-p`后面跟端口号

> ## Mac scp命令

**把本地文件copy到远程服务器上：**

```
scp <local file> <remote user>@<remote machine>:<remote path>
```

**把远程服务器上的文件copy到本地：**

```
scp <remote user>@<remote machine>:<remote path> <local file>
```

-1                        强制scp命令使用协议ssh1 
-2                        强制scp命令使用协议ssh2 
-4                        强制scp命令只使用IPv4寻址 
-6                        强制scp命令只使用IPv6寻址 
-B                        使用批处理模式（传输过程中不询问传输口令或短语） 
-C                        允许压缩。（将-C标志传递给ssh，从而打开压缩功能） 
-p                         保留原文件的修改时间，访问时间和访问权限。 
-q                         不显示传输进度条。 
**-r                          递归复制整个目录。** 
-v                          详细方式显示输出。scp和ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。 
-c cipher              以cipher将数据传输进行加密，这个选项将直接传递给ssh。 
-F ssh_config      指定一个替代的ssh配置文件，此参数直接传递给ssh。 
-i identity_file      从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh。 
-l limit                    限定用户所能使用的带宽，以Kbit/s为单位。 
-o ssh_option      如果习惯于使用ssh_config(5)中的参数传递方式， 
**-P port                  注意是大写的P, port是指定数据传输用到的端口号** 
-S program         指定加密传输时所使用的程序。此程序必须能够理解ssh(1)的选项。