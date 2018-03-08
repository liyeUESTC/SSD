# readme  训练笔记

## 数据准备
（1）SSD利用VOC07和VOC12对模型进行训练

（2）VOC07和VOC12数据介绍

  [VOC数据集介绍](http://blog.csdn.net/zhangjunbob/article/details/52769381).

（3）训练数据处理


（4）处理结果


## 模型



## 测试阶段

以下将结合理论讲解、实例图解来说明ssd在目标检测测试阶段的流程。

（1）提取特征

输入一张图片，利用卷积提取特征，在提取特征过程中分别对6个输出结果进行目标检测，VGG-16（conv4_3）、fc7、
conv、conv、conv以及conv。如图figure1所示。

（2）特征图目标检测  以大小为5 * 5 * 256的特征图进行讲解

- default box generator生成default box

特征图为5*5，每个像素点选取3个不同尺度的default box，所以一共选取75个default box

- conv操作确定location

每个default box对应1个4维的location矫正值（左上角和右下角坐标值），每个像素点有3个default box，所以每个像素点对应12个location矫正值。因此选取12个filter，生成特征图的大小为5 * 5 * 12，深度信息12分别代表3个default box的矫正值。

- conv操作确定confidence

confidence是对应分类的置信度。考虑到要分20类物体和1类背景类，共21类，每个default box对应1个21维的confidence，每个像素点对应3个default box，所以选取63个filter，生成特征图的大小为5 * 5 * 63，深度信息63分别代表3个default box对应21个类别的置信度。

（3）多特征图目标合并及筛选

在每张特征图中，根据confidence筛选default box，小于设定阈值的default box被舍弃，通过计算IOU，合并default box。不同特征图中的default box利用fase NMS计算IOU后进行合并。

（4）输出最终目标 

输出保留的default box，并结合location信息，确定目标的具体位置。

 ![目标检测整体框架](https://github.com/liyeUESTC/SSD/blob/ssd/train/QQ%E6%88%AA%E5%9B%BE20180307222220.jpg)
 
  [参考资料ppt](https://docs.google.com/presentation/d/1rtfeV_VmdGdZD5ObVVpPDPIODSDxKnFSU0bsN_rgZXc/pub?start=false&loop=false&delayms=3000&slide=id.g179f601b72_0_106).

