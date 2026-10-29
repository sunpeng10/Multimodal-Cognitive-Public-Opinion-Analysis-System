# CAER-Net 阅读记录

[返回论文索引](README.md) · [返回研究主页](../readme.md) · [复现笔记](../reproductions/CAER-Net.md)

## Paper Information

- 正式题名：Context-Aware Emotion Recognition Networks。
- 作者：Jiyoung Lee、Seungryong Kim、Sunok Kim、Jungin Park、Kwanghoon Sohn。
- 发表：ICCV 2019，pp. 10143–10152。
- 方法名称：CAER-Net；官方代码链接待核实，不能将个人实现直接标为官方实现。
- 来源：[CVF 官方论文页](https://openaccess.thecvf.com/content_ICCV_2019/html/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.html)、[作者项目页](https://caer-dataset.github.io/)。

## Research Background

单独分析面部表情，在表情模糊或情绪线索不足时可能难以确定人的情绪；周围场景、动作和交互可提供补充信息。论文围绕人脸和上下文联合建模展开。[论文摘要及引言](https://openaccess.thecvf.com/content_ICCV_2019/papers/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.pdf)

## Problem Statement

针对图像或视频中的目标人物，结合面部表情与有辨识力的上下文预测离散情绪类别。核心问题是如何从背景中选择有效上下文并进行融合。[论文原文](https://openaccess.thecvf.com/content_ICCV_2019/papers/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.pdf)

## Previous Methods and Limitations

论文指出，主要依赖裁剪人脸的方法对上下文利用有限；仅使用整幅图像的整体外观，也不一定能定位最相关的上下文区域。具体比较方法及公平性待精读核对。[论文引言](https://openaccess.thecvf.com/content_ICCV_2019/papers/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.pdf)

## Main Contributions

- 使用人脸与上下文双流编码，并通过自适应融合结合两种信息。
- 在上下文输入中遮挡人脸，通过注意力寻找补充线索。
- 提出 CAER 视频基准及从视频采样得到的静态图像基准 CAER-S。[作者项目页](https://caer-dataset.github.io/)

## Method Overview

人脸流编码裁剪的人脸；上下文流处理遮挡人脸的输入，并通过注意力定位上下文区域。自适应融合网络整合两个流的特征。论文分别讨论视频动态模型与图像静态模型，具体网络层配置待核实。[论文 §3](https://openaccess.thecvf.com/content_ICCV_2019/papers/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.pdf)

## Key Formulas

待核实：尚未逐式核对原文中的特征提取、上下文注意力、融合权重及训练目标公式。后续记录应保留原文公式编号并解释变量，当前不填写推测公式。

## Datasets and Evaluation Metrics

- CAER：视频情绪识别基准。
- CAER-S：从 CAER 采样的静态图像基准。[作者项目页](https://caer-dataset.github.io/)
- 其他实验数据集、各实验划分、评价指标定义及聚合方式：待核实，尚未逐表整理。

## Experimental Results

论文报告其方法在多个基准上体现了上下文对情绪识别的作用；具体实验设置、消融结果及比较范围待逐表核对。本笔记不填实验数值。[CVF 官方摘要](https://openaccess.thecvf.com/content_ICCV_2019/html/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.html)

## Strengths and Limitations

- 阅读判断：双流结构将表情线索和上下文线索的作用区分得较清楚，适合作为后续融合方法的比较起点。
- 待验证关注点：遮挡人脸、注意力选择与人脸检测质量对静态图像预测的影响。
- 论文明确讨论的局限及适用边界：待精读核实。

## Reproduction Status

状态待确认，尚未提供可验证的环境、训练或评估运行记录，不能据此认定已完成复现。官方实现链接待核实。后续环境、数据准备和运行证据记录在 [CAER-Net 复现笔记](../reproductions/CAER-Net.md)。

## Potential Research Ideas

- 待验证设想：以静态模型为基线，分别测试人物周边局部上下文与整图上下文。
- 待验证设想：固定人脸分支，比较不同上下文选择策略，以分离上下文建模带来的影响。

## Personal Notes

用户自述此前已阅读、讨论本论文；当前仓库没有可核对的逐篇历史笔记，精读程度待确认。此前讨论的具体观点、关键图示理解和未解决问题待补充；本文件不是历史阅读结论的还原。
