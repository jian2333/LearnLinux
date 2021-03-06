### diff 命令

- **diff** 命令是 **Linux** 上非常重要的工具，用于比较文件的内容，特别是比较两个版本不同的文件以找到改动的地方。**diff** 在命令行中打印每一行的改动。最新版的 **diff** 还支持二进制文件。**diff** 程序的输出被称为补丁（**patch**），因为 **Linux** 系统中还有一个 **patch** 程序，可以根据 **diff** 的输出将 **a.c** 的文件内容更新为 **b.c** 。**diff** 是 **svn、cvs、git** 等版本控制工具不可或缺的一部分；

- **命令格式** - diff [参数] [文件1或目录1] [文件2或目录2]

- **命令功能** - 

  - **diff** 命令能比较单个文件或目录内容；
  - 如果指定比较的是文件，则只有当输入为文本文件时才有效。以逐行的方式，比较文本文件的异同处；
  - 如果指定比较的是目录的时候，**diff** 命令会比较两个目录下名字相同的文本文件。列出不同的二进制文件、公共子目录和只在一个目录出现的文件；

- **命令参数** - 

  - **-\<行数\>** ：指定要显示多少行的文本。此参数必须与 **-c** 或 **-u** 参数一并使用；
  - **-a或--text** ：**diff** 预设只会逐行比较文本文件；
  - **-b或--ignore-space-change** ：不检查空格字符的不同；
  - **-B或--ignore-blank-lines** ：不检查空白行；
  - **-c** ：显示全文内容，并标出不同之处；
  - **-C\<行数\>或--context\<行数\>** ：与执行 "**-c\<行数\>**" 指令相同；
  - **-d或--minimal** ：使用不同的演算法，以小的单位来做比较；
  - **-D\<巨集名称\>或ifdef\<巨集名称\>** ：此参数的输出格式可用于前置处理器巨集；
  - **-e或--ed** ：此参数的输出格式可用于 **ed** 的 **script** 文件；
  - **-f或-forward-ed** ：输出的格式类似 **ed** 的 **script** 文件，但按照原来文件的顺序来显示不同处；
  - **-H或--speed-large-files** ：比较大文件时，可加快速度；
  - **-l\<字符或字符串\>或--ignore-matching-lines\<字符或字符串\>** ：若两个文件在某几行有所不同，而之前同时都包含了选项中指定的字符或字符串，则不显示这两个文件的差异；
  - **-i或--ignore-case** ：不检查大小写的不同；
  - **-l或--paginate** ：将结果交由 **pr** 程序来分页；
  - **-n或--rcs** ：将比较结果以 **RCS** 的格式来显示；
  - **-N或--new-file** ：
    - 在比较目录时，若 **文件A** 仅出现在某个目录中，预设会显示：**Only in 目录，文件A** ；
    - 若使用 **-N** 参数，则 **diff** 会将 **文件A** 与一个空白的文件比较；
  - **-p** ：若比较的文件为 **c语言的程序码文件** 时，显示差异所在的函数名称；
  - **-P或--unidirectional-new-file** ：与 **-N** 类似，但只有当第二个目录包含了第一个目录所没有的文件时，才会将这个文件与空白的文件做比较；
  - **-q或--brief** ：仅显示有无差异，不显示详细信息；
  - **-r或--recursive** ：比较子目录中的文件；
  - **-s或--report-identical-files** ：若没有发现差异，仍然显示信息；
  - **-S\<文件\>或--starting-file\<文件\>** ：在比较目录时，从指定的文件开始比较；
  - **-t或--expand-tabs** ：在输出时，将 **tab** 字符展开；
  - **-T或--initial-tabs** ：在每行前面加上 **tab** 字符以便对其；
  - **-u或-U\<列数\>或--unified=\<列数\>** ：以合并的方式来显示文件内容的不同；
  - **-v或--version** ：显示版本信息；
  - **-w或--ignore-all-space** ：忽略全部的空格字符；
  - **-W\<宽度\>或--width\<宽度\>** ：在使用 **-y** 参数时，指定栏宽；
  - **-x\<文件名或目录\>或--exclude\<文件名或目录\>** ：不比较选项中指定的文件或目录；
  - **-X\<文件\>或--exclude-from\<文件\>** ：你可以将文件或目录类型存成文本文件，然后在 **=\<文件\>** 中指定此文本文件；
  - **-y或--side-by-side** ：以并列的方式显示文件的异同处；
  - **--help** ：显示帮助；
  - **--left-column** ：若使用 **-y** 参数时，若两个文件某一行内容相同，则仅在左侧的栏位显示改行内容；
  - **--suppress-common-lines** ：在使用 **-y** 参数时，仅显示不同之处；

- **命令实例** - 

- **实例一：比较两个文件**

- **命令**

  ```bash
  diff log2014.log log2013.log
  ```

- **输出**

  ```bash
  [root@localhost test3]# diff log2014.log log2013.log 
  3c3
  < 2014-03
  ---
  > 2013-03
  8c8
  < 2013-07
  ---
  > 2013-08
  11,12d10
  < 2013-11
  < 2013-12
  ```

- **说明**

  上面的 **3c3** 和 **8c8** 表示 log2014.log 和 log2013.log 文件在第3行和第8行内容有所不同；

  **11,12d10** 表示第一个文件比第二个文件多了第11和第12行；

  **diff 的 normal 显示格式有三种提示 ：** 

  a - add

  c - change

  d - delete

- **实例二：并排格式输出**

- **命令**

  ```bash
  diff log2013.log log2014.log -y -W 50
  ```

- **输出**

  ```bash
  [root@localhost test3]# diff log2014.log log2013.log  -y -W 50
  2013-01                 2013-01
  2013-02                 2013-02
  2014-03               | 2013-03
  2013-04                 2013-04
  2013-05                 2013-05
  2013-06                 2013-06
  2013-07                 2013-07
  2013-07               | 2013-08
  2013-09                 2013-09
  2013-10                 2013-10
  2013-11               <
  2013-12               <
  [root@localhost test3]# diff log2013.log log2014.log  -y -W 50
  2013-01                 2013-01
  2013-02                 2013-02
  2013-03               | 2014-03
  2013-04                 2013-04
  2013-05                 2013-05
  2013-06                 2013-06
  2013-07                 2013-07
  2013-08               | 2013-07
  2013-09                 2013-09
  2013-10                 2013-10
                        > 2013-11
                        > 2013-12
  ```

- **说明**

  **|** 	表示前后两个文件内容有不同

  **\<**	 表示后面的文件比前面的文件少了1行内容

  **\>** 	表示后面的文件比前面的文件多了1行内容

- **实例三：上下文格式输出**

- **命令**

  ```bash
  diff log2013.log log2014.log -c
  ```

- **输出**

  ```bash
  [root@localhost test3]# diff log2013.log log2014.log  -c
  *** log2013.log 2012-12-07 16:36:26.000000000 +0800
  --- log2014.log 2012-12-07 18:01:54.000000000 +0800
  ***************
  *** 1,10 ****
    2013-01
    2013-02
  ! 2013-03
    2013-04
    2013-05
    2013-06
    2013-07
  ! 2013-08
    2013-09
    2013-10
  --- 1,12 ----
    2013-01
    2013-02
  ! 2014-03
    2013-04
    2013-05
    2013-06
    2013-07
  ! 2013-07
    2013-09
    2013-10
  + 2013-11
  + 2013-12[root@localhost test3]# diff log2014.log log2013.log  -c
  *** log2014.log 2012-12-07 18:01:54.000000000 +0800
  --- log2013.log 2012-12-07 16:36:26.000000000 +0800
  ***************
  *** 1,12 ****
    2013-01
    2013-02
  ! 2014-03
    2013-04
    2013-05
    2013-06
    2013-07
  ! 2013-07
    2013-09
    2013-10
  - 2013-11
  - 2013-12
  --- 1,10 ----
    2013-01
    2013-02
  ! 2013-03
    2013-04
    2013-05
    2013-06
    2013-07
  ! 2013-08
    2013-09
    2013-10[root@localhost test3]#
  ```

- **说明**

  **开头作了比较文件的说明，这里有三种特殊字符：**

  **+** 	比较的文件的后者比前者多一行

  **-** 	 比较的文件的后者比前者少一行

  **!** 	 比较的文件两者有差别

- **实例四：统一格式输出**

- **命令**

  ```bash
  diff log2014.log log2013.log -u
  ```

- **输出**

  ```bash
  [root@localhost test3]# diff log2014.log log2013.log  -u
  --- log2014.log 2012-12-07 18:01:54.000000000 +0800
  +++ log2013.log 2012-12-07 16:36:26.000000000 +0800
  @@ -1,12 +1,10 @@
   2013-01
   2013-02
  -2014-03
  +2013-03
   2013-04
   2013-05
   2013-06
   2013-07
  -2013-07
  +2013-08
   2013-09
   2013-10
  -2013-11
  -2013-12
  ```

- **说明**

  它的第一部分，也就是文件的基本信息：

  --- log2014.log 2012-12-07 18:01:54.000000000 +0800

  +++ log2013.log 2012-12-07 16:36:26.000000000 +0800

  **---** 表示变动前的文件，**+++** 表示变动后的文件；

  第二部分，变动的位置用两个 **@** 作为起首和结束：

  @@ -1,12 +1,10 @@

  前面的 **-1,12** 分为三个部分：**-** 表示第一个文件（即log2014.log），**1** 表示第1行，**12** 表示连续12行。合在一起，就表示下面是第一个文件从第1行开始的连续12行。

  同样的，**+1,10** 表示变动后，成为第2个文件的从第1行开始的连续10行；

- **实例五：比较文件夹不同**

- **命令**

  ```bash
  diff test3 test6
  ```

- **输出**

  ```bash
  [root@localhost test]# diff test3 test6
  Only in test6: linklog.log
  Only in test6: log2012.log
  diff test3/log2013.log test6/log2013.log
  1,10c1,3
  < 2013-01
  < 2013-02
  < 2013-03
  < 2013-04
  < 2013-05
  < 2013-06
  < 2013-07
  < 2013-08
  < 2013-09
  < 2013-10
  ---
  > hostnamebaidu=baidu.com
  > hostnamesina=sina.com
  > hostnames=true
  diff test3/log2014.log test6/log2014.log
  1,12d0
  < 2013-01
  < 2013-02
  < 2014-03
  < 2013-04
  < 2013-05
  < 2013-06
  < 2013-07
  < 2013-07
  < 2013-09
  < 2013-10
  < 2013-11
  < 2013-12
  Only in test6: log2015.log
  Only in test6: log2016.log
  Only in test6: log2017.log
  [root@localhost test]# 
  ```

- **说明**

- **实例六：比较两个文件不同，并产生补丁**

- **命令**

  ```bash
  diff -ruN log2013.log log2014.log >patch.log
  ```

- **输出**

  ```bash
  [root@localhost test3]# diff -ruN log2013.log log2014.log >patch.log
  [root@localhost test3]# ll
  总计 12
  -rw-r--r-- 2 root root  80 12-07 16:36 log2013.log
  -rw-r--r-- 1 root root  96 12-07 18:01 log2014.log
  -rw-r--r-- 1 root root 248 12-07 21:33 patch.log
  [root@localhost test3]# cat patch.log 
  --- log2013.log 2012-12-07 16:36:26.000000000 +0800
  +++ log2014.log 2012-12-07 18:01:54.000000000 +0800
  @@ -1,10 +1,12 @@
   2013-01
   2013-02
  -2013-03
  +2014-03
   2013-04
   2013-05
   2013-06
   2013-07
  -2013-08
  +2013-07
   2013-09
   2013-10
  +2013-11
  +2013-12[root@localhost test3]#
  ```

- **说明**

- **实例七：打补丁**

- **命令**

  ```bash
  patch log2013.log patch.log
  ```

- **输出**

  ```bash
  [root@localhost test3]# cat log2013.log
  2013-01
  2013-02
  2013-03
  2013-04
  2013-05
  2013-06
  2013-07
  2013-08
  2013-09
  2013-10[root@localhost test3]# patch log2013.log patch.log 
  patching file log2013.log
  [root@localhost test3]# 
  [root@localhost test3]# cat log2013.log 
  2013-01
  2013-02
  2014-03
  2013-04
  2013-05
  2013-06
  2013-07
  2013-07
  2013-09
  2013-10
  2013-11
  2013-12[root@localhost test3]#
  ```

- **说明**

  