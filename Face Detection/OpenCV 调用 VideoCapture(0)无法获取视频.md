**OpenCV 调用 VideoCapture(0)无法获取视频**

VideoCapture()：参数0表示打开默认摄像头，但是返回是false

> 原因：
>
> [Page Link](https://blog.csdn.net/deiki/article/details/71123947)
>
> 因为树莓派中的camera module是放在/boot/目录中以固件形式加载的，不是一个标准的V4L2的摄像头驱动，所以加载起来之后会找不到/dev/video0的设备节点 
>
> 在/etc/modules里面添加一行bcm2835-v4l2（小写的L）就能解决问题 

```
sudo nano /etc/modules  
 	add bcm2835-v4l2  
 reboot
```

