### chmod 命令

- **chmod** 命令用于改变 **Linux** 系统文件或目录的访问权限。用它控制文件或目录的访问权限。该命令有两种用法。一种是包含字母和操作符表达式的 **文字设定法** ；另一种是包含数字的 **数字设定法** 。

- **Linux** 系统中的每个文件和目录都有访问许可权限，用它来确定谁可以通过何种方式对文件和目录进行访问和操作。

- 文件或目录的访问权限分为只读，只写和可执行三种。以文件为例，只读权限表示只允许读其内容，而禁止对其做任何的更改操作。可执行权限表示允许将该文件作为一个程序执行。文件被创建时，文件所有者自动拥有对该文件的读、写和可执行权限，以便于对文件的阅读和修改。用户也可根据需要把访问权限设置为需要的任何组合。

- 有三种不同类型的用户可对文件或目录进行访问：**文件所有者，同组用户、其他用户**。所有者一般是文件的创建者。所有者可以允许同组用户有权访问文件，还可以将文件的访问权限赋予系统中的其他用户。在这种情况下，系统中每一位用户都能访问该用户拥有的文件或目录。

- 每一文件或目录的访问权限都有三组，每组用三位表示，分别为 **文件属主** 的读、写和执行权限；与 **属主同组的用户** 的读、写和执行权限；**系统中其他用户** 的读、写和执行权限。当用ls -l命令显示文件或目录的详细信息时，最左边的一列为文件的访问权限。 例如：

- **命令**

  ```bash
  ls -al
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -al
  total 16
  -rw-r--r--@ 1 qiu  staff  136  4 26 09:45 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  drwxrwxr-x  5 qiu  staff  160  4 23 11:05 test1
  ```

- **说明**

  以 **log.log** 为例：

  **-rw-r--r--@ 1 qiu  staff  136  4 26 09:45 log.log**

  第一列共有10个位置，第一个字符指定了文件类型。在通常意义上，一个目录也是一个文件。如果第一个字符是横线，表示是一个非目录的文件（普通文件）。如果是d，表示是一个目录。从第二个字符开始到第十个共9个字符，3个字符一组，分别表示了3组用户对文件或者目录的权限。权限字符用横线代表空许可，r代表只读，w代表写，x代表可执行。

- **例如**

  **- rw- r- - r- -**

  表示 **log.log** 是一个普通文件；文件属主有读写权限；与属主同组的用户具有只读权限；其他用户也只有只读权限；

- 确定了一个文件的访问权限后，用户可以利用 **Linux** 系统提供的 **chmod** 命令来重新设定不同的访问权限。也可以利用 **chown** 命令来更改某个文件或目录的所有者。利用 **chgrp** 命令来更改某个文件或目录的用户组。
- **chmod** 命令是非常重要的，用于改变文件或目录的访问权限。用户用它控制文件或目录的访问权限。**chmod** 命令详细情况如下。

#### chmod 命令介绍

- **命令格式** - chmod [-cfvR] [—help] [—version] mode file

- **命令功能** - 用于改变文件或目录的访问权限，用它控制文件或目录的访问权限

- **命令参数**

  - **必要参数**

    **-c** ：当发生改变时，报告处理信息；

    **-f** ：错误信息不输出；

    **-R** ：处理指定目录及其子目录下的所有文件；

    **-v** ：运行时显示详细信息；

  - **选择参数**

    **—reference=<目录或者文件>** ：设置成具有指定目录或者文件具有相同的权限；

    **—version** ：显示版本信息；

    **\<权限范围\>+\<权限设置\>** ：使权限范围内的目录或者文件具有指定的权限；

    **\<权限范围\>-\<权限设置\>** ：删除权限范围的目录或者文件的指定权限；

    **\<权限范围\>=\<权限设置\>** ：设置权限范围内的目录或者文件的权限为指定的值；

    **权限范围**

    **u** ：目录或者文件的当前的 **用户** ；

    **g** ：目录或者文件的当前的 **用户所在组** ；

    **o** ：除了目录或者文件的当前用户和群组之外的 **用户或群组** ；

    **a** ：**所有的用户和群组** ；

    **权限代号**

    **r** ：读权限，用数字 **4** 表示；

    **w** ：写权限，用数字 **2** 表示；

    **x** ：执行权限，用数字 **1** 表示；

    **-** ：删除权限，用数字 **0** 表示；

    **s** ：特殊权限

    - 该命令有两种用法。一种是包含字母和操作符表达式的 **文字设定法** ；另一种是包含数字的 **数字设定法** ；

    - **1. 文字设定法**

      **chmod [who] [+|-|=] [mode] 文件名**

    - **2. 数字设定法**

      数字的含义：**0** 表示没有权限，**1** 表示可执行权限，**2** 表示可写权限，**4** 表示可读权限，然后将其现价。所以数字属性的格式应为3个从 **0** 到 **7** 的八进制数，其顺序是 **(u) (g) (o)** ；

      例如，如果想让某个文件的属主具有"读/写"两种权限，只需要把 **4(可读) + 2(可写) = 6(读/写)** ；

      数字设定法的一般形式为：

      **chmod [mode] 文件名**

    - **数字与字符的对应关系如下：**

      **r=4，w=2，x=1**

      若要 **rwx** 属性则 **4+2+1=7** ;

      若要 **rw-** 属性则 **4+2=6** ；

      若要 **r-x** 属性则 **4+1=5** ；

- **命令实例**

- **实例一：增加文件所有用户可执行权限**

- **命令**

  ```bash
  chmod a+x log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rw-r--r--@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ chmod a+x log.log
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rwxr-xr-x@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ 
  ```

- **实例二：同时修改不同用户权限**

- **命令**

  ```bash
  chmod ug+w,o-x log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rwxr-xr-x@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ chmod ug+w,o-x log.log
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rwxrwxr--@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ 
  ```

- **实例三：删除文件权限**

- **命令**

  ```bash
  chmod a-x log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rwxrwxr--@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ chmod a-x log.log
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rw-rw-r--@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ 
  ```

- **实例四：使用 "=" 设置权限**

- **命令**

  ```bash
  chmod u=x log.log
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  -rw-rw-r--@ 1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ chmod u=x log.log
  Qs-MacBook-Pro:dir1 qiu$ ls -l log.log
  ---xrw-r--  1 qiu  staff  136  4 26 09:45 log.log
  Qs-MacBook-Pro:dir1 qiu$ 
  ```

- **说明**

  只改变当前 **u** 组；

- **实例五：对一个目录及其子目录所有文件添加权限**

- **命令**

  ```bash
  chmod -R u+x dir1
  ```

- **输出**

  ```bash
  Qs-MacBook-Pro:dir1 qiu$ ls -lR dir1
  total 16
  ---xrw-r--  1 qiu  staff  136  4 26 09:45 log.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 log1.log
  drwxrwxr-x  5 qiu  staff  160  4 23 11:05 test1
  
  dir1/test1:
  total 16
  -rw-r--r--@ 1 qiu  staff  136  4 22 10:15 t1-1.log
  -rw-r--r--  1 qiu  staff   21  4 22 10:07 t1-2.log
  Qs-MacBook-Pro:dir1 qiu$ chmod -R u+x dir1
  Qs-MacBook-Pro:dir1 qiu$ ls -lR dir1
  total 16
  ---xrw-r--  1 qiu  staff  136  4 26 09:45 log.log
  -rwxr--r--  1 qiu  staff   21  4 22 10:07 log1.log
  drwxrwxr-x  5 qiu  staff  160  4 23 11:05 test1
  
  dir1/test1:
  total 16
  -rwxr--r--@ 1 qiu  staff  136  4 22 10:15 t1-1.log
  -rwxr--r--  1 qiu  staff   21  4 22 10:07 t1-2.log
  Qs-MacBook-Pro:dir1 qiu$ 
  ```

- **一些其他实例！！**

- **1）.**

- **命令**

  ```bash
  chmod 751 file
  ```

- **输出**

  给 **file** 的属主分配读、写、执行(7)的权限；给 **file** 所在组分配读、执行(5)的权限；给其他用户分配执行(1)的权限；

- **2）.**

- **命令**

  ```bash
  chmod u=rwx,g=rx,o=x file
  ```

- **输出**

  上例的另一种形式；

- **3）.**

- **命令**

  ```bash
  chmod =r file
  chmod 444 file
  ```

- **输出**

  为 **所有用户** 分配读权限；

- **4）.**

- **命令**

  ```bash
  chmod a-wx,a+r file
  ```

- **输出**

  同上例；