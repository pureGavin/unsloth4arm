# Introduction

Since the official unsloth repository does not provide Docker images for the ARM architecture, this project was created.

# how to use

As mentioned in the official unsloth documentation, you must first install [Docker](https://docs.docker.com/engine/install/ubuntu/) and the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation) locally before using this project.

Due to the specific nature of the machine I am using (NVIDIA GB10), all installation methods posted here are for Ubuntu.

Once your local environment is ready, you can use either of the following two methods to obtain the image

## Build your own image

Use the following command to build your own Docker image

```shell
docker build -t unsloth4arm:202512 .
```

## Download the image

You can also download the Docker image I uploaded.

```shell
docker pull ghcr.io/puregavin/unsloth4arm:latest
```

## Run Image

I use the Docker command to run the image. Note that whether port 22 for the Jupyter server is mapped depends on your own configuration.

Before running the command, remember to modify the image name to the latest image or the image you want.

```shell
docker run -d --name=unsloth4arm --restart=always  -p 8888:8888 -v ./work/:/work/ -w /work --gpus=all unsloth4arm:202512
```

You can also use the provided Docker Compose file to run the image, though I haven't tried this method myself :p

```shell
docker compose up -d
```

After startup, you'll also need to run the following command in the terminal to obtain the Jupyter server token for login purposes.

```shell
docker exec -it unsloth4arm jupyter server list
```

I have prepared an IPython notebook file in the work folder to test whether your local setup was successful.

# Reminder

1. I am using NVIDIA's GB10 compute card. Please refrain from inquiring about the usage of M-series chips.

2. Given that the GB10 chip has only recently been released, there are bound to be numerous software compatibility issues. If you intend to use it commercially, please proceed with caution.

3. For questions regarding the use of unsloth, please consult the [official unsloth](https://github.com/unslothai/unsloth) documentation.