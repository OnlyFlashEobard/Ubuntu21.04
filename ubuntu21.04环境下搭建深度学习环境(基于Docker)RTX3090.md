<h1>Ubuntu21.04环境下搭建深度学习环境(基于Docker)RTX3090</h1>

<h2>1.安装docker
</h2>

安装过程参考官网https://docs.docker.com/install/linux/docker-ce/ubuntu/，注：这里安装的Docker是docker-ce采用基于仓库的方式安装。

1.设置仓库

​	更新软件源

```sudo apt-get update```

​	安装相关包允许apt通过https协议使用仓库

```sudo apt-get install \
   sudo apt-transport-https \
   ca-certificates \
   curl \
   gnupg-agent \
   software-properties-common
```

​		在这报错![](https://gitee.com/liuliuaobidao/github-graph/raw/master/image-20210707102045883.png)

解决方法：

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys +上面报错的密钥(我的是7EA0A9C3F273FCD8)
```

![image-20210707102132331](https://gitee.com/liuliuaobidao/github-graph/raw/master/image-20210707102132331.png)

解决成功

​	添加Docker官方的GPS密钥

```curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun```

​		报错找不到有效的OpenPGP 数据

​		解决方法：

```bash
wget https://download.docker.com/linux/ubuntu/gpg
sudo apt-key add gpg
```

<h3>2.验证是否安装成功</h3>

```docker --version```

由于每次使用docker需用root权限很麻烦，为了解决这个问题，需要将当前用户加入docker用户组

```bash
sudo groupadd docker
sudo gpasswd -a ${USER} docker
sudo service docker restart
```

并使用指令查看当前用户能否操作用户组

```bash
docker ps
```

![image-20210707103402994](https://gitee.com/liuliuaobidao/github-graph/raw/master/image-20210707103402994.png)

出现以上内容表示添加成功

使用docker打印hello-world

```sudo docker run hello-world```

![](https://gitee.com/liuliuaobidao/github-graph/raw/master/image-20210707103522179.png)

<h2>安装deepo

使用网易源下载deepo

```docker pull hub-mirror.c.163.com/ufoym/deepo```

使用官方源下载

```
docker pull ufoym/deepo
```

等待下载

![image-20210707104059307](https://gitee.com/liuliuaobidao/github-graph/raw/master/image-20210707104043547.png)

安装好镜像，创建镜像：

![image-20210707115416087](https://gitee.com/liuliuaobidao/github-graph/raw/master/image-20210707115416087.png)

docker run -it -p [端口号]:22 -p [端口号]:3389 --ipc=host -v /home/[name]/:/[name] --name [容器名字] ufoym/deepo:all-jupyter

