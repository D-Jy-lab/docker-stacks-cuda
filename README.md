# Jupyter Docker Stacks with NVIDIA GPU

本项目基于原有的Jupyter Docker Stacks项目，添加了常用工具和对NVIDIA GPU的支持，便于开箱即用。

## 快速开始

在使用本项目之前，您需要参考NVIDIA的[教程](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)来配置环境（假设您已安装好GPU驱动和Docker环境，如未配置，请先行配置）。

### 容器说明

详细信息请参考[Jupyter Docker Stacks官方文档](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html)。以下是本项目提供的Docker镜像：

- [duan2001/docker-stacks-foundation](https://hub.docker.com/r/duan2001/docker-stacks-foundation)：基础镜像，不包含Jupyter。
- [duan2001/base-notebook](https://hub.docker.com/r/duan2001/base-notebook)：添加了基础Jupyter应用程序。
- [duan2001/minimal-notebook](https://hub.docker.com/r/duan2001/minimal-notebook)：添加了常用命令行工具。
- [duan2001/r-notebook](https://hub.docker.com/r/duan2001/r-notebook)：包含R语言的流行软件包。
- [duan2001/julia-notebook](https://hub.docker.com/r/duan2001/julia-notebook)：包含Julia语言的流行软件包。
- [duan2001/scipy-notebook](https://hub.docker.com/r/duan2001/scipy-notebook)：包含科学计算的流行软件包。
- [duan2001/tensorflow-notebook](https://hub.docker.com/r/duan2001/tensorflow-notebook)：包含TensorFlow深度学习库。
- [duan2001/pytorch-notebook](https://hub.docker.com/r/duan2001/pytorch-notebook)：包含PyTorch深度学习库。
- [duan2001/datascience-notebook](https://hub.docker.com/r/duan2001/datascience-notebook)：包含来自Python、R和Julia社区的数据分析库。
- [duan2001/npl-notebook](https://hub.docker.com/r/duan2001/npl-notebook)：包含以上所有内容和其他深度学习相关的库。
- [duan2001/pyspark-notebook](https://hub.docker.com/r/duan2001/pyspark-notebook)：包含Apache Spark。
- [duan2001/all-spark-notebook](https://hub.docker.com/r/duan2001/all-spark-notebook)：包含Apache Spark和R语言支持。

### 使用示例

```bash
# 临时使用
docker run --gpus all --ipc=host -it --rm -p 10000:8888 -v "${PWD}":/home/duan/work duan2001/npl-notebook
# 查看登录token
jupyter server list

# 后台运行
docker run --gpus all -d --shm-size="8g" -p <开放的端口>:8888 --name=jupyter --restart=unless-stopped -v <外部存储路径>:/home/duan/work -e GRANT_SUDO=yes --user root duan2001/npl-notebook
# 查看登录token
docker exec jupyter jupyter server list
```

如需指定某几个GPU请参考[文档](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/docker-specialized.html)。
另外--ipc=host参数可能存在安全隐患，建议对外开放时使用--shm-size="8g"(数字为共享内存大小)。

## 其他信息

请参考原始项目的[官方说明](https://github.com/jupyter/docker-stacks/blob/main/README.md)。如果您已经安装了Docker，知道您想使用哪个Docker镜像，并且想在容器中启动单个Jupyter应用程序，下面的例子可以帮助您开始。

[Jupyter Docker Stacks 用户指南](https://jupyter-docker-stacks.readthedocs.io/en/latest/)详细描述了其他用法和特性。

## Resources

- [Documentation on ReadTheDocs](https://jupyter-docker-stacks.readthedocs.io/en/latest/)
- [Issue Tracker on GitHub](https://github.com/jupyter/docker-stacks/issues)
- [Jupyter Discourse Forum](https://discourse.jupyter.org/)
- [Jupyter Website](https://jupyter.org)
- [Images on Quay.io](https://quay.io/organization/jupyter)


## Contributing

Please see the [Contributor Guide on ReadTheDocs](https://jupyter-docker-stacks.readthedocs.io/en/latest/)
for information about how to contribute recipes, features, tests, and community-maintained stacks.

## Alternatives

- [jupyter/repo2docker](https://github.com/jupyterhub/repo2docker) -
  Turn git repositories into Jupyter-enabled Docker Images
- [openshift/source-to-image](https://github.com/openshift/source-to-image) -
  A tool for building artifacts from source code and injecting them into docker images
- [jupyter-on-openshift/jupyter-notebooks](https://github.com/jupyter-on-openshift/jupyter-notebooks) -
  OpenShift compatible S2I builder for basic notebook images
