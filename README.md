## “项目名称”进展报告

### 1. 数据获取及预处理

> 主要说明一下数据的来源，原始数据的基本情况，如数量，字段，含义等
> 再就是到目前为止，对数据预处理的情况，如噪声的处理，缺失值的处理等。

#### 1.1 数据来源

#### 1.2 数据说明

#### 1.3 数据预处理

### 2. 数据分析与可视化

> 数据探索性分析的结果，可以使用统计工具，聚类分析等工具
> 使用可视化来展示分析结果

### 3. 模型选取

选择使用ResNet50模型进行数据挖掘，ResNet50模型是CNN模型的一种，常用于对图像数据进行处理，选择它的原因有两点：  
1、由于心跳信号是一组有序的数据，其中单独的一个信号往往与其相邻的信号存在一定的联系，因此使用ResNet50这种CNN模型对心跳信号数据进行处理是较为合理的，可以充分发挥CNN所具有的局部感知能力，即它的每一次卷积运算都会考虑多个相邻的信号。  
2、ResNet50模型具有残差结构，容易优化，并且能够通过增加网络深度来提高准确率。

我们所使用的Resnet50 网络中包含了 49 个卷积层和2个全连接层。Resnet50网络结构可以分成七个部分，第一部分不包含残差块，主要对输入进行卷积、正则化、激活函数、最大池化的计算。第二、三、四、五部分结构都包含了残差块，每个残差块都有三层卷积，网络总共有1+3×(3+4+6+3)=49个卷积层，加上最后的全连接层总共是 51 层。网络的输入为batch_size×1×205，输出为batch_size×4。此外，为了使原本用于图像等二维数据的ResNet50模型能够适应心跳信号这种一维数据，我们将模型中的所有二维卷积层，二维池化层以及二维BatchNorm层改为了一维的形式。



### 4. 挖掘实验的结果

### 5. 存在的问题

### 6. 下一步工作

### 7. 任务分配与完成情况
