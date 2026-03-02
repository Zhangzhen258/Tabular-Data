# 表格基础模型 TabPFN 学习过程总结

## 一、TabPFN 模型的由来

### 1. [TabTransformer：Tabular Data Modeling Using Contextual Embeddings](https://arxiv.org/abs/2012.06678)

TabTransformer首次提出使用Transformer处理表格数据，通过将每一个类别特征列视为一个token，TabTransformer在单条样本内部建模特征之间的依赖关系。推理阶段，TabTransformer对每一行数据独立处理，在测试时执行标准的前向传播预测，不涉及基于数据集上下文的自适应过程。

### 2. [Transformers Can Do Bayesian Inference](https://openreview.net/forum?id=KSugKcbNf9)

首次提出PFN网络，发现Transformer能够很好的完成近似贝叶斯推断，即使用TabPFN中所运用的ICL学习策略进行输入，并初步发现在表格数据中表现良好。

### 3. [TabNet: Attentive Interpretable Tabular Learning](https://arxiv.org/abs/1908.07442)

首次提出PFN网络，发现Transformer能够很好的完成近似贝叶斯推断，即使用TabPFN中所运用的ICL学习策略进行输入，并初步发现在表格数据中表现良好。

## 二、TabPFN模型提出，及其迭代版本
