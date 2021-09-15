## Docker简介

docker可以简单的理解为一个轻量级的虚拟机，我们将docker中的虚拟机称为`容器` ,`container`，用来创建容器的文件则被称为`镜像`,`image`, 实际运行虚拟机的服务器称之为`宿主机`。

通过docker，我们可以快速的在不同的服务器上部署运行程序，无须重复配置运行环境。

## Docker安装

https://cloud.tencent.com/developer/article/1541709

## 查看镜像与容器状态

```shell
docker images  # 查看服务器中镜像
docker container ls  # 查看所有正在运行的容器
docker container ls -a  # 查看所有容器（包括已经停止的）
```

如果本地没有基础的镜像，可以通过`https://hub.docker.com/`查询网络仓库中可用镜像，建议使用官方提供的镜像

```shell
docker pull [OPTIONS] NAME[:TAG|@DIGEST]  # 从dockerhub下载镜像到本地宿主机
```

### 注意！容器和镜像默认都是存在系统盘里，请定期清理无用的容器和镜像！

## 容器创建与进入

```shell
# 从镜像运行一个没有GPU的容器
docker container run --name [set a name] -dit [IMAGE_ID] bash

# 从镜像运行一个没有GPU的容器并将宿主机目录映射到容器中
docker container run --name [set a name] -v /src_dir:/dst_dir -dit [IMAGE_ID] bash

# 从镜像运行一个分配有GPU的容器
docker container run --runtime nvidia --gpus all --name [set a name] -dit [IMAGE_ID] bash

# 进入容器
docker exec -it [CONTAINER_ID/NAME] bash
```

参数说明：

`-dit`: 创建终端但是不进入

`-it`: 创建终端并进入

`-v`: 将宿主机的目录映射到容器中（相当于在容器内建立了一个软连接），例`-v /home/victoria/Documents:/home/Documents`是将宿主机的`/home/victoria/Documents`目录映射到容器的`/home/Documents`目录中，可选项

`-p`: 将容器中的端口映射到宿主机上，例`-p 16006:6006`是将容器的6006端口映射到宿主机的16006端口，可选项

`--runtime nvidia --gpus all`需要用**显卡**的容器的必选项，`--gpus all`可以换成指定的`gpu_id`

`--shm-size`: 给容器分配指定的内存大小，可选项

## Container与宿主机之间的文件传输

### 1. 在运行容器时把宿主机的目录映射到容器中

```shell
docker container run -v /host_dir:/dst_dir
```

-v代表使用目录映射，/host_dir是宿主机中的文件目录，dst_dir是容器中对应的目录，这两个目录之间的内容是共享的。需要注意的是目录映射里的文件不会随container的导出而导出。

### 2. 使用docker cp复制文件

```shell
# 把container中的文件复制到宿主机中
docker cp [container_id]:/file_dir /dst_dir

# 把宿主机的文件复制到container中
docker cp /dst_dir [container_id]:/file_dir
```

## Docker的导出与导入

#### Step 1: 将容器保存为镜像

```shell
# 首先停止运行container
docker container stop [CONTAINER]

# 将正在运行的容器导出为镜像
docker commit [CONTAINER] [REPOSITORY[:TAG]]

# 示例
docker commit pytorch cocorrecting:v1
```

### Step 2: 导出镜像为tar文件

```shell
# 将镜像导出为tar文件
docker save -o [FILE_NAME] [IMAGE]

# 示例
docker save -o cocorrecting.tar cocorrecting:v1
```

其中-o表示输出到文件，`nginx.tar`为目标文件，`nginx:latest`是源镜像名（name:tag）Step 2: 导出镜像为tar文件

### Step 3: 从tar文件加载镜像

```shell
# 将镜像导出为tar文件
docker load -i [FILE_NAME]

# 示例
docker load -i cocorrecting.tar
```

其中-o表示输出到文件，`nginx.tar`为目标文件，`nginx:latest`是源镜像名（name:tag）

