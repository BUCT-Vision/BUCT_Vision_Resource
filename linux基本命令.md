## 基本文件/目录操作命令

```shell
ls  # 查看当前路径下文件和子路径
ls -a # 查看当前路径下文件和子路径(包括隐藏文件)

# 路径切换
cd [dir]  # 切换到XX目录下
cd ..  # 切换到上一级目录下
cd ~  # 切换到主目录下

# 文件复制、移动、删除等操作
mkdir  # 创建目录
cp [source] [dst]  # 把文件从source复制到dst
mv [source] [dst]  # 把文件从source移动到dst
rm [file]  # 删除file
rm -rf [dir]  # 删除路径[dir]及其子目录下所有文件

# 权限相关
sudo [command]  # 使用管理员权限进行操作
chmod 777 [dir]  # 开放目录的读写权限
```

## 其他

```shell
# 文件编辑
vim [file] # vim编辑器，使用方法请自查

# 显卡状态查询
# [请不要改变服务器的显卡驱动和CUDA]
nvidia-smi  # 查看显卡状态
watch -n 1 nvidia-smi  # 查看显卡状态,每隔一秒刷新一次
nvcc -V # 查看cuda版本

htop # CPU,内存使用情况查看
```

