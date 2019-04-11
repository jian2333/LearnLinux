### touch 命令

- 修改文件的创建时间或修改时间，或创建新文件；

- **命令格式** - touch [选项]… 文件...(源文件 目标文件)

- **命令功能** - 更改目录或文档的创建时间和修改时间，以及创建新的文档；

- **命令参数** -

  - **-a** ：只修改 **创建时间**；
    - **注意：Mac_Terminal 下该参数无效**；
  - **-c** ：不建立任何文档；
    - 默认情况下，**touch 文件的含义是**
    - 文件存在：修改 **修改时间** 为当前时间；
    - 文件不存在：创建文件；
  - **-d** ：使用指定的日期，而非现在的时间；
    - **注意：Mac_Terminal 下该参数无效**；
  - **-f** ：不使用，是为了与其他 unix 系统的相容性而保留；
  - **-m** ：只修改 **修改时间**；
  - **-r** ：把指定文档或目录的 **修改时间**，统统设成与参考文档或目录的 **修改时间** 相同；
  - **-t** ：使用指定的日期时间，而非现在的时间；

- **命令实例**

  - **实例一：创建不存在的文件**

  - **命令**

    ```bash
    touch log1.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    Qs-MacBook-Pro:dir1 qiu$ touch log1.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:30 log1.log
    ```

    **如果文件不存在，不创建文件**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    Qs-MacBook-Pro:dir1 qiu$ touch log1.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:36 log1.log
    Qs-MacBook-Pro:dir1 qiu$ touch -c log2.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:36 log1.log
    ```

  - **实例二：修改已存在文件的修改时间**

  - **命令**

    ```bash
    touch log1.log
    touch -m log1.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:30 log1.log
    Qs-MacBook-Pro:dir1 qiu$ touch log1.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:33 log1.log
    ```

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:33 log1.log
    Qs-MacBook-Pro:dir1 qiu$ touch -m log1.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11 09:34 log1.log
    ```

  - **实例三：把log2.log的修改时间改成和log1.log的修改时间一样**

  - **命令**

    ```bash
    touch -r log1.log log2.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  1  1  2017 log1.log
    -rw-r--r--  1 qiu  staff  0  5  6  2018 log2.log
    Qs-MacBook-Pro:dir1 qiu$ touch -r log1.log log2.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  1  1  2017 log1.log
    -rw-r--r--  1 qiu  staff  0  1  1  2017 log2.log
    ```

  - **实例四：设定文件的(修改)时间戳**

  - **命令**

    ```bash
    touch -t 201904111012 log1.log
    ```

  - **输出**

    ```bash
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  1  1  2017 log1.log
    Qs-MacBook-Pro:dir1 qiu$ touch -t 201904111012 log1.log
    Qs-MacBook-Pro:dir1 qiu$ ll
    total 0
    -rw-r--r--  1 qiu  staff  0  4 11  2019 log1.log
    ```

  - **说明**

    **-t** 使用指定的时间值 time 作为指定文件相应修改时间的值，time 格式如下：

    **[[CC]YY]MMDDhhmm[.SS]**

    **CC** - 世纪数；

    **YY** - 年数后两位。如果不给出 CC 的值，touch 自动将年数 CCYY 限定在 1969~2068之间；

    **MM** - 月数；

    **DD** - 天数；

    **hh** - 小时数；

    **mm** - 分钟数；

    **SS** - 秒数；范围为 0~61，这样可以处理闰秒；

    这些数字组成的时间是环境变量 TZ 指定的时区中的一个时间。

    由于系统限制，早于 1970.1.1 的时间是错误的。