### chown 命令

- **chown** 将指定文件的拥有者改为指定的用户和组，用户可以是用户名或者用户ID，组可以是组名或者组ID；

- 文件是以空格分开的要改变权限的文件列表，支持通配符；

- 系统管理员经常使用 **chown** 命令，在将文件拷贝到一个用户的目录下后，让用户拥有该文件的权限；

- **命令格式** - chown [选项]… [所有者]\[:[组]] [文件...]

- **命令功能** - 

  - 通过 **chown** 改变文件的拥有者和群组；
  - 在改变文件的所有者和群组时，可以使用用户名和用户识别码设置；
  - 普通用户不能将自己的文件改变成其他的拥有者，其操作权限一般为管理员；

- **命令参数** - 

  - **必要参数** -

    **-c** ：显示更改部分的信息；

    **-f** ：忽略错误信息；

    **-h** ：修复符号链接；

    **-R** ：处理指定目录及其子目录下的所有文件；

    **-v** ：显示详细的处理信息；

    **—deference** ：作用于符号链接的指向，而不是链接文件本身；

  - **可选参数** - 

    **—reference=\<指定的目录或文件\>** ：把指定的目录/文件作为参考，把操作的目录/文件设置成 和 指定的目录/文件 一样的拥有者和群组；

    **—from=\<当前用户:当前群组\>** ：只有当前用户和群组和指定的用户和群组相同时才进行改变；

    **--help** ：显示帮助信息；

    **--version** ：显示版本信息；

- **命令实例** -

- **实例一：改变拥有者和群组**

- **命令**

  ```bash
  chown mail:mail log2012.log
  ```

- **输出**

  ```bash
  [root@localhost test6]# ll
  ---xr--r-- 1 root users 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 root users 302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root users     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2017.log
  [root@localhost test6]# chown mail:mail log2012.log 
  [root@localhost test6]# ll
  ---xr--r-- 1 root users 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 mail mail  302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root users     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2017.log
  [root@localhost test6]#
  ```

- **实例二：改变拥有者和群组**

- **命令**

  ```bash
  chown root: log2012.log
  ```

- **输出**

  ```bash
  [root@localhost test6]# ll
  总计 604
  ---xr--r-- 1 root users 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 mail mail  302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root users     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2017.log
  [root@localhost test6]# chown root: log2012.log 
  [root@localhost test6]# ll
  总计 604
  ---xr--r-- 1 root users 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 root root  302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root users     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2017.log
  [root@localhost test6]#
  ```

- **实例三：改变文件群组**

- **命令**

  ```bash
  chown :mail log2012.log
  ```

- **输出**

  ```bash
  [root@localhost test6]# ll
  总计 604
  ---xr--r-- 1 root users 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 root root  302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root users     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2017.log
  [root@localhost test6]# chown :mail log2012.log 
  [root@localhost test6]# ll
  总计 604
  ---xr--r-- 1 root users 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 root mail  302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root users     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root users      0 11-30 08:39 log2017.log
  ```

- **实例四：改变指定目录及其子目录下的所有文件的拥有者和群组**

- **命令**

  ```bash
  chown -R -v root:mail test6
  ```

- **输出**

  ```bash
  [root@localhost test]# ll
  drwxr-xr-x 2 root users   4096 11-30 08:39 test6
  [root@localhost test]# chown -R -v root:mail test6
  “test6/log2014.log” 的所有者已更改为 root:mail
  “test6/linklog.log” 的所有者已更改为 root:mail
  “test6/log2015.log” 的所有者已更改为 root:mail
  “test6/log2013.log” 的所有者已更改为 root:mail
  “test6/log2012.log” 的所有者已保留为 root:mail
  “test6/log2017.log” 的所有者已更改为 root:mail
  “test6/log2016.log” 的所有者已更改为 root:mail
  “test6” 的所有者已更改为 root:mail
  [root@localhost test]# ll
  drwxr-xr-x 2 root mail   4096 11-30 08:39 test6
  [root@localhost test]# cd test6
  [root@localhost test6]# ll
  总计 604
  ---xr--r-- 1 root mail 302108 11-30 08:39 linklog.log
  ---xr--r-- 1 root mail 302108 11-30 08:39 log2012.log
  -rw-r--r-- 1 root mail     61 11-30 08:39 log2013.log
  -rw-r--r-- 1 root mail      0 11-30 08:39 log2014.log
  -rw-r--r-- 1 root mail      0 11-30 08:39 log2015.log
  -rw-r--r-- 1 root mail      0 11-30 08:39 log2016.log
  -rw-r--r-- 1 root mail      0 11-30 08:39 log2017.log
  ```

  