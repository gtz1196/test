## 报告

### 数据集介绍

1、数据集中有标注的数据共计100000条，选取80000条数据作为训练集，选取20000条数据作为测试集。  
2、数据集中的每一条数据由三个字段构成：id为心跳信号分配的唯一表述，范围是[0,99999]；heartbeat_signals是心跳信号的序列，可以视为由205个值构成的特征向量，经过特征工程后变为由709个值构成的特征向量；label是心跳信号的类别，范围是0~3。

### 模型选取

选择使用ResNet50模型进行数据挖掘，ResNet50模型是CNN模型的一种，常用于对图像数据进行处理，选择它的原因有两点：    
1、由于心跳信号是一组有序的数据，其中单独的一个信号往往与其相邻的信号存在一定的联系，因此使用ResNet50这种CNN模型对心跳信号数据进行处理是较为合理的，可以充分发挥CNN所具有的局部感知能力，即它的每一次卷积运算都会考虑多个相邻的信号。    
2、ResNet50模型具有残差结构，容易优化，并且能够通过增加网络深度来提高准确率。

### 模型结构

我们所使用的Resnet50 网络中包含了 49 个卷积层和2个全连接层。Resnet50网络结构可以分成七个部分，第一部分不包含残差块，主要对输入进行卷积、正则化、激活函数、最大池化的计算。第二、三、四、五部分结构都包含了残差块，每个残差块都有三层卷积，网络总共有1+3×(3+4+6+3)=49个卷积层，加上最后的全连接层总共是 51 层。网络的输入为batch_size×1×205，输出为batch_size×4。此外，为了使原本用于图像等二维数据的ResNet50模型能够适应心跳信号这种一维数据，我们将模型中的所有二维卷积层，二维池化层以及二维BatchNorm层改为了一维的形式。

### 评价标准

1、平均指标：针对某一信号，若真实值为[y_1,y_2,y_3,y_4]，模型预测概率值为[a_1,a_2,a_3,a_4]那么该模型的平均指标abs_sum为

![y等于x的平方](https://latex.codecogs.com/svg.image?abs\_sum=\sum_{j=1}^{n}\sum_{i=1}^{4}\left|y_i-a_i\right|)

例如，心跳信号为1，会通过编码转成[0, 1, 0, 0]，预测不同心跳信号概率为[0.1, 0.7, 0.1, 0.1]，那么这个预测结果的平均指标为。

abs\_sum=

2、预测准确率：若预测结果与真实值一致，认为预测正确，否则认为预测不正确，那么该模型的预测准确率为

abs\_sum=

### 实验结果

准确率：0.9872  
平均指标：679.14
