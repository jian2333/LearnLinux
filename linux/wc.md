### wc 命令

- **Linux** 中的 **wc(Word Count)** 命令的功能为统计指定文件中的字节数、字数、行数，并将统计结果显示输出；

- **命令格式** - wc [选项] [文件]

- **命令描述** - 

  - 统计指定文件中的字节数、字数、行数，并将结果显示输出；
  - 如果没有给出文件名，则从标准输入读取；
  - **wc** 同时也给出所指定文件的总统计数；

- **命令参数** - 

  - **-c** ：统计字节数；
  - **-l** ：统计行数；
  - **-m** ：统计字符数。不能与 **-c** 一起使用；
  - **-w** ：统计字数。一个字被定义为由空白、跳格或换行字符分隔的字符串；
  - **-L** ：打印最长行的长度；
  - **-help** ：显示帮助信息；
  - **--verison** ：显示版本信息；

- **命令实例** -

- **实例一：查看文件的字节数、字数、行数**

- **命令**

  ```bash
  cat tset.txt
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir5 qiu$ cat test.txt
  hnlinux
  peida.cnblogs.com
  ubuntu
  ubuntu linux
  redhat
  Redhat
  linuxmint
  Qs-MacBook-Pro:dir5 qiu$ wc test.txt
         7       8      70 test.txt
  Qs-MacBook-Pro:dir5 qiu$ wc -l test.txt
         7 test.txt
  Qs-MacBook-Pro:dir5 qiu$ wc -c test.txt
        70 test.txt
  Qs-MacBook-Pro:dir5 qiu$ wc -w test.txt
         8 test.txt
  Qs-MacBook-Pro:dir5 qiu$ wc -m test.txt
        70 test.txt
  Qs-MacBook-Pro:dir5 qiu$ 
  ```

- **说明**

  行数：7

  单词数：8

  字节数：70

  文件名：test.txt

- **实例二：用wc命令做到只统计打印数字不打印文件名**

- **命令**

  ```bash
  cat test.txt |wc -l
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir5 qiu$ wc -l test.txt
         7 test.txt
  Qs-MacBook-Pro:dir5 qiu$ cat test.txt |wc -l
         7
  ```

- **说明**

  使用 **管道线** ，在编写 **shell** 脚本时特别有用

- **实例三：用来统计当前目录下的文件数**

- **命令**

  ```bash
  ls -l |wc -l
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir4 qiu$ ls -l
  total 16
  lrwxr-xr-x  1 qiu  staff   11  5 10 11:43 link2019 -> log2019.log
  -rw-rw-rw-@ 2 qiu  staff   61  5 10 11:52 ln2019
  -rw-r--r--@ 4 qiu  staff   52  5 10 12:10 log2019.log
  drwxr-xr-x  4 qiu  staff  128  5 10 12:10 test
  Qs-MacBook-Pro:dir4 qiu$ ls -l | wc -l
         5
  ```

- **说明**

  在统计时要注意，**ls -l** 时会有一行总计，所以 **wc** 统计出的 **行数 - 1** 才是文件个数，即上面例子中文件个数为 **5 - 1 = 4** ；