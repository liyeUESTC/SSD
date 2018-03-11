# readme  训练笔记

## 目标检测方法性能对比

 ![性能对比](https://github.com/liyeUESTC/SSD/blob/ssd/train/%E7%9B%AE%E6%A0%87%E6%A3%80%E6%B5%8B%E6%96%B9%E6%B3%95%E6%80%A7%E8%83%BD%E5%AF%B9%E6%AF%94.png)

 ![方法对比](https://github.com/liyeUESTC/SSD/blob/ssd/train/%E8%AF%A6%E7%BB%86%E5%AF%B9%E6%AF%94%E5%9B%BE.png)

## 数据准备
（1）SSD利用VOC07和VOC12对模型进行训练

（2）VOC07和VOC12数据介绍

  [VOC数据集介绍](http://blog.csdn.net/zhangjunbob/article/details/52769381).

（3）训练数据处理

** 遵循一定挑选机制，先挑选正样本，按照正负样本1：3的比例，继而挑选负样本**

 ![正负样本筛选](https://github.com/liyeUESTC/SSD/blob/ssd/train/%E6%AD%A3%E8%B4%9F%E6%A0%B7%E6%9C%AC%E7%AD%9B%E9%80%89.jpg)

+ 正样本获取

1. 针对每一个ground truth box找到距离它最近的default box作为正样本。

2. 计算每个default box和ground truth box的IOU，挑选IOU > 0.5的default box作为正样本。

3. 分别计算


+ 负样本获取



（4）处理结果


## 模型

+ SSD网络结构在VGG16网络结构的基础上进行修改。最终的网络结构为：con1-1 -> conv1-2 -> conv2-1 -> conv2-2 -> conv3-1 -> conv3-2 -> conv3-3
-> conv4-1 -> conv4-2 -> conv4-3 -> conv5-1 -> conv5-2 -> conv5-3(512) -> conv6 -> conv7 -> conv6-1 -> conv6-2 -> conv7-1 -> conv7-2
-> conv8-1 -> conv8-2 -> conv9-1 -> conv9-2  

![标准网络结构](https://github.com/liyeUESTC/SSD/blob/ssd/train/%E6%A0%87%E5%87%86%E7%BD%91%E7%BB%9C%E6%A8%A1%E5%9E%8B.png)

![模型结构图](https://github.com/liyeUESTC/SSD/blob/ssd/train/%E6%A8%A1%E5%9E%8B%E7%BB%93%E6%9E%84.png)


## 测试阶段

以下将结合理论讲解、实例图解来说明ssd在目标检测测试阶段的流程。

（1）提取特征

输入一张图片，利用卷积提取特征，在提取特征过程中分别对6个输出结果进行目标检测，conv4_3（4）、fc7（6）、
conv6-2（6）、conv7-2（6）、conv8-2（4）以及conv9-2（4）。如图figure1所示。

 ![目标检测整体框架](https://github.com/liyeUESTC/SSD/blob/ssd/train/QQ%E6%88%AA%E5%9B%BE20180307222337.jpg)

（2）特征图目标检测  以大小为5 * 5 * 256的特征图进行讲解

- default box generator生成default box

特征图为5*5，每个像素点选取3个不同尺度的default box，所以一共选取75个default box

- conv操作确定location

每个default box对应1个4维的location矫正值（左上角和右下角坐标值），每个像素点有3个default box，所以每个像素点对应12个location矫正值。因此选取12个filter，生成特征图的大小为5 * 5 * 12，深度信息12分别代表3个default box的矫正值。

- conv操作确定confidence

confidence是对应分类的置信度。考虑到要分20类物体和1类背景类，共21类，每个default box对应1个21维的confidence，每个像素点对应3个default box，所以选取63个filter，生成特征图的大小为5 * 5 * 63，深度信息63分别代表3个default box对应21个类别的置信度。

 ![目标检测整体框架](https://github.com/liyeUESTC/SSD/blob/ssd/train/QQ%E6%88%AA%E5%9B%BE20180307222301.jpg)

（3）多特征图目标合并及筛选

在每张特征图中，根据confidence筛选default box，小于设定阈值的default box被舍弃，通过计算IOU，合并default box。不同特征图中的default box利用fase NMS计算IOU后进行合并。

 ![目标检测整体框架](https://github.com/liyeUESTC/SSD/blob/ssd/train/QQ%E6%88%AA%E5%9B%BE20180307222244.jpg)

（4）输出最终目标 

输出保留的default box，并结合location信息，确定目标的具体位置。

 ![目标检测整体框架](https://github.com/liyeUESTC/SSD/blob/ssd/train/QQ%E6%88%AA%E5%9B%BE20180307222220.jpg)
 
  [检测阶段参考资料ppt](https://docs.google.com/presentation/d/1rtfeV_VmdGdZD5ObVVpPDPIODSDxKnFSU0bsN_rgZXc/pub?start=false&loop=false&delayms=3000&slide=id.g179f601b72_0_106).
  
  [网络结构、正负样本选取、loss函数定义参考资料](https://www.cnblogs.com/xuanyuyt/p/7447111.html).

