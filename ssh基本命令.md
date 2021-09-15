## 概述

ssh是一种通过网络连接服务器的方式，在linux/mac中默认安装，windows中可以通过powershell或xshell/putty进行连接。

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
