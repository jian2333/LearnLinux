### find 命令概览

- **Linux** 下 **find** 命令在目录结构中搜索文件，并执行指定的操作；

- **Linux** 下的 **find** 命令提供了相当多的查找条件，功能强大。即使文件中含有网络文件系统(**NFS**)，**find** 命令在该文件系统中同样有效，只要你具有相应的权限；

- 在运行一个非常消耗资源的 **find** 命令时，很多人都倾向于把它放在后台执行，因为遍历一个大的文件系统可能会花费很长的时间（这里指 30G 字节以上的文件系统）；

- **命令格式** - find pathname -options [-print -exec -ok ...]

- **命令功能** - 用于在文件树中查找文件，并作出相应的处理；

- **命令参数** - 
  - **pathname** ：**find** 命令所查找的目录路径。
    - **\*** 表示当前目录；
    - **/** 表示系统根目录；
    - **必填！必填！必填！**；
  - **-print** ：**find** 命令将匹配的文件输出到标准输出中；
  - **-exec** ：**find** 命令对匹配的文件执行该参数所给出的 **shell** 命令；
    - 相应命令的形式为 **'command' { } \\;** ，注意 **{ }** 和 **\\;** 之间的空格；
  - **-ok** ：和 **-exec** 的作用相同，只不过以一种更为安全的模式来执行该参数所给出的 **shell** 命令，在执行每一个命令之前，都会给出提示，让用户来确定是否执行；
  
- **命令选项** - 
  - **-name** ：按照文件名来查找文件；
  - **-perm** ：按照文件权限来查找文件；
  - **-prune** ：使用这一选项可以使 **find** 命令不在当前指定的目录中查找，如果同时使用 **-depth** ，那么 **-prune** 将会被 **find** 命令忽略；
  - **-depth** ：从指定目录下的最深层的子目录开始查找；
  - **-user\<拥有者名称\>** ：查找符合指定拥有者名称的文件或目录；
  - **-group\<群组名称\>** ：查找符合指定之群组名称的文件或目录；
  - **-nouser** ：超早无有效所属拥有者的文件，即该文件所属的拥有者在 **/etc/passwd** 中不存在；
  - **-nogroup** ：查找无有效所属群组的文件，即该文件所属的组在 **/etc/groups** 中不存在；
  - **-mtime -n +n** ：按照文件的更改时间来查找文件；
    - **-n** 表示更改时间距现在 **n** 天以内；
    - **+n** 表示更改时间距现在 **n** 天以外；
    - 类似的还有 **-atime** 和 **-ctime** ，参数和 **-mtime** 一样，功能在下方介绍；
  - **-newer file1 ! file2** ：查找更改时间比文件 **file1** 新但比文件 **file2** 旧的文件；
  - **-type** 查找某一类型的文件：
    - **b** ：块设备文件；
    - **d** ：目录；
    - **c** ：字符设备文件；
    - **p** ：管道文件；
    - **l** ：符号链接文件；
    - **f** ：普通文件；
  - **-size n[c]** ：查找长度为 **n** 的文件，**c** 的类型有：
    - **b** ：块（512字节）；
    - **c** ：字节；
    - **w** ：字（2字节）；
    - **k** ：千字节（kb）；
    - **M** ：兆字节（M）；
    - **G** ：吉字节（G）；
  - **-fstype** ：查找位于某一类型文件系统中的文件，这些文件系统类型通常可以在配置文件 **/etc/fstab** 中找到，该配置文件中包含了本系统中有关系统文件的信息；
  - **-mount** ：在查找文件时不跨越文件系统 **mount** 点；
  - **-follow** ：如果 **find** 明星遇到符号链接文件，就跟踪至链接所指向的文件；
  - **-cpio** ：对匹配的文件使用 **cpio** 命令，将这些文件备份到磁带设备中。
  - 另外，下面三个的区别：
    - **-amin n** ：查找文件系统中正好 **前n分钟时** **访问** 的文件；
    - **-atime n** ：查找文件系统中正好 **前n*24小时时** **访问** 的文件；
    - **-cmin n** ：查找系统中正好 **前n分钟时** ，文件 **状态** 被改变的文件；
    - **-ctime n** ：查找系统中正好 **前n*24小时时** ，文件 **状态** 被改变的文件；
    - **-mmin n** ：查找系统中正好 **前n分钟时** ，文件 **数据** 被改变的文件；
    - **-mtime n** ：查找系统中正好 **前n*24小时时**，文件 **数据** 被改变的文件；
    - **-n** ：**n** （分钟/小时）以内；
    - **n** ：正好 **n**（分钟/小时）时；
    - **+n** ：**n** （分钟/小时）以外； 
  
- **命令实例** - 

- **实例一：查找当前目录下 2 天内访问过的文件；**

- **命令**

  ```bash
  find . -atime -2
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:personal qiu$ find . -atime -2
  .
  ./es1.html
  ./t1.json
  ./es1.js
  ./es1.css
  ./js1.js
  ./t1
  ./t1/test1
  ./t1/test1/dir1
  ./t1/test1/dir1/dir2
  ./t1/test1/dir1/dir3
  ./t1/test1/dir1/dir1
  ./t1/log2.log
  ./t1/log3.log
  ```

- **实例二：根据关键字查找**

- **命令**

  ```bash
  find . -name "*.log"
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:personal qiu$ find . -name "*.log"
  ./t1/test1/dir1/dir2/log2.log
  ./t1/test1/dir1/dir2/log1.log
  ./t1/test1/dir1/dir3/log1.log
  ./t1/test1/dir1/dir1/log.log
  ./t1/test1/dir1/dir1/log1.log
  ./t1/log2.log
  ./t1/log3.log
  ```

- **实例三：按文件大小查找**

- **命令**

  ```bash
  find . -size +10c -print
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:personal qiu$ find . -size +10c -print
  .
  ./es1.html
  ./.DS_Store
  ./t1.json
  ./es1.js
  ./es1.css
  ./js1.js
  ./t1
  ./t1/.DS_Store
  ./t1/test1
  ./t1/test1/.DS_Store
  ./t1/test1/dir1
  ./t1/test1/dir1/.DS_Store
  ./t1/test1/dir1/dir2
  ./t1/test1/dir1/dir2/.DS_Store
  ./t1/test1/dir1/dir3
  ./t1/test1/dir1/dir3/.DS_Store
  ./t1/test1/dir1/dir1
  ./t1/test1/dir1/dir1/log.log
  ./t1/test1/dir1/dir1/.DS_Store
  ./t1/test1/dir1/dir1/log1.log
  ./t1/log3.log
  ```

- **实例四：按照目录或文件的权限来查找**

- **命令**

  ```bash
  find /opt/soft/test/ -perm 777
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:personal qiu$ find /opt/soft/test/ -perm 777
  /opt/soft/test/log_link.log
  /opt/soft/test/test4
  /opt/soft/test/test5/test3
  /opt/soft/test/test3
  ```

- **实例五：按类型查找**

- **命令**

  ```bash
  find . -type f -name "*.log"
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:personal qiu$ find . -type f -name "*.log"
  ./t1/test1/dir1/dir2/log2.log
  ./t1/test1/dir1/dir2/log1.log
  ./t1/test1/dir1/dir3/log1.log
  ./t1/test1/dir1/dir1/log.log
  ./t1/test1/dir1/dir1/log1.log
  ./t1/log2.log
  ./t1/log3.log
  
  ```

- **实例六：查找当前所有目录并排序**

- **命令**

  ```bash
  find . -type d | sort
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:personal qiu$ find . -type d | sort
  .
  ./t1
  ./t1/test1
  ./t1/test1/dir1
  ./t1/test1/dir1/dir1
  ./t1/test1/dir1/dir2
  ./t1/test1/dir1/dir3
  
  ```

  