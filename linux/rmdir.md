### rmdir 命令

- 删除一个空目录；

- **命令格式** - rmdir [选项] 目录...

- **命令功能** - 从一个目录中删除一个或多个子目录；

  - 必须对目录有写权限；
  - 必须是空目录；

- **命令参数** - 

  - **-p** ：递归删除目录，当子目录删除后其父目录为空时，父目录也一同被删除。如果整个路径被删除或者由于某些原因保留部分路径，则系统在标准输出上显示相应的信息；
  - **-v** ：显示指令执行的过程；

- **命令实例** - 

  - rmdir 不能删除非空目录；

    ```bash
    Qs-MacBook-Pro:personal qiu$ rmdir t1
    rmdir: t1: Directory not empty
    ```

  - rmdir -p 当子目录被删除后使它也成为空目录的话，则顺便一并删除；

    和 mkdir -p 对应；

    ```bash
    Qs-MacBook-Pro:t1 qiu$ ls -R
    t21
    ./t21:
    t211
    ./t21/t211:
    t2111
    ./t21/t211/t2111:
    Qs-MacBook-Pro:t1 qiu$ rmdir -p t21/t211/t2111
    Qs-MacBook-Pro:t1 qiu$ ls -R
    ```

    