### rm 命令

- 删除一个目录中的一个或多个文件或目录；

- **命令格式** - rm [选项] 文件；

- **命令功能** - 删除一个目录中的一个或多个文件或目录；

  - 必读对文件或目录有写权限；
  - 如果没有使用 **-r** 选项，则 **rm** 不会删除目录；
  - **rm** 删除的文件，一般都可恢复；

- **命令参数** - 

  - **-f** ：—force，忽略不存在的文件，从不给出提示；
  - **-i** ：—interactive，进行交互式删除；
  - **-r，-R** ：—recursive，将参数中列出的全部目录和子目录均递归删除；
  - **-v** ：—verbose，详细显示进行的步骤；

- **命令实例** -

  - 删除文件file，系统会先询问是否删除；

    **注意** ：**Mac_Terminal** 下直接删除；

    ```bash
    rm log.log
    rm：是否删除 一般文件 “log.log”? y
    ```

  - 强行删除file，系统不提示；

    ```bash
    rm -f log.log
    ```

  - 删除任何 .log 文件，删除前逐一确认；

    ```bash
    rm -i *.log
    rm：是否删除 一般文件 “log1.log”? y
    rm：是否删除 一般文件 “log2.log”? y
    ```

  - 将 test1 子目录及子目录中的所有档案删除；

    ```bash
    rm -r test1
    rm：是否进入目录 “test1”? y
    rm：是否删除 一般文件 “test1/log3.log”? y
    rm：是否删除 目录 “test1”? y
    ```

  - 将 test2 子目录及子目录中的所有档案删除，并且不用一一确认；

    **所以 rm -rf xx 是很危险滴！**；

    ```bash
    rm -rf test2
    ```

  - 删除以 -f 开头的文件'

    **在 Mac_Terminal** 下无效；

    ```bash
    rm -- -f
    rm：是否删除 一般空文件 “-f”? y
    ```

    ```bash
    rm ./-f
    rm：是否删除 一般空文件 “./-f”? y
    ```

  - 自定义回收站功能；

    就是把删除操作变成把文件放到一个临时目录中；

    ```bash
    myrm(){ D=/tmp/$(date +%Y%m%d%H%M%S); mkdir -p $D; mv "$@" $D && echo "moved to $D ok"; }
    ```

    ```bash
    [root@localhost test]# myrm(){ D=/tmp/$(date +%Y%m%d%H%M%S); mkdir -p $D;  mv "$@" $D && echo "moved to $D ok"; }
    [root@localhost test]# alias rm='myrm'
    [root@localhost test]# touch 1.log 2.log 3.log
    [root@localhost test]# ll
    总计 16
    -rw-r--r-- 1 root root    0 10-26 15:08 1.log
    -rw-r--r-- 1 root root    0 10-26 15:08 2.log
    -rw-r--r-- 1 root root    0 10-26 15:08 3.log
    drwxr-xr-x 7 root root 4096 10-25 18:07 scf
    drwxrwxrwx 2 root root 4096 10-25 17:46 test3
    drwxr-xr-x 2 root root 4096 10-25 17:56 test4
    drwxr-xr-x 3 root root 4096 10-25 17:56 test5
    [root@localhost test]# rm [123].log
    moved to /tmp/20121026150901 ok
    [root@localhost test]# ll
    总计 16drwxr-xr-x 7 root root 4096 10-25 18:07 scf
    drwxrwxrwx 2 root root 4096 10-25 17:46 test3
    drwxr-xr-x 2 root root 4096 10-25 17:56 test4
    drwxr-xr-x 3 root root 4096 10-25 17:56 test5
    [root@localhost test]# ls /tmp/20121026150901/
    1.log  2.log  3.log
    [root@localhost test]#
    ```

    