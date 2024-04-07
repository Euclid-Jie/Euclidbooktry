以下内容适用于windows系统下的docker使用

## 安装docker desktop

安装这个[软件](https://www.docker.com/products/docker-hub/)，相当于在WSL中安装了一个docker虚拟机，所以要先开启虚拟化，跟着[Windows 10/11 · Docker -- 从入门到实践教程](https://docker-practice.github.io/zh-cn/install/windows.html)走就行

## 使用docker

一般在 GitHub 上的项目，如果其支持docker的话，作者都会很友好的叫你运行一行代码，兼顾拉docker + 运行，但我自己一般在 docker hub官网上直接搜索想要的镜像，然后按照说明文档进行部署

### Images

下载的镜像都会在这，我理解的是，这就类似于执行 git clone 后，文件被拉到了本地

![image-20240323233757720](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202403232337857.png)

### Containers

在我粗浅的认识里，基于每个image，都会生产一个虚拟机，可以理解为单独的Linux系统，然后这个系统会按照docker作者的配置进行配置，然后运行一些东西，由于 docker直接从系统开始配置，所以保证了在任何机器上都能成功运行，而Containers就是运行的一个个的虚拟机

![image-20240323234034283](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202403232340444.png)

## Docker List

这里放一些自己用到过的Docker, 并记录配置使用过程，方便日后捡起来

### Click House

[Click House 使用](ClickHouse.md)

windows不能安装 click house，故使用 docker 的方式解决，只需要开放两个端口（关于为什么是两个，不甚清楚，只是知道比较特殊）

- 地址: [bitnami/clickhouse - Docker Image | Docker Hub](https://hub.docker.com/r/bitnami/clickhouse)

- pull: `docker pull bitnami/clickhouse`

- run: 如图所示，设置两个端口和密码即可，特殊的点是，默认用户为 `default`

  ![image-20240323234824827](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202403232348902.png)