### mv 命令

- 用来移动文件(或目录)或修改文件名(目录名)；

- **命令格式** - mv [选项] 源文件或目录 目标文件或目录

- **命令功能** - 视 mv 命令中第二个参数类型的不同(是目标文件还是目标目录)，mv 命令将文件重命名或将其移至一个新目录中；

  - **参数2为文件** ：文件重命名。源文件只能有一个(也可以是源目录名)，它将所给的源文件或目录重命名为给定的目标文件名；
  - **参数2为目录名** ：将源文件或源目录名移至目标目录。源文件和源目录名可以有多个。在跨文件系统移动文件时，mv 先拷贝，再将原有文件删除，而链接至该文件的链接也将丢失。

- **命令参数** - 

  - **-b** ：若需覆盖文件，则覆盖前先行备份；
    - **注意：Mac_Terminal 下该参数无效**；
  - **-f** ：若目标文件已存在时，**不会** 询问而直接覆盖；
  - **-i** ：若目标文件已经存在时，**会** 询问是否覆盖；
  - **-u** ：若目标文件已经存在，且 source 比较新，才会更新；
  - **-t** ：—target-directory=DIRECTORY move all SOURCE arguments into DIRECTORY，即指定 mv 的目标目录，用于移动多个源文件到一个目录的情况；此时目标目录在前，源文件在后；
    - **注意：Mac_Terminal 下该参数无效**；

- **命令实例** - 

  - **实例一：文件改名**

  - **命令**

    ```bash
    mv log1.log log2.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir3 qiu$ ll
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 10:03 log1.log
    Qs-MacBook-Pro:dir3 qiu$ mv log1.log log2.log
    Qs-MacBook-Pro:dir3 qiu$ ll
    total 8
    -rw-r--r--@ 1 qiu  staff  9  4 10 10:03 log2.log
    ```

  - **实例二：移动文件**

  - **命令**

    ```bash
    mv log2.log test1
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:t1 qiu$ ls -lR
    total 8
    -rw-r--r--@ 1 qiu  staff  14  4 10 09:50 log2.log
    drwxr-xr-x  3 qiu  staff  96  4 10 09:56 test1
    
    ./test1:
    Qs-MacBook-Pro:t1 qiu$ mv log2.log test1
    Qs-MacBook-Pro:t1 qiu$ ls -lR
    total 0
    drwxr-xr-x  4 qiu  staff  128  4 10 09:57 test1
    
    ./test1:
    total 8
    -rw-r--r--@ 1 qiu  staff  14  4 10 09:50 log2.log
    Qs-MacBook-Pro:t1 qiu$ 
    ```

  - **实例三：将文件 log1.log log2.log log3.log 移动到目录 test2 中**

  - **命令**

    ```bash
    mv log1.log log2.log log3.log test2
    ```

    ```bash
    mv -t test3/ log1.log log2.log log3.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:t1 qiu$ ll
    total 24
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log1.log
    -rw-r--r--@ 1 qiu  staff  14  4 10 09:50 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    drwxr-xr-x  3 qiu  staff  96  4 10 10:02 test1
    Qs-MacBook-Pro:t1 qiu$ mv log1.log log2.log log3.log test1
    Qs-MacBook-Pro:t1 qiu$ ll
    total 0
    drwxr-xr-x  6 qiu  staff  192  4 10 10:04 test1
    Qs-MacBook-Pro:t1 qiu$ cd test1/
    Qs-MacBook-Pro:test1 qiu$ ll
    total 24
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log1.log
    -rw-r--r--@ 1 qiu  staff  14  4 10 09:50 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    Qs-MacBook-Pro:test1 qiu$ 
    ```

    ```bash
    // Mac_Terminal 下 该方法无效 -t参数无效
    [root@localhost test3]# ll
    总计 20
    -rw-r--r-- 1 root root    8 10-28 06:15 log1.txt
    -rw-r--r-- 1 root root   12 10-28 06:15 log2.txt
    -rw-r--r-- 1 root root   13 10-28 06:16 log3.txt
    drwxr-xr-x 2 root root 4096 10-28 06:21 logs
    -rw-r--r-- 1 root root   29 10-28 06:05 test1.txt
    [root@localhost test3]# mv -t /opt/soft/test/test4/ log1.txt log2.txt 	log3.txt 
    [root@localhost test3]# cd ..
    [root@localhost test]# cd test4/
    [root@localhost test4]# ll
    总计 12
    -rw-r--r-- 1 root root  8 10-28 06:15 log1.txt
    -rw-r--r-- 1 root root 12 10-28 06:15 log2.txt
    -rw-r--r-- 1 root root 13 10-28 06:16 log3.txt
    ```

  - **实例四：将文件 file1 改名为 file2，如果 file2 已经存在，则询问是否覆盖**

  - **命令**

    ```bash
    mv -i log1.log log2.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:t1 qiu$ ll
    total 24
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log1.log
    -rw-r--r--@ 1 qiu  staff  14  4 10 09:50 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    drwxr-xr-x  3 qiu  staff  96  4 10 10:05 test1
    Qs-MacBook-Pro:t1 qiu$ mv -i log1.log log2.log
    overwrite log2.log? (y/n [n]) y
    Qs-MacBook-Pro:t1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    drwxr-xr-x  3 qiu  staff  96  4 10 10:05 test1
    ```

  - **实例五：将文件 file1 改名为 file2，即使file2 存在，也直接覆盖掉**

  - **命令**

    ```bash
    mv -f log1.log log2.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:t1 qiu$ ll
    total 24
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log1.log
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    drwxr-xr-x  3 qiu  staff  96  4 10 10:05 test1
    Qs-MacBook-Pro:t1 qiu$ mv -f log1.log log2.log
    Qs-MacBook-Pro:t1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    drwxr-xr-x  3 qiu  staff  96  4 10 10:05 test1
    ```

  - **实例六：目录的移动**

  - **命令**

    **注意：dir2 已经存在**

    ```bash
    mv dir1 dir2
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:test1 qiu$ ll
    total 0
    drwxr-xr-x  2 qiu  staff  64  4 10 10:17 dir1
    drwxr-xr-x  2 qiu  staff  64  4 10 10:17 dir2
    Qs-MacBook-Pro:test1 qiu$ mv dir1 dir2
    Qs-MacBook-Pro:test1 qiu$ ll
    total 0
    drwxr-xr-x  3 qiu  staff  96  4 10 10:18 dir2
    Qs-MacBook-Pro:test1 qiu$ cd dir2/
    Qs-MacBook-Pro:dir2 qiu$ ll
    total 0
    drwxr-xr-x  2 qiu  staff  64  4 10 10:17 dir1
    ```

  - **实例七：目录的改名**

  - **命令**

    **注意：dir2 不存在**

    ```bash
    mv dir1 dir2
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir2 qiu$ ll
    total 0
    drwxr-xr-x  2 qiu  staff  64  4 10 10:17 dir1
    Qs-MacBook-Pro:dir2 qiu$ mv dir1 dir2
    Qs-MacBook-Pro:dir2 qiu$ ll
    total 0
    drwxr-xr-x  2 qiu  staff  64  4 10 10:17 dir2
    ```

  - **实例八：移动当前文件夹下的所有文件到上一级目录**

  - **命令**

    ```bash
    mv * ../
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir2 qiu$ ll
    total 16
    drwxr-xr-x  2 qiu  staff  64  4 10 10:24 dir3
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    Qs-MacBook-Pro:dir2 qiu$ mv * ../
    Qs-MacBook-Pro:dir2 qiu$ ll
    Qs-MacBook-Pro:dir2 qiu$ cd ../
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 16
    drwxr-xr-x  2 qiu  staff  64  4 10 10:26 dir2
    drwxr-xr-x  2 qiu  staff  64  4 10 10:24 dir3
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    ```

  - **实例九：将当前目录的一个子目录中的文件移动到另一个子目录中**

  - **命令**

    ```bash
    mv dir2/* dir3
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 0
    drwxr-xr-x  5 qiu  staff  160  4 10 10:27 dir2
    drwxr-xr-x  2 qiu  staff   64  4 10 10:24 dir3
    
    ./dir2:
    total 16
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    
    ./dir3:
    Qs-MacBook-Pro:dir1 qiu$ mv dir2/* dir3
    Qs-MacBook-Pro:dir1 qiu$ ls -lR
    total 0
    drwxr-xr-x  3 qiu  staff   96  4 10 10:30 dir2
    drwxr-xr-x  4 qiu  staff  128  4 10 10:30 dir3
    
    ./dir2:
    
    ./dir3:
    total 16
    -rw-r--r--@ 1 qiu  staff   9  4 10 10:03 log2.log
    -rw-r--r--@ 1 qiu  staff  12  4 10 10:03 log3.log
    ```

  - **实例十：文件被覆盖前做简单备份，前面加参数 -b**

  - **命令**

    ```bash
    mv log1.txt -b log2.txt
    ```

  - **输出**

    ```bash
    // Mac_Terminal 下该方法无效，-b参数无效
    [root@localhost test5]# ll
    -rw-r--r-- 1 root root   25 10-28 07:02 log1.txt
    -rw-r--r-- 1 root root   13 10-28 06:16 log2.txt
    -rw-r--r-- 1 root root   29 10-28 06:05 test1.txt
    drwxr-xr-x 2 root root 4096 10-25 17:56 test5-1
    [root@localhost test5]# mv log1.txt -b log2.txt
    mv：是否覆盖“log2.txt”? y
    [root@localhost test5]# ll
    -rw-r--r-- 1 root root   25 10-28 07:02 log2.txt
    -rw-r--r-- 1 root root   13 10-28 06:16 log2.txt~
    -rw-r--r-- 1 root root   29 10-28 06:05 test1.txt
    drwxr-xr-x 2 root root 4096 10-25 17:56 test5-1
    ```

  - **说明**

    - **-b** 不接收参数，mv 会去读取环境变量 **VERSION_CONTROL** 来作为备份策略；
    - 共有四种备份策略：
      - **CONTROL=none或off** ：不备份；
      - **CONTROL=numbered或t** ：数字编号的备份；
      - **CONTROL=existing或nil** ：如果存在以数字编号的备份，则继续编号备份 m+1…n：执行mv操作前已存在以数字编号的文件 log2.txt.~1~，那么再次执行将产生 log2.txt.~2~，以此类推；如果之前没有以数字编号的文件，则使用下面讲到的简单备份；
      - **CONTROL=simple或never** ：简单备份：在备份前进行了简单备份，简单备份只能有一份，再次被覆盖时，简单备份也会被覆盖；