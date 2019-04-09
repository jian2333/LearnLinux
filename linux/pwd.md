### pwd 命令

- 显示当前目录；

- **命令格式** - pwd [选项]；

- **命令功能** - 查看 "当前工作目录"的完整路径；

- **常用命令参数** - 

  - **-L** ：目录为链接时，显示链接路径；
  - **-P** ：目录为链接时，显示实际物理路径；

- **常用范例** - 

  - 显示当前路径

    ```bash
    pwd
    ```

  - 显示链接目录的路径

    ```bash
    pwd
    pwd -L
    
    Qs-MacBook-Pro:/ qiu$ cd /etc/
    Qs-MacBook-Pro:etc qiu$ pwd -L
    /etc
    ```

  - 显示链接目录的实际物理路径

    ```bash
    pwd -P
    
    Qs-MacBook-Pro:/ qiu$ cd /etc/
    Qs-MacBook-Pro:etc qiu$ pwd -P
    /private/etc
    ```

- **补充** -

  - **/bin/pwd** ：和 **pwd** 一样，是 **pwd** 这个命令在 mac 中的实际物理路径；
  - 当前目录被删除后，用 **pwd** 命令仍能显示该目录名称；