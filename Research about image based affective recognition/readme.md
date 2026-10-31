# Research about image based affective recognition

> 多模态认知舆情分析系统 · Image-based Affective Recognition

这是一个涉及到image based affective recognition的研究目录。

## Research Overview

本目录用于长期记录基于图像的情感识别研究，包括论文阅读、模型复现、实验与研究想法。当前重点是自然场景下结合人物与上下文的情绪识别，逐步探索其与舆情分析的关联。

**记录原则**：论文结论、个人推测与本地实验分别注明来源；阅读过论文不等于完成复现；缺少证据的内容标为“待核实/待补充”。本次仅整理文档，没有安装依赖或运行模型。

## Research Motivation

自然场景中的人脸可能较小、被遮挡或表情不明显。人物姿态、周围物体、其他人物及场景关系可能提供补充线索；背景也可能与人物情绪冲突，成为误导因素。因此需要研究人物与上下文各自的贡献、融合方式及预测可靠性，而非预先认定上下文总能提升性能。

这一路线的论文依据见 [CAER-Net](papers/CAER-Net.md)、[CocoER](papers/CocoER.md) 与[场景图论文](papers/Scene-Graph-Emotion.md)。

## Research Topics

| 方向 | 关注内容 | 当前定位 |
| --- | --- | --- |
| Context-aware Emotion Recognition | 人脸、身体与场景上下文的互补及冲突 | 当前文献整理主线；复现完成度待核实 |
| Scene Graph | 人物、物体及其关系的情绪线索 | 计划：阅读与基线可行性评估 |
| Vision-Language Models | CLIP、情绪语义提示及视觉与文本对齐 | 计划：阅读 CLIP-CAER，评估静态图像适用性 |
| Uncertainty-aware Learning | 置信度校准、不确定性与预测一致性 | 备选：尚无入库实验记录 |
| 图文情感关联 | 图像情绪与文本情感的标签及样本对应 | 备选：先确认任务与标签语义 |

## Repository Structure

| 目录 | 用途 | 入口 |
| --- | --- | --- |
| `papers/` | 论文索引、统一阅读记录及待核实项 | [论文阅读](papers/README.md) · [模板](papers/paper_template.md) |
| `reproductions/` | 按模型记录环境、运行证据、问题与实际进度 | [模型复现](reproductions/README.md) · [模板](reproductions/reproduction_template.md) |
| `experiments/` | 按实验记录假设、设置、结果与消融 | [实验记录](experiments/README.md) · [模板](experiments/experiment_template.md) |
| `ideas/` | 研究问题与 A+B=C 备选思路 | [研究想法](ideas/README.md) · [研究问题](ideas/research_questions.md) · [模板](ideas/idea_template.md) |

本目录沿用原有路径及小写 `readme.md`，原位增量完善，避免在 Windows 上创建大小写重复文件或新增重复研究入口。

## Research Progress

初始文档整理日期为 2026-10-29；CAER-Net-S 推理与前端记录于 2026-10-31 补充核验。“用户说明”与“仓库证据”分别标注。

| 论文/项目 | 研究内容 | 阅读状态 | 复现状态 | 实验状态 | 备注 |
| --- | --- | --- | --- | --- | --- |
| [CAER-Net](papers/CAER-Net.md) | 人脸与上下文融合 | 曾阅读/讨论（用户说明）；精读程度待确认 | 第三方静态版 CAER-Net-S 的真实权重推理与前端验证有证据；未训练 | [单图推理与前端工程验证](experiments/CAER-Net-S-Frontend.md)，非数据集性能实验 | ICCV 2019；见[复现记录](reproductions/CAER-Net.md) |
| [CocoER](papers/CocoER.md) | 多层级特征的竞争与协调 | 曾阅读/讨论（用户说明）；精读程度待确认 | 曾开展代码复现相关工作（用户说明）；完成度待核实 | 无本方向入库记录 | CVPR 2025；见[复现记录](reproductions/CocoER.md) |
| [CLIP-CAER](papers/CLIP-CAER.md) | 学业场景下的视觉语言情绪识别 | 曾阅读/讨论（用户说明）；精读程度待确认 | 待核实，无入库证据 | 无本方向入库记录 | ICCV 2025；方法名与正式题名有别，视频到图像迁移待验证 |
| [Scene Graph Emotion](papers/Scene-Graph-Emotion.md) | 层级上下文与场景图 | 曾阅读/讨论（用户说明）；精读程度待确认 | 待核实，无入库证据 | 无本方向入库记录 | TNNLS 2024，early access 2022 |

**证据范围**：当前仓库版本 `8e32e2f` 的研究目录原来仅有一句介绍；检索现有文档、配置及版本控制文件清单，未找到上述模型的专属实现、运行日志或环境清单。仓库之外的历史复现材料尚未纳入本次核验，不能据此断言相关工作未开展。

**2026-10-31 更新**：已读取 CAER-Net-S 原聊天与 `D:\CAER-Net` 本地工程，依据原始推理 JSON、历史报告与已有截图形成[工程验证记录](experiments/CAER-Net-S-Frontend.md)。以上初始证据范围保留为历史说明；本次未新增其他模型的核验结果，也未进行训练或数据集性能评估。

## 与原系统的关系

[仓库首页](../README.md)记录了 RoBERTa + Integrated Gradients 文本情感分析、BASNet 图像显著性分析、GAT 图网络分析及前后端展示。本目录在这些系统模块之外维护研究文档，后续是否接入系统需另行设计和验证。

**Salient Object Detection（显著性目标检测）与 Image-based Affective Recognition（图像情感识别）是不同任务**：前者定位显著区域，后者预测情感标签。BASNet 输出或已有 GAT 结果不能作为本方向情绪识别实验结果；已有系统的 GAT 也不等同于论文中的 Scene Graph。

其他方向（S3OD 候选纠错、果蝇视觉连接组）不纳入本目录核心范围，不迁入其代码或材料。

## Future Work

1. 补齐四篇论文的逐节阅读笔记，核对公式编号、数据划分及指标定义。
2. 整理 CAER-Net、CocoER 的历史源码版本、Windows/AutoDL 环境和原始日志，逐项确认推理、评估与训练状态。
3. 在[复现记录](reproductions/README.md)中建立可追溯基线后，再按[实验模板](experiments/experiment_template.md)登记真实实验。
4. 优先评估人物与上下文贡献、冲突场景及跨域泛化；不确定性和图文关联作为备选方向，见[研究问题](ideas/research_questions.md)。
