### ln 命令

- **ln** 的功能是为某一个文件在另外一个位置建立一个同步的链接；

- 当我们需要在不同的目录中，用到相同的文件时，我们不需要在每一个用到的地方都创建一个相同的文件，我们只要在某个固定的目录下，放上该文件，然后在其他目录下用 **ln** 命令链接( **link** ) 它就可以了，不必重复的占用磁盘空间；

- **命令格式** - ln [选项] [源文件或目录] [目标文件或目录]

- **命令功能** - 

  - **Linux** 系统中，所谓的链接( **link** ) ，我们可以将其视为档案的别名。链接又分两种：**硬链接（hard link）** 与 **软链接（symbolic link）** 。

  - 硬链接的意思是一个档案可以有多个名称，而软链接的方式则是产生一个特殊的档案，该档案的内容是指向另一个档案的位置。硬链接是存在同一个文件系统中，而软链接却可以跨越不同的文件系统；

  - **软链接**

    1.软链接，以路径的形式存在，类似 **Windows** 下的快捷方式；

    2.软链接可以跨文件系统，硬链接不可以；

    3.软链接可以对一个不存在的文件名进行链接；

    4.软链接可以对目录进行链接；

  - **硬链接**

    1.硬链接以文件副本的形式存在，但不占用实际空间（硬链接和源文件在磁盘是同一份文件，只是指针不同，使用硬链接可以达到备份数据(实际是节点)的效果，但是，**硬链接也会随源文件同步，怎么达到备份效果？**）；

    2.硬链接不允许跨文件系统；

    3.硬链接不允许对目录进行链接；

  - **几点要注意的：**

    第一，**ln** 命令会保持每一处链接文件的同步性。也就是说，无论你改动了哪一处，其他的文件都会发生相同的变化；

    第二，**ln** 的链接又分软链接和硬链接两种。软链接就是 **[ ln -s 源文件 目标文件 ]** ，它只会在你选定的位置上生成一个文件的镜像，不会占用磁盘空间；硬链接就是 **[ ln 源文件 目标文件 ]** ，没有参数 **-s** ，它会在你选定的位置上生成一个和源文件大小相同的文件。**无论是软链接还是硬链接，文件都保持同步变化** ；

    **ln** 命令用在链接文件或目录时，如同时指定两个以上的文件或目录，且最后的目的地是一个已经存在的目录，则会把前面指定的所有文件或目录复制到该目录中；若同时指定多个文件或目录，且最后的目的地并非是一个已存在的目录，则会出现错误信息。

- **命令参数** - 

  - **必要参数** - 

    **-b** ：删除，覆盖以前建立的链接

    **-d** ：允许超级用户制作目录的硬链接

    **-f** ：强制执行

    **-i** ：交互模式，文件存在则提示用户是否覆盖；

    **-n** ：把符号链接视为一般目录

    **-s** ：软链接（符号链接）

    **-v** ：显示详细的处理过程

  - **选择参数** - 

    **-S\<字尾备份字符串\>**

    **-V\<备份方式\>**

    **--help** ：显示帮助信息

    **--version** ：显示版本信息

- **命令实例** - 

- **实例一：给文件创建软链接**

- **命令**

  ```bash
  ln -s log2019.log link2019
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 8
  -rw-rw-rw-@ 2 qiu  staff  136  4 26 09:45 log2019.log
  Qs-MacBook-Pro:dir4 qiu$ ln -s log2019.log link2019
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 8
  lrwxr-xr-x  1 qiu  staff   11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff  136  4 26 09:45 log2019.log
  ```

- **说明**

  为 **log2019.log** 文件创建软链接 **link2019** ，如果 **log2019.log** 丢失，**link2019** 将失效；

- **实例二：给文件创建硬链接**

- **命令**

  ```bash
  ln log2019.log ln2019
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 8
  lrwxr-xr-x  1 qiu  staff   11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff  136  4 26 09:45 log2019.log
  Qs-MacBook-Pro:dir4 qiu$ ln log2019.log ln2019
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 16
  lrwxr-xr-x  1 qiu  staff   11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 3 qiu  staff  136  4 26 09:45 ln2019
  -rw-rw-rw-@ 3 qiu  staff  136  4 26 09:45 log2019.log
  ```

- **说明**

  为 **log2019.log** 创建硬链接 **ln2019** ，**log2019.log** 与 **ln2019** 的各项属性相同；

- **实例三：接上面两实例，链接完毕后，删除和重建链接源文件**

- **命令**

  ```bash
  rm -rf log2019.log
  touch log2019.log
  vi log2019.log
  cat link2019
  cat ln2019
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 16
  lrwxr-xr-x  1 qiu  staff  11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 3 qiu  staff  61  5 10 11:52 ln2019
  -rw-rw-rw-@ 3 qiu  staff  61  5 10 11:52 log2019.log
  Qs-MacBook-Pro:dir4 qiu$ cat log2019.log
  hostnamebaidu=baidu.com
  hostnamesina=sina.com
  hostnames=true
  Qs-MacBook-Pro:dir4 qiu$ rm -rf log2019.log
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 8
  lrwxr-xr-x  1 qiu  staff  11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff  61  5 10 11:52 ln2019
  Qs-MacBook-Pro:dir4 qiu$ touch log2019.log
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 8
  lrwxr-xr-x  1 qiu  staff  11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff  61  5 10 11:52 ln2019
  -rw-r--r--  1 qiu  staff   0  5 10 11:53 log2019.log
  Qs-MacBook-Pro:dir4 qiu$ vi log2019.log
  2019-01
  2019-02
  2019-03
  
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 8
  lrwxr-xr-x  1 qiu  staff  11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff  61  5 10 11:52 ln2019
  -rw-r--r--  1 qiu  staff   0  5 10 11:53 log2019.log
  Qs-MacBook-Pro:dir4 qiu$ cat link2019
  2019-01
  2019-02
  2019-03
  
  Qs-MacBook-Pro:dir4 qiu$ cat ln2019
  hostnamebaidu=baidu.com
  hostnamesina=sina.com
  hostnames=true
  Qs-MacBook-Pro:dir4 qiu$ 
  ```

- **说明**

  1.源文件被删除后，并没有影响硬链接文件；软链接文件在 **centos** 系统下不断的闪烁，提示源文件已经不存在；

  2.重建源文件后，软链接不再提示闪烁，说明已经链接成功，找到了链接文件系统；重建后，硬链接文件并没有受到源文件影响，硬链接文件的内容还是保留了删除前源文件的内容，说明硬链接已经失效；

- **实例四：将文件链接到另一个目录中的相同名字**

- **命令**

  ```bash
  ln log2019.log test1
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir4 qiu$ ls -lR
  total 16
  lrwxr-xr-x  1 qiu  staff  11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff  61  5 10 11:52 ln2019
  -rw-r--r--@ 3 qiu  staff  28  5 10 12:01 log2019.log
  drwxr-xr-x  3 qiu  staff  96  5 10 12:08 test
  
  ./test:
  Qs-MacBook-Pro:dir4 qiu$ cat log2019.log
  2019-01
  2019-02
  2019-03
  wq
  
  Qs-MacBook-Pro:dir4 qiu$ ln log2019.log test
  Qs-MacBook-Pro:dir4 qiu$ ls -lR
  total 16
  lrwxr-xr-x  1 qiu  staff   11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff   61  5 10 11:52 ln2019
  -rw-r--r--@ 4 qiu  staff   28  5 10 12:01 log2019.log
  drwxr-xr-x  4 qiu  staff  128  5 10 12:09 test
  
  ./test:
  total 8
  -rw-r--r--@ 4 qiu  staff  28  5 10 12:01 log2019.log
  Qs-MacBook-Pro:dir4 qiu$ cd test
  Qs-MacBook-Pro:test qiu$ vi log2019.log
  2019-01
  2019-02
  2019-03
  wq
  
  In test directory !!!!
  
  Qs-MacBook-Pro:test qiu$ ll
  total 8
  -rw-r--r--@ 4 qiu  staff  52  5 10 12:10 log2019.log
  Qs-MacBook-Pro:test qiu$ cd ..
  Qs-MacBook-Pro:dir4 qiu$ ll
  total 16
  lrwxr-xr-x  1 qiu  staff   11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff   61  5 10 11:52 ln2019
  -rw-r--r--@ 4 qiu  staff   52  5 10 12:10 log2019.log
  drwxr-xr-x  4 qiu  staff  128  5 10 12:10 test
  Qs-MacBook-Pro:dir4 qiu$ cat log2019.log
  2019-01
  2019-02
  2019-03
  wq
  
  In test directory !!!!
  
  Qs-MacBook-Pro:dir4 qiu$ 
  ```

- **说明**

  在 **test** 目录中创建了 **log2019.log** 的硬链接，修改 **test** 目录中的 **log2019.log** 文件，同时也会同步到源文件(内容和修改时间)；

- **实例五：给目录创建软链接**

- **命令**

  ```bash
  ln -sv /opt/soft/test/test3 /opt/soft/test/test5
  ```

- **输出**

  ```bash
  [root@localhost test]# ll
  drwxr-xr-x 2 root root   4096 12-07 16:36 test3
  drwxr-xr-x 2 root root   4096 12-07 16:57 test5
  [root@localhost test]# cd test5
  [root@localhost test5]# ll
  lrwxrwxrwx 1 root root 5 12-07 16:57 test3 -> test3
  [root@localhost test5]# cd test3
  -bash: cd: test3: 符号连接的层数过多
  [root@localhost test5]# 
  [root@localhost test5]# 
  [root@localhost test5]# ll
  lrwxrwxrwx 1 root root 5 12-07 16:57 test3 -> test3
  [root@localhost test5]# rm -rf test3
  [root@localhost test5]# ll
  [root@localhost test5]# ln -sv /opt/soft/test/test3 /opt/soft/test/test5
  创建指向“/opt/soft/test/test3”的符号链接“/opt/soft/test/test5/test3”
  [root@localhost test5]# ll
  lrwxrwxrwx 1 root root 20 12-07 16:59 test3 -> /opt/soft/test/test3
  [root@localhost test5]# 
  [root@localhost test5]# cd test3
  [root@localhost test3]# ll
  总计 4
  -rw-r--r-- 2 root root 80 12-07 16:36 log2013.log
  [root@localhost test3]# touch log2014.log
  [root@localhost test3]# ll
  总计 4
  -rw-r--r-- 2 root root 80 12-07 16:36 log2013.log
  -rw-r--r-- 1 root root  0 12-07 17:05 log2014.log
  [root@localhost test3]# cd ..
  [root@localhost test5]# cd ..
  ```

- **说明**

  1.目录只能创建软链接；

  2.目录创建链接必须使用绝对路径，相对路径创建不会成功，会提示：符号连接的层数过多 这样的错误；

  3.在链接目标目录中修改文件都会在源文件目录中同步变化；

  4.**Mac_Terminal** 下貌似可以用相对路径创建目录链接；