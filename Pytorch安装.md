## pytorch安装全流程

最近做项目需要安装一下pytorch，记录一下全流程

1、安装miniconda

2、添加清华镜像源：

方法一：

```
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/peterjc123/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
conda config --set show_channel_urls true
```

方法二：（1）在C:\Users\17675目录下创建  .condarc记事本，然后加入：

	channels:
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/peterjc123/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
	-http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
	show_channel_urls: true

3、创建虚拟环境

 	1）打开miniconda prompt 进入普通的base环境

​	输入：conda create -n pytorch python=3.7（-n后面跟的是新建环境的名字）并指定python的版本

​	后面一直打y (yes)就行了

​	进入命令行模式

1. conda info -e （查看所有的虚拟环境）
2. conda activate -name(虚拟环境名字)（进入到该虚拟环境中）

​	[史上最成功安装Pytorch快速方法【亲测绝对有效，很好用很好用】 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1837355)

4、安装pytorch

进入官网，找到合适的pytorch版本。

在命令行中输入相应命令





下载各种包时，若镜像源不能用，尝试后面加上 trusted

1、下载pillow（使用numpy）
	pip install pillow -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com

2、下载matplotlib
	pip install matplotlib -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

3、下载opencv-python
	pip install opencv-python -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
	(trusted-host pypi.douban.com表示将指定网站设置为信任服务器)







