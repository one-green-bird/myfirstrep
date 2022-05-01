# 神经网络的输出

输入层，隐藏层，输出层

![image-20211116210910082](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20211116210910082.png)

f(x)在这里表示激活函数；

# 神经网络的训练

![image-20211116211143663](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20211116211143663.png)



1、网络初始化

* 需要确定：偏置，权重，损失函数，激活函数(该函数的选取会影响到权值的更新效率)，学习速率
* 对于激活函数：例如Sigmiod函数，Tanh函数

2、隐藏层输出

3、输出层输出

4、误差的计算(用到损失函数)

5、权值的更新(链式求导法则)

6、偏置的更新

7、判断算法迭代是否结束(是否收敛)



# 矩阵的运算

1、一般把输入神经元作为行向量，然后每层的权重矩阵的行和列根据前后神经元的个数决定

2、正向传播numpy.dot(X,W)

# 各个变量的表示

1、X输入，Y输出真值，Wi第i层的权重矩阵，Bi第i层的偏置矩阵(用行向量表示)，学习率r

2、ipk第k层神经元的输入（行向量），opk第k层神经元的输出（行向量）

# 权重更新

公式：

​	损失函数求导*激活函数求导 @权重矩阵1转置 *激活函数求导@权重矩阵2转置 *输入向量(必须是列向量因为最后要扩展)

总之只有在遇到权重矩阵的时候才需要转置。



```python
 #利用更新好的隐藏层与输出层权重，计算输入层与隐藏层的误差
    W1=W1-lr*(op2-Y[i])*dsigmoid(ip2)@W2.T*dsigmoid(ip1)*X[i].T
    B1=B1-lr*(op2-Y[i])*dsigmoid(ip2)@W2.T*dsigmoid(ip1)
```

# 关于链式求导法则

1、对谁的偏导就只考虑该变量所在的因式，其它变量忽略不计

2、如果存在复合函数，直接将外函数求导

3、sigmoid(x)函数求导的结果就是sigmoid(x)*(1-sigmoid(x))



# numpy库

#### 开辟数组

* 一维：array[range(10)]
* 二维：array[[range(10),range(10)]]
* numpy.arange(a,b,c)  从 数字a起, 步长为c, 到b结束，生成array
* numpy.arange(a,b,c).reshape(m,n) ：将array的维度变为m 行 n列。

```python

```

## 索引 

* 二维a[1:2,3:4]，取多行很多列

#### random.seed(1)：

当seed()没有参数时，每次生成的随机数是不一样的，而当seed()有参数时，每次生成的随机数是一样的，同时选择不同的参数生成的随机数也不一样

#### numpy.random.rand(3,4)：

生成一个3行4列的随机矩阵

#### numpy.random.randint(1,20,(3,4))：

生成一个1到20之内的整数矩阵

#### numpy.dot(A,B):

矩阵相乘

#### reshape

![image-20211118130249702](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20211118130249702.png)

array[[1,2,3],

​			[1,2,3],

​			[1,2,3]]

对于array数组中的每一个[1,2,3]是一个数组,一般运算时要使用的是向量，所以使用a.reshape(1,-1)可以将它转换为向量

#### python中numpy模块下函数array()和mat()的区别

![image-20211120114151851](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20211120114151851.png)

Array.shape查看数组形状

Array,dtype查看数组元素类型







## Python图像库PIL(Python Image Library)是python的第三方图像处理库

#### 图像类Image class

Image类是PIL中的核心类，你有很多种方式来对它进行初始化，比如从文件中加载一张图像，处理其他形式的图像，或者是从头创造一张图像等。Image模块操作的基本方法都包含于此模块内。如**open**、**save**、**conver**、**show**…等方法。



#### open方法

img = Image.open(r'D:\picture\220.jpg')

print(img):查看图片的特征，属性，大小，格式等

img.show():展示图片



遍历读取图片

```python
for i in range(1,10):
	Image.open(r'D:\picture\data\seg_train\seg_train\buildings\{}.jpg'.format(str(i)))
```



