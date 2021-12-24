## 概述

ssh是一种通过网络连接服务器的方式，在linux/mac中默认安装，windows中可以通过windows terminal, powershell或xshell/putty进行连接。

## 命令行连接

```shell
# 基本连接方式
ssh <user_name>@ip_ad

# 示例
ssh victoria@192.168.1.2
```

其中，`<user_name>`是目标服务器中的用户名，连接后会需要我们输入对应用户的密码。

## 服务器文件上传/下载

最基础的命令行操作方式

```shell
# 把文件从source传输到dst，-r表示支持传输目录，单个文件传输可以不加
scp -r [src_username]@[src ip address]:/abs/dir/to/src/file [target_username]@[target ip address]:/abs/dir/to/target/file

# 文件传输示例
scp -r futong@172.12.51.234:/home/futong/jiarunliu fgldlb@192.168.1.101:/home/Documents/
```

文件传输建议使用`FileZilla`、`Xftp`等软件，不需要敲命令方便使用

## 公钥连接

通常情况下，ssh连接需要输入系统密码进行安全验证。实际上，ssh提供了另一种更加安全、便捷的安全验证方式：公钥连接。使用公钥连接时，ssh会自动的对本机上的私钥文件和服务器上的公钥文件进行配对验证。

### 生成公钥/私钥文件

在命令行中输入`ssh-keygen`，之后选择默认设置回车即可，系统会在`～/.ssh`下生成`id_rsa`(私钥文件)和`id_rsa.pub`(公钥文件)两个文件。

### 在服务器中添加公钥内容

使用公钥访问服务器，需要将公钥文件的内容存放在服务器的`~/.ssh/authorized_keys`文件中。分为如下两步：

- 在本机使用`cat ~/.ssh/id_rsa.pub`查看公钥内容，并复制出来
- 在服务器使用`echo "${PUB_KEY}" >> ~/.ssh/authorized_keys`命令，将本机公钥文件内容添加到文件末尾，其中`${PUB_KEY}`为上一步查看得到的公钥内容。

### 使用公钥ssh连接服务器

```shell
# 第一次使用公钥连接需指定公钥文件
ssh <user_name>@ip_ad -i <key_file>

# 示例
ssh victoria@192.168.1.2 -i ~/.ssh/id_rsa
```

第一次连接需要使用`-i`命令指定私钥文件，使用公钥连接无需输入密码，如需输入系统密码则表明公钥连接失败，需要检查ssh/公钥配置。
