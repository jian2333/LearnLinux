### cp 命令

- 复制文件或目录；

- **命令格式** -

  - cp [选项] [-T] 源 目标
  - cp [选项] 源 目标
  - cp [选项] -t 目标 源

- **命令功能** - 将源文件复制至目标文件，或将多个源文件复制至目标目录；

- **命令参数** - 

  - **-a** ：为每个已存在的目标文件创建备份。即新文件与已存在的文件完全一样，保留链接、文件属性，并复制目录下的所有内容。其作用等于dpR参数组合；
  - **-b**：类似 —backup 但不接收参数，在递归处理时复制特殊文件的内容；
  - **-d** ：复制时保留链接。这里所说的链接相当于Windows里的快捷方式；
  - **-f** ：覆盖已经存在的目标文件而不给出提示；
  - **-i** ：与 **-f** 相反，覆盖目标文件之前给出提示；
  - **-l** ：对源文件建立 **硬链接** ，不复制文件，只是生成链接文件；
    - **注意：Mac_Terminal 下该参数无效**；
  - **-p** ：除复制文件的内容外，还把修改时间和访问权限也复制到新文件中；
  - **-R，-r** ：若给出的源文件是一个目录文件，此时也将复制该目录下所有的子目录和文件；
  - **-s** ：对源文件建立 **符号链接** ，而非复制文件；
    - **注意：Mac_Terminal 下该参数无效**；
  - 关于 **硬链接** 和 **符号链接**  的区别：
    - 硬链接 和 源文件 是同一个文件；符号链接 和 源文件 是两个不同的文件；
    - 符号链接 相当于 Windows 下的快捷方式；
    - 大部分系统不能创建 目录 的硬链接，符号链接 则没有该限制；
    - 硬链接 不能跨文件系统(分区)，符号链接 则没有这个限制；

- **命令实例** -

  - **实例一：复制单个文件到目标目录，文件在目标文件中不存在**

  - **命令**

    ```bash
    cp log1.log dir2
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ls -R
    dir2     log1.log
    
    ./dir2:
    Qs-MacBook-Pro:dir1 qiu$ cp log1.log dir2
    Qs-MacBook-Pro:dir1 qiu$ ls -R
    dir2     log1.log
    
    ./dir2:
    log1.log
    ```

  - **说明**

    没有带 **-a** 参数时，两个文件的时间是不一样的。在带了 **-a** 参数时，两个文件的时间是一致的；

  - **实例二：目标文件存在时，会询问是否覆盖**

  - **命令**

    ```bash
    cp -i log1.log dir2
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 8
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir2
    -rw-r--r--@ 1 qiu  staff    9  4 10 10:03 log1.log
    
    ./dir2:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:50 log1.log
    Qs-MacBook-Pro:dir1 qiu$ cp -i log1.log dir2
    overwrite dir2/log1.log? (y/n [n]) y
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 8
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir2
    -rw-r--r--@ 1 qiu  staff    9  4 10 10:03 log1.log
    
    ./dir2:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    ```

  - **说明**

    - 在 **Linux** 下，cp 和 cp -i 是一样的；
    - 在 **Mac_Terminal** 下，cp 和 cp -f 是一样的；

  - **实例三：复制整个目录**

  - **命令**

    ```bash
    cp -a dir1 dir2
    cp -a dir1 dir3
    ```

  - **输出**

    ```bash
    // 目标目录存在时
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 0
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir1
    drwxr-xr-x  4 qiu  staff  128  4 10 11:54 dir2
    
    ./dir1:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    
    ./dir2:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log2.log
    Qs-MacBook-Pro:dir1 qiu$ cp -a dir1 dir2
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 0
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir1
    drwxr-xr-x  5 qiu  staff  160  4 10 11:57 dir2
    
    ./dir1:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    
    ./dir2:
    total 8
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir1
    -rw-r--r--@ 1 qiu  staff    9  4 10 11:52 log2.log
    
    ./dir2/dir1:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    ```

    ```bash
    // 目标目录不存在时
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 0
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir1
    drwxr-xr-x  4 qiu  staff  128  4 10 12:00 dir2
    
    ./dir1:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    
    ./dir2:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log2.log
    Qs-MacBook-Pro:dir1 qiu$ cp -a dir1 dir3
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 0
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir1
    drwxr-xr-x  4 qiu  staff  128  4 10 12:00 dir2
    drwxr-xr-x  4 qiu  staff  128  4 10 11:47 dir3
    
    ./dir1:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    
    ./dir2:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log2.log
    
    ./dir3:
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 11:52 log1.log
    ```

  - **说明**

    目标目录存在时，复制源目录到目标目录 **里面**；

    目标目录不存在时，创建新目录；

  - **实例四：复制 log.log 建立一个 链接档 log_link.log**

  - **命令**

    ```bash
    cp -s log.log log_link.log
    ```

  - **输出**

    ```bash
    // Mac_Terminal 下该方法无效，-s 参数无效
    [root@localhost test]# cp -s log.log log_link.log
    [root@localhost test]# ll
    lrwxrwxrwx 1 root root    7 10-28 15:18 log_link.log -> log.log
    -rw-r--r-- 1 root root    0 10-28 14:48 log.log
    drwxr-xr-x 6 root root 4096 10-27 01:58 scf
    drwxrwxrwx 2 root root 4096 10-28 14:47 test3
    drwxrwxrwx 2 root root 4096 10-28 14:47 test4
    drwxr-xr-x 3 root root 4096 10-28 15:11 test5
    ```

  - **说明**

    那个 log_link.log 是由 -s 参数生成的，建立的是一个 "快捷方式" ，所以在文件的最右边，会显示这个文件是 "链接" 到哪去的！