# readme  训练笔记

## 数据准备
（1）SSD利用VOC07和VOC12对模型进行训练

（2）VOC07和VOC12数据介绍

  [VOC数据集介绍](http://blog.csdn.net/zhangjunbob/article/details/52769381).

（3）训练数据处理


（4）处理结果


## 模型



## 测试阶段
以下讲结合理论讲解、实例图解来说明ssd在目标检测测试阶段的流程。
（1）提取特征。输入一张图片，经过卷积提取特征，在提取特征过程中分别对6个输出结果进行目标检测，VGG-16（conv4_3）、fc7、
conv、conv、conv以及conv。根据每张特征图像素点的个数，分别确定default box个数，根据default box个数、localization信息以及confidence信息确定filter个数，利用filter处理特征图，每个default box分别对应一个location（4维）和一个confidence（1维），结合default box对应原图位置、location对原图的矫正信息以及confidence置信度三方面考虑，最后给出框的位置以及框中是哪种物体的置信度。然后每张特征图都可以找到对应在原图中的位置，再根据location信息，确定default box的最终位置信息。
（2）
（3）
[参考资料]（https://docs.google.com/presentation/d/1rtfeV_VmdGdZD5ObVVpPDPIODSDxKnFSU0bsN_rgZXc/pub?start=false&loop=false&delayms=3000&slide=id.g179f601b72_0_106）.
