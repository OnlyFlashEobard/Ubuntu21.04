<h1>
    ubuntu21.04安装RTX3090显卡驱动
</h1>


<h2>1.首先去英伟达官网下载驱动</h2>

官网链接：https://www.nvidia.cn/

右上角驱动程序搜索自己的显卡驱动

![image-20210707093817393](/home/gait/.config/Typora/typora-user-images/image-20210707093817393.png)



下载好显卡驱动后在文件/下载中找到.run文件

![image-20210707094442896](/home/gait/.config/Typora/typora-user-images/image-20210707094442896.png)

<h2>2.安装Nvidia驱动
</h2>


​	(1)屏蔽noueau驱动

​		ubuntu系统集成的显卡驱动程序是nouveau，是第三方为Nvidia开发的开源驱动，我们需要先将其屏蔽才能安装GPU驱动。

​		1)将驱动加入blasklist.conf黑名单中

```sudo gedit /etc/modprobe.d/blacklist.conf```

​		2)在最后一行加入下面的所有语句并保存退出

```
blacklist vga16fb
blacklist nouveau
blacklist rivafb
blacklist rivatv
blacklist nvidiafb
```

​		3)更新文件

```
sudo update-initramfs -u
```

(2)安装驱动		



​		返回.run文件夹下，右键打开终端输入以下命令

```
sudo chmod a+x NVIDIA-Linux-x86_64-xxx.run　　　　　　　　 //修改权限
sudo ./NVIDIA-Linux-x86_64-xxx.run -no-x-check -no-nouveau-check -no-opengl-files   //执行安装
```

在初次安装过程中会出现的错误：

1.

![image-20210707100439652](/home/gait/.config/Typora/typora-user-images/image-20210707100439652.png)

解决方法：

安装GCC

```sudo apt-get update
 sudo apt-get update
 sudo apt-get install gcc
```

2.

![image-20210707100550842](/home/gait/.config/Typora/typora-user-images/image-20210707100550842.png)

解决方法：

安装make

```sudo apt-get update
sudo apt-get update
apt-get install make
```

解决这两个可能出现的错误后再次安装.run文件：

```
sudo ./NVIDIA-Linux-x86_64-xxx.run -no-x-check -no-nouveau-check -no-opengl-files 
```



<h2>3.验证安装
</h2>

```nvidia-smi```

出现显卡信息证明安装成功

![image-20210707100915422](/home/gait/.config/Typora/typora-user-images/image-20210707100915422.png)
