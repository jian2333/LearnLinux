### tail 命令

- **tail** 命令从指定点开始将文件写到标准输出。使用 **tail** 命令的 **-f** 选项可以方便的查阅正在改变的日志文件。 **tail -f filename** 会不停的把 **filename** 里最尾部的内容显示在屏幕上，并不断刷新，使你看到最新的内容；

- **命令格式** - tail [必要参数 ] [选择参数] [文件]

- **命令功能** - 用于显示指定文件末尾的内容。不指定文件时，作为输入信息进行处理。常用查看日志文件；

- **命令参数** - 

  - **-f** ：循环读取；
  - **-q** ：不显示处理信息；
  - **-v** ：显示详细的处理信息；
  - **-c\<数目\>** ：显示的字节数；
  - **-n\<行数\>** ：显示的行数；
  - **--pid** ：与 **-f** 合用，表示在进程 ID，PID 死掉之后结束；
  - **-q** ：从不输出给文件名的首部；
  - **-s** ：与 **-f** 合用，表示在每次反复的间隔休眠 **S** 秒；

- **命令实例** -  

- **实例一：显示文件最后五行的内容**

- **命令**

  ```bash
  tail -n 5 log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ cat log.log
  2019-01
  2019-02
  2019-03
  2019-04
  2019-05
  2019-06
  2019-07
  2019-08
  2019-09
  2019-10
  2019-11
  2019-12
  Qs-MacBook-Pro:dir1 qiu$ tail -n 5 log.log
  2019-08
  2019-09
  2019-10
  2019-11
  2019-12
  ```

- **实例二：从第五行开始显示文件**

- **命令**

  ```bash
  tail -n +5 log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ cat log.log
  2019-01
  2019-02
  2019-03
  2019-04
  2019-05
  2019-06
  2019-07
  2019-08
  2019-09
  2019-10
  2019-11
  2019-12
  Qs-MacBook-Pro:dir1 qiu$ tail -n +5 log.log
  2019-05
  2019-06
  2019-07
  2019-08
  2019-09
  2019-10
  2019-11
  2019-12
  ```

- **实例三：循环查看文件内容**

- **命令**

  ```bash
  tail -f ping.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ping www.baidu.com > ping.log &
  [1] 70780
  Qs-MacBook-Pro:dir1 qiu$ tail -f ping.log
  64 bytes from 14.215.177.38: icmp_seq=1 ttl=55 time=8.985 ms
  64 bytes from 14.215.177.38: icmp_seq=2 ttl=55 time=15.752 ms
  64 bytes from 14.215.177.38: icmp_seq=3 ttl=55 time=9.019 ms
  64 bytes from 14.215.177.38: icmp_seq=4 ttl=55 time=16.222 ms
  64 bytes from 14.215.177.38: icmp_seq=5 ttl=55 time=16.906 ms
  64 bytes from 14.215.177.38: icmp_seq=6 ttl=55 time=16.518 ms
  64 bytes from 14.215.177.38: icmp_seq=7 ttl=55 time=17.124 ms
  64 bytes from 14.215.177.38: icmp_seq=8 ttl=55 time=9.387 ms
  64 bytes from 14.215.177.38: icmp_seq=9 ttl=55 time=16.489 ms
  64 bytes from 14.215.177.38: icmp_seq=10 ttl=55 time=16.249 ms
  64 bytes from 14.215.177.38: icmp_seq=11 ttl=55 time=8.921 ms
  64 bytes from 14.215.177.38: icmp_seq=12 ttl=55 time=9.414 ms
  64 bytes from 14.215.177.38: icmp_seq=13 ttl=55 time=9.179 ms
  64 bytes from 14.215.177.38: icmp_seq=14 ttl=55 time=8.885 ms
  64 bytes from 14.215.177.38: icmp_seq=15 ttl=55 time=9.149 ms
  64 bytes from 14.215.177.38: icmp_seq=16 ttl=55 time=9.079 ms
  64 bytes from 14.215.177.38: icmp_seq=17 ttl=55 time=15.465 ms
  64 bytes from 14.215.177.38: icmp_seq=18 ttl=55 time=9.257 ms
  64 bytes from 14.215.177.38: icmp_seq=19 ttl=55 time=16.327 ms
  ```

- **说明**

  **ping www.baidu.com > ping.log &** // 在后台ping远程主机，并输出文件到 **ping.log** ；

  这种做法也适用于一个以上的监视；

  用 **Ctrl + c** 来终止；