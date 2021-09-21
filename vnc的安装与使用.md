# VNC的安装与使用（centos7）

1、在服务端下载vncserver。

```
1、进入root用户下载vncserver
yum install -y tigervnc-server
```

![image-20210728224201753](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728224201753.png)

2、退出root用户设置vnc密码

```
vncpasswd
```

![image-20210726220316060](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210726220316060.png)

3、vnc的配置

1）切换root用户

```
sudo su
```

![image-20210726220637842](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210726220637842.png)

2）拷贝配置文件到指定目录下

```
cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service
```

3）修改该配置文件

```
/etc/systemd/system/vncserver@:1.service
```

4）vim打开此配置文件将里面参数<user>替换成要登陆的用户

```
vim /etc/systemd/system/vncserver@:1.service
```

![168be24a2ce5278a1e16935f4b19566](C:\Users\wpc\Desktop\168be24a2ce5278a1e16935f4b19566.png)

![image-20210728224807278](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728224807278.png)

5）加载配置

```
systemctl daemon-reload
```

6）开启服务

```
systemctl start vncserver@:1.server
```

7)设置开机服务自启

```
systemctl enable vncserver@:1.service
```

![image-20210728225007466](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728225007466.png)

8）开放端口5901，vnc默认端口从5901开始。

```
firewall-cmd --add-port=5901/tcp
```

![image-20210728225159325](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728225159325.png)9)保存端口设置，保证以后开机不需要重复设置

```
firewall-cmd --add-port=5901/tcp --permanent
```

![image-20210728225314455](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728225314455.png)

10)重新加载防火墙设置

```
firewall-cmd --reload
```

![image-20210728225346155](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728225346155.png)

11)查看vnc端口状态

```
vncserver -list
```

![image-20210728225540406](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728225540406.png)

12）开启一个vnc服务，并设置分辨率

```
vncserver -geometry 1920x1080
```

![image-20210728230033921](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230033921.png)

13）使用vnc -list查看设置好的端口

![image-20210728230111253](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230111253.png)

14）在windows端（客户端）下载一个vnc viewer

![image-20210728230224706](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230224706.png)

15）点击File->New connection

![image-20210728230348590](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230348590.png)

16）输入ip和连接名字点击确定

![image-20210728230551191](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230551191.png)

17）右击选择Connect

![image-20210728230700851](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230700851.png)

18）输入vncserver密码点击确定

![image-20210728230806334](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230806334.png)

19）登录成功

![image-20210728230833247](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728230833247.png)

20）如果想配置多用户同时访问，需要将上面`vncserver@:1.service`，改为`vncserver@:2.service`，然后配置其中用户名、分辨率参数，按照骤走一遍就可以了。

