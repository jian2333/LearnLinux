### locate 命令

- **locate** 让使用者可以很快速的搜寻档案系统内是否有指定的档案。

- 其方法是先建立一个包括系统内所有档案名及路径的数据库，之后查询时就 **只查询这个数据库** ，而不必实际深入档案系统之中了。

- 在一般的 **distribution** 中，数据库的建立都被放在 **crontab** 中自动执行；

- **命令格式** - locate [选择参数] [样式]

- **命令功能** - 

  - **locate** 命令可以在搜寻数据库时快速找到档案。数据库由 **updatedb** 程序来更新，**updatedb** 是由 **cron daemon** 周期性建立的。**locate** 命令在搜寻数据库时比整个由硬盘资料来搜寻资料来的更快，但较差劲的是 **locate** 所找到的档案若是最近才建立的或刚更名的，可能会找不到。在内定值内，**update** 每天会跑一次，可以由修改 **crontab** 来更新设定值（**etc/crontab**）；
  - **locate** 指定用在搜寻符合条件的档案，它会去储存档案与目录名称的数据库内，寻找合乎范本样式条件的档案或目录名，可以使用特殊字元（如 **\*** 或 **?** 等）来指定范本样式，如指定范本为 **kcpa\*ner** ，**locate** 会找出所有起始字串为 **kcpa** 且结尾为 **ner** 的档案或目录，如名称为 **kcpartner**，若目录名称为 **kcpartner** 则会列出该目录下 **包括子目录在内** 的所有档案；
  - **locate** 命令和 **find** 找寻档案的类似，但 **locate** 是透过 **update** 程序将硬盘中的所有档案和目录资料先建立一个索引数据库，在执行 **locate** 时直接找该索引，查询速度会比较快，索引数据库一般由操作系统管理，但也可以直接下达 **update** 强迫系统立即修改索引数据库；

- **命令参数** - 

  - **-e** ：将排除在寻找的范围之外；
  - **-1** ：如果是1，则启动安全模式。在安全模式下，使用者不会看到权限无法看到的档案。则会使速度减慢，因为 **locate** 必须至实际档案系统中取得档案的 权限资料；
  - **-f** ：将特定的档案系统排除在外，例如我们没有道理要把 **proc** 档案系统中的档案放在资料库中；
  - **-q** ：安静模式，不会显示任何错误讯息；
  - **-n** ：至多显示 **n** 个输出；
  - **-r** ：使用正规表达式，做寻找的条件；
  - **-o** ：指定资料库存的名称；
  - **-d** ：指定资料库的路径；
  - **-h** ：显示辅助讯息；
  - **-V** ：显示程式的版本讯息；

- **命令实例** - 

- **实例一：系统第一次使用时，创建该数据库**

- **命令**

  ```bash
  // 任何与数据库有关的操作，比如
  locate pwd
  // Mac_Terminal 下
  sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ locate pwd
  
  WARNING: The locate database (/var/db/locate.database) does not exist.
  To create the database, run the following command:
  
    sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
  
  Please be aware that the database can take some time to generate; once
  the database has been created, this message will no longer appear.
  
  Qs-MacBook-Pro:dir1 qiu$ sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist
  Password:
  Qs-MacBook-Pro:dir1 qiu$
  ```

- **实例二：查找和 pwd 相关的所有文件**

- **命令**

  ```bash
  locate pwd
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ locate pwd
  /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/test/test_pwd.py
  /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/test/test_pwd.pyc
  /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/test/test_pwd.pyo
  /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/test/test_spwd.py
  /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/test/test_spwd.pyc
  /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/test/test_spwd.pyo
  /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/share/ri/2.3.0/system/Dir/pwd-c.ri
  /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/share/ri/2.3.0/system/FileUtils/pwd-c.ri
  /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/share/ri/2.3.0/system/FileUtils/pwd-i.ri
  /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/share/ri/2.3.0/system/Net/FTP/pwd-i.ri
  /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/share/ri/2.3.0/system/Pathname/pwd-c.ri
  /System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/share/ri/2.3.0/system/Shell/pwd-i.ri
  /System/Library/Frameworks/Tcl.framework/Versions/8.5/Resources/Documentation/Reference/Tcl/TclCmd/pwd.htm
  /System/Library/PrivateFrameworks/JavaScriptAppleEvents.framework/Versions/A/Resources/BridgeSupportCache/pwd.plist
  /System/Library/Tcl/8.5/tclx8.4/help/tcl/status/pwd
  /Users/qiu/mine/project/JianEssay/md/linux/pwd.html
  /Users/qiu/mine/project/LearnLinux/linux/pwd.md
  /Users/qiu/mine/project/vueDemo/my-project/node_modules/_shelljs@0.7.8@shelljs/src/pwd.js
  /Users/qiu/mine/study/mdTemp/pwd.html
  /bin/pwd
  /usr/sbin/pwd_mkdb
  /usr/share/cracklib/pw_dict.pwd
  /usr/share/man/man1/pwd.1
  /usr/share/man/man8/pwd_mkdb.8
  /usr/share/man/mann/pwd.ntcl
  /usr/share/zsh/5.3/functions/_external_pwds
  /usr/share/zsh/5.3/functions/chpwd_recent_add
  /usr/share/zsh/5.3/functions/chpwd_recent_dirs
  /usr/share/zsh/5.3/functions/chpwd_recent_filehandler
  /usr/share/zsh/5.3/functions/zftp_chpwd
  /usr/share/zsh/5.3/help/pwd
  Qs-MacBook-Pro:dir1 qiu$
  ```

- **实例三：搜索 etc 目录下所有以 m 开头的文件**

- **命令**

  ```bash
  locate /etc/m
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ locate /etc/m
  /private/etc/mach_init.d
  /private/etc/mach_init_per_login_session.d
  /private/etc/mach_init_per_user.d
  /private/etc/mail.rc
  /private/etc/man.conf
  /private/etc/manpaths
  /private/etc/manpaths.d
  /private/etc/master.passwd
  /usr/share/emacs/22.1/etc/ms-kermit
  ```

  