# 表格基础模型 TabPFN 学习过程总结

## 一、TabPFN的前身

### 1. [TabTransformer：Tabular Data Modeling Using Contextual Embeddings](https://arxiv.org/abs/2012.06678)

TabTransformer首次提出使用Transformer处理表格数据，通过将每一个类别特征列视为一个token，TabTransformer在单条样本内部建模特征之间的依赖关系。推理阶段，TabTransformer对每一行数据独立处理，在测试时执行标准的前向传播预测，不涉及基于数据集上下文的自适应过程。

### 2. [Transformers Can Do Bayesian Inference](https://openreview.net/forum?id=KSugKcbNf9)

首次提出PFN网络，发现Transformer能够很好的完成近似贝叶斯推断，即使用TabPFN中所运用的ICL学习策略进行输入，并初步发现在表格数据中表现良好。

### 3. [TabNet: Attentive Interpretable Tabular Learning](https://arxiv.org/abs/1908.07442)

作者提出了一个面向表格的深度学习架构TabNet，其在每个决策步骤利用transformer的注意力机制生成特征掩码，选择合适的特征进行建模，最终积累多个步骤的推理结果来进行预测。

### 4. [Can Transformers Learn Full Bayesian Inference In Context?](https://arxiv.org/abs/1908.07442)
作者在PFN网络的基础上进行了扩展，实现对更复杂的分布进行完全贝叶斯推断。作者训练了一个flow matching网络，首先使用transformer读取数据集中数据，产生对应的上下文embedding。将得到的embedding输入到folw matching网络中，该网络以简单的分布为起点，在数据集x的embedding的约束下学习一个向量场，通过该向量场逐步将简单的分布转化为x对应的后验分布样本P(z|x)，实现对x的完全贝叶斯推断。

## 二、TabPFN模型提出，及其迭代版本

### 1.使用TabPFN处理时间预测问题

#### （1）RaFLA: Regime-Aware Price Forecasting under Heterogeneous Temporal Granularity via a Financial Agent

将Agent代理与TabPFN结合，使用TabPFN完成股票价格预测问题。（动机存在问题，引入TabPFN进行预测的理由没有阐明，使用agent帮助tabpfn进行特征筛选的动机的必要性未知）。

### 2.通过数据扩充提升TabPFN性能

#### （2）[Causal Data Augmentation for Robust Fine-Tuning of Tabular Foundation Models](https://arxiv.org/abs/2601.04110)

当下游数据集数据量较少时，仅使用少量真实数据进行微调，往往难以使 TabPFN 充分适应下游任务。为此，作者首先使用 PC 和 FCI 结构发现算法估计特征之间的结构依赖关系，并将结果聚合为概率邻接矩阵；随后基于该结构使用 DoWhy 的 SCM 框架拟合目标数据集对应的结构因果模型，进而生成结构一致的合成数据。最后，作者将合成数据与原始数据混合，共同用于微调 TabPFN。
