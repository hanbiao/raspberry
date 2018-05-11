**How to operate DS18B20**

[link](http://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/temperature/)

1. Once a user is logged on to the Pi, type these commands into a terminal, or just at the prompt given upon login and before typing "startx": 

   ```
   sudo modprobe w1-gpio	//向内核注册模块
   sudo modprobe w1-therm	
   cd /sys/bus/w1/devices/
   ls
   ```

2. The entry on the screen that is mostly numbers is the serial number of the sensor. The sensor used for this tutorial has the serial number "10-000802824e58". 

   ```
   cd 10-000802824e58
   cat w1_slave
   ```

3. Two lines of text will be printed. On the second line, the section starting "t=" is the temperature in degrees Celsius. A decimal point goes after the first two digits 

   ```
   pi@raspberry:/sys/bus/w1/devices $ ls
   28-0315b233b1ff  w1_bus_master1
   pi@raspberry:/sys/bus/w1/devices $ cd 28-0315b233b1ff
   pi@raspberry:/sys/bus/w1/devices/28-0315b233b1ff $ cat w1_slave
   67 01 4b 46 7f ff 0c 10 c4 : crc=c4 YES
   67 01 4b 46 7f ff 0c 10 c4 t=22437
   pi@raspberry:/sys/bus/w1/devices/28-0315b233b1ff $
   
   ```

   

***遇到的问题***

找不到设备号  或者  显示的设备号是 00-

[how to slave](http://shumeipai.nxez.com/2013/10/03/raspberry-pi-temperature-sensor-monitors.html)

> 修改配置
>
> ```
> sudo nano /boot/config.txt
> ```
>
> 在最后一行手动添加这个，保存并重启树莓派 
>
> ```
> dtoverlay=w1-gpio-pullup,gpiopin=4   //如果加了外部上拉电阻，可以去掉 -pullup
> ```



**配置说明**

效果等同于在raspi-config中enable 1-wire接口

可以参看 /boot/overlay/README 查看所有的模块说明

在/boot/overlay 找到所有的配置模块

