### mkdir 命令

- 创建指定名称的目录；

- **命令格式** - mkdir [选项] 目录…；

- **命令功能** - 在当前位置创建指定名称的目录，可一次创建多个目录或文件夹。

  - 必须对父文件夹有写权限；
  - 创建的目录在同级目录下不能重名(区分大小写)；

- **命令参数** - 

  - **-m** ：模式，设定权限\<模式\>；
  - **-p** ：一个路径名称。创建路径时若某些目录不存在，会报错，加上此选项后，系统将自动创建那些不存在的目录；
  - **-v** ：每次创建新目录都显示信息；
  - **注意** -
    - **t1,t2,t3** 是 **一个** 名称为 **"t1,t2,t3"** 的目录；
    - **{t1,t2,t3}** 是 **三个** 目录，名称分别为 **t1，t2，t3**；
    - **a/b** 是 **一个** 递归目录，表示 a目录下 的 b目录；

- **命令实例** -

  - 创建一个空目录

    ```bash
    mkdir test1
    ```

  - 递归创建多个目录

    ```bash
    mkdir -p test2/test22/test222
    ```

  - 创建权限为777的目录

    ```bash
    mkdir -m 777 test3
    ```

  - 创建目录并显示信息

    ```bash
    mkdir -v test4
    ```

  - 一个命令创建项目的目录结构

    ```bash
    // 下面是示例是Linux下的；
    // mac OS X 的terminal稍有不同
    // 1.-v和-p一起使用时，-v会失效；
    // 2.没有 tree 命令，关于添加 tree 指令，可参考下方链接；
    
    mkdir -vp scf/{lib/,bin/,doc/{info,product},logs/{info,product},service/deploy/{info,product}}
    mkdir: 已创建目录 “scf”
    mkdir: 已创建目录 “scf/lib”
    mkdir: 已创建目录 “scf/bin”
    mkdir: 已创建目录 “scf/doc”
    mkdir: 已创建目录 “scf/doc/info”
    mkdir: 已创建目录 “scf/doc/product”
    mkdir: 已创建目录 “scf/logs”
    mkdir: 已创建目录 “scf/logs/info”
    mkdir: 已创建目录 “scf/logs/product”
    mkdir: 已创建目录 “scf/service”
    mkdir: 已创建目录 “scf/service/deploy”
    mkdir: 已创建目录 “scf/service/deploy/info”
    mkdir: 已创建目录 “scf/service/deploy/product”
    tree scf/
    scf/
    |-- bin
    |-- doc
    |   |-- info
    |   `-- product
    |-- lib
    |-- logs
    |   |-- info
    |   `-- product
    `-- service
       	 	`-- deploy
      	    	|-- info
            	`-- product
    12 directories, 0 files
    ```

    - [mac 添加 tree 命令](http://yijiebuyi.com/blog/c0defa3a47d16e675d58195adc35514b.html "mac添加tree命令")；