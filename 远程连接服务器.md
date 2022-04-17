1、ping 192.168.192.1 

ssh lcx@192.168.192.1

password 123456

后面再用的话，直接ssh就行.

2、ssh nuo@172.25.6.99

password 123456

服务器记得添加防火墙，并添加端口规则（入站规则）

3、远程服务器安装miniconda

[(12条消息) Miniconda在服务器上的安装与使用_FiOQA的博客-CSDN博客_服务器安装miniconda](https://blog.csdn.net/weixin_46005813/article/details/120622098)

亲测，请放心食用，一步步按教程来。

运行文件一定要cd到文件路径，切忌。

4、在使用conda命令安装包的时候如果报错这个

![image-20220409165143204](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20220409165143204.png)

就检查网络有没有连接，尝试命令ping 8.8.8.8如果没有显示，就是没有连接成功。

在官网下载个linux的curl 包，下载完毕后，找到该文件夹目录，右击用git bash上传过去

```git bash
scp filename username@xxx.xxx.xxx.xxx:dest_dir
```

如果上传文件夹就用：

```git bush
scp -r filename username@xxx.xxx.xxx.xxx:dest_dir
```

传上去之后，cd到该文件夹,运行

```
curl -s "http://10.0.1.5/login?DDDDD=1803304004&upass=160108&0MKKey=1"
```

如果返回一个html格式的输出就说明登录成功了，

如果不成功把这个传上去 [curl-amd64](C:\Users\17675\Documents\curl-amd64) 后，cd到该文件的地方，给它执行权限：

```
chmod 777 curl-amd64
```

然后运行：

```
./curl-amd64 -s "http://10.0.1.5/login?DDDDD=1803304004&upass=160108&0MKKey=1"
```

到此应该成功返回html 格式的输出了，ping 8.8.8.8 成功，连接成功。

5、如果下载包还报错，把./condrac里面的内容全删了,再把所有添加的镜像源全删了：linux下打开文件用命令：

```
sudo nano ./condrac
```

删除镜像源操作：

```
conda config --remove-key channels
```

应该就可以安装各种包了。

二、pycharm连接远程服务器。

只有专业版的pycharm才能设置远程连接，免费的专业版要通过校园邮箱申请。

[(12条消息) pycharm远程连接服务器完整教程_hehedadaq的博客-CSDN博客_pycharm连接服务器](https://blog.csdn.net/hehedadaq/article/details/118737855)

##### 按照这个来。

第三步设置远程服务器解释器的时候，configuration选择上一步已经拥有的，即  Existing server configuration，点击下划线提示即可.

注意添加解释器的路径的时候，到指定环境里：

```
python
import sys
sys.executable
```

查看解释器路径在哪里。不要随意添加

![image-20220409204217907](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20220409204217907.png)

如果连接失败，把下面Execute去掉。

三、安装nvidia驱动

[(12条消息) Ubuntu20.04安装nvidia显卡驱动——超详细_道阻且长！的博客-CSDN博客_ubuntu安装nvidia驱动](https://blog.csdn.net/Perfect886/article/details/119109380)

注：

1、打开文件夹命令

```
sudo gedit /etc/modprobe.d/blacklist.conf 或者(blacklist-nouveau.conf)
```

若报错，将gedit 改成nano,经历了很多，发现只要是打开文件，只有nano才能成功。why?

2、

```
sudo update-initramfs –u
```

命令若报错，进行

```
conda clean -i
```

之后再尝试，成功后

3、重启系统

```
reboot
```

重启系统，若报错: 权限不够

```
sudo reboot
```

4、等待系统重启后，在终端输入如下，没有输出则表示屏蔽成功

```
lsmod | grep nouveau
```

5、按照步骤走，切记更新软件列表和安装必要工具

6、

```
sudo telinit 3
cd 指定路径
sudo chmod 777 NVIDIAxxx.run
sudo ./NVIDIAxxx.run --no-opengl-files
```

若安装不成功，看下面两个报错

[(13条消息) ubuntu安装英伟达显卡驱动报错_yingqubaifumei的博客-CSDN博客](https://blog.csdn.net/yingqubaifumei/article/details/105753059)

[没有可用的软件包 build-essential，但是它被其他的软件包引用了【解决方法】 - 鲸小鱼|相信所以选择 - 博客园 (cnblogs.com)](https://www.cnblogs.com/lixuejian/p/11926011.html)

