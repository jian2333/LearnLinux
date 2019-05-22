### at 命令

- 在 **windows** 系统中，**windows** 提供了计划任务这一功能，在控制面板-->性能与维护-->计划任务，它的功能就是安排自动运行的任务。通过添加任务计划的一步步引导，则可建立一个定时执行的任务；

- **命令格式** - at [参数] [时间]

- **命令功能** - 

  - 在一个指定的时间执行一个指定的任务，只能执行一次，且需要开启 **atd** 进程；
  - **ps -ef | grep atd** ：查看
  - **/etc/init.d/atd start or restart** ：开启
  - **chkconfig -- level 2345 atd on** ：开机即启动

- **命令参数** - 

  - **-m** ：当指定的任务被完成之后，将给用户发送邮件，即使没有标准输出；

  - **-l** ：**atd** 的别名；

  - **-d** ：**atrm** 的别名；

  - **-v** ：显示任务即将被执行的时间；

  - **-c** ：打印任务的内容到标准输出；

  - **-V** ：显示版本信息；

  - **-q\<队列\>** ：使用指定的队列；

  - **-f\<文件\>** ：从指定文件读入任务而不是从标准输出读入任务；

  - **-t\<时间\>** ：以时间参数的形式提价要运行的任务；

  - **at** 允许使用一套相对复杂的指定时间的方法；

    - 它能够接受在当天的 **hh:mm(小时:分钟)** 式的时间指定。假如该时间已过去，那么就放在第二天执行。
    - 当然也能够使用 **midnight(深夜)、noon(中午)、teatime(饮茶时间，一般是下午4点)** 等比较模糊的词语来指定时间；
    - 用户还能够采用12小时计时制，即在事假后面加上 **AM(上午)** 或 **PM(下午)** 来说明是上午还是下午；
    - 也能够指定命令执行的具体日期，指定格式为 **month day(月 日)** 或 **mm/dd/yy(月/日/年)** 或 **dd.mm.yy(日.月.年) ** ；
    - 指定的日期必须跟在指定的时间后面；
    - 上面介绍的都是绝对计时法，其实还能够使用相对计时法，这对于安排不就就要执行的命令式很有好处的；
    - 指定格式为 ： now + count time-units，
      - now：当前时间；
      - time-units：是时间单位，这里能够是 **minutes(分钟)、hours(小时)、days(天)、weeks(星期)** ；
      - count 是时间的数量，究竟是几天，还是几小时，等等；
    - 更有一种计时方法直接使用 **today(今天)、tomorrow(明天)** 来指定完成命令的时间；

  - **TIME** ：时间格式，这里可以定义出什么时候要执行 **at** 这项任务的时间，格式有：

    - **HH:MM** 

      ex > 04:00

      在今天的 **HH:MM** 时刻进行，若该时刻已超过，则明天的 **HH:MM** 进行此任务；

    - **HH:MM YYYY-MM-DD**

      ex > 04:00 2009-03-17

      强制规定在某年某月的某一天的特殊时刻进行该项任务

    - **HH:MM[am|pm] [Month] [Date]**

      ex > 04pm March 17

      也是一样，强制在某年某月某日的某时刻进行该项任务

    - **HH:MM[am|pm] + number [minutes|hours|days|weeks]**

      ex > now + 5 minutes

      ex > 04pm + 3 days

      就是说，在某个时间点再加几个时间后才进行该项任务

- **命令实例** - 

- **实例一：三天后的下午 5 点钟执行 /bin/ls**

- **命令**

  ```bash
  at 5pm+3 days
  ```

- **输出**

  ```bash
  [root@localhost ~]# at 5pm+3 days
  at> /bin/ls
  at> <EOT>
  job 7 at 2013-01-08 17:00
  [root@localhost ~]#
  ```

- **说明**

- **实例二：明天 17 点钟，输出时间到指定文件内**

- **命令**

  ```bash
  at 17:20 tomorrow
  ```

- **输出**

  ```bash
  [root@localhost ~]# at 17:20 tomorrow
  at> date >/root/2013.log         
  at> <EOT>
  job 8 at 2013-01-06 17:20
  [root@localhost ~]#
  ```

- **说明**

- **实例三：计划任务设定后，在没有之前之前我们可以用 atq 命令来查看系统 没有执行工作任务**

- **命令**

  ```bash
  atq
  ```

- **输出**

  ````bash
  [root@localhost ~]# atq
  8       2013-01-06 17:20 a root
  7       2013-01-08 17:00 a root
  [root@localhost ~]
  ````

- **说明**

- **实例四：删除已经设置的任务**

- **命令**

  ```bash
  atrm 7
  ```

- **输出**

  ```bash
  [root@localhost ~]# atq
  8       2013-01-06 17:20 a root
  7       2013-01-08 17:00 a root
  [root@localhost ~]# atrm 7
  [root@localhost ~]# atq
  8       2013-01-06 17:20 a root
  [root@localhost ~]#
  ```

- **说明**

- **实例五：显示已经设置的内容**

- **命令**

  ```bash
  at -c 8
  ```

- **输出**

  ```bash
  [root@localhost ~]# at -c 8
  #!/bin/sh
  # atrun uid=0 gid=0
  # mail     root 0
  umask 22此处省略n个字符
  date >/root/2013.log
  [root@localhost ~]#
  ```

- **说明**

- **其他：atd 的启动或 at 运行的方式**

  - **atd 的启动**

    要使用一次性计划任务时，我们的 **Linux** 系统上面必须要有负责这个计划任务的服务，那就是 **atd** 服务。不过并非所有的 **Linux distributions** 都默认会把它打开，所以，某些时刻我们需要手动将 **atd** 服务激活才行。激活的方法很简单，这样：

    **命令**

    ```bash
    /etc/init.d/atd start
    /etc/inti.d/atd restart
    ```

    **输出**

    ```bash
    [root@localhost /]# /etc/init.d/atd start
    [root@localhost /]# /etc/init.d/atd 
    用法：/etc/init.d/atd {start|stop|restart|condrestart|status}
    [root@localhost /]# /etc/init.d/atd stop
    停止 atd：[确定]
    [root@localhost /]# ps -ef|grep atd
    root     25062 24951  0 14:53 pts/0    00:00:00 grep atd
    [root@localhost /]# /etc/init.d/atd start
    [确定]td：[确定]
    [root@localhost /]# ps -ef|grep atd
    root     25068     1  0 14:53 ?        00:00:00 /usr/sbin/atd
    root     25071 24951  0 14:53 pts/0    00:00:00 grep atd
    [root@localhost /]# /etc/init.d/atd restart
    停止 atd：[确定]
    [确定]td：[确定]
    [root@localhost /]#
    ```

    **说明**

    **/etc/init.d/atd start** ：没有启动的时候，直接启动 **atd** 服务

    **/etc/init.d/atd restart** ：服务已经启动后，重启 **atd** 服务

    **备注：配置一下启动时就启动这个服务，以后就不用每次重启都要再启动一遍了**

  - **at 的运行方式**

    既然是计划任务，那么应该会有任务执行的方式，并且将这些任务排进行程表中。那么产生计划任务的方式是怎么进行的? 事实上，我们使用 **at** 这个命令来产生所要运行的计划任务，并将这个计划任务以文字档的方式写入 `/var/spool/at/` 目录内，该工作便能等待 **atd** 这个服务的取用与运行了。就这么简单。

    不过，并不是所有的人都可以进行 at 计划任务。为什么? 因为系统安全的原因。很多主机被所谓的攻击破解后，最常发现的就是他们的系统当中多了很多的黑客程序， 这些程序非常可能运用一些计划任务来运行或搜集你的系统运行信息,并定时的发送给黑客。 所以，除非是你认可的帐号，否则先不要让他们使用 at 命令。那怎么达到使用 at 的可控呢?

    我们可以利用 `/etc/at.allow` 与 `/etc/at.deny` 这两个文件来进行 at 的使用限制。加上这两个文件后， at 的工作情况是这样的：

    先找寻 `/etc/at.allow` 这个文件，写在这个文件中的使用者才能使用 **at** ，没有在这个文件中的使用者则不能使用 **at** (即使没有写在 `at.deny` 当中);

    如果 `/etc/at.allow` 不存在，就寻找 `/etc/at.deny` 这个文件，若写在这个 `at.deny` 的使用者则不能使用 **at** ，而没有在这个 `at.deny` 文件中的使用者，就可以使用 **at** 命令了。

    如果两个文件都不存在，那么只有 **root** 可以使用 **at** 这个命令。

    透过这个说明，我们知道 `/etc/at.allow` 是管理较为严格的方式，而 `/etc/at.deny` 则较为松散 (因为帐号没有在该文件中，就能够运行 **at** 了)。在一般的 **distributions** 当中，由于假设系统上的所有用户都是可信任的， 因此系统通常会保留一个空的 `/etc/at.deny` 文件，意思是允许所有人使用 **at** 命令的意思 (您可以自行检查一下该文件)。 不过，万一你不希望有某些使用者使用 **at** 的话，将那个使用者的帐号写入 `/etc/at.deny` 即可！ 一个帐号写一行。