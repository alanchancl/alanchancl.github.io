---
layout: post
title: 利用skip connections模块生成迁移性强的对抗样本
date: 2021-09-05 13:20:17
categories: 论文笔记
tags: AI安全 对抗攻击
description: 利用skip connections模块生成迁移性强的对抗样本的研究，探讨其在对抗攻击中的应用与效果。
---

>- 论文名称：[《Skip Connections Matter: On The Transferability Of Adversarial Examples Generated With ResNets》](http://link.zhihu.com/?target=https%3A//arxiv.org/abs/2002.05990)
>- 作者单位：Dongxian Wu/ Tsinghua University
>- 收录时间：2020 ICLR
>- 文章亮点：发现了深度神经网络中skip connections模块的使用导致了迁移性强的对抗样本的产生。

<!--more-->

## Motivation

- 在深度神经网络中，skip connection 将residual module（残差模块）的输入直接与输出相连，建立从浅层到深层的捷径。有助于保留低级特征。且在添加多层时避免性能下降。
- 白盒攻击算法，如FGSM、BIM、PGD和CW由于其迁移性差，难以应用在日常生活中更常见的黑盒模型中。因此很多研究也旨在提高基于替身模型的黑盒攻击的可迁移性，例如：(Dong et al., 2018)的Momentum Boosting、(Xie et al., 2019)的Diverse Input和(Dong et al., 2019) Translation Invariance。
- 但是上述的无论时白盒攻击还是黑盒攻击，是目标攻击还是替身攻击。在考虑增强对抗攻击的可迁移性的思路上，都是将整个网络看成是一个整体，却忽略了网络内部的体系结构特征。（这个思路好厉害）
- 基于实验观察利用skip connection跳过残差模块可以大大增加黑盒攻击的成功率。

### 文章的技术贡献

1. 提出了Skip Gradient Method（SGM），利用类ResNet神经网络中的Skip Connection可以很容易生成迁移性强的对抗样本。

2. 实验证明了SGM可以极大地提高对抗样本的迁移性。

## Skip Gradient Method（SGM）：

为了更多的利用skip connection的梯度信息，文章在梯度计算公式中引入了一个衰减参数γ来降低residual module模块的梯度。γ∈（0，1]

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0" style="text-align: center;">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/img202211231648825.png" title="梯度计算公式" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">梯度计算公式</div>
### Skip connection的迁移性实例研究：

对抗样本生成方法：10-step PGD和其对应的SGM版本

实验替身模型：ResNet(RN)-18/34/50/101/152 and DenseNet(DN)-121/169/201

攻击目标模型：Inception V3

数据集：ImageNet

参数设置：PGD步长α=2、SGM衰减参数γ=0.5

实验结果：对抗样本攻击的迁移性大大提高
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0" style="text-align: center;">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/img202211231648006.png" title="实验结果" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">实验结果</div>

且当替身模型中具有更多的Skip Connection时，其生成的对抗样本就更加具有可迁移性。

## Comparison To Exising Transfer Attacks：

1. 单独实验说明：
* Baselines：将SGM与FGSM、PGD、MI、DI、TI攻击算法进行对比
* Threat Model：采用黑盒攻击模型
* Target Models：
- 攻击的目标模型有未经过对抗训练的传统模型：VGG19、ResNet-152、DenseNet-201、154 layer Squeeze-and-Excitation network、Inception V3、Inception V4、Inception-ResNet V2
- 攻击的目标还有经过对抗性训练的安全模型：IncV3ens3、IncV3ens4 、IncResV2ens3

* Sourse Models：即替代模型所使用的模型，利用对抗样本的迁移性，用来生成可以攻击其他网络的对抗样本。用了ResNet-18、ResNet-34、ResNet-50、ResNet-101、ResNet-152 、DenseNet-121、DenseNet-169、DenseNet-201.

1. 将SGM与其他攻击方法结合，测试其迁移性。如MI+SGM、DI+SGM和MI+DI+SGM的攻击效果提升

2. 实验还探究了SGM衰减率γ对攻击迁移性能的影响