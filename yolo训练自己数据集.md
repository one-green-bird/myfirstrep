基于YOLO-V3训练自己的数据与任务：

(一)：数据打标签：

1、安装好labelme工具

pip install labelme

pip install pyqt5

pip install pillow=4.0.0

2、标注我们的数据

（二）写好模型所需的配置文件

1、进入到config中

右击选择git bush

2、bash create_custom_model.sh 2 （后面的数字表示你的任务的类别个数）

3、自动生成 yolo3_custom.cfg

(三）标签格式转换：

1、labelme---->x1,y1,x2,y2           YOLO-V3---->Cx,Cy,W,H 相对位置（取值范围0-1）

2、json2yolo.py用它来把标签转换成对的格式

（四）写好数据和标签的路经

转换好的输出路劲：data\custom\labels

json_floder_path:labelme 生成标签的文件夹

（五）完成其它配置操作

1、数据放到相应位置，注意名字和label的一致

2、classes.names 改成你任务里有的类别名字

3、在train.txt与val.txt中写好对应的路径

4、custom.data

(六)：训练代码更改

1.train.py需要设置的参数

--model_def config/yolov3-custom.cfg

--data-config config/custom,data

--pretrained_weights weights/darknet53.conv.74

 （七）预测操作

--image_folder data/samples/          #需要把预测的数据放到这里

--checkpoint_model checkpoints/yolov3_ckpt_100.pth         #训练好模型的路径

--class-path data/custom/classes.names          #画图时候要把框上显示出来 name

额外注意：create_custom_model.sh不能重复执行,要先把yolov3-custom.cfg删除掉才可以