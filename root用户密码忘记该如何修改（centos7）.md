# root用户密码忘记该如何修改（centos7）

1、重启系统，在开机过程中，快速按下键盘上的方向键↑和↓。目的是告知引导程序，我们需要在引导页面选择不同的操作，以便让引导程序暂停。 以下是暂停后的界面，可以查看下方的英文可知↑和↓的作用。 

![image-20210728233602688](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728233602688.png)

2、选择目的操作系统第一个按下键盘“e”，会出现如下界面。

![image-20210728233737141](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728233737141.png)

3、将光标一直移动到 LANG=en_US.UTF-8 后面，空格，再追加init=/bin/sh。这里特别注意，需要写在UTF-8后，保持在同一行，并注意空格。由于屏幕太小，会自动添加\换行，这个是正常的。

![7a2f016711a098fb4d07aa36b62c36d](C:\Users\wpc\Desktop\7a2f016711a098fb4d07aa36b62c36d.png)

4、按下CTRL+X进行引导启动，成功后进入下面的界面

![image-20210728234115140](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728234115140.png)

5、输入以下命令

1）挂载根目录 

```
mount -o remount, rw /
```

2）选择要修改密码的用户名，这里选择root用户进行修改，可以更换为你要修改的用户 

```
passwd root
```

3）输入2次一样的新密码，注意输入密码的时候屏幕上不会有字符出现。 

如果输入的密码太简单，会提示警告（BAD PASSWORD：The password fails the dictionary check - it is too simplistic/systematic），可以无视它，继续输入密码，不过建议还是设置比较复杂一些的密码，以保证安全性

4）如果已经开启了SElinux，则需要输入以下命令 

```
touch /.autorelabel
```

5）最后输入以下命令重启系统即可

```
exec /sbin/init 或
exec /sbin/reboot
```

![image-20210728234621422](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728234621422.png)

![image-20210728235809011](C:\Users\wpc\AppData\Roaming\Typora\typora-user-images\image-20210728235809011.png)
