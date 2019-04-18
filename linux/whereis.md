### whereis 命令

- **where** 命令只能用于 **程序名** 的搜索，而且只搜索二进制文件（参数 **-b**），man说明文件（参数 **-m**）和源代码文件（参数 **-s**）。如果省略参数，则 **返回所有信息** ；

- 和 **find** 相比，**whereis** 查找速度非常快，因为 **Linux** 系统会将系统内的所有文件都记录在一个数据库文件中，当使用 **whereis** 和下面即将介绍的 **locate** 时，会从数据库查找数据，而不是像 **find** 命令那样，通过遍历硬盘来查找文件，效率自然会很高；

- 但该数据库不是实时更新的，默认情况下一星期更新一次。因此，我们在用 **whereis** 和 **locate** 查找文件时，有时会找到已经被删除的数据，或者刚刚建立的文件，却无法查找到，原因就是数据库文件还没有更新；

- **命令格式** - whereis [-bmsu] [BMS 目录名 -f] 文件名

- **命令功能** - 

  - 定位 可执行文件、源代码文件、帮助文件 在系统文件中的位置。
  - 还具有搜索 源代码、指定设备路径和搜索不寻常项的能力；

- **命令参数** -

  - **注意：Mac_Terminal 下所有参数无效** ；
  - **-b** ：定位可执行(二进制)文件；
  - **-m** ：定位帮助(man)文件；
  - **-s** ：定位源代码文件；
  - **-u** ：搜索默认路径下，除可执行文件、源代码文件、帮助文件以外的其他文件；
  - **-B** ：指定搜索可执行(二进制)文件的路径；
  - **-M** ：指定搜索帮助文件的路径；
  - **-S** ：指定搜索源代码文件的路径；

- **命令实例** - 

- **实例一：将和 xx 文件相关的文件都查找出来**

- **命令**

  ```bash
  whereis svn
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ whereis tomcat
  Qs-MacBook-Pro:dir1 qiu$ whereis svn
  /usr/bin/svn
  ```

- **说明**

  **tomcat** 没安装，找不出来；**svn** 安装了；

- **实例二：只将二进制文件找出来**

- **命令**

  ```bash
  whereis -b svn
  ```

- **输出**

  ```bash
  // Mac_Terminal 下 whereis 无任何参数
  // 该实例是 Linux 下的
  [root@localhost ~]# whereis -b svn
  svn: /usr/bin/svn /usr/local/svn
  [root@localhost ~]# whereis -m svn
  svn: /usr/share/man/man1/svn.1.gz
  [root@localhost ~]# whereis -s svn
  svn:
  [root@localhost ~]#
  ```

  