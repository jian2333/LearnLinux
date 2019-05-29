### ping 命令

- **Linux** 系统的 **ping** 命令是常用的网络命令，它通常用来测试与目标主机的连通性。它通过发送 **ICMP ECHO_REQUEST 数据包** 到网络主机，并显示响应情况，这样我们就可以根据它输出的信息来确定目标主机是否可访问(但这不是绝对的)。有些服务器为了防止通过 **ping** 探测到，通过防火墙设置了禁止 **ping** 或者在内核参数中禁止 **ping**，这样就不能通过 **ping** 确定该主机是否还处于开启状态。

- **Linux** 下的 **ping** 和 **windows** 下的 **ping** 稍有不同，**Linux** 下的 **ping** 不会自动终止，需要按 `ctrl+c` 终止或使用参数 `-c` 来指定要求完成的回应次数。

- **命令格式** - ping [参数] [主机名或IP地址]

- **命令功能** - 

  - **ping** 命令用于：确定网路和外部主机的状态；跟踪和隔离硬件和软件问题；测试、苹果和管理网络。如果主机正在运行并连接网上，它就对回送信号进行响应。每个回送信号包含一个网际协议(**IP**)和 **ICMP** 头，后面紧跟一个 **tim** 结构，以及来填写这个信息包的足够的字节。缺省情况是连续发送回送信号请求直到接收到中断信号( `ctrl-c` ) ；
  - **ping** 命令每秒发送一个数据报并为每个接收到的响应打印一行输出。**ping** 命令计算信号往返时间和(信息)包丢失情况的统计信息，并且在完成之后显示一个简要总结。**ping** 命令在程序超时或当接收到 **SIGINT** 信号时结束。**Host** 参数或者是一个有效的主机名或者是因特网地址；

- **命令参数** - 

  - **-d** ：使用 **Socket** 的 **SO_DEBUG** 功能；
  - **-f** ：极限检测。大量且快速地送网络封包给一台机器，看它的回应；
  - **-n** ：只输出数值；
  - **-q** ：不显示任何传送封包的信息，只显示最后的结果；
  - **-r** ：忽略普通的 **Routing Table** ，直接将数据包送到远端主机上，通常是查看本机的网络接口是否有问题；
  - **-R** ：记录路由过程；
  - **-v** ：详细显示指令的执行过程；
  - **\<p\>-c 数目** ：在发送指定数目的包后停止；
  - **-i 秒数** ：设定间隔几秒发送一个网络封包给一台机器，默认是一秒发送一次；
  - **-l 网络界面** ：使用指定的网络界面送出数据包；
  - **-l 前置载入** ：设置在送出要求信息之前，先行发出的数据包；
  - **-p 范本样式** ：设置填满数据包的范本样式；
  - **-s 字节数** ：指定发送的数据字节数，默认值是56，加上8字节的 **ICMP** 头，一共是64     **ICMP** 数据字节；
  - **-t 存活数值** ：设置存活数值 **TTL** 的大小；

- **命令实例** -

- **实例一：ping 的同的情况**

- **命令**

  ```bash
  ping 192.168.120.205
  ```

- **输出**

  ```bash
  [root@localhost ~]# ping 192.168.120.205
  PING 192.168.120.205 (192.168.120.205) 56(84) bytes of data.
  bytes from 192.168.120.205: icmp_seq=1 ttl=64 time=0.720 ms
  bytes from 192.168.120.205: icmp_seq=2 ttl=64 time=0.181 ms
  bytes from 192.168.120.205: icmp_seq=3 ttl=64 time=0.191 ms
  bytes from 192.168.120.205: icmp_seq=4 ttl=64 time=0.188 ms
  bytes from 192.168.120.205: icmp_seq=5 ttl=64 time=0.189 ms
  
  --- 192.168.120.205 ping statistics ---
  packets transmitted, 5 received, 0% packet loss, time 4000ms
  rtt min/avg/max/mdev = 0.181/0.293/0.720/0.214 ms
  [root@localhost ~]#
  ```

- **实例二：ping 不同的情况**

- **命令**

  ```bash
  ping 192.168.120.202
  ```

- **输出**

  ```bash
  [root@localhost ~]# ping 192.168.120.202
  PING 192.168.120.202 (192.168.120.202) 56(84) bytes of data.
  From 192.168.120.204 icmp_seq=1 Destination Host Unreachable
  From 192.168.120.204 icmp_seq=2 Destination Host Unreachable
  From 192.168.120.204 icmp_seq=3 Destination Host Unreachable
  From 192.168.120.204 icmp_seq=4 Destination Host Unreachable
  From 192.168.120.204 icmp_seq=5 Destination Host Unreachable
  From 192.168.120.204 icmp_seq=6 Destination Host Unreachable
  
  --- 192.168.120.202 ping statistics ---
  packets transmitted, 0 received, +6 errors, 100% packet loss, time 7005ms
  , pipe 4
  [root@localhost ~]#
  ```

- **实例三：ping 网关**

- **命令**

  ```bash
  ping -b 192.168.120.1
  ```

- **输出**

  ```bash
  [root@localhost ~]# route
  Kernel IP routing table
  Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
  192.168.120.0   *               255.255.255.0   U     0      0        0 eth0
  192.168.0.0     192.168.120.1   255.255.0.0     UG    0      0        0 eth0
  10.0.0.0        192.168.120.1   255.0.0.0       UG    0      0        0 eth0
  default         192.168.120.240 0.0.0.0         UG    0      0        0 eth0
  [root@localhost ~]# ping -b 192.168.120.1
  PING 192.168.120.1 (192.168.120.1) 56(84) bytes of data.
  bytes from 192.168.120.1: icmp_seq=1 ttl=255 time=2.02 ms
  bytes from 192.168.120.1: icmp_seq=2 ttl=255 time=1.83 ms
  bytes from 192.168.120.1: icmp_seq=3 ttl=255 time=1.68 ms
  bytes from 192.168.120.1: icmp_seq=4 ttl=255 time=1.98 ms
  bytes from 192.168.120.1: icmp_seq=5 ttl=255 time=1.88 ms
  
  --- 192.168.120.1 ping statistics ---
  packets transmitted, 5 received, 0% packet loss, time 4000ms
  rtt min/avg/max/mdev = 1.682/1.880/2.020/0.129 ms
  ```

- **实例四：ping 指定次数**

- **命令**

  ```bash
  ping -c 192.168.120.206
  ```

- **输出**

  ```bash
  [root@localhost ~]# ping -c 10 192.168.120.206
  PING 192.168.120.206 (192.168.120.206) 56(84) bytes of data.
  bytes from 192.168.120.206: icmp_seq=1 ttl=64 time=1.25 ms
  bytes from 192.168.120.206: icmp_seq=2 ttl=64 time=0.260 ms
  bytes from 192.168.120.206: icmp_seq=3 ttl=64 time=0.242 ms
  bytes from 192.168.120.206: icmp_seq=4 ttl=64 time=0.271 ms
  bytes from 192.168.120.206: icmp_seq=5 ttl=64 time=0.274 ms
  bytes from 192.168.120.206: icmp_seq=6 ttl=64 time=0.295 ms
  bytes from 192.168.120.206: icmp_seq=7 ttl=64 time=0.269 ms
  bytes from 192.168.120.206: icmp_seq=8 ttl=64 time=0.270 ms
  bytes from 192.168.120.206: icmp_seq=9 ttl=64 time=0.253 ms
  bytes from 192.168.120.206: icmp_seq=10 ttl=64 time=0.289 ms
  
  --- 192.168.120.206 ping statistics ---
  packets transmitted, 10 received, 0% packet loss, time 9000ms
  rtt min/avg/max/mdev = 0.242/0.367/1.251/0.295 ms
  [root@localhost ~]#
  ```

- **实例五：时间间隔和次数限制的 ping**

- **命令**

  ```bash
  ping -c 10 -i 0.5 192.168.120.206
  ```

- **输出**

  ```bash
  [root@localhost ~]# ping -c 10 -i 0.5 192.168.120.206
  PING 192.168.120.206 (192.168.120.206) 56(84) bytes of data.
  bytes from 192.168.120.206: icmp_seq=1 ttl=64 time=1.24 ms
  bytes from 192.168.120.206: icmp_seq=2 ttl=64 time=0.235 ms
  bytes from 192.168.120.206: icmp_seq=3 ttl=64 time=0.244 ms
  bytes from 192.168.120.206: icmp_seq=4 ttl=64 time=0.300 ms
  bytes from 192.168.120.206: icmp_seq=5 ttl=64 time=0.255 ms
  bytes from 192.168.120.206: icmp_seq=6 ttl=64 time=0.264 ms
  bytes from 192.168.120.206: icmp_seq=7 ttl=64 time=0.263 ms
  bytes from 192.168.120.206: icmp_seq=8 ttl=64 time=0.331 ms
  bytes from 192.168.120.206: icmp_seq=9 ttl=64 time=0.247 ms
  bytes from 192.168.120.206: icmp_seq=10 ttl=64 time=0.244 ms
  
  --- 192.168.120.206 ping statistics ---
  packets transmitted, 10 received, 0% packet loss, time 4499ms
  rtt min/avg/max/mdev = 0.235/0.362/1.241/0.294 ms
  [root@localhost ~]# ping -c 10 -i 0.01 192.168.120.206
  PING 192.168.120.206 (192.168.120.206) 56(84) bytes of data.
  bytes from 192.168.120.206: icmp_seq=1 ttl=64 time=0.244 ms
  bytes from 192.168.120.206: icmp_seq=2 ttl=64 time=0.195 ms
  bytes from 192.168.120.206: icmp_seq=3 ttl=64 time=0.219 ms
  bytes from 192.168.120.206: icmp_seq=4 ttl=64 time=0.204 ms
  bytes from 192.168.120.206: icmp_seq=5 ttl=64 time=3.56 ms
  bytes from 192.168.120.206: icmp_seq=6 ttl=64 time=1.93 ms
  bytes from 192.168.120.206: icmp_seq=7 ttl=64 time=0.193 ms
  bytes from 192.168.120.206: icmp_seq=8 ttl=64 time=0.193 ms
  bytes from 192.168.120.206: icmp_seq=9 ttl=64 time=0.202 ms
  bytes from 192.168.120.206: icmp_seq=10 ttl=64 time=0.211 ms
  
  --- 192.168.120.206 ping statistics ---
  packets transmitted, 10 received, 0% packet loss, time 90ms
  rtt min/avg/max/mdev = 0.193/0.716/3.564/1.080 ms
  [root@localhost ~]#
  ```

- **实例六：通过域名 ping 公网上的站点**

- **命令**

  ```bash
  ping -c 5 www.58.com
  ```

- **输出**

  ```bash
  peida-VirtualBox ~ # ping -c 5 www.58.com
  PING www.58.com (211.151.111.30) 56(84) bytes of data.
  bytes from 211.151.111.30: icmp_req=1 ttl=49 time=14.7 ms
  bytes from 211.151.111.30: icmp_req=2 ttl=49 time=16.4 ms
  bytes from 211.151.111.30: icmp_req=3 ttl=49 time=15.2 ms
  bytes from 211.151.111.30: icmp_req=4 ttl=49 time=14.6 ms
  bytes from 211.151.111.30: icmp_req=5 ttl=49 time=19.9 ms
  
  --- www.58.com ping statistics ---
  packets transmitted, 5 received, 0% packet loss, time 20101ms
  rtt min/avg/max/mdev = 14.618/16.192/19.917/1.965 ms
  peida-VirtualBox ~ #
  ```

- **实例七：多参数使用**

- **命令**

  ```bash
  ping -i 3 -s 1024 -t 255 192.168.120.206
  ```

- **输出**

  ```bash
  [root@localhost ~]# ping -i 3 -s 1024 -t 255 192.168.120.206
  PING 192.168.120.206 (192.168.120.206) 1024(1052) bytes of data.
  bytes from 192.168.120.206: icmp_seq=1 ttl=64 time=1.99 ms
  bytes from 192.168.120.206: icmp_seq=2 ttl=64 time=0.694 ms
  bytes from 192.168.120.206: icmp_seq=3 ttl=64 time=0.300 ms
  bytes from 192.168.120.206: icmp_seq=4 ttl=64 time=0.481 ms
  bytes from 192.168.120.206: icmp_seq=5 ttl=64 time=0.415 ms
  bytes from 192.168.120.206: icmp_seq=6 ttl=64 time=0.600 ms
  bytes from 192.168.120.206: icmp_seq=7 ttl=64 time=0.411 ms
  bytes from 192.168.120.206: icmp_seq=8 ttl=64 time=0.281 ms
  bytes from 192.168.120.206: icmp_seq=9 ttl=64 time=0.318 ms
  bytes from 192.168.120.206: icmp_seq=10 ttl=64 time=0.362 ms
  bytes from 192.168.120.206: icmp_seq=11 ttl=64 time=0.408 ms
  bytes from 192.168.120.206: icmp_seq=12 ttl=64 time=0.445 ms
  bytes from 192.168.120.206: icmp_seq=13 ttl=64 time=0.397 ms
  bytes from 192.168.120.206: icmp_seq=14 ttl=64 time=0.406 ms
  bytes from 192.168.120.206: icmp_seq=15 ttl=64 time=0.458 ms
  
  --- 192.168.120.206 ping statistics ---
  packets transmitted, 15 received, 0% packet loss, time 41999ms
  rtt min/avg/max/mdev = 0.281/0.531/1.993/0.404 ms
  [root@localhost ~]#
  ```

- **说明**

  **-i 3** 发送周期为 3秒；

  **-s 1024** 发送包的大小为 1024；

  **-t 255** TLL 值为255；