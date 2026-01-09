# 介绍 [English](./README.md)

由于官方的 unsloth 仓库并未提供适用于 ARM 架构的 Docker 镜像，因此创建了本项目。

# 如何使用

如官方 unsloth 文档所述，在使用本项目之前，你必须先在本地安装 [Docker](https://docs.docker.com/engine/install/ubuntu/) 和 [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation)。由于我使用的机器比较特殊（NVIDIA GB10），因此这里发布的所有安装方式均基于 Ubuntu。

当你的本地环境准备就绪后，你可以使用以下两种方式之一来获取镜像。

## 自行构建镜像

使用以下命令构建你自己的 Docker 镜像：

```shell
docker build -t ghcr.io/puregavin/unsloth4arm:latest .
```

## 下载镜像

你也可以下载我上传的 Docker 镜像。

```shell
docker pull ghcr.io/puregavin/unsloth4arm:latest
```

## 运行镜像

我使用 Docker 命令来运行镜像。请注意，是否映射用于 Jupyter 服务器的 22 端口取决于你自己的配置。在运行命令之前，记得将镜像名称修改为最新镜像或你想要使用的镜像。

```shell
docker run -d --name=unsloth4arm --restart=always  -p 8888:8888 -v ./work/:/work/ -w /work --gpus=all ghcr.io/puregavin/unsloth4arm:latest
```

你也可以使用提供的 Docker Compose 文件来运行镜像，不过我本人还没有尝试过这种方法 :p

```shell
docker compose up -d
```

启动后，你还需要在终端中运行以下命令来获取用于登录的 Jupyter 服务器 token。

```shell
docker exec -it unsloth4arm jupyter server list
```

我在 work 文件夹中准备了一个 .ipynb 文件，用于测试你的本地设置是否成功。

# 提醒

1.  我使用的是 NVIDIA 的 GB10 计算卡。请不要询问 M 系列芯片的使用问题。
    
2.  鉴于 GB10 芯片刚发布不久，软件兼容性问题在所难免。如果你打算用于商业用途，请谨慎评估。
    
3.  关于 unsloth 的使用问题，请参考 [官方 unsloth](https://github.com/unslothai/unsloth) 文档。
