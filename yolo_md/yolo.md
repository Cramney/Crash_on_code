0、环境配置：

配置全局变量Path:方便终端可以调用python和conda

1、标注

下载X-anylabeling，然后左上角打开待标注文件夹，一般使用方框（快捷键R）标注，两次点击标注后写入标签
完成标注后，点击Export的第一项，然后选择class的.txt文件，txt文件内容为标签名（单个名后隔空行）
然后再同文件夹下会输出一个labels文件夹，里面为frame_xxxx样式的txt文件，文件内容为标记的坐标
举行坐标为（x1，y1，x2，y2），是左上角和右下角总计两点的坐标

2、训练

总体概述：首先我们是利用yolov8的预训练模型基础上，进行标注测试集的再训练，从而实现模型的定制，达成利用yolov8达成办公室的人脸检测
训练的py文件：train_detect_foot.py：
首先加载训练好的模型，从官网上拉取的yolo11s
然后测试模型的代码部分，data=foot.yaml，yaml是数据集配置文件路径，再设置epochs（训练轮数），imgsz（图片尺寸），batch（批量大小），device（使用GPU或CPU）

3、测试

使用val.py进行测试，输出mAP50指标，代码fork自https://zhuanlan.zhihu.com/p/1892875667449823836

在训练完成之后，会生成一个runs的文件夹，进入runs/train/weights，其中两个.pt文件就是训练所得的权重模型，其中best是效果最好的一次，last是最后一次，一般选取last
然后在.yaml配置文件里设置train训练集，val验证集，进行结果验证，最后会生成val3的效果图，各种参数表明了数据和模型的效果和优良程度。



！！！！
