### find 命令之 exec

- **find exec** 表示查找出文件后，再进行进一步操作；

- **exec解释**

  - **-exec** 参数后面跟的是 **command** 命令，它的终止是以 **;** 为结束标志的，所以这句命令后面的分号是不可缺少的。考虑到不同系统中分号会有不同的意义，所以前面 **加反斜杠\\** ；

  - **{}** 花括号代表前面 **find** 查找出来的文件名；

  - 使用 **find** 时，只要把想要的操作写在一个文件里，就可以用 **exec** 来配合 **find** 查找，很方便的；

  - 在有些操作系统中只允许 **-exec** 选项执行诸如 **ls** 或 **ls -l** 这样的命令。大多数用户使用这一选项是为了 **查找旧文件并删除它们** 。建议在真正执行 **rm** 命令删除文件之前，最好先用 **ls** 命令查看一下，确保它们是所要删除的文件；

  - **exec** 选项后面跟随着要执行的命令或脚本，然后是一对 **{}** ，一个空格和一个 **\\** ，最后是一个分号 **;** ；

  - 为了使用 **exec** 选项，必须要同时使用 **print** 选项。如果验证一下 **find** 命令，会发现该命令只输出从 **当前路径(find找到的路径)起的相对路径及文件名** ；

  - **实例一：ls -l 命令放在 find 命令的 -exec 选项中**

  - **命令**

    ```bash
    find . -type f -exec ls -l {} \;
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:personal qiu$ find . -type f -exec ls -l {} \;
    -rw-r--r--@ 1 qiu  staff  642  4 19 17:48 ./es1.html
    -rw-r--r--@ 1 qiu  staff  6148  4 10 12:48 ./.DS_Store
    -rw-r--r--@ 1 qiu  staff  153  4  5 22:24 ./t1.json
    -rw-r--r--@ 1 qiu  staff  8432  4 20 14:17 ./es1.js
    -rw-r--r--@ 1 qiu  staff  392  4 19 17:52 ./es1.css
    -rw-r--r--@ 1 qiu  staff  186  4  5 22:24 ./js1.js
    -rw-r--r--@ 1 qiu  staff  6148  4 19 23:02 ./t1/.DS_Store
    -rw-r--r--@ 1 qiu  staff  6148  4 10 10:23 ./t1/test1/.DS_Store
    -rw-r--r--@ 1 qiu  staff  6148  4 11 17:06 ./t1/test1/dir1/.DS_Store
    -rw-r--r--@ 1 qiu  staff  6148  4 10 12:00 ./t1/test1/dir1/dir2/.DS_Store
    -rw-r--r--@ 1 qiu  staff  9  4 11 09:44 ./t1/test1/dir1/dir2/log2.log
    -rw-r--r--  1 qiu  staff  0  4 11 09:09 ./t1/test1/dir1/dir2/log1.log
    -rw-r--r--@ 1 qiu  staff  6148  4 10 12:00 ./t1/test1/dir1/dir3/.DS_Store
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 ./t1/test1/dir1/dir3/log1.log
    -rw-r--r--@ 1 qiu  staff  96  4 16 15:25 ./t1/test1/dir1/dir1/log.log
    -rw-r--r--@ 1 qiu  staff  6148  4 18 10:17 ./t1/test1/dir1/dir1/.DS_Store
    -rw-r--r--  1 qiu  staff  50  4 14 11:01 ./t1/test1/dir1/dir1/log1.log
    -rw-r--r--@ 1 qiu  staff  9  4 10 10:03 ./t1/log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 ./t1/log3.log
    ```

  - **实例二：查找目录中更改时间在 1日以内 的文件并删除它们**

  - **命令**

    ```bash
    find . -type f -ctime -1 -exec rm {} \;
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1
    ./lognew.log
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1 -exec rm {} \;
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1 
    Qs-MacBook-Pro:dir1 qiu$ 
    ```

    

  - **实例三：查找目录中更改时间在 1日以内 的文件并删除它们，删除前给出提示**

  - **命令**

    ```bash
    find . -type f -ctime -1 -ok rm {} \;
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1
    ./lognew1.log
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1 ok rm {} \;
    find: ok: unknown primary or operator
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1 -ok rm {} \;
    "rm ./lognew1.log"? n
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1 
    ./lognew1.log
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1 -ok rm {} \;
    "rm ./lognew1.log"? y
    Qs-MacBook-Pro:dir1 qiu$ find . -type f -ctime -1
    Qs-MacBook-Pro:dir1 qiu$ 
    ```

  - **说明**

    按 **y + 回车** 删除，按 **n + 回车** 不删除； 

  - **实例四：-exec 中使用 grep 命令查看这些文件是否存在一个 root 用户**

  - **命令**

    ```bash
    find /etc -name "passwd" -exec grep "root" {} \;
    ```

  - **输出**

    ```bash
    [root@localhost test]# find /etc -name "passwd*" -exec grep "root" {} \;
    root:x:0:0:root:/root:/bin/bash
    root:x:0:0:root:/root:/bin/bash
    [root@localhost test]#
    ```

  - **说明**

    任何形式的命令都可以在 **-exec** 选项中使用。

    在上面的例子中我们使用 **grep** 命令。**find** 命令首先匹配所有文件名为 **passwd** 的文件，例如 **passed、passwd.old、passwd.bak** ，然后执行 **grep** 命令看看这些文件中是否存在一个 **root** 用户；

  - **实例五：查找文件移动到指定目录 mv**

  - **命令**

    ```bash
    find . -name "*.log" -exec mv {} ../ \;
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ pwd
    /Users/qiu/mine/personal/t1/test1/dir1/dir1
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    drwxr-xr-x  4 qiu  staff  128  4 21 10:08 test1
    Qs-MacBook-Pro:dir1 qiu$ cd test1
    Qs-MacBook-Pro:test1 qiu$ pwd
    /Users/qiu/mine/personal/t1/test1/dir1/dir1/test1
    Qs-MacBook-Pro:test1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff  96  4 16 15:25 log.log
    -rw-r--r--  1 qiu  staff  50  4 14 11:01 log1.log
    Qs-MacBook-Pro:test1 qiu$ find . -name "*.log" -exec mv {} ../ \;
    Qs-MacBook-Pro:test1 qiu$ ll
    Qs-MacBook-Pro:test1 qiu$ cd ../
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff  96  4 16 15:25 log.log
    -rw-r--r--  1 qiu  staff  50  4 14 11:01 log1.log
    drwxr-xr-x  2 qiu  staff  64  4 21 10:09 test1
    ```

  - **实例六：查找文件复制到指定目录 cp**

  - **命令**

    ```bash
    find . -name "*.log" -exec cp {} test \;
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:test qiu$ pwd
    /Users/qiu/mine/personal/t1/test1/dir1/dir1/test
    Qs-MacBook-Pro:test qiu$ ll
    Qs-MacBook-Pro:test qiu$ cd ../
    Qs-MacBook-Pro:dir1 qiu$ pwd
    /Users/qiu/mine/personal/t1/test1/dir1/dir1
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff  96  4 16 15:25 log.log
    -rw-r--r--  1 qiu  staff  50  4 14 11:01 log1.log
    drwxr-xr-x  2 qiu  staff  64  4 21 10:03 test
    Qs-MacBook-Pro:dir1 qiu$ find . -name "*.log" -exec cp {} test \;
    cp: test/log.log and ./test/log.log are identical (not copied).
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff   96  4 16 15:25 log.log
    -rw-r--r--  1 qiu  staff   50  4 14 11:01 log1.log
    drwxr-xr-x  4 qiu  staff  128  4 21 10:04 test
    Qs-MacBook-Pro:dir1 qiu$ cd test
    Qs-MacBook-Pro:test qiu$ pwd
    /Users/qiu/mine/personal/t1/test1/dir1/dir1/test
    Qs-MacBook-Pro:test qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff  96  4 21 10:04 log.log
    -rw-r--r--  1 qiu  staff  50  4 21 10:04 log1.log
    ```

    