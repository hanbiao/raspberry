# how to enter startX #

[page link](https://www.zhihu.com/question/22556729)

树莓派通过SSH登录，无法运行“startx”命令进入系统。

想进入系统，首先切换到root用户，输入“startx”命令时却出现下图的提示 ![img](https://pic3.zhimg.com/50/0f289f19b8dac16f981692473611d49b_hd.jpg) 

ssh 本质上 就算是控制台，只有字符，不支持任何图像 ，所以运行图像处理脚本不能显示出图像，而是报 segment fault 错误。。

Putty只支持命令行.你可以下个软件xrdp然后用windows自带的远程登录工具

1. 在Win10系统下使用“WIN+R”组合快捷键打开运行对话框，然后输入“mstsc" 打开远程连接
2. 输入树莓派的局域网地址
3. 输入树莓派的用户名和登陆密码
4. 进入到树莓派的LXDE
5. 树莓派默认的图片浏览工具 gpicview--支持BMP格式
6. 运行图像处理脚本可以显示处理后的图像

