#### 如何通过SFTP远程下载/上传文件到树莓派

只要不特意禁止，SSH都会附带SFTP——安全FTP功能，用来做和FTP类似的，上传/下载/管理文件的操作



很多FTP软件就“顺便”支持SFTP， 推荐FileZilla。理由和PuTTY用汉化版一样——无需设置直接UTF-8编码，中文名文件上传树莓派不乱码。



只需在“快速连接”中输入：

主机：sftp://192.168.1.102 （换成您的树莓派的IP地址。前面的sftp://一定要加）

用户名和密码照实填。（Raspbian默认是pi/raspberry）



出现问题：可以用ftp协议连接pi，但无法用sftp协议连接，表现为连接超时。
原因：树莓派SSH默认开启反向解析DNS功能，遍历DNS服务器查域名费时，导致FileZilla连接超时
解决：关闭反向解析DNS。sudo nano /etc/ssh/sshd_config  ->  在文件最后添加：UseDNS=no  ->   保存退出  ->   重启ssh服务：sudo service ssh restart


参考链接

<https://shumeipai.nxez.com/2013/09/07/use-the-remote-sftp-file-transfer-raspberry-pi.html>

<https://blog.csdn.net/oldwangold/article/details/95187821>