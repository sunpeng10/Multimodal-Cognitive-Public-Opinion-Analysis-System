# CLEF框架 · 论文阅读记录

[返回论文索引](README.md) · [研究主页](../readme.md) · [论文模板](paper_template.md)

> 整理日期：2026-11-01。用户已阅读；本记录依据作者公开原文核对，不代表完成模型复现。原文结果与待验证的个人思路分别记录。

## Paper Information

| 字段 | 内容 |
| --- | --- |
| 正式题名 | Robust Emotion Recognition in Context Debiasing |
| 作者 | Dingkang Yang、Kun Yang、Mingcheng Li、Shunli Wang、Shuaibing Wang、Lihua Zhang |
| 年份与会议 / 期刊 | CVPR 2024，pp. 12447–12457 |
| 框架名称 | CLEF：counterfactual emotion inference（反事实情绪推断） |
| 官方论文链接 | [CVF 论文页](https://openaccess.thecvf.com/content/CVPR2024/html/Yang_Robust_Emotion_Recognition_in_Context_Debiasing_CVPR_2024_paper.html) · [作者 arXiv 条目](https://arxiv.org/abs/2403.05963) · [原文 HTML，v3](https://arxiv.org/html/2403.05963v3) |
| 官方项目 / 代码链接 | 待核实；本次未确认可归属于作者的实现链接，不将同名第三方项目标为官方 |
| 阅读状态 | 已阅读（用户说明）；本次按模板整理，具体个人批注待补充 |
| 复现状态 | 本次仅整理文档，未开展 CLEF 代码复现、训练或评估；历史状态如有另行补证 |

## Research Background

上下文既能补充模糊的人物线索，也可能形成“场景—情绪”捷径。本文研究如何区分有用先验与有害偏差。[原文 §1](https://arxiv.org/html/2403.05963v3)

## Problem Statement

在作者的因果图中，保留经联合表征传递的信息，扣除上下文直接影响预测的偏差。[原文 §4.1–4.2](https://arxiv.org/html/2403.05963v3)

## Previous Methods and Limitations

常规融合未必消除背景捷径；作者认为，预定义混杂因素的干预方案也难完全分离两种上下文效应。[原文 §2](https://arxiv.org/html/2403.05963v3)

## Main Contributions

- 建立 CAER 因果图。
- 为现有模型增加独立上下文分支。
- 用事实与反事实输出之差实现推断去偏。[原文 §1、§4](https://arxiv.org/html/2403.05963v3)

## Method Overview

原模型建模人物与上下文；新增分支遮蔽目标人物，估计直接上下文效应。论文实例化使用 Places365 预训练 ResNet-152。无处理输出采用共享可学习参数，并以 KL 正则约束。[原文 §4.3、§5.3](https://arxiv.org/html/2403.05963v3)

## Key Formulas

以下保留原文编号。$C$ 为上下文，$S$ 为人物，$E$ 为联合表征，$Y$ 为预测分数；星号表示无处理条件。

**效应分解（式 6、7、9）：**

$$
\begin{aligned}
\mathrm{TE}&=Y_{c,e}(X)-Y_{c^*,e^*}(X),\\
\mathrm{NDE}&=Y_{c,e^*}(X)-Y_{c^*,e^*}(X),\\
\mathrm{TIE}&=\mathrm{TE}-\mathrm{NDE}
=Y_{c,e}(X)-Y_{c,e^*}(X).
\end{aligned}
$$

TE、NDE、TIE 分别是总效应、自然直接效应、总间接效应；反事实保留上下文而阻断联合表征路径。

**实现（式 11、15）：**

$$
\phi(Y_c,Y_e)=\log\sigma(Y_c+Y_e),\qquad
\mathrm{TIE}=\phi(Y_c,Y_e)-\phi(Y_c,Y_{e^*}).
$$

$\sigma$ 为 sigmoid；$Y_c$、$Y_e$ 是两条分支的输出，$Y_{e^*}$ 是共享的无处理输出近似。不能直接改写成两个 Softmax 概率相减。[原文 §4.2–4.3](https://arxiv.org/html/2403.05963v3)

## Datasets and Evaluation Metrics

| 数据集 | 任务 | 原文指标 |
| --- | --- | --- |
| EMOTIC | 26 类多标签情绪 | AP / mAP |
| CAER-S | 7 类静态图像情绪 | Accuracy |

两者原文划分均为 7:1:2；后续复现仍需核对划分清单及人物框。[原文 §5.1](https://arxiv.org/html/2403.05963v3)

## Experimental Results

**仅摘录论文报告，非个人复现结果。**

| 数据集 / 指标 | CAER-Net | CAER-Net + CLEF | 增量（百分点） |
| --- | --- | --- | --- |
| EMOTIC / mAP (%) | 23.85 | 27.44 | +3.59 |
| CAER-S / Accuracy (%) | 73.47 | 75.86 | +2.39 |

来源：[原文表 2、3](https://arxiv.org/html/2403.05963v3)。表 4 检查了分支、遮蔽、KL 和无处理假设；总体提升不意味着每个类别都提升。

## Strengths and Limitations

- 阅读判断：将“利用上下文”和“抑制背景捷径”分开处理，适合组织后续对照实验。
- 待验证边界：新增分支的计算开销、人物框误差，以及因果图和无处理近似在新域中的适用性。不能仅凭原文两套基准推断普遍跨域有效。

## Reproduction Status

本次未运行 CLEF。现有 [CAER-Net-S 前端报告](../experiments/CAER-Net-S-Frontend.md)只验证原模型单图推理与展示，**不包含 CLEF，也不构成本文结果复现**。代码来源、训练配置与标准数据评估仍需补证。

## Potential Research Ideas

以下均为备选计划，未实现或验证：

1. 先固定 CAER-Net-S 数据划分、人脸框和预处理，再比较原模型与 CLEF，单列训练成本与推理开销。
2. 检查“遮脸”与“遮整个人物”的区别，控制其余条件，避免身体线索泄露影响偏差估计。
3. 对人物—背景冲突样本分析反事实校正幅度和预测错误的关系；不预设校正幅度等于不确定性。

## Personal Notes

本次整理的理解：先区分信息路径，再讨论去偏；当前前端显示的融合权重或 Attention 不能直接充当 CLEF 的因果效应。

后续精读问题：无处理参数究竟如何优化？哪些类别可能因扣除上下文而受损？应结合原文式 12–14、逐类结果和实际实现核对。用户个人批注与讨论结论尚未提供，不代写为既有观点。
