### top 命令

- **top** 命令是 **Linux** 下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况，类似于 **Windows** 的任务管理器；

- **top** 是一个动态显示的过程，即可以通过用户按键来不断刷新当前状态；

- 如果在前台执行该命令，它将 **独占前台** ，直到用户终止该程序为止；比较准确的说，**top** 命令提供了实时的对系统处理器的状态监视。它将显示系统中 **CPU** 最敏感的任务列表；该命令可以按 **CPU使用，内存使用，执行时间** 对任务进行排序，而且该命令的很多特性都可以通过交互式命令或者在个人定制文件中进行设定；

- **命令格式** - top [参数]

- **命令功能** - 显示当前系统正在执行的进程的相关信息。包括 **进程ID、内存占用率、CPU占用率** 等

- **命令参数** - 

  - **-b** ：批处理
  - **-c** ：显示完整的治命令
  - **-l** ：忽略失效过程
  - **-s** ：保密模式
  - **-S** ：积累模式
  - **-i\<时间\>** ：设置时间间隔
  - **-u\<用户名\>** ：指定用户名
  - **-p\<进程号\>** ：指定进程
  - **-n\<行号\>** ：循环显示的次数

- **命令实例** -

- **注意：Mac下很多参数与Linux不同**

- **实例一：显示进程信息**

- **命令**

  ```bash
  top
  ```

- **输出**

  ```bash
  [root@TG1704 log]# top
  top - 14:06:23 up 70 days, 16:44,  2 users,  load average: 1.25, 1.32, 1.35
  Tasks: 206 total,   1 running, 205 sleeping,   0 stopped,   0 zombie
  Cpu(s):  5.9%us,  3.4%sy,  0.0%ni, 90.4%id,  0.0%wa,  0.0%hi,  0.2%si,  0.0%st
  Mem:  32949016k total, 14411180k used, 18537836k free,   169884k buffers
  Swap: 32764556k total,        0k used, 32764556k free,  3612636k cached
    PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND                                                                
  28894 root      22   0 1501m 405m  10m S 52.2  1.3   2534:16 java                                                                   
  18249 root      18   0 3201m 1.9g  11m S 35.9  6.0 569:39.41 java                                                                   
   2808 root      25   0 3333m 1.0g  11m S 24.3  3.1 526:51.85 java                                                                   
  25668 root      23   0 3180m 704m  11m S 14.0  2.2 360:44.53 java                                                                   
    574 root      25   0 3168m 611m  10m S 12.6  1.9 556:59.63 java                                                                   
   1599 root      20   0 3237m 1.9g  11m S 12.3  6.2 262:01.14 java                                                                   
   1008 root      21   0 3147m 842m  10m S  0.3  2.6   4:31.08 java                                                                   
  13823 root      23   0 3031m 2.1g  10m S  0.3  6.8 176:57.34 java                                                                   
  28218 root      15   0 12760 1168  808 R  0.3  0.0   0:01.43 top                                                                    
  29062 root      20   0 1241m 227m  10m S  0.3  0.7   2:07.32 java                                                                   
      1 root      15   0 10368  684  572 S  0.0  0.0   1:30.85 init                                                                   
      2 root      RT  -5     0    0    0 S  0.0  0.0   0:01.01 migration/0                                                            
      3 root      34  19     0    0    0 S  0.0  0.0   0:00.00 ksoftirqd/0                                                            
      4 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/0                                                             
      5 root      RT  -5     0    0    0 S  0.0  0.0   0:00.80 migration/1                                                            
      6 root      34  19     0    0    0 S  0.0  0.0   0:00.00 ksoftirqd/1                                                            
      7 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/1                                                             
      8 root      RT  -5     0    0    0 S  0.0  0.0   0:20.59 migration/2                                                            
      9 root      34  19     0    0    0 S  0.0  0.0   0:00.09 ksoftirqd/2                                                            
     10 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/2                                                             
     11 root      RT  -5     0    0    0 S  0.0  0.0   0:23.66 migration/3                                                            
     12 root      34  19     0    0    0 S  0.0  0.0   0:00.03 ksoftirqd/3                                                            
     13 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/3                                                             
     14 root      RT  -5     0    0    0 S  0.0  0.0   0:20.29 migration/4                                                            
     15 root      34  19     0    0    0 S  0.0  0.0   0:00.07 ksoftirqd/4                                                            
     16 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/4                                                             
     17 root      RT  -5     0    0    0 S  0.0  0.0   0:23.07 migration/5                                                            
     18 root      34  19     0    0    0 S  0.0  0.0   0:00.07 ksoftirqd/5                                                            
     19 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/5                                                             
     20 root      RT  -5     0    0    0 S  0.0  0.0   0:17.16 migration/6                                                            
     21 root      34  19     0    0    0 S  0.0  0.0   0:00.05 ksoftirqd/6                                                            
     22 root      RT  -5     0    0    0 S  0.0  0.0   0:00.00 watchdog/6                                                             
     23 root      RT  -5     0    0    0 S  0.0  0.0   0:58.28 migration/7
  ```

- **说明**

  - **统计信息区：**

    前五行是当前系统情况整体的统计信息区。

    **第一行，任务队列信息，同 uptime 命令的执行结果，具体参数说明情况如下：**

    14:06:23 — 当前系统时间

    up 70 days, 16:44 — 系统已经运行了70天16小时44分钟（在这期间系统没有重启过的吆！）

    2 users — 当前有2个用户登录系统

    load average: 1.15, 1.42, 1.44 — load average后面的三个数分别是1分钟、5分钟、15分钟的负载情况。

    load average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。

    **第二行，Task -- 任务（进程），具体信息说明如下：**

    系统现在共有206个进程，其中处于运行中的有1个，205个在休眠（sleep），stoped状态的有0个，zombie状态（僵尸）的有0个。

    **第三行，cpu状态信息，具体属性说明如下：**

    5.9%us — 用户空间占用CPU的百分比。

    3.4% sy — 内核空间占用CPU的百分比。

    0.0% ni — 改变过优先级的进程占用CPU的百分比

    90.4% id — 空闲CPU百分比

    0.0% wa — IO等待占用CPU的百分比

    0.0% hi — 硬中断（Hardware IRQ）占用CPU的百分比

    0.2% si — 软中断（Software Interrupts）占用CPU的百分比

    **备注：在这里CPU的使用比率和windows概念不同，需要理解linux系统用户空间和内核空间的相关知识！**

    **第四行，内存状态，具体信息如下：**

    32949016k total — 物理内存总量（32GB）

    14411180k used — 使用中的内存总量（14GB）

    18537836k free — 空闲内存总量（18GB）

    169884k buffers — 缓存的内存量 （169M）

    **第五行，swap交换分区信息，具体信息说明如下：**

    32764556k total — 交换区总量（32GB）

    0k used — 使用的交换区总量（0K）

    32764556k free — 空闲交换区总量（32GB）

    3612636k cached — 缓冲的交换区总量（3.6GB）

    **备注：**

    第四行中使用中的内存总量（used）指的是现在系统内核控制的内存数，空闲内存总量（free）是内核还未纳入其管控范围的数量。纳入内核管理的内存不见得都在使用中，还包括过去使用过的现在可以被重复利用的内存，内核并不把这些可被重新使用的内存交还到free中去，因此在linux上free内存会越来越少，但不用为此担心。

    如果出于习惯去计算可用内存数，这里有个近似的计算公式：第四行的free + 第四行的buffers + 第五行的cached，按这个公式此台服务器的可用内存：18537836k +169884k +3612636k = 22GB左右。

    对于内存监控，在top里我们要时刻监控第五行swap交换分区的used，如果这个数值在不断的变化，说明内核在不断进行内存和swap的数据交换，这是真正的内存不够用了。

    **第六行，空行**

    **第七行以下：各进程（任务）的状态监控，项目列信息说明如下：**

    PID — 进程id

    USER — 进程所有者

    PR — 进程优先级

    NI — nice值。负值表示高优先级，正值表示低优先级

    VIRT — 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES

    RES — 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA

    SHR — 共享内存大小，单位kb

    S — 进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程

    %CPU — 上次更新到现在的CPU时间占用百分比

    %MEM — 进程使用的物理内存百分比

    TIME+ — 进程使用的CPU时间总计，单位1/100秒

    COMMAND — 进程名称（命令名/命令行）

  - **其他使用技巧：**

    **多核多CPU监控**

    在 **top** 基本视图中，按键盘数字 **1**，可监控每个逻辑CPU的状况；

    **高亮显示当前运行进程**

    敲击键盘 **b** (打开/关闭高亮效果)；

    **进程字段排序**

    默认进入 **top** 时，各进程是按照 CPU 的占用量来排序的；

    敲击键盘 **x** (打开/关闭拍序列的加亮效果)；

    **通过 shift+\> 或 shift+\< 可以向右或向左改变排序列**

    ···

- **实例二：显示完整命令**

- **命令**

  ```shell
  top -c
  ```

- **输出**

  ```bash
  top -c
  ```

- **说明**

- **实例三：以批处理模式显示程序信息**

- **命令**

  ```bash
  top -b
  ```

- **输出**

  ```bash
  top -b
  ```

- **说明**

- **实例四：以累积模式显示程序信息**

- **命令**

  ```bash
  top -S
  ```

- **输出**

  ```bash
  top -S
  
  Processes: 425 total, 2 running, 423 sleeping, 2083 threads                                                     17:00:06
  Load Avg: 2.06, 2.45, 2.15  CPU usage: 5.36% user, 2.97% sys, 91.65% idle
  SharedLibs: 296M resident, 71M data, 81M linkedit. MemRegions: 139731 total, 5513M resident, 117M private, 2109M shared.
  PhysMem: 16G used (2992M wired), 324M unused.
  VM: 3761G vsize, 1298M framework vsize, 2966743(0) swapins, 3247458(0) swapouts. Swap: 99M + 926M free.
  Purgeable: 926M 95922(0) pages purged.   Networks: packets: 19586526/17G in, 32185361/18G out.
  Disks: 5859888/75G read, 3961484/72G written.
  
  PID    COMMAND      %CPU TIME     #TH    #WQ  #PORTS MEM    PURG   CMPRS  PGRP  PPID  STATE    BOOSTS          %CPU_ME
  64447  node         0.0  00:00.75 7      0    25     35M    0B     0B     26460 26460 sleeping *0[1]           0.00000
  64442  top          4.6  00:05.27 1/1    0    26     6304K  0B     0B     64442 63713 running  *0[1]           0.00000
  64378  mdworker_sha 0.0  00:00.04 3      1    56     3232K  0B     0B     64378 1     sleeping *0[1]           0.00000
  64342  ocspd        0.0  00:00.01 2      1    34     1620K  0B     0B     64342 1     sleeping *0[1]           0.00000
  63713  zsh          0.0  00:01.15 1      0    21     3344K  0B     0B     63713 63712 sleeping *0[1]           0.00000
  63712  login        0.0  00:00.03 2      1    31     1116K  0B     0B     63712 63711 sleeping *0[9]           0.00000
  63711  iTerm2       0.0  00:00.04 2      1    33     3148K  0B     0B     63711 53115 sleeping *0[1]           0.00000
  63678  Google Chrom 0.0  00:23.34 16     1    151    83M    4096B  0B     26455 26455 sleeping *0[5]           0.00000
  63677  Google Chrom 0.0  00:00.10 15     1    115    13M    4096B  0B     26455 26455 sleeping *0[4]           0.00000
  63663  mdworker_sha 0.0  00:00.23 3      1    56     3376K  0B     0B     63663 1     sleeping *0[1]           0.00000
  63626  com.apple.We 0.0  00:02.71 5      1    93     24M    0B     0B     63626 1     sleeping  0-[123]        0.00000
  63619  mdworker_sha 0.0  00:00.06 3      1    56     3316K  0B     0B     63619 1     sleeping *0[1]           0.00000
  ```

- **说明**

- **实例五：设置信息更新次数**

- **命令**

  ```bash
  top -n 2
  ```

- **输出**

- **说明**

  表示更新两次后终止更新显示

- **实例六：设置信息更新时间**

- **命令**

  ```bash
  top -d 3
  ```

- **输出**

- **说明**

  表示更新周期为3秒

- **实例七：显示指定的进程信息**

- **命令**

  ```bash
  top -p 574
  ```

- **输出**

  ```bash
  // Mac下，与Linux稍有不同
  top -pid 63060
  Processes: 424 total, 2 running, 422 sleeping, 2022 threads                                                     17:05:08
  Load Avg: 1.83, 2.01, 2.02  CPU usage: 8.88% user, 4.73% sys, 86.37% idle
  SharedLibs: 296M resident, 71M data, 81M linkedit. MemRegions: 139465 total, 5503M resident, 117M private, 2011M shared.
  PhysMem: 16G used (2885M wired), 354M unused.
  VM: 3757G vsize, 1298M framework vsize, 2966743(0) swapins, 3247458(0) swapouts.
  Networks: packets: 19605680/17G in, 32207332/18G out. Disks: 5861254/75G read, 3969721/72G written.
  
  PID    COMMAND      %CPU TIME     #TH  #WQ  #POR MEM   PURG CMPR PGRP  PPID STATE    BOOSTS     %CPU_ME %CPU_OTHRS UID
  63060  BetterTouchT 0.0  00:00.01 2    1    24   844K  0B   0B   63060 1    sleeping  0[1]      0.00000 0.00000    501
  ```

- **说明**

- **top交互命令**

  - 在 **top** 命令执行过程中可以使用一些交互命令。这些命令都是单字母的，如果在命令行中使用了 **s** 选项，其中一些命令可能会被屏蔽；
  - **h** ：显示帮助画面
  - **k** ：终止一个进程
  - **i** ：忽略闲置和僵死进程。这是一个开关式命令
  - **q** ：退出程序
  - **r** ：重新安排一个进程的优先级别
  - **S** ：切换到累积模式
  - **s** ：改变两次刷新之间的延迟时间(单位为s)，如果有小数，就换算成 ms。直接输入0则系统将不断刷新。默认是 5s 
  - **f或者F** ：从当前显示中添加或删除项目
  - **o或者O** ：改变显示项目的顺序
  - **l** ：切换显示平均负载和启动时间信息
  - **m** ：切换显示内存信息
  - **t** ：切换显示进程和CPU状态信息
  - **c** ：切换显示命令名称和完整命令行
  - **M** ：根据驻留内存大小进行排序
  - **P** ：根据CPU使用百分比大小进行排序
  - **T** ：根据时间/累积时间进行排序
  - **W** ：将当前设置写入 ~/.toprc 文件中