---
layout: post
title:  "Community Interaction and Conflict on the Web 学习笔记（一）"
date:   2019-09-02 18:16:18 +0800
categories: notes
---

## 前言
本文记录自己学习 [Community Interaction and Conflict on the Web](http://snap.stanford.edu/conflict/) 的笔记。作者提供了详细的代码和数据，均可以在这里找到：<br />[http://snap.stanford.edu/conflict/](http://snap.stanford.edu/conflict/)

由于作者的代码基于 python 2.7，而且使用的scikit-learn和scipy都是历史版本，故搭建开发环境需要多费点力气。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558244167489-b7fc69de-9499-4a82-beb8-96b54bf046a2.png#align=left&display=inline&height=376&name=image.png&originHeight=752&originWidth=1198&size=90586&status=done&width=599)
## 
## 在Mac OS上搭建环境

### 一、下载并安装Anaconda
为了更全面的模拟作者的开发环境，我使用Anaconda这个工具。它能提供一个可指定python版本的虚拟环境，并且包含conda、numpy等上百个科学包及其依赖项。

官网提供的有安装教程：<br />[https://docs.anaconda.com/anaconda/install/mac-os/](https://docs.anaconda.com/anaconda/install/mac-os/)

安装完成后，打开终端，输入conda，显示下图即为安装成功（如果提示没有conda命令，那么需要把"/anaconda2/bin"添加到环境变量里）。

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558244817312-b9b9ecda-d4b9-47eb-afa2-7681386b7ba0.png#align=left&display=inline&height=1210&name=image.png&originHeight=1210&originWidth=1528&size=761903&status=done&width=1528)

### 
### 二、创建一个python 2.7 的虚拟环境
如下图所示，打开anaconda 图标，使用图形模式创建一个python2.7的虚拟环境，命名为lstmNew（图中是因为我已经创建了lstmNew，改成了lstmLearn）。

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558245469296-8b92554e-09b4-44fb-ab2b-cc3dbba9681f.png#align=left&display=inline&height=822&name=image.png&originHeight=1644&originWidth=2880&size=510498&status=done&width=1440)

稍等片刻，等待其创建虚拟环境并安装一些默认的科学包工具。然后我们便可以安装其他的包。


### 三、安装其他必须包
作者列出的必须包有：
```
torch
scikit-learn==0.18.2
scipy==0.19.1
```

但是我们在anaconda里搜索scikit-learn和scipy包的时候，仅有更新版的版本：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558245977613-27767d1e-6b4e-423b-9046-2fbe04b1894f.png#align=left&display=inline&height=219&name=image.png&originHeight=438&originWidth=1852&size=56310&status=done&width=926)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558246017291-310b4558-833a-4802-a542-c3303011b5c4.png#align=left&display=inline&height=236&name=image.png&originHeight=472&originWidth=1806&size=62054&status=done&width=903)


所以我们需要在终端使用pip工具安装指定版本。
#### 
#### a. 打开终端，激活刚刚创建的lstmNew环境：

```
source activate lstmNew
```

激活成功，并且测试当前python版本和pip，如下图：<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558246364663-29cb1fb5-1727-4207-b275-6f7d5e185967.png#align=left&display=inline&height=212&name=image.png&originHeight=424&originWidth=1608&size=271462&status=done&width=804)

#### b. 安装torch，scikit-learn 和 scipy
```
pip install torch torchvision # 由于作者并未指出版本号，这里选择安装最新版
pip install scikit-learn==0.18.2
pip install scipy==0.19.1
```

等待安装完成后，测试是否安装成功：

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558246718293-d0afabc5-6849-4184-a9a5-07584929fb98.png#align=left&display=inline&height=164&name=image.png&originHeight=328&originWidth=1568&size=197140&status=done&width=784)

未报错，就是成功了。


### 四、可以开始训练了！

作者提供的数据有：
```
├── prediction
│   ├── README.txt
│   ├── detailed_data
│   │   ├── full_embeds.npy
│   │   ├── full_ids.txt
│   │   ├── handcrafted_features.tsv
│   │   ├── label_info.tsv
│   │   ├── lstm_embeds-ids.pkl
│   │   ├── lstm_embeds.npy
│   │   ├── post_crosslinks_info.tsv
│   │   └── tokenized_posts.tsv
│   ├── embeddings
│   │   ├── glove_word_embeds.txt
│   │   ├── sub_vecs.npy
│   │   ├── sub_vecs.vocab
│   │   ├── user_vecs.npy
│   │   └── user_vecs.vocab
│   ├── preprocessed_test_data.pkl
│   ├── preprocessed_train_data.pkl
│   └── preprocessed_val_data.pkl
├── subreddit_embeddings.csv
└── user_embeddings.csv
```

修改 constants.py 文件。如果你和我一样用的是mac OS，由于mac版本的pytorch并不支持GPU，所以要把CUDA这一项改为False。再修改数据文件和日志文件地址：

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558247175336-1c22f675-346c-4c98-a520-b89619c707e4.png#align=left&display=inline&height=697&name=image.png&originHeight=1394&originWidth=1926&size=421672&status=done&width=963)


**One more thing！**我在运行 social_lstm_model.py 的时候，遇到了两个报错：

#### a. RuntimeError: expected Float tensor (got Long tensor)
这里需要对文件118行进行如下改动：

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558247962486-a3fd4b41-1dd3-4e22-9aac-a452e35fd380.png#align=left&display=inline&height=611&name=image.png&originHeight=1222&originWidth=2480&size=377477&status=done&width=1240)

#### b. invalidindex of a 0-dim tensor. Use tensor.item() to convert a 0-dim tensor to aPython number
这里需要对文件267行和269行进行如下改动（参考[这里](https://github.com/NVIDIA/flownet2-pytorch/issues/113)）：

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558247923777-86c3d9a2-e478-4cae-b9b4-0a8887169b5c.png#align=left&display=inline&height=611&name=image.png&originHeight=1222&originWidth=2480&size=405956&status=done&width=1240)

#### c. 测试
现在就可以运行了，大约执行20分钟后，得到训练结果：
### ![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558248082517-4a6e268f-5dfa-44c8-8542-43dc490afa39.png#align=left&display=inline&height=1800&name=image.png&originHeight=1800&originWidth=2880&size=1062207&status=done&width=2880)


### 五、使用 jupyter notebook
Anaconda另一个好处就是，安装并使用jupyter notebook也十分方便。

![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558248642760-a5b6b32b-463e-48c3-b9e6-49cd6efafb67.png#align=left&display=inline&height=822&name=image.png&originHeight=1644&originWidth=2880&size=412669&status=done&width=1440)


作者也提供的有 nonneural_models.ipynb 文件可供对比测试训练结果。使用notebook打开此文件，同样，在执行将近20分钟后，得到结果如图：


![image.png](https://cdn.nlark.com/yuque/0/2019/png/114285/1558248386820-d9a41d94-b524-416f-b992-e89eb59b916b.png#align=left&display=inline&height=900&name=image.png&originHeight=1800&originWidth=2880&size=1931122&status=done&width=1440)

#### TIP：快速打开 jupyter notebook 
在安装完jupyter notebook后，如果以后只是想打开jupyter notebook，而不使用需要 Anaconda-Navigator，可以使用如下命令打开你创建的py环境中的jupyter notebook，非常快捷：

```
source activate py27 # 这里py27是我的虚拟python环境名
jupyter notebook
```

