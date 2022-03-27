## 概述

ssh是一种通过网络连接服务器的方式，在linux/mac中默认安装，windows中可以通过windows terminal (推荐), powershell或xshell/putty等进行连接。本文中主要介绍命令行连接的方式。

## 命令行连接

### 基本ssh连接方式

```shell
# 基本连接方式
ssh <user_name>@<ip_address>

# 示例
ssh victoria@192.168.1.1
```

其中，`<user_name>`是目标服务器中的用户名，连接后会需要我们输入对应用户的密码。

### 指定ssh连接端口

ssh连接的默认端口是`22`端口，有时会改为其他端口，这时我们需要手动指定端口：

```shell
# 两种指定ssh连接端口的方式
ssh -p <port> <user_name>@<ip_address>
ssh <user_name>@<ip_address>:<port>

# 示例
ssh -p 22 victoria@192.168.1.1
ssh victoria@192.168.1.1:22
```

### 使用跳板机进行跳转连接

在一些情况下，我们无法直接访问到服务器，需要通过跳板机进行一次跳转，这时我们可以使用`-J`参数进行ssh跳转连接：

```shell
ssh -J <jump_user_name>@<jump_ip_address> <user_name>@<ip_address>

# 示例
ssh -J victoria@192.168.1.1:112 victoria@192.168.1.2
# ssh支持多次跳转，用“,”连接
ssh -J victoria@192.168.1.1:123,victoria@192.168.2.1:231 victoria@192.168.1.2
```

### 将远程服务器的端口映射到本地

除了使用ssh进行远程连接，我们还可以使用ssh进行端口映射，在本地查看服务器中运行的各类程序(如tensorboard):

```shell
# 基本格式
ssh -L <port_in_local>:localhost:<prot_in_server> <user_name>@<ip_address>

# 将服务器6006端口映射到本机6007,这样在本地机器访问http://127.0.0.1:6007就能打开服务器上运行的tensorboard界面
ssh -L 6007:localhost:6006 victoria@192.168.1.1 
```

除此之外，我们还可以使用`-fN`参数将ssh连接放到后台进行:

```shell
ssh -L 6007:localhost:6006 victoria@192.168.1.1 -fN
```

## 服务器文件上传/下载

### 使用scp进行文件传输

最基础的命令行操作方式:

```shell
# 把文件从source传输到dst，-r表示支持传输目录，单个文件传输可以不加
scp -r <src_username>@<src ip address>:/abs/dir/to/src/file <target_username>@<target ip address>:/abs/dir/to/target/file

# 文件传输示例
scp -r victoria@192.168.1.1:/home/jiarunliu fgldlb@192.168.1.2:/home/Documents/
```

文件传输建议使用`FileZilla`、`Xftp`等软件，不需要敲命令方便使用。

### 使用跳板机进行scp文件传输

需要通过跳板机进行scp文件传输时，需通过`-o “ProxyJump”`参数指定跳板机:

```shell
# 通过跳板机把文件从source传输到dst，ProxuJump后为跳板机
scp -o "ProxyJump <jump_user_name>@<jump_ip_address>" -r <src_username>@<src ip address>:/abs/dir/to/src/file <target_username>@<target_ip_address>:/abs/dir/to/target/fileaddress]:/abs/dir/to/target/file

# 通过跳板机scp文件传输示例
scp -o "ProxyJump victoria@192.168.2.1" -r victoria@192.168.1.1:/home/jiarunliu fgldlb@192.168.1.2:/home/Documents/
```

## 密钥连接

通常情况下，ssh连接需要输入系统密码进行安全验证。实际上，ssh提供了另一种更加安全、便捷的安全验证方式：密钥连接。使用密钥连接时，ssh会自动的对本机上的私钥文件和服务器上的公钥文件进行配对验证。

### 生成公钥/私钥文件

在命令行中输入`ssh-keygen`，之后选择默认设置回车即可，系统会在`～/.ssh`下生成`id_rsa`(私钥文件)和`id_rsa.pub`(公钥文件)两个文件。

### 在服务器中添加公钥

使用公钥访问服务器，需要将公钥文件的内容存放在服务器的`~/.ssh/authorized_keys`文件中。分为如下两步：

- 在本机使用`cat ~/.ssh/id_rsa.pub`查看公钥内容，并复制出来
- 在服务器使用`echo "${PUB_KEY}" >> ~/.ssh/authorized_keys`命令，将本机公钥文件内容添加到文件末尾，其中`${PUB_KEY}`为上一步查看得到的公钥内容。

### 使用密钥ssh连接服务器

```shell
# 第一次使用密钥连接需指定私钥文件
ssh <user_name>@ip_ad -i <key_file>

# 示例
ssh victoria@192.168.1.2 -i ~/.ssh/id_rsa
```

第一次连接需要使用`-i`命令指定私钥文件，使用公钥连接无需输入密码，如需输入系统密码则表明公钥连接失败，需要检查ssh/公钥配置。

## 配置config文件实现快捷连接

可以配置本机的`～/.ssh/config`文件，实现快捷连接:

```shell
# 添加如下信息到config文件中即可
Host <set_name>  # 自己设置一个快捷名称
  HostName <ip_address>  # 服务器ip地址
  Prot <port>  # 默认22,有时会设置为其他的端口,根据实际端口选择
  User <user_name> # 服务器用户名
  IdentityFile ~/.ssh/id_rsa  # 本机上的私钥文件，没有配置密钥连接的可以省略
 
# 示例
Host orange
  HostName 192.168.1.1
  Prot 22
  User victoria
  IdentityFile ~/.ssh/id_rsa

# 配置一次，无需复杂命令即可连接
ssh orange

```

## 使用公网连接服务器

如有公网连接的使用需求，请私聊[管理员](jiarunliu@foxmail.com)获取详细信息。
