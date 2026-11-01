# Hierarchical Context-Based Emotion Recognition With Scene Graphs 阅读记录

[返回论文索引](README.md) · [返回研究主页](../readme.md)

## Paper Information

- 正式题名：Hierarchical Context-Based Emotion Recognition With Scene Graphs。
- 作者：Shichao Wu、Lei Zhou、Zhengxi Hu、Jingtai Liu。
- 发表：IEEE Transactions on Neural Networks and Learning Systems（TNNLS），2024，35(3): 3725–3739；这是一篇期刊论文。[作者出版物列表](https://cratial.github.io/publication/index.html)
- IEEE 页面另列首次发表日期为 2022-08-26；正式卷期年份与首次在线发表年份应区分。
- DOI：10.1109/TNNLS.2022.3196831；官方代码链接待核实。[IEEE 官方条目](https://ieeexplore.ieee.org/abstract/document/9868807)

## Research Background

在非受控场景中，人脸表情与身体姿态等可观察信息可能不足，导致情绪误判。论文借鉴人类对场景的层级理解，研究能补充人物状态的上下文表达。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Problem Statement

如何从图像提取并融合不同抽象层次的上下文，利用实体及其关系辅助目标人物的情绪识别。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Previous Methods and Limitations

论文指出，仅依据面部表情和身体姿态的方法在受控环境中有效，但在非受控环境里可能因有效输入不足而误判。具体相关方法、图推理基线及各方法差异待精读核对。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Main Contributions

- 提取 entity context、global context、scene context 三类层级上下文。
- 在场景上下文中表达实体标签及实体间关系的抽象信息。
- 融合多类上下文进行情绪识别，并构造基于 BoLD 的图像任务 BoLD-Img。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Method Overview

从输入图像提取实体上下文、全局上下文和场景上下文；其中场景上下文包含实体标签及其关系，再融合这些信息进行情绪识别。场景图生成器、节点和边定义、图编码结构及融合实现细节待原文精读核实，不据论文标题推断具体图网络类型。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Key Formulas

待核实：图表示、关系编码、层级融合和损失函数尚未逐式核对。当前不填写推测的图卷积或注意力公式。

## Datasets and Evaluation Metrics

- CAER-S：摘要报告 accuracy。
- EMOTIC：摘要报告 C-F1。
- BoLD / BoLD-Img：论文基于 BoLD 构建图像任务 BoLD-Img，摘要报告 emotion recognition score（ERS）。
- 各指标的精确定义、数据划分、其他指标以及跨任务可比性：待核实。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Experimental Results

原文报告层级上下文有助于识别，消融实验表明不同上下文提供互补信息。具体比较方法、图模块消融及实验设置待原文逐表核实；本笔记不填实验数值。[IEEE 摘要](https://ieeexplore.ieee.org/abstract/document/9868807)

## Strengths and Limitations

- 阅读判断：将视觉实体、整体环境和实体关系分层表达，便于组织对不同上下文来源的分析。
- 待验证关注点：实体检测及关系预测错误是否传递到情绪分类，稀疏场景和复杂场景中的表现是否不同。
- 论文明确陈述的局限、模型成本及适用边界：待精读核实。

## Reproduction Status

官方代码链接与可运行实现待核实。当前尚未提供环境、数据、训练或评估的可验证记录，复现状态待确认，不能认定已完成复现。

## Potential Research Ideas

- 待验证设想：固定视觉特征，比较有无实体关系信息的预测差异，检验关系信息的独立作用。
- 待验证设想：对低置信度实体或关系设置筛选规则，分析图构建噪声对情绪识别的影响。

## Personal Notes

这篇文章提出了一种“基于场景图的分层上下文情绪识别方法”（Hierarchical Context-Based Emotion Recognition With Scene Graphs）。它希望让模型不仅看人物的脸部表情或身体姿态，还能结合人物所处环境及人与物之间的关系，来更准确地判断人物情绪。[src-1]

它主要解决的问题是：在真实、非受控场景中，人物的脸可能被遮挡、表情不明显，或身体姿态信息不足；如果只依赖人物本身的视觉线索，容易误判情绪。因此，文章将情绪识别扩展为“上下文感知”的推理任务。[src-1]

具体而言，方法从图像中提取并融合三类上下文信息：

- 实体上下文：图中人物、物体等实体本身的视觉信息。
- 全局上下文：整张图片的整体环境和场景特征。
- 场景上下文：通过场景图表示实体类别及其相互关系，例如“人物正在拿着某物”“人物位于某个场所”。这种关系信息可提供更抽象的语义线索。[src-1]

这些层次化信息随后被融合，用于预测情绪类别。文章在 CAER-S、EMOTIC 和 BoLD-Img 等上下文情绪识别数据集上验证，结果表明三类上下文能够互补，并提升情绪识别表现；例如在 CAER-S 上准确率达到 90.83%。[src-1]
