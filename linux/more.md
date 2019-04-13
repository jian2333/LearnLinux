### more 命令

- 功能类似 **cat** 。**cat** 是把整个文件的内容从上到下显示出来，**more** 则是一页一页的显示出来；

- **命令格式** - more [-dlfpcsu] [-num] [+/pattern] [+linenum] [file...]

- **命令功能** - 

  - 将文件一页一页的显示出来；
  - 空白键（space）下一页显示；
  - b 键 前一页显示；
  - 还有搜索字符串的功能；

- **命令参数** - 

  - **+n** ：从第 n 行开始显示；
  - **-n** ：定义屏幕每页显示 n 行；
    - **注意：Mac_Terminal 下第一页默认显示，第二个开始每页显示 n 行；**
  - **+/pattern** ：在每个档案显示前搜索该字符串（pattern），然后从该字符串前两行之后开始显示；
    - **注意：Mac_Terminal 下直接从该字符串处输出显示；**
  - **-c** ：从顶部开始清屏，然后显示；
  - **-d** ：提示 "Press space to continue, 'q' to quit（按空格键继续，按q键退出）"，禁用响铃功能；
  - **-l** ：忽略 **Ctrl+l** (换页) 字符；
  - **-p** ：通过清除窗口而不是滚屏来对文件进行换页，类似 **-c** ；
  - **-s** ：把连续的多个空行显示为一行；
  - **-u** ：把文件内容的下划线去掉；

- **常用操作命令** - 

  - **Enter** ：向下 **n** 行，需要定义。默认为 1 行；
  - **Ctrl+F** ：向下滚动一屏；
    - **Mac_Terminal ：F ；**
  - **空格键(space)** ：向下滚动一屏；
  - **Ctrl+B** ：向上滚动一屏；
    - **Mac_Terminal ：B ；**
  - **=** ：输出当前行的行号；
  - **：f** ：输出文件名和当前行的行号；
  - **V** ：调用 **vi** 编辑器；
  - **!命令** ：调用 **Shell** ，并执行命令；
  - **q** ：退出 **more** ；

- **命令实例** - 

- **实例一：显示文件，从第三行开始**

- **命令**

  ```bash
  more +3 log2.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ cat log2.log
  2019-01
  2019-02
  2019-03
  2019-04-day1
  2019-04-day2
  2019-04-day3
  
  Qs-MacBook-Pro:dir1 qiu$ more +3 log2.log
  2019-03
  2019-04-day1
  2019-04-day2
  2019-04-day3
  ```

- **实例二：查找文件中第一个出现的 "day" 字符串，并从该处的前两行开始显示输出**

- **命令**

  ```bash
  more +/day log2.log
  ```

- **输出**

  ```bash
  // Linux 
  Qs-MacBook-Pro:dir1 qiu$ cat log2.log
  2019-01
  2019-02
  2019-03
  2019-04-day1
  2019-04-day2
  2019-04-day3
  
  Qs-MacBook-Pro:dir1 qiu$ more +/day log2.log
  2019-02
  2019-03
  2019-04-day1
  2019-04-day2
  2019-04-day3
  ```

  ```bash
  // Mac_Terminal
  Qs-MacBook-Pro:dir1 qiu$ cat log2.log
  2019-01
  2019-02
  2019-03
  2019-04-day1
  2019-04-day2
  2019-04-day3
  
  Qs-MacBook-Pro:dir1 qiu$ more +/day log2.log
  2019-04-day1
  2019-04-day2
  2019-04-day3
  ```

- **设定每屏显示的行数**

- **命令**

  ```bash
  more -3 log2.log
  ```

- **输出**

  ```bash
  // Mac_Terminal 下第一页默认显示，第二页开始每页显示n行
  [root@localhost test]# more +/day3 log2012.log 
  ...skipping
  2012-04-day1
  2012-04-day2
  2012-04-day3
  2012-05
  2012-05-day1
  ======[root@localhost test]#
  ```

- **实例四：用 more + ls 来分页显示目录，使用管道 | 来结合**

- **命令**

  ```bash
  ls -l | more -3
  ```

- **输出**

  ```bash
  // Mac_Terminal 下第一页默认显示，第二页开始每页显示n行
  // f,space 下一页
  // b 上一页
  Qs-MacBook-Pro:dir1 qiu$ ls -cltr
  total 280
  -rw-r--r--  1 qiu  staff  95  4 13 13:01 log.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 2.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 3.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 4.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 5.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 6.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 7.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 8.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 9.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 10.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 11.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 12.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 13.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 14.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 15.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 16.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 17.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 18.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 19.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 20.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 21.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 22.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 23.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 24.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 25.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 26.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 27.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 28.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 29.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 30.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 31.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 32.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 33.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:08 log的副本 34.log
  
  Qs-MacBook-Pro:dir1 qiu$ ls -cltr | more -2
  total 280
  -rw-r--r--  1 qiu  staff  95  4 13 13:01 log.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 2.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 3.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 4.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 5.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 6.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 7.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 8.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 9.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 10.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 11.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 12.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 13.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 14.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 15.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 16.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 17.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 18.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 19.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 20.log
  -rw-r--r--  1 qiu  staff  95  4 13 13:02 log的副本 21.log
  :
  // 开始输入指令
  ```

  