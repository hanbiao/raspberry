**How to change Software download source**



由于树莓派软件官方源在国外，所以连接不稳定，且速度慢，所以安装初次进入系统后，一定要修改一下软件源

> 中国科学技术大学 Raspbian
>
> <http://mirrors.ustc.edu.cn/raspbian/raspbian/>
>
> 清华大学 Raspbian <http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/> 

```
sudo -s
echo -e "deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ jessie main non-free contrib \n deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ jessie main non-free contrib" > /etc/apt/sources.list
echo -e "deb http://mirrors.ustc.edu.cn/archive.raspberrypi.org/ jessie main" > /etc/apt/sources.list.d/raspi.list
exit
sudo apt-get update && sudo apt-get -y upgrade
```

使用管理员权限（经由sudo），编辑`/etc/apt/sources.list`文件 

```
$ sudo nano /etc/apt/sources.list
//用#注释掉原文件内容，用以下内容取代： 
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ jessie main contrib non-free rpi
deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ jessie main contrib non-free rpi
//更新
$ apt-get update && apt-get -y upgrade  
```



