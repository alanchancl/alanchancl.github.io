---
layout: post
title: PyTorch Geometric(PyG) 库的安装
date: 2023-02-01 14:20:17
description: PyTorch Geometric(PyG)库的安装教程，包括环境配置、CUDA安装和依赖包安装的详细步骤
tags: PyG
categories: 技术笔记
---

PyG库简介PyG的全称是 PyTorch Geometric,是一款基于 PyTorch 的几何深度学习框架,可以简单方便的实现图神经网络。以下为安装过程。

以下是我的Requirements.txt：
~~~
Python == 3.8
cuda == 10.2
Pytorch == 1.5.1
torch-geometric==1.5.0
~~~

## 1.创建新的conda环境
新建一个名字为PyG的python版本为3.8的新环境，记住这里安装的python版本，后续选择包的时候需要。
~~~
conda create -n PyG python=3.8 -y
activate PyG
~~~

## 2.安装Pytorch和CUDA

选择Pytorch的版本和对应版本的cuda，具体安装指令可以参考[官网](https://pytorch.org/get-started/previous-versions/)。

~~~
conda install pytorch==1.5.1 torchvision==0.6.1 cudatoolkit=10.2 -c pytorch -y
~~~

## 3.安装PyG库

需要的安装包（需要安装以下顺序安装）：
~~~
torch_scatter
torch_sparse
torch_cluster
torch_spline_conv
torch-geometric
~~~

下载网址：[https://data.pyg.org/whl/](https://data.pyg.org/whl/)

选择torch和cuda的版本：
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0" style="text-align: center;">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/img202302011720951.png" title="PyG安装包版本选择" class="img-fluid rounded z-depth-1" zoomable=true  width="50%"%}
    </div>
</div>
<div class="caption">PyG安装包版本选择</div>

进入后下载**torch_scatter 、torch_sparse 、torch_cluster 、torch_spline_conv**四个包：

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0" style="text-align: center;">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/img202302011722505.png" title="PyG依赖包下载" class="img-fluid rounded z-depth-1" zoomable=true width="50%" %}
    </div>
</div>
<div class="caption">PyG依赖包下载</div>

python版本是3.8的选cp38，还要判断是win还是linux。

下载后将四个包放置在同一个文件夹。

~~~python
cd D:\XXX\XX\  # 安装包所存的位置
pip install torch_scatter-2.0.5-cp38-cp38-win_amd64.whl
pip install torch_sparse-0.6.7-cp38-cp38-win_amd64.whl
pip install torch_cluster-1.5.7-cp38-cp38-win_amd64.whl
pip install torch_spline_conv-1.2.0-cp38-cp38-win_amd64.whl
~~~

最后选择好版本PyG版本直接安装即可。

~~~
pip install torch-geometric==1.5.0
~~~

### 4. 测试

最后，在安装完毕后可以用下面的这段代码进行测试一下。

~~~python
import torch
import torch.nn as nn
import torch.nn.functional as F
from torch_geometric.nn import MessagePassing
from torch_geometric.utils import softmax, add_remaining_self_loops


class GATConv(MessagePassing):
    def __init__(self, in_feats, out_feats, alpha, drop_prob=0.0):
        super().__init__(aggr="add")
        self.drop_prob = drop_prob
        self.lin = nn.Linear(in_feats, out_feats, bias=False)
        self.a = nn.Parameter(torch.zeros(size=(2*out_feats, 1)))
        self.leakrelu = nn.LeakyReLU(alpha)
        nn.init.xavier_uniform_(self.a)

    def forward(self, x, edge_index):
        edge_index, _ = add_remaining_self_loops(edge_index)
        # 计算 Wh
        h = self.lin(x)
        # 启动消息传播
        h_prime = self.propagate(edge_index, x=h)
        return h_prime

    def message(self, x_i, x_j, edge_index_i):
        # 计算a(Wh_i || wh_j)
        e = torch.matmul((torch.cat([x_i, x_j], dim=-1)), self.a)
        e = self.leakrelu(e)
        alpha = softmax(e, edge_index_i)
        alpha = F.dropout(alpha, self.drop_prob, self.training)
        return x_j * alpha


if __name__ == "__main__":
    conv = GATConv(in_feats=3, out_feats=3, alpha=0.2)
    x = torch.rand(4, 3)
    edge_index = torch.tensor(
        [[0, 1, 1, 2, 0, 2, 0, 3], [1, 0, 2, 1, 2, 0, 3, 0]], dtype=torch.long)
    x = conv(x, edge_index)
    print(x.shape)
~~~

