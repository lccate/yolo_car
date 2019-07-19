# 1 yolo训练自己的数据集实现对汽车的识别
实验环境（ubuntu+cpu）  
## 1 ubuntu与windows双系统安装  
windows下也可以运行，但是配置环境比较麻烦，建议使用linux系统  
[笔记本参考网址：](https://morvanzhou.github.io/tutorials/others/linux-basic/1-2-install/)  
[台式机参考网址（经过试验，台式机安装时可能会出现内存分区的问题）：](https://blog.csdn.net/jiajinrang93/article/details/63892208)  
## 2 使用已经训练好的yolo模型
打开终端，下载官网的yolov3：  
```
git clone https://github.com/pjreddie/darknet
```
会提示git命令不存在，按照提示安装即可  
然后打开darknet：  
```
cd darknet
```
```
make
```
make时会出现要安装命令的提示，按提示操作，可能出现的问题：  
```
make: gcc: Command not found
Makefile:85: recipe for target 'obj/gemm.o' failed

make: *** [obj/gemm.o] Error 127
```
解决方法：  
```
sudo apt-get install build-essential
```
下载weights文件：  
```
wget https://pjreddie.com/media/files/yolov3.weights
```
运行检测器：  
```
sudo ./darknet detect cfg/yolov3.cfg yolov3.weights data/doa.jpg
```
## 3 使用yolo来训练自己的数据集
针对车辆检测，要训练自己的数据集存在的几个问题：  
（1）数据集的获取：要获取十字路口车辆运行场景下的大量视频或图片  
（2）数据集的标注：非常麻烦，考虑到十字路口的复杂场景，每张图片的标注可能需要5分钟左右  
（3）训练：对设备要求较高，如果在普通电脑上训练模型可能需要十几天  
（4）用自己的数据集训练后也不一定能达到原来的模型的效果  
目前只是测试阶段，暂不考虑上述问题，尽量使用已经训练好的yolo模型  
# 2 解决连续帧之间车辆重复计数问题
人为标定基准线，通过此线的车辆计数一次，因此需要求出车辆的运行轨迹，将运行轨迹绘制的线与认为标定线相交，根据交点来进行计数  
# 3 解决多目标轨迹跟踪的问题

