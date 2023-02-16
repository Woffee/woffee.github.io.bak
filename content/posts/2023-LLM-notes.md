+++
author = "Woffee"
title = "关于LLM的笔记"
date = "2023-02-15T11:55:41-05:00"
tags = [
    "LLM",
    "NLP",
]
+++

GPT-3 的出现可以说是一个分水岭
<!--more-->

原文链接：[https://zhuanlan.zhihu.com/p/597586623](https://zhuanlan.zhihu.com/p/597586623)

## 四大范式

![四大范式](/images/nlp_4_paradigms.png)

* Feature Engineering：即使用文本特征，例如词性，长度等，在使用机器学习的方法进行模型训练。（无预训练语言模型）
* Architecture Engineering：在W2V基础上，利用深度模型，加上固定的embedding。（有固定预训练embedding，但与下游任务无直接关系）
* Objective Engineering：在bert 的基础上，使用动态的embedding，在加上fine-tuning。（有预训练语言模型，但与下游任务有gap）
* Prompt Engineering：直接利用与训练语言模型辅以特定的prompt。（有预训练语言模型，但与下游任务无gap）


### GPT-3 的出现可以说是一个分水岭

在GPT-3之前，就是第三范式，GPT-3之后，就进入了第四范式

![Prompting](/images/prompting.png)

### GPT-3 发布后带来的影响

#### 影响一：中间任务的消亡

按理说，“中间任务”就不应该出现，而之所以会存在，这是NLP技术发展水平不够高的一种体现。

自从Bert／GPT出现之后，其实就没有必要做这些中间任务了，


#### 影响二：不同研究方向技术路线的统一

自从Bert/GPT模型诞生后，出现了明显的技术统一趋向。首先，NLP中不同的子领域，其特征抽取 器都逐渐从LSTM/CNN统一到Transformer上

#### 影响三：很多NLP子领域不再具备独立研究价值


## 过渡期：以GPT 3.0为代表的“自回归语言模型+Prompting”模式占据统治地位

Prompt其实是一个过渡期的技术，之所以有 Prompt这个技术，是因为LLM暂时不具备完全理解自然语言的能力。需要人们准确告诉它任务细节，激活LLM里与该任务相关的神经节点。

这里有一个假设，或者说是前提，就是LLM具备自主学习能力。在此之上，我们才可以谈Prompt。

最近几年相关的文章可分为：
* Few shot prompting
* Zero shot prompting
* In Context Learning
* Instruct

这些名词实际上都是在说prompt，但只是具体做法不同，所以叫法也不同。

Fine-tuning中：是预训练语言模型“迁就“各种下游任务。具体体现就是上面提到的通过引入各种辅助任务loss，将其添加到预训练模型中，然后继续pre-training，以便让其更加适配下游任务。总之，这个过程中，预训练语言模型做出了更多的牺牲。

Prompting中，是各种下游任务“迁就“预训练语言模型。具体体现也是上面介绍的，我们需要对不同任务进行重构，使得它达到适配预训练语言模型的效果。总之，这个过程中，是下游任务做出了更多的牺牲。


Prompt 分为离散和连续两种。离散就是说我们的prompt是一个个 token。
连续是说，我们的prompt 是一个 embedding。

### 连续 Prompting

![连续 Prompting](/images/continuous_prompting.png)

### 离散 Prompting

![prompting1](/images/prompting1.png)

CoT的意思是让LLM模型明白一个道理；就是 在推理过程中，步子不要迈得太大，否则很容易出错，改变思维模式，化大问题为小问题

![prompting1](/images/prompting2.png)

“Self-Consistency”则不然，它要求LLM输出多个 不同的推理过程和答案，然后采用投票的方式选出最佳答案，思路非常简单直接，但是效果也确实好

![prompting1](/images/prompting3.png)

## 从预训练模型走向通用人工智能

人适配 LLM的典型例子，比如绞尽脑汁去尝试各种不同的prompt，以试图找到好的提示语，

ChatGPT的最大贡献在于：基本实现了理想LLM的接口层，让LLM适配人的习惯命令表 达方式，而不是反过来让人去适配LLM，绞尽脑汁地想出一个能Work的命令（这就是instruct技术 出来之前，prompt技术在做的事情），而这增加了LLM的易用性和用户体验。是 InstructGPT/ChatGPT首先意识到这个问题，并给出了很好的解决方案，这也是它最大的技术贡 献。相对之前的few shot prompting，它是一种更符合人类表达习惯的人和LLM进行交互的人机接口技术。


