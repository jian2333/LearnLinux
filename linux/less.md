### less 命令

- **less** 工具也是对文件或其他输出进行分页显示的工具，应该说是 **Linux** 正统查看文件的工具，功能极其强大。**less** 的用法比 **more** 更加有弹性。在 **more** 的时候，我们没有办法向前翻页，只能往后面看，但若使用 **less** ，就可以使用 **[pageup] [pagedown]** 等按键的功能来往前往后翻页查看文件。此外，在 **less** 里还拥有更多的搜索功能，比如向下搜索，向上搜索。

- **命令格式** - less [参数] 文件

- **命令功能** - 与 **more** 类似，可以随意浏览文件，并且 **less** 在查看之前不会加载整个文件；

- **命令参数** - 

  - **-b \<缓冲区大小\> ** ：设置缓冲区的大小；
  - **-e** ：当文件显示结束后，自动离开；
  - **-f** ：强迫打开特殊文件，比如外围设备代号、目录和二进制文件；
  - **-g** ：只标志最后搜索的关键词；
  - **-i** ：忽略搜索时的大小写；
  - **-m** ：显示类似 **more** 命令的百分比；
  - **-N** ：显示每行的行号；
  - **-o \<文件名\>** ：将 **less** 输出的内容在指定文件中保存起来；
  - **-Q** ：不使用警告音；
  - **-s** ：显示连续空行为一行；
  - **-S** ：行过长时间将超出部分舍弃；
  - **-x \<数字\>** ：将 **tab** 键显示为规定的数字空格；

- **命令内部操作** - 

  - **按键功能如下** ：
    - **b** ：向后翻一页；
    - **d** ：向后翻半页；
    - **h** ：显示帮助界面；
    - **Q** ：退出 **less** 命令；
    - **u** ：向前滚动半页；
    - **y** ：向前滚动一行；
    - **空格键** ：滚动一页；
    - **回车键** ：滚动一行；
  - **搜索** ：
    - **/字符串** ：向下搜索 "字符串" 的功能；
    - **?字符串** ：向上搜索 "字符串" 的功能；
    - **n** ：重复前一个搜索（与 / 或 ? 有关）；
    - **N** ：反向重复前一个搜索（与 / 或 ? 有关）；
  - **全屏导航** ：
    - **ctrl + F** ：向前移动一屏；
    - **ctrl + B** ：向后移动一屏；
    - **ctrl + D** ：向前移动半屏；
    - **ctrl + U** ：向后移动半屏；
  - **单行导航** ：
    - **j** ：向前移动一行；
    - **k** ：向后移动一行；
  - **其他导航** ：
    - **G** ：移动到最后一行；
    - **g** ：移动到第一行；
    - **q** ：退出 **less** 命令；
    - **ZZ** ：退出 **less** 命令；
  - **编辑文件** ：
    - **v** ：进入编辑模式，使用配置的编辑器编辑当前文件；
  - **标记导航** ：
    - 当使用 **less** 查看大文件时，可以在任何一个位置作标记，可以通过命令导航到有特殊标记的文本位置；
    - **ma** ：使用 **a** 标记文本的当前位置；
    - **'a** ：导航到标记 **a** 处；

- **命令实例** - 

- **实例一：查看文件**

- **命令**

  ```bash
  less log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ less log.log
  2019-01
  2019-02
  2019-03
  
  2019-04
  2019-05
  log.log (END)
  ```

- **实例二：ps查看进程信息并通过 less 分页显示**

- **命令**

  ```bash
  ps -ef | less
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ps -ef | less
  UID   PID  PPID   C STIME   TTY           TIME CMD
      0     1     0   0  4 419  ??        36:23.20 /sbin/launchd
      0    33     1   0  4 419  ??         0:29.45 /usr/sbin/syslogd
      0    34     1   0  4 419  ??         0:58.69 /usr/libexec/UserEventAgent (System)
      0    37     1   0  4 419  ??         0:17.00 /System/Library/PrivateFrameworks/Uninstal
  l.framework/Resources/uninstalld
      0    38     1   0  4 419  ??         1:58.00 /usr/libexec/kextd
      0    39     1   0  4 419  ??        22:29.84 /System/Library/Frameworks/CoreServices.fr
  amework/Versions/A/Frameworks/FSEvents.framework/Versions/A/Support/fseventsd
      0    41     1   0  4 419  ??         0:34.46 /System/Library/PrivateFrameworks/MediaRem
  ote.framework/Support/mediaremoted
     55    44     1   0  4 419  ??         0:03.53 /System/Library/CoreServices/appleeventsd 
  --server
      0    45     1   0  4 419  ??        56:24.11 /usr/sbin/systemstats --daemon
      0    47     1   0  4 419  ??         1:06.93 /usr/libexec/configd
      0    48     1   0  4 419  ??        10:55.03 /System/Library/CoreServices/powerd.bundle
  /powerd
  ```

- **实例三：查看命令历史使用记录并通过 less 分页显示**

- **命令**

  ```bash
  history | less
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ history | less
    201  pwd
    202  ll
    203  cls
    204  ls -R
    205  cp log1.log dir2
    206  ls -R
    207  cp -a log1.log dir2
    208  cls
    209  ls -R
    210  cp log1.log dir2
    211  cp log1.log dir2
    212  cp -i log1.log dir2
    213  ls
    214  cls
    215  ls -lR
    216  cp -i log1.log dir2
    217  ls -lR
    218  pwd
  ```

- **实例四：浏览多个文件**

- **命令**

  ```bash
  less log.log log1.log
  //	打开文件后
  :n	//切换到下一个文件
  :p	//切换到上一个文件
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ less log.log log1.log
  log.log
  
  2019-01
  2019-02
  2019-03
  
  2019-04
  2019-05
  log.log (file 1 of 2) (END) - Next: log1.log
  
  :n
  log1.log
  
  2019-01
  2019-02
  2019-03
  2019-04
  2019-05
  ~
  ~
  log1.log (file 2 of 2) (END)
  
  :p
  log.log
  
  2019-01
  2019-02
  2019-03
  
  2019-04
  2019-05
  ~
  ~
  log.log (file 1 of 2) (END) - Next: log1.log
  
  ```

  