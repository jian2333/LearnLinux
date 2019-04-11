### cat 命令

- 用途是连接文件或标准输入并打印设备。这个命令常用来显示文件内容，或者将几个文件连接起来显示，或者从标准输入读取内容并显示，常与重定向符号配合使用；

- **命令格式** - 

  - cat [选项] [文件]...

- **命令功能** - 

  - 一次显示整个文件：cat filename；
  - 从键盘创建一个文件：cat > filename 只能创建新文件，不能编辑已有文件；
  - 将几个文件内容合并到一个文件里(覆盖)：cat file1 file2 > file；
  - 将几个文件内容合并到一个文件里(继续添加)：cat file1 file2 >> file；

- **命令参数** - 

  - **-A** ：等价于 -vET；
  - **-b** ：对非空输出行编号；
  - **-e** ：等价于 -vE；
  - **-E** ：在每行结束处显示 $；
  - **-n** ：对输出的所有行编号，由1开始；
  - **-s** ：有连续两行以上的空白行，就替换为一行的空白行；
  - **-t** ：等价于 -vT；
  - **-T** ：将 TAB 字符显示为 ^|；
  - **-u** ：被忽略；
  - **-v** ：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外；

- **命令实例** - 

  - **实例一：将 log1.log 和 log2.log 的文件内容加上行号后一起显示出来**

  - **命令**

    ```bash
    cat -n log1.log log2.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ cat log1.log
    2012-01
    2012-02
    
    Qs-MacBook-Pro:dir1 qiu$ cat log2.log
    
    2013-01
    2013-02
    
    2013-03
    
    Qs-MacBook-Pro:dir1 qiu$ cat -n log1.log log2.log
         1	2012-01
         2	2012-02
         3	
         1	
         2	2013-01
         3	2013-02
         4	
         5	2013-03
         6	
    ```

  - **实例二：将 log1.log 和 log2.log 的文件内容加上行号(空白行不加)之后，将内容添加到 log.log 里**

  - **命令**

    ```bash
    cat -b log1.log log2.log > log.log
    cat -b log1.log log2.log >> log.log
    ```

  - **说明**

    **cat > file** ：重新编辑(**即覆盖**) file 文件内容；

    **cat >> file** ：在 file 里 **继续** 添加内容；

  - **输出**

    ```bash
    // >示例
    Qs-MacBook-Pro:dir1 qiu$ cat log.log
    
    我已有内容！！
    
    Qs-MacBook-Pro:dir1 qiu$ cat log1.log
    log1的内容
    Qs-MacBook-Pro:dir1 qiu$ cat log2.log
    log2的内容
    Qs-MacBook-Pro:dir1 qiu$ cat -b log1.log log2.log > log.log
    Qs-MacBook-Pro:dir1 qiu$ cat log.log
         1	log1的内容
         1	log2的内容
    ```

    ```bash
    // >>示例
    Qs-MacBook-Pro:dir1 qiu$ cat log.log
    
    我已有内容！！
    Qs-MacBook-Pro:dir1 qiu$ cat log1.log
    log1的内容
    Qs-MacBook-Pro:dir1 qiu$ cat log2.log
    log2的内容
    Qs-MacBook-Pro:dir1 qiu$ cat -b log1.log log2.log >> log.log
    Qs-MacBook-Pro:dir1 qiu$ cat log.log
    
    我已有内容！！
         1	log1的内容
         1	log2的内容
    ```

  - **实例三：反向显示**

  - **命令**

    **注意：Mac_Terminal 下该参数无效**；

    ```bash
    tac log.txt
    ```

  - **输出**

    ```bash
    [root@localhost test]# cat log.txt 
    Hello
    World
    Linux
    [root@localhost test]# tac log.txt 
    Linux
    World
    Hello
    ```

  - **实例四：创建新文件 - 方法1**

  - **命令**

    ```bash
    cat > log1.log
    // 输入文件内容
    ctrl+Z 退出
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 8
    -rw-r--r--@ 1 qiu  staff  18  4 11 11:05 log.log
    Qs-MacBook-Pro:dir1 qiu$ cat > log1.log
    11
    22
    33
    ^Z
    [2]+  Stopped                 cat > log1.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff  18  4 11 11:05 log.log
    -rw-r--r--  1 qiu  staff   9  4 11 11:17 log1.log
    Qs-MacBook-Pro:dir1 qiu$ cat log1.log
    11
    22
    33
    ```

  - **实例五：创建新文件 - 方法2**

  - **命令**

    ```bash
    cat > log2.log << EOF
    // 输入文件内容
    EOF 退出
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 16
    -rw-r--r--@ 1 qiu  staff  18  4 11 11:05 log.log
    -rw-r--r--  1 qiu  staff   9  4 11 11:17 log1.log
    Qs-MacBook-Pro:dir1 qiu$ cat > log2.log << EOF
    > EOF11
    > EOF22
    > EOF33
    > EOF
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 24
    -rw-r--r--@ 1 qiu  staff  18  4 11 11:05 log.log
    -rw-r--r--  1 qiu  staff   9  4 11 11:17 log1.log
    -rw-r--r--  1 qiu  staff  18  4 11 11:20 log2.log
    Qs-MacBook-Pro:dir1 qiu$ cat log2.log
    EOF11
    EOF22
    EOF33
    ```

    