### find 命令之 xargs

- 在使用 **find** 命令的 **-exec** 选项处理匹配到的文件时，**find** 命令将所有匹配到的文件一起传递给 **exec** 执行。但有些系统对能够传递给 **exec** 的参数的命令长度有限制，这样在 **find** 命令运行几分钟之后，就会出现溢出错误。错误信息通常是 **参数列太长** 或 **参数列溢出** 。这就是 **xargs** 命令的用处所在，特别是与 **find** 命令一起使用；

- **find** 把匹配到的文件传递给 **xargs** 命令，而 **xargs** 命令每次只获取一部分文件而不是全部，不像 **-exec** 选项那样。这样它可先处理最先获取的一部分文件，然后是下一批，并如此继续下去；

- 在有些系统中，使用 **-exec** 选项会为处理每一个匹配到的文件发起一个相应的进程，并非将匹配到的文件全部作为参数一次执行；这样在有些情况下就会出现进程过多，系统性能下降的问题，因而效率不高；而使用 **xargs** 命令则只有一个进程。另外，在使用 **xargs** 命令时，究竟是一次获取所有的参数，还是分批取得参数，以及每一次获取参数的数目都会根据该命令的选项及系统内核中相应的可调参数来确定。

- **命令实例**

- **实例一：查找系统中的每一个普通文件，然后使用 xargs 命令来测试它们分别属于哪类文件**

- **命令**

  ```bash
  find . -type f -print | xargs file
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ll
  total 8
  -rw-r--r--@ 1 qiu  staff  110  4 21 22:20 log.log
  -rw-r--r--  1 qiu  staff    0  4 22 09:45 log1.log
  Qs-MacBook-Pro:dir1 qiu$ find . -type f -print | xargs file
  ./log.log:   ASCII text
  ./.DS_Store: Apple Desktop Services Store
  ./log1.log:  empty
  ```

- **实例二：在整个系统中查找内存信息转储文件（core dump），然后把结果保存到/tmp/core.log 文件中**

- **命令**

  ```bash
  find / -name "core" -print | xargs echo "" > /tmp/core.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ find / -name "core" -print | xargs echo "" >/tmp/core.log
  find: /usr/sbin/authserver: Permission denied
  find: /.Spotlight-V100: Operation not permitted
  find: /.PKInstallSandboxManager-SystemSoftware: Permission denied
  find: /Library/Application Support/Apple/ParentalControls/Users: Permission denied
  find: /Library/Application Support/Apple/AssetCache/Data: Permission denied
  find: /Library/Application Support/ApplePushService: Permission denied
  
  // 一大串文件
  ...
  
  Qs-MacBook-Pro:dir1 qiu$ cd /tmp
  Qs-MacBook-Pro:tmp qiu$ ll
  total 32
  ...
  drwxr-xr-x  2 qiu           wheel    64  4 18 09:24 com.sogou.inputmethod
  -rw-r--r--  1 qiu           wheel  1285  4 22 09:55 core.log
  drwxr-xr-x  2 root          wheel    64  4 19 00:13 npm-94100-e1134393
  ```

- **实例三：在当前目录下查找所有用户具有读、写和执行权限的文件，并收回相应的写权限**

- **命令**

  ```bash
  find . -perm -7 -print | xargs chmod o-w
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ll
  total 8
  drwxrwxrwx  2 qiu  staff   64  4 22 10:04 log
  -rw-r--r--@ 1 qiu  staff  110  4 21 22:20 log.log
  -rw-r--r--  1 qiu  staff    0  4 22 09:45 log1.log
  Qs-MacBook-Pro:dir1 qiu$ find . -perm -7 -print | xargs chmod o-w
  Qs-MacBook-Pro:dir1 qiu$ ll
  total 8
  drwxrwxr-x  2 qiu  staff   64  4 22 10:04 log
  -rw-r--r--@ 1 qiu  staff  110  4 21 22:20 log.log
  -rw-r--r--  1 qiu  staff    0  4 22 09:45 log1.log
  ```

- **说明**

  执行命令后，文件夹 **log** 的权限发生改变

- **实例四：用 grep 命令在当前目录下的所有普通文件中搜索 hostname 这个词**

- **命令**

  ```bash
  find . -type f -print | xargs grep "hostname"
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ find . -type f -print | xargs grep "hostname"
  ./log.log:hostname = google.com
  ./log1.log:hostname = sina.com
  
  ```

- **实例五：使用 xargs 执行 mv**

- **命令**

  ```bash
  find . -name "*.log" | xargs -i mv {} test4
  ```

- **输出**

  ```bash
  [root@localhost test]# ll
  总计 316
  -rw-r--r-- 1 root root 302108 11-03 06:19 log2012.log
  -rw-r--r-- 1 root root     61 11-12 22:44 log2013.log
  -rw-r--r-- 1 root root      0 11-12 22:25 log2014.log
  drwxr-xr-x 6 root root   4096 10-27 01:58 scf
  drwxrwxr-x 2 root root   4096 11-12 22:54 test3
  drwxrwxr-x 2 root root   4096 11-12 19:32 test4
  [root@localhost test]# cd test4/
  [root@localhost test4]# ll
  总计 0[root@localhost test4]# cd ..
  [root@localhost test]# find . -name "*.log" | xargs -i mv {} test4
  [root@localhost test]# ll
  总计 12drwxr-xr-x 6 root root 4096 10-27 01:58 scf
  drwxrwxr-x 2 root root 4096 11-13 05:50 test3
  drwxrwxr-x 2 root root 4096 11-13 05:50 test4
  [root@localhost test]# cd test4/
  [root@localhost test4]# ll
  总计 304
  -rw-r--r-- 1 root root 302108 11-12 22:54 log2012.log
  -rw-r--r-- 1 root root     61 11-12 22:54 log2013.log
  -rw-r--r-- 1 root root      0 11-12 22:54 log2014.log
  ```

- **实例六：find 后执行 xargs 提示 xargs: argument line too long 解决方法**

- **命令**

  ```bash
  find . -type f -atime +0 -print0 | xargs -0 -l1 -t rm -f
  ```

- **输出**

  ```bash
  [root@pd test4]#  find . -type f -atime +0 -print0 | xargs -0 -l1 -t rm -f
  rm -f 
  [root@pdtest4]#
  ```

- **说明**

  **-l1** 是一次处理一个；**-t** 是处理之前打印出命令

- **实例七：xargs 的 -p 参数的使用**

- **命令**

  ```bash
  find . -name "*.log" | xargs -p -i mv {} ...
  ```

- **输出**

  ```bash
  [root@localhost test3]# ll
  总计 0
  -rw-r--r-- 1 root root 0 11-13 06:06 log2015.log
  [root@localhost test3]# cd ..
  [root@localhost test]# ll
  总计 316
  -rw-r--r-- 1 root root 302108 11-13 06:03 log2012.log
  -rw-r--r-- 1 root root     61 11-13 06:03 log2013.log
  -rw-r--r-- 1 root root      0 11-13 06:03 log2014.log
  drwxr-xr-x 6 root root   4096 10-27 01:58 scf
  drwxrwxr-x 2 root root   4096 11-13 06:06 test3
  drwxrwxr-x 2 root root   4096 11-13 05:50 test4
  [root@localhost test]# cd test3
  [root@localhost test3]#  find . -name "*.log" | xargs -p -i mv {} ..
  mv ./log2015.log .. ?...y
  [root@localhost test3]# ll
  总计 0[root@localhost test3]# cd ..
  [root@localhost test]# ll
  总计 316
  -rw-r--r-- 1 root root 302108 11-13 06:03 log2012.log
  -rw-r--r-- 1 root root     61 11-13 06:03 log2013.log
  -rw-r--r-- 1 root root      0 11-13 06:03 log2014.log
  -rw-r--r-- 1 root root      0 11-13 06:06 log2015.log
  drwxr-xr-x 6 root root   4096 10-27 01:58 scf
  drwxrwxr-x 2 root root   4096 11-13 06:08 test3
  drwxrwxr-x 2 root root   4096 11-13 05:50 test4
  [root@localhost test]#
  ```

- **说明**

  **-p** 参数会提示让你确认是否执行后面的命令。**y** 执行， **n** 不执行