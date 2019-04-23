### find 参数详解

**find** 一些常用参数的一些常用实例和一些具体用法和注意事项；

#### 1. 使用 name 选项

- 文件名选项是 **find** 命令最常用的选项，要么单独使用该选项，要么和其他选项一起使用；
- 可以使用某种文件名模式来匹配文件，记住要用引号将文件名模式引起来；
- **~** 代表根目录；
- **.** 代表当前目录；

**实例**

- **实例一：查找根目录及其子目录下的所有文件名为 '*.log' 文件**

  ```bash
  find ~ -name "*.log" -print
  ```

- **实例二：查找当前目录及其子目录下的所有文件名为 '*.log' 文件**

  ```bash
  find . -name "*.log" -print
  ```

- **实例三：查找当前目录及其子目录下所有文件名以一个大写字母开头的文件**

  ```bash
  find . -name "[A-Z]*" -print
  ```

- **实例四：查找 /etc 目录下所有文件名以 host 开头的文件**

  ```bash
  find /ect -name "host*" -print
  ```

- **实例五：查找 $HOME 目录中的文件**

  ```bash
  find ~ -name "*" -print
  ```

- **实例六：想要让系统高负荷运行，就从根目录开始查找所有文件**

  ```bash
  find ~ -name "*" -print
  ```

- **实例七：在当前目录查找文件名以一个小写字母开头，最后是 4~9 加上 .log 结束的文件**

  ```bash
  find . -name "[a-z]*[4-9].log" -print
  ```

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ll
  total 16
  drwxrwxr-x  3 qiu  staff   96  4 22 10:35 log
  -rw-r--r--@ 1 qiu  staff  136  4 22 10:15 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  Qs-MacBook-Pro:dir1 qiu$ find . -name "[a-z]*[0-9].log" -print
  ./log1.log
  ```

#### 2. 使用 perm 选项

- 按照文件权限模式用 **-perm** 选项，按文件权限模式来查找文件的话，最好使用八进制的权限表示法；

- 如在当前目录下查找文件权限为 **755** 的文件，即文件属主可以读、写、执行，其他用户可以读、执行的文件，可以用

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ll
  total 16
  drwxrwxr-x  3 qiu  staff   96  4 22 10:35 log
  -rw-r--r--@ 1 qiu  staff  136  4 22 10:15 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  Qs-MacBook-Pro:dir1 qiu$ find . -perm 775 -print
  ./log
  ```

- 还有一种表示法，在八进制数字前面要加一个横杆 **-** ，表示 **权限至少是** ，如 **-007** 表示至少是 **007** ，**-005** 表示至少是 **005**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ll
  total 16
  drwxrwxr-x  3 qiu  staff   96  4 22 10:35 log
  -rw-r--r--@ 1 qiu  staff  136  4 22 10:15 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  Qs-MacBook-Pro:dir1 qiu$ find . -perm -004 -print
  .
  ./log.log
  ./.DS_Store
  ./log1.log
  ./log
  ./log/.DS_Store
  ```

#### 3. 忽略某个目录

- 使用 **-prune** 选项来指出要忽略的目录；
- 如果同时使用了 **-depth** ，那么 **-prune** 会被 **find** 命令忽略；

**实例**

- 在 **dir1** 目录下查找，但不希望在 **dir1/log** 目录下查找

  ```bash
  find dir1 -path "dir1/log" -prune -o -print
  ```

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -lR dir1
  total 16
  drwxrwxr-x  5 qiu  staff  160  4 23 10:44 log
  -rw-r--r--@ 1 qiu  staff  136  4 22 10:15 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  
  dir1/log:
  total 16
  -rw-r--r--@ 1 qiu  staff  136  4 22 10:15 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  Qs-MacBook-Pro:dir1 qiu$ find dir1 -path "dir1/log" -prune -o -print
  dir1
  dir1/log.log
  dir1/.DS_Store
  dir1/log1.log
  Qs-MacBook-Pro:dir1 qiu$ 
  ```

#### 4. 使用 find 查找文件的时候怎么避开某个文件目录

- **实例一：在 dir1 目录下查找不在 log 目录下的所有文件**

  ```bash
  // 同上一个实例！！
  ```

- **说明**

  - find [-path…] [expression]

  - 在路径列表后面的是表达式

  - **-path "test" -prune -o -print** 是 **-path "test" -a -prune -o -print** 的简写表达式按顺序求值；**-a** 和 **-o** 都是短路求值，与 **shell** 的 **&&** 和 **||** 效果类似；

  - **-path "test"** 为真，则求值 **-prune** , **-prune** 返回真，与逻辑表达式为真；否则不求值 **-prune**，与逻辑表达式为假。如果 **-path "test" -a -prune** 为假，则求值 **-print** ，**-print** 返回真，或逻辑表达式为真；否则不求值 **-print**，或逻辑表达式为真。

  - 这个表达式组合特例可以用伪代码写为：

    ```code
    if -path "test" then 
    -prune 
    else 
    -print
    ```

- **实例二：避开多个文件夹**

  ```bash
  find dir1 \(-path dir1/test1 -o -path dir1/test2 \) -prune -o -print
  ```

  ```bash
  // Mac_Terminal 下无效
  [root@localhost soft]# find test \( -path test/test4 -o -path test/test3 \) -prune -o -print
  test
  test/log2014.log
  test/log2015.log
  test/scf
  test/scf/lib
  test/scf/service
  test/scf/service/deploy
  test/scf/service/deploy/product
  test/scf/service/deploy/info
  test/scf/doc
  test/scf/bin
  test/log2013.log
  test/log2012.log
  [root@localhost soft]#
  ```

- 说明

  圆括号表示表达式的组合。**\\** 表示引用，即指示 **shell** 不对后面的字符串作特殊解释，而留给 **find** 命令去解释其意义；

- **实例三：查找某一确定文件，-name 等选项加在 -o 之后**

  ```bash
  find test \(-path test/test4 -o -path test/test3 \) -prune -o -name "*.log" -print
  ```

  ```bash
  [root@localhost soft]# find test \( -path test/test4 -o -path test/test3 \) -prune -o -name "*.log" -print
  test/log2014.log
  test/log2015.log
  test/log2013.log
  test/log2012.log
  [root@localhost soft]#
  ```

#### 5. 使用 user 和 nouser 选项

- 按文件属主查找文件

- **实例一：在 $HOME 目录中查找文件属主为 peida 的文件**

  ```bash
  find ~ -user peida -print
  ```

- **实例二：在 /etc 目录下查文件属主为 peida 的文件**

  ```bash
  find /etc -user peida -print
  ```

- **实例三：为了查找属主账户已经被删除的文件，可以使用 -nouser 选项。在 /home 目录下查找所有的这类文件**

  ```bash
  find /home -nouser -print
  ```

#### 6. 使用 group 和 nogroup 选项

- 和 **user** 一样，只是把 **-user** 改成 **-group** ，把 **-nouser** 改成 **-nogroup**

  ```bash
  find /app -group gem -print
  ```

  ```bash
  find / -nogroup -print
  ```

#### 7. 按照更改时间或访问时间等查找文件

- 在 [find 命令](http://www.jianwill.cn/md/linux/find.html) 页面有详细描述；
- **-atime、-ctime、tmtime** ；
- **+n、n、-n** ；

#### 8. 查找比某个文件新或旧的文件

- 使用 **-newer** 选项；

- **实例一：查找更改时间比文件 log2012.log 更新，但比文件 log2017.log 更旧 的文件**

  ```bash
  find -newer log2012.log ! -newer log2017.log
  ```

  ```bash
  [root@localhost test]# ll
  总计 316
  -rw-r--r-- 1 root root 302108 11-13 06:03 log2012.log
  -rw-r--r-- 1 root root     61 11-13 06:03 log2013.log
  -rw-r--r-- 1 root root      0 11-13 06:03 log2014.log
  -rw-r--r-- 1 root root      0 11-13 06:06 log2015.log
  -rw-r--r-- 1 root root      0 11-16 14:41 log2016.log
  -rw-r--r-- 1 root root      0 11-16 14:43 log2017.log
  drwxr-xr-x 6 root root   4096 10-27 01:58 scf
  drwxrwxr-x 2 root root   4096 11-13 06:08 test3
  drwxrwxr-x 2 root root   4096 11-13 05:50 test4
  [root@localhost test]# find -newer log2012.log ! -newer log2017.log
  .
  ./log2015.log
  ./log2017.log
  ./log2016.log
  ./test3
  [root@localhost test]#
  ```

- **实例二：查找更改时间比 log2012.log 文件新的文件**

  ```bash
  find . -newer log2012.log -print
  ```

  ```bash
  [root@localhost test]# find -newer log2012.log
  .
  ./log2015.log
  ./log2017.log
  ./log2016.log
  ./test3
  [root@localhost test]#
  ```

#### 9. 使用 type 选项

- 在 [find 命令](http://www.jianwill.cn/md/linux/find.html) 页面有详细描述；
- 参考 **find 命令 - 实例五** ；

#### 10. 使用 size 选项

- 在 [find 命令](http://www.jianwill.cn/md/linux/find.html) 页面有详细描述；
- 参考 **find 命令 - 实例三** ；

#### 11. 使用 depth 选项

#### 12. 使用 mount 选项

- 在当前的文件系统中查找文件（不进入其他文件系统(windows 下为不进入其他盘，C盘下查询不查询D,E,F盘等)）；

- **实例一：在当前目录下查找位于本文件系统中文件名以 XC 结尾的文件**

  ```bash
  find . -name "*.XC" -mount -print
  ```

  