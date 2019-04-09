### ls 命令

- 打印目录下的清单；

- **命令格式** - ls [选项] [目录名]；

- **命令功能** - 列出目标目录下的所有子目录和文件；

- **常用命令参数** - 

  - -a，-all ：列出目录下(不包括孙目录)所有文件，包括以 . 开头的隐藏文件；
  - -A ：同 -a，但不列出 "."(表示当前目录) 和 ".."(表示当前目录的父目录)；
  - -c ：
    - 配合 -lt：根据 ctime 排序及显示 ctime(文件状态最后修改时间)；
    - 配合 -l ：显示 ctime 但根据名称排序；
    - 其他情况 ：以 ctime 排序；
  - -f ：直接列出结果不排序；
  - -g ：列表显示结果，和 -l 类似，但不显示文件所有者；
  - -G ：–no-group 不列出任何有关组的信息；
    - mac终端下：目录列表以 **彩色** 显示；
  - -h ：将文件内容大小以 GB、KB等易读的方式显示；
  - -i ：列出每个文件的 inode 号；
  - -l ：除了文件名外，还列出 文件的权限，所有者，文件大小等信息；
  - -r ： 倒序排序；
  - -R ：同时列出所有子目录层；
  - -S ：以文件大小排序(大的在前)；
  - -t ：以文件修改时间排序(旧的在前)；
  - -1 ：每行只列出1个文件；

- **常用范例** - 

  - 列出 /home/aa 文件下的所有文件和目录的详细资料

    ```bash
    ls -lR /home/aa
    ```

  - 列出当前目录下所有以 "t" 开头的目录的详细内容

    ```bash
    ls -l t*
    ```

  - 只列出文件下的子目录

    - 列出 /opt/soft 文件下面的子目录

      ```bash
      ls -F /opt/soft |grep /$
      ```

    - 列出 /opt/soft 文件下的子目录详细情况

      ```bash
      ls -l/opt/soft |grep "^d"
      ```

  - 列出当前目录下所有名称是s 开头的，新的排后面

    ```bash
    ls -ltr s*
    ```

  - 列出当前目录下的文件数和目录数

    - 文件个数

      ```bash
      ls -l * |grep "^-"|wc -l
      ```

    - 目录个数

      ```bash
      ls -l * |grep "^d"|wc -l
      ```

  - 在ls中列出文件的绝对路径

    ```bash
    ls | sed "s:^:pwd/:"
    ```

  - 列出当前目录下的所有文件(包括隐藏文件)的绝对路径，对目录不做递归

    ```bash
    find $PWD -maxdepth 1 | xargs ls -ld
    ```

  - 递归列出当前目录下的所有文件(包括隐藏文件)的绝对路径

    ```bash
    find $PWD | xargs ls -ld
    ```