## cifar10（170M）
- CIFAR-10包含10个类别，50,000个训练图像，彩色图像大小：32x32，10,000个测试图像。
- CIFAR-100与CIFAR-10类似，包含100个类，每类有600张图片，其中500张用于训练，100张用于测试；这100个类分组成20个超类。
图像类别均有明确标注。CIFAR对于图像分类算法测试来说是一个非常不错的中小规模数据集。


## coco（40G）
COCO(Common Objects in Context)是一个新的图像识别、分割和图像语义数据集，它有如下特点：
- 1）Object segmentation
- 2）Recognition in Context
- 3）Multiple objects per image
- 4）More than 300,000 images
- 5）More than 2 Million instances
- 6）80 object categories
- 7）5 captions per image
- 8）Keypoints on 100,000 people
COCO数据集由微软赞助，其对于图像的标注信息不仅有类别、位置信息，还有对图像的语义文本描述，
COCO数据集的开源使得近两三年来图像分割语义理解取得了巨大的进展，
也几乎成为了图像语义理解算法性能评价的“标准”数据集

## ilsvrc12

## PASCAL VOC（2G）
PASCAL VOC挑战赛是视觉对象的分类识别和检测的一个基准测试，提供了检测算法和学习性能的标准图像注释数据集和标准的评估系统。
PASCAL VOC图片集包括20个目录：人类；动物（鸟、猫、牛、狗、马、羊）；
交通工具（飞机、自行车、船、公共汽车、小轿车、摩托车、火车）；
室内（瓶子、椅子、餐桌、盆栽植物、沙发、电视）。
PASCAL VOC挑战赛在2012年后便不再举办，但其数据集图像质量好，标注完备，非常适合用来测试算法性能。

## VOC0712

## mnist（12M）
- MNIST是一个手写数字数据库，它有60000个训练样本集和10000个测试样本集，每个样本图像的宽高为28*28。
- 此数据集是以二进制存储的，不能直接以图像格式查看。
- 目前主流深度学习框架都以mnist数据集作为入门教程。应用于最早的卷积网络LeNet。



## imagenet（1T）
- 
MNIST将初学者领进了深度学习领域，而Imagenet数据集对深度学习的浪潮起了巨大的推动作用。
深度学习领域大牛Hinton在2012年发表的论文《ImageNet Classification with Deep Convolutional Neural Networks》在计算机视觉领域带来了一场“革命”，此论文的工作正是基于Imagenet数据集。

Imagenet数据集有1400多万幅图片，涵盖2万多个类别；
其中有超过百万的图片有明确的类别标注和图像中物体位置的标注，具体信息如下：
- 1）Total number of non-empty synsets: 21841
- 2）Total number of images: 14,197,122
- 3）Number of images with bounding box annotations: 1,034,908
- 4）Number of synsets with SIFT features: 1000
- 5）Number of images with SIFT features: 1.2 million

Imagenet数据集是目前深度学习图像领域应用得非常多的一个领域，关于图像分类、定位、检测等研究工作大多基于此数据集展开。Imagenet数据集文档详细，有专门的团队维护，使用非常方便，在计算机视觉领域研究论文中应用非常广，几乎成为了目前深度学习图像领域算法性能检验的“标准”数据集。

与Imagenet数据集对应的有一个享誉全球的“ImageNet国际计算机视觉挑战赛(ILSVRC)”，以往一般是google、MSRA等大公司夺得冠军，今年（2016）ILSVRC2016中国团队包揽全部项目的冠军。
