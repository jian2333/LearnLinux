### SecureCRT 上传和下载文件

用 **SSH** 管理 **Linux** 服务器时经常需要远程与本地之间交互文件，而直接用 **SecureCRT** 自带的上传下载功能无疑是最方便的，**SecureCRT** 下的文件传输协议有 **ASCII**、**Xmodem**、**Zmodem** 。

#### 文件传输协议：

- 文件传输是数据交互的主要形式。在进行文件传输时，为使文件能被正确识别和传送，我们需要在两台计算机之间建立统一的传输协议。这个协议包括了文件的识别、传送的起止时间、错误的判断和纠正等内容。常见的传输协议有以下几种：
- **ASCII** ：这是最快的传输协议，但只能传输文本文件；
- **Xmodem** ：这种古老的传输协议速度较慢，但由于使用了 **CRC** 错误侦测方法，传输的准确率可高达 **99.6%** ；
- **Ymodem** ：这是 **Xmodem** 的改良版，使用了 **1024** 位区段传送，速度比 **Xmodem** 要快；
- **Zmodem** ：**Zmodem** 采用了串流式（**streaming**）传输方式，传输速度较快，而且还具有自动改变区段大小和判断续点上传、快速错误侦测等功能。这是目前最流行的文件传输协议；
- 除以上几种外，还有 **Imodem**、**Jmodem**、**Bimodem**、**Kermit**、**Lynx** 等协议。

#### SecureCRT 使用 zmodem 传送文件步骤：

##### 一. 在使用 SecureCRT 上传下载之前需要给服务器安装 Lrzsz

1. 从下面的地址下载 **Lrzsz-0.12.20.tar.gz**

   ```http
   http://down1.chinaunix.net/distfiles/lrzsz-0.12.20.tar.gz
   ```

2. 查看里面的 **INSTALL** 文档了解安装参数说明和细节；

3. 解压文件

   ```bash
   tar zxvf lrzsz-0.12.20.tar.gz
   ```

4. 进入目录

   ```bash
   cd lrzsz-0.12.20
   ```

5. ~

   ```bash
   ./configure --prefix=/usr/local/lrzsz
   ```

6. ~

   ```bash
   make
   ```

7. ~

   ```bash
   make install
   ```

8. 建立软链接

   ```bash
   #cd /usr/bin
   #ln -s /usr/local/lrzsz/bin/lrz rz
   #ln -s /usr/local/lrzsz/bin/lsz sz
   ```

9. 测试

   运行 **rz** 弹出 **SecureCRT** 上传窗口，用 **SecureCRT** 来上传和下载文件；

##### 二. 设置 SecureCRT 上传和下载的默认目录

- **options -> session options -> Terminal -> Xmodem/Zmodem** 下在右栏 **directory** 设置上传和下载目录；

##### 三. 使用 Zmodem 从客户端上传文件到服务器

- 在用 **SecureCRT** 登录 **Linux** 终端；
- 选中你要放置上传文件的路径，在目录下然后输入 **rz** 命令，**SecureCRT** 会弹出文件选择对话框，在查找范围中找到你要上传的文件，按 **Add** 按钮。然后 **OK** 就可以把文件上传到 **Linux** 上了；
- 或者在 **Transfer -> Zmodem Upload list** 弹出文件选择框，选好文件后按 **Add** 按钮，然后 **OK** 窗口自动关闭。然后在 **Linux** 下选中存放文件的目录，输入 **rz** 命令。**Linux** 就把那个文件上传到这个目录下了；

##### 四. 使用 Zmodem 下载文件到客户端

- **sz filename** ；
- **zomdem** 接收可以自行启动。下载的文件存放在你设定的默认下载目录下；

**rz**，**sz** 是 **Linux/Unix** 同 **Windows** 进行 **ZModem** 文件传输的命令行工具。**windows** 端需要支持 **ZModem** 的 **telnet/ssh** 客户端，**SecureCRT** 就可以用 **SecureCRT** 登录到 **Linux/Unix** 主机(**telnet** 或 **ssh** 均可)；

**O** 运行命令 **rz** ，即使接收文件，**SecureCRT** 就会弹出文件选择对话框，选好文件之后关闭对话框，文件就会上传到当前目录；

**O** 运行命令 **sz file1 file2** ，就是发文件到 **windows** 上(保存的目录是可以配置的)，比 **ftp** 命令方便多了，而且服务器不用再开 **FTP** 服务了；