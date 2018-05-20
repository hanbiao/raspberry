**How to Use Pi-Cam**

按照以下步骤来将树莓派摄像头模块连接搭配树莓派：

1. 找到 CSI 接口(CSI接口在以太网接口旁边)，拉起 CSI 接口挡板。

2. 拿起你的摄像头模块，将贴在镜头上的塑料保护膜撕掉。确保黄色部分的PCB(有字的一面)是安装完美的（可以轻轻按一下黄色的部分来保证安装完美）。

3. 将排线插入CSI接口。记住，有蓝色胶带的一面应该面向以太网接口方向。同样，这时也确认一下排线安装好了之后，将挡板拉下。

   ![img](https://dn-linuxcn.qbox.me/data/attachment/album/201408/21/130426pxvuxrqtnpppxx17.jpg) 

在安装完摄像头模块之后，你将会使用三个应用程序来访问这个模块：raspistill, raspiyuv 和raspivid。其中前两个应用用来捕捉图像，第三个应用来捕捉视频。raspistill 工具生成标准的图片文件，例如 .jpg 图像，而 raspiyuv 可以通过摄像头生成未处理的 raw 图像文件。 

```
//更新固件
$ sudo apt-get update
$ sudo apt-get upgrade 
//配置摄像头
$ sudo raspi-config 
	enable camera
//拍照测试
$ raspistill -o test.jpg -t 2000 
//视频测试
$ raspivid -o test.h264 -t 10000 -w 1280 -h 720
```

raspivid 的输出是一段未压缩的 H.264 视频流，为了能被通常的视频播放器所播放，这个 raw 的 H.264 视频还需要转换。可以使用 gpac 包中所带有的 MP4Box 应用 

```
$ sudo apt-get install -y gpac 
$ MP4Box -fps 30 -add test.h264 test.mp4
```

安装 omxplayer ，这是一个命令行的播放器 

```
sudo apt-get install omxplayer
omxplayer -o hdmi /path/to/filename.mp4  //通过HDMI输出
```

