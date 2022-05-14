## Faster-Rcnn：Two-Stage目标检测模型在Pytorch当中的实现
---

## 目录
1. [所需环境](#所需环境)
2. [文件下载](#文件下载)
3. [预测步骤](#预测步骤)
4. [训练步骤](#训练步骤)
5. [评估步骤](#评估步骤)
6. [Tensorboard可视化](#tensorboard可视化)
7. [可视化四张测试图片的第一阶段proposalbox](#可视化四张测试图片的第一阶段proposalbox)
 

## 所需环境
linux操作系统，torch == 1.2.0

## 文件下载
训练所需的voc_weights_resnet.pth主干的网络权重可以在百度云下载。  
voc_weights_resnet.pth是resnet为主干特征提取网络用到的；    
链接: https://pan.baidu.com/s/1S6wG8sEXBeoSec95NZxmlQ      
提取码: 8mgp    

VOC07+12数据集下载地址如下：  
链接: https://pan.baidu.com/s/1fXg-h0YDihGqxSg_td_Zng?pwd=j7qk
提取码：j7qk

## 训练步骤
1. 数据集的准备   
**使用VOC格式进行训练，训练前需要下载好VOC07+12的数据集，解压后放在根目录**  

2. 数据集的处理   
运行voc_annotation.py生成根目录下的2007_train.txt和2007_val.txt。   

3. 开始网络训练   
train.py的默认参数用于训练VOC数据集，可以调整batchsize，learning rate，epoch等参数。设置完成后直接运行train.py即可开始训练。   

## 预测步骤 
### 使用自己训练的权重
1.  训练结果预测需要用到两个文件，分别是frcnn.py和predict.py。
**model_path指向已训练好的权值文件，训练好的权值文件百度网盘链接: https://pan.baidu.com/s/1Kl7QaBTU2CQEuADINl8vsA?pwd=m8b5 提取码: m8b5 
从百度网盘中下载训练好的权值文件并放在logs文件夹里。**  

2. 运行predict.py进行检测，输入  
```python
img/文件名.jpg/jpeg,三张测试图片为catdog1.jpeg，railwaystaion.jpeg和test1.jpg
```  

3. 预测出的图片保存在根目录下，文件名为predict.jpg

## 评估步骤 
### 评估VOC07+12的测试集
1. 运行get_map.py即可获得评估结果，评估结果会保存在map_out文件夹中。

## Tensorboard可视化
1. 训练后会在logs/loss_xx文件夹下生成events.out.tfevents.xxx文件。

2. 进入到logs/loss_xx文件夹下后输入tensorboard --logdir='log保存路径' --port=6006

3. 运行以上命令后打开生成的网址即可查看利用Tensorboard可视化后的train loss和val loss曲线。

## 可视化四张测试图片的第一阶段proposalbox
1. 将根目录下的frcnn.py文件中的第165-171行的注释取消

2. 运行predict.py进行检测，输入  
```python
img/文件名.jpg/jpeg,四张测试图片为box.jpg，box1.jpeg，box2.jpeg，box3.jpeg
```  

3. 预测出的图片保存在根目录下，文件名为predict.jpg