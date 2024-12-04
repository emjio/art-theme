---
title:  Linux 命令手册
description:  Linux 命令手册
pubDate: 2022/2/25
author: cabbage
heroImage: "https://www.notion.so/images/page-cover/nasa_reduced_gravity_walking_simulator.jpg"
tags: ["linux"]
---

## 查找文件

(1)`find`命令是根据文件的属性进行查找，如文件名，文件大小，所有者，所属组，是否为空，访问时间，修改时间等。

(2)`grep`是根据文件的内容进行查找，会对文件的每一行按照给定的模式(patter)进行匹配查找。

(3)`which` 查看可执行文件的位置 ，只有设置了环境变量的程序才可以用

(4)`whereis` 寻找特定文件，只能用于查找二进制文件、源代码文件和man手册页

(5)`locate` 配合数据库查看文件位置 ,详情：locate -h查看帮助信息 (安装，安装完成之后执行`updatedb` 更新数据库)

一.find命令

基本格式：`find path expression`

1.按照文件名查找

(1)`find / -name httpd.conf`　#在根目录下查找文件httpd.conf，表示在整个硬盘查找　(2)`find /etc -name httpd.conf`　#在/etc目录下文件httpd.conf　(3)`find /etc -name '*srm*`'　#使用通配符*(0或者任意多个)。表示在/etc目录下查找文件名中含有字符串‘srm’的文件　(4)find . -name 'srm*'　#表示当前目录下查找文件名开头是字符串‘srm’的文件

2.按照文件特征查找

(1)find / -amin -10　# 查找在系统中最后10分钟访问的文件(access time)　(2)find / -atime -2 # 查找在系统中最后48小时访问的文件　(3)find / -empty　# 查找在系统中为空的文件或者文件夹　(4)find / -group cat　# 查找在系统中属于 group为cat的文件　(5)find / -mmin -5　# 查找在系统中最后5分钟里修改过的文件(modify time)　(6)find / -mtime -1　#查找在系统中最后24小时里修改过的文件　(7)find / -user fred　#查找在系统中属于fred这个用户的文件　(8)find / -size +10000c　#查找出大于10000000字节的文件(c:字节，w:双字，k:KB，M:MB，G:GB)　(9)find / -size -1000k　#查找出小于1000KB的文件

3.使用混合查找方式查找文件

参数有： ！，-and(-a)，-or(-o)。

(1). find /tmp -size +10000c -and -mtime +2　#在/tmp目录下查找大于10000字节并在最后2分钟内修改的文件。
(2). find / -user fred -or -user george　#在/目录下查找用户是fred或者george的文件文件。
(3). find /tmp ! -user panda　#在/tmp目录中查找所有不属于panda用户的文件 。

二、grep命令

基本格式：find expression

1.主要参数

[options]主要参数：

- c:只输出匹配行的计数。
- i：不区分大小写
- h：查询多文件时不显示文件名。
- l：查询多文件时只输出包含匹配字符的文件名。
- n：显示匹配行及行号。
- s：不显示不存在或无匹配文本的错误信息。
- v：显示不包含匹配文本的所有行。

pattern正则表达式主要参数：

- \： 忽略正则表达式中特殊字符的原有含义。
- ^：匹配正则表达式的开始行。
- $: 匹配正则表达式的结束行。
- \<：从匹配正则表达 式的行开始。
- \>：到匹配正则表达式的行结束。
- ：单个字符，如[A]即A符合要求 。
- [ - ]：范围，如[A-Z]，即A、B、C一直到Z都符合要求 。
- .：所有的单个字符。
- * ：有字符，长度可以为0。

2.实例

 **grep -r "字符串" 很方便**

(1). grep 'test' d*`　#显示所有以d开头的文件中包含 test的行
(2). grep ‘test’ aa bb cc #显示在aa，bb，cc文件中包含test的行
(3). grep ‘[a-z]\{5\}’ aa　#显示所有包含每行字符串至少有5个连续小写字符的字符串的行
(4). grep magic /usr/src　#显示/usr/src目录下的文件(不含子目录)包含magic的行
(5). grep -r magic /usr/src　#显示/usr/src目录下的文件(包含子目录)包含magic的行
(6). grep -w pattern files ：只匹配整个单词，而不是字符串的一部分(如匹配’magic’，而不是’magical’)，

# *centos8 安装docker*

```bash
yum install wget

wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo

yum clean all

yum makecache

*# 1.更新yum*

*# 2.安装依赖包*

yum install -y yum-utils device-mapper-persistent-data lvm2

*# 3.设置源*

yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

*# 4.查看docker版本*

yum list docker-ce --showduplicates | sort -r

*# 5.安装对应版本*

yum install docker-ce -y

*# 6.启动*

systemctl start docker

systemctl enable docker

*# 停止firewall*

systemctl stop firewalld

*# 禁止firewall开机启动*

systemctl disable firewalld

*# 防火墙状态*

firewall-cmd --state

*# 开放5672端口*

firewall-cmd --zone=public --add-port=6379/tcp --permanent

*#关闭5672端口*

firewall-cmd --zone=public --remove-port=6379/tcp --permanent

*# 配置立即生效*

firewall-cmd --reload

*# 查看防火墙所有开放的端口*

firewall-cmd --zone=public --list-ports

```

```

清除 SSH 登录日志使用下面命令。

## **清除 Bash 历史命令**

Bash 执行过的命令存在用户目录下的`.bash_history`文件里，用`history`命令查看。

清除所有历史命令记录，第二条命令表示立即更新日志文件。

```bash
history -c
history -w
```

### 数据库管理

### 创建用户

~~~mysql CREATE USER '{username}'@'{ip_addr}' IDENTIFIED BY '{password}'; ~~~

{username} 用户名

{ip_addr} ip地址 （localhost）

{password} 密码

### 删除用户

~~~mysql DROP USER ‘username’@'ip_addr'; ~~~

### 更改密码

不需要刷新

~~~mysql SET PASSWORD FOR 'username' = PASSWORD('password'); ~~~

需要刷新

~~~mysql UPDATE mysql.user SET PASSWORD = PASSWORD('1234') WHERE user='username'; FLUSH PRIVILEGES; ~~~

### 用户分配权限

**全部权限**

~~~mysql GRANT ALL PRIVILEGES ON db.* to 'username'@'ip_addr' IDENTIFIED BY 'password'; FLUSH PRIVILEGES; ~~~

**部分权限**

~~~mysql GRANT CREATE,ALTER,DROP,SELECT,INSERT,UPDATE,DELETE ON db.* to 'username'@'ip_addr'; ~~~

部分权限筛选：INSERT、UPDATE、SELECT

不开放删除与表结构的修改，统一回收到一个账号上

### 查看用户权限

~~~mysql show grants for root@localhost; ~~~

### MySQL权限详解

- All/All Privileges权限代表全局或者全数据库对象级别的所有权限
- Alter权限代表允许修改表结构的权限，但**必须要求有create和insert权限配合**。如果是rename表名，则要求有alter和drop原表， create和insert新表的权限
- Alter routine权限代表允许修改或者删除存储过程、函数的权限
- Create权限代表允许创建新的数据库和表的权限
- Create routine权限代表允许创建存储过程、函数的权限
- Create tablespace权限代表允许创建、修改、删除表空间和日志组的权限
- Create temporary tables权限代表允许创建临时表的权限
- Create user权限代表允许创建、修改、删除、重命名user的权限
- Create view权限代表允许创建视图的权限
- Delete权限代表允许删除行数据的权限
- Drop权限代表允许删除数据库、表、视图的权限，包括truncate table命令
- Event权限代表允许查询，创建，修改，删除MySQL事件
- Execute权限代表允许执行存储过程和函数的权限
- File权限代表允许在MySQL可以访问的目录进行读写磁盘文件操作，可使用的命令包括load data infile,select … into outfile,load file()函数
- Grant option权限代表是否允许此用户授权或者收回给其他用户你给予的权限,重新付给管理员的时候需要加上这个权限
- Index权限代表是否允许创建和删除索引
- Insert权限代表是否允许在表里插入数据，同时在执行analyze table,optimize table,repair table语句的时候也需要insert权限
- Lock权限代表允许对拥有select权限的表进行锁定，以防止其他链接对此表的读或写
- Process权限代表允许查看MySQL中的进程信息，比如执行show processlist, mysqladmin processlist, show engine等命令
- Reference权限是在5.7.6版本之后引入，代表是否允许创建外键
- Reload权限代表允许执行flush命令，指明重新加载权限表到系统内存中，refresh命令代表关闭和重新开启日志文件并刷新所有的表
- Replication client权限代表允许执行show master status,show slave status,show binary logs命令
- Replication slave权限代表允许slave主机通过此用户连接master以便建立主从复制关系
- Select权限代表允许从表中查看数据，某些不查询表数据的select执行则不需要此权限，如Select 1+1， Select PI()+2；而且select权限在执行update/delete语句中含有where条件的情况下也是需要的
- Show databases权限代表通过执行show databases命令查看所有的数据库名
- Show view权限代表通过执行show create view命令查看视图创建的语句
- Shutdown权限代表允许关闭数据库实例，执行语句包括mysqladmin shutdown
- Super权限代表允许执行一系列数据库管理命令，包括kill强制关闭某个连接命令， change master to创建复制关系命令，以及create/alter/drop server等命令
- Trigger权限代表允许创建，删除，执行，显示触发器的权限
- Update权限代表允许修改表中的数据的权限
- Usage权限是创建一个用户之后的默认权限，其本身代表连接登录权限

### 禁止没有加WHERE 的UPDATE操作

```sql
SET sql_safe_updates=1;
SHOW VARIABLES LIKE 'sql_safe_updates';
```

# 数据库操作

**创建数据库**

~~~mysql CREATE DATABASE IF NOT EXISTS kylin_cloud_prod DEFAULT CHARSET utf8 COLLATE utf8_general_ci; ~~~

今天在linux服务器上创建的用户，登录后发现此用户的CRT的终端提示符显示的是-bash-4.2# 而不是user@主机名 + 路径的显示方式，以往一直用的脚本也不能执行起来；原因是在用useradd添加普通用户时，有时会丢失家目录下的环境变量文件，丢失文件如下：1、.bash_profile2、.bashrc以上这些文件是每个用户都必备的文件。此时可以使用以下命令从主默认文件/etc/skel/下重新拷贝一份配置信息到此用户家目录下

```bash
cp /etc/skel/.bashrc  /home/user
cp /etc/skel/.bash_profile   /home/user
```

查看所有磁盘（包括未挂载的）

```bash
fdisk -l
df -h  已经挂载的
df -T 查看已经挂载的分区的文件系统
```

创建一个新的用户。

useraddd username 

在username 目录下创建文件夹为.ssh

在.ssh 文件夹下面创建文件 authorized_keys 将 ssh 密钥放置在里面 并将权限设置为 700 所有者为用户名
