### du 命令

- **Linux** **du** 命令也是对空间的查看，但是和 **df** 命令不同的是，**du** 命令是对文件和目录磁盘使用的空间进行查看。

- **命令格式** - du [选项] [文件或目录]

- **命令功能** - 显示每个文件或目录的磁盘使用空间

- **命令参数** - 

  - **-a或-all** ：显示目录中个别文件的大小；
  - **-b或-bytes** ：显示文件或目录大小时，以 **byte** 为单位；
  - **-c或--total** ：除了显示个别目录或文件的大小外，同时也显示所有文件或目录的总和；
  - **-k或--kilobytes** ：以 **KB(1024bytes)** 为单位输出；
  - **-m或--megabytes** ：以 **MB** 为单位输出；
  - **-s或--summarize** ：仅显示总和，只列出最后总和的值；
  - **-h或--human-readable** ：以 **K，M，G** 为单位，提高信息的可读性；
  - **-x或--one-file-xystem** ：以一开始处理时的文件系统为准，若遇上其他不同的文件系统则略过；
  - **-L\<符号链接\>或--dereference\<符号链接\>** ：显示选项中所指定符号链接的源文件大小；
  - **-S或--separate-dirs** ：显示个别目录大小时，不包含其子目录的大小；
  - **-X\<文件\>或--exclude-from=\<文件\>** ：在 \<文件\> 指定目录或文件；
  - **--exclude=\<目录或文件>** ：略过指定的目录或文件；
  - **-D或--dereference-args** ：显示指定符号链接的源文件大小；
  - **-H或--si** ：与 **-h** 参数相同，但是 **K，M，G** 是以 1000 为单位换算的；
  - **-l或--count-links** ：重复计算硬件链接的文件；

- **命令实例** - 

- **实例一：显示目录或文件所占空间**

- **命令**

  ```bash
  du
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du
  32	./test1
  64	.
  
  ```

- **说明**

  只显示当前目录下面的子目录大小和当前目录的总的大小。最下面的64为当前目录的总大小

- **实例二：显示指定文件所占空间**

- **命令**

  ```bash
  du log1.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du log1.log
  8	log1.log
  ```

- **说明**

- **实例三：显示指定目录所占空间**

- **命令**

  ```bash
  du test1
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du test1
  32	test1
  
  ```

- **说明**

- **实例四：显示多个文件所占空间**

- **命令**

  ```bash
  du log.log log1.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du log.log log1.log
  8	log.log
  8	log1.log
  ```

- **说明**

- **实例五：只显示总和的大小**

- **命令**

  ```bash
  du -s
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du -s
  64	.
  Qs-MacBook-Pro:dir1 qiu$ du -s test1
  32	test1
  ```

- **说明**

- **实例六：方便阅读的格式显示**

- **命令**

  ```bash
  du -h
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du -h
   16K	./test1
   32K	.
  
  ```

- **说明**

- **实例七：文件和目录都显示**

- **命令**

  ```bash
  du -ah 
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du -ah
  4.0K	./log.log
  8.0K	./.DS_Store
  8.0K	./test1/.DS_Store
  4.0K	./test1/t1-2.log
  4.0K	./test1/t1-1.log
   16K	./test1
  4.0K	./log1.log
   32K	.
  
  ```

- **说明**

- **实例八：显示几个文件或目录各自占用磁盘空间的大小，并统计它们的总和**

- **命令**

  ```bash
  du -c log.log log1.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ du -c log.log log1.log
  8	log.log
  8	log1.log
  16	total
  ```

- **说明**

  加上 **-c** 选项后，**du** 不仅显示两个目录各自占用磁盘空间的大小，还在最后一行统计它们的总和；

- **实例九：按照空间大小排序**

- **命令**

  ```bash
  du|sort -nr|more
  ```

- **输出**

  ```bash
  [root@localhost test]# du|sort -nr|more
  1288    .
  608     ./test6
  308     ./test4
  32      ./scf
  16      ./scf/service
  12      ./scf/service/deploy
  8       ./test3
  4       ./scf/service/deploy/product
  4       ./scf/service/deploy/info
  4       ./scf/lib
  4       ./scf/doc
  4       ./scf/bin
  ```

- **说明**

- **实例十：输出当前目录下各个子目录所使用的空间**

- **命令**

  ```bash
  du -h --max-depth=1
  ```

- **输出**

  ```bash
  [root@localhost test]# du -h  --max-depth=1
  608K    ./test6
  308K    ./test4
  32K     ./scf
  8.0K    ./test3
  1.3M    .
  [root@localhost test]#
  ```

- **说明**