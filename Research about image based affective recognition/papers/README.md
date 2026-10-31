# 论文阅读记录

[返回研究主页](../readme.md)

本目录整理图像情感识别相关论文，也收录用于比较研究范围的视频学业情绪识别工作。用户自述此前已阅读、讨论这些论文；当前仓库没有可核对的逐篇历史笔记，因此各篇精读程度待确认。本次内容依据官方论文页、作者项目页与官方代码仓库补充，不代表已完成精读或复现。

| 阅读记录 | 正式题名与发表 | 研究内容 | 阅读状态 | 复现状态 | 来源 |
| --- | --- | --- | --- | --- | --- |
| [CAER-Net](CAER-Net.md) | Context-Aware Emotion Recognition Networks；ICCV 2019 | 人脸与上下文双流编码、注意力及自适应融合；CAER/CAER-S | 此前阅读讨论过（用户自述）；精读程度待确认 | CAER-Net-S 第三方静态版推理与前端验证有证据；无数据集性能复现；[工程报告](../experiments/CAER-Net-S-Frontend.md) · [复现笔记](../reproductions/CAER-Net.md) | [CVF](https://openaccess.thecvf.com/content_ICCV_2019/html/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.html)、[作者项目页](https://caer-dataset.github.io/) |
| [CocoER](CocoER.md) | CocoER: Aligning Multi-Level Feature by Competition and Coordination for Emotion Recognition；CVPR 2025 | 头部、身体与上下文多层级特征对齐，通过竞争与协调处理预测冲突 | 此前阅读讨论过（用户自述）；精读程度待确认 | 待确认；未提供可验证运行记录；[复现笔记](../reproductions/CocoER.md) | [CVF](https://openaccess.thecvf.com/content/CVPR2025/html/Shen_CocoER_Aligning_Multi-Level_Feature_by__Competition_and_Coordination_for_CVPR_2025_paper.html)、[官方代码](https://github.com/bisno/CocoER) |
| [CLIP-CAER](CLIP-CAER.md) | Context-Aware Academic Emotion Dataset and Benchmark；ICCV 2025 | RAER 视频学业情绪数据集；CLIP 提示学习融合表情和学习上下文 | 此前阅读讨论过（用户自述）；精读程度待确认 | 待确认；未提供可验证运行记录；静态图像迁移待验证 | [CVF](https://openaccess.thecvf.com/content/ICCV2025/html/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.html)、[项目页](https://zgsfer.github.io/CAER/)、[官方代码](https://github.com/zgsfer/CLIP-CAER) |
| [Scene-Graph Emotion](Scene-Graph-Emotion.md) | Hierarchical Context-Based Emotion Recognition With Scene Graphs；TNNLS 2024，35(3): 3725–3739 | 融合实体、全局和场景图上下文进行情绪识别 | 此前阅读讨论过（用户自述）；精读程度待确认 | 待确认；未提供可验证运行记录；官方代码待核实 | [IEEE](https://ieeexplore.ieee.org/abstract/document/9868807)、[作者出版物列表](https://cratial.github.io/publication/index.html) |

CLIP-CAER 是方法名，其正式论文题名以 CVF 书目为准。场景图论文是期刊论文；正式卷期为 2024，IEEE 页面另列 2022 年的首次发表日期，引用时应区分。[CLIP-CAER 官方书目](https://openaccess.thecvf.com/content/ICCV2025/html/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.html)；[场景图论文 IEEE 条目](https://ieeexplore.ieee.org/abstract/document/9868807)

后续记录可使用 [论文阅读模板](paper_template.md)。未核实的公式、指标定义和实现细节统一标注“待核实”；研究想法标注“待验证设想”，不作为论文结论。
