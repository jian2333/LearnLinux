### /etc/group 文件详解

- **Linux** **/etc/group** 文件和 **/etc/passwd**  和 **/etc/shadow** 文件都是有关于系统管理员对用户和用户组管理时相关的文件。

  - **linux** **/etc/group** 文件是有关于系统管理员对用户和用户组管理的文件。**linux** 用户组的所有信息都存放在 **/etc/group** 文件中；
  - 具有某种共同特性的用户集合就是 **用户组(Group)** 。**用户组(Group)** 配置文件主要有 **/etc/group** 和 **/etc/gshadow** ，其中 **/etc/gshadow** 是 **/etc/group** 的加密信息文件；

- 将用户分组是 **Linux** 系统中对用户进行管理及控制访问权限的一种手段。每个用户都属于某个用户组；

  - 一个用户组中可以有多个用户，一个用户也可以属于多个不同的用户组；
  - 当一个用户同时是多个组中的成员时，在 **/etc/passwd** 文件中记录的用户所属的主组，也就是登录时所属的默认组，而其他组称为附加组；

- 用户组的所有信息都存放在 **/etc/group** 文件中。此文件的格式是由冒号 **(:)** 隔开的若干个字段，这些字段具体如下：

  - **组名:口令:组号标识:组内用户列表**

  - **具体解释**

  - **组名**

    组名是用户组的名称，由数字和字母组成。与 **/etc/group** 中的登录名一样，组名不应该重复；

  - **口令**

    口令字段存放的是用户组加密后的口令字。一般 **Linux** 系统的用户组都没有口令，即这个字段一般为空，或者是 **\*** ；

  - **组号标识**

    组号标识符与用户标识符类似，也是一个整数，被系统内部用来表示组。别称 **GID** ；

  - **组内用户列表**

    是数组这个组的所有用户的列表。不同用户之间用逗号 **(,)** 分隔。这个用户组可能是用户的主组，也可能是附加组；

- **使用实例**

- **命令**

  ```bash
  cat /etc/group
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir3 qiu$ cat /etc/group
  ##
  # Group Database
  # 
  # Note that this file is consulted directly only when the system is running
  # in single-user mode.  At other times this information is provided by
  # Open Directory.
  #
  # See the opendirectoryd(8) man page for additional information about
  # Open Directory.
  ##
  nobody:*:-2:
  nogroup:*:-1:
  wheel:*:0:root
  daemon:*:1:root
  kmem:*:2:root
  sys:*:3:root
  tty:*:4:root
  operator:*:5:root
  mail:*:6:_teamsserver
  bin:*:7:
  procview:*:8:root
  procmod:*:9:root
  owner:*:10:
  everyone:*:12:
  _taskgated:*:13:_taskgated
  group:*:16:
  staff:*:20:root
  ...
  ```

  