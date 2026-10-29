# CLIP-CAER 阅读记录

[返回论文索引](README.md) · [返回研究主页](../readme.md)

## Paper Information

- 正式题名：Context-Aware Academic Emotion Dataset and Benchmark。
- 作者：Luming Zhao、Jingwen Xuan、Jiamin Lou、Yonghui Yu、Wenwu Yang。
- 发表：ICCV 2025，pp. 13859–13868。
- CLIP-CAER 是论文提出的方法名；仓库标题“CLIP-based Context-aware Academic Emotion Recognition”不作为最终正式论文题名。
- 来源：[CVF 官方论文页](https://openaccess.thecvf.com/content/ICCV2025/html/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.html)、[作者项目页](https://zgsfer.github.io/CAER/)、[官方代码](https://github.com/zgsfer/CLIP-CAER)。

## Research Background

真实学习环境中的学业情绪识别缺少公开且场景多样的数据。基本表情类别与学业情绪之间的语义对应并不简单，学习物品、姿态等上下文会影响对学生状态的判断。[论文摘要及引言](https://openaccess.thecvf.com/content/ICCV2025/papers/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.pdf)

## Problem Statement

结合学生的视频面部表情与学习上下文，识别真实学习场景中的学业情绪。原任务包含视频时序信息；不能直接将其结果视为一般静态图像情绪识别结果。[CVF 官方摘要](https://openaccess.thecvf.com/content/ICCV2025/html/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.html)

## Previous Methods and Limitations

论文指出，已有部分学业情绪数据集中于在线学习或刺激诱导场景，真实课堂和自主学习环境的覆盖有限；面向基本情绪的视频表情识别方法，也未充分利用学业场景上下文。具体数据集和比较模型的适用条件待精读核实。[论文引言](https://openaccess.thecvf.com/content/ICCV2025/papers/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.pdf)

## Main Contributions

- 提出 RAER 视频学业情绪数据集，覆盖课堂、图书馆、实验室和宿舍等自然学习环境。
- 为数据提供粗粒度与细粒度两套学业情绪标签。
- 提出 CLIP-CAER，在 CLIP 中使用可学习文本提示整合表情与上下文。[官方论文页](https://openaccess.thecvf.com/content/ICCV2025/html/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.html)、[论文 §2.2](https://openaccess.thecvf.com/content/ICCV2025/papers/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.pdf)

## Method Overview

文本侧将情绪类别对应的表情、学习上下文描述与可学习提示共同输入 CLIP 文本编码器。视觉侧逐帧提取人脸与上下文特征，再通过时序编码模块形成视频表征，最后利用视觉表征与类别文本表征的相似度分类。具体参数冻结策略、采样和时序结构待核实。[官方实现 README](https://github.com/zgsfer/CLIP-CAER)

## Key Formulas

待核实：视觉与文本 token 的构造、时序聚合、相似度计算以及训练目标尚未逐式核对。当前不填写推测公式。

## Datasets and Evaluation Metrics

- 核心数据集：RAER，属于视频学业情绪识别，覆盖真实学习场景。
- 粗粒度标签：engaged、distracted；细粒度标签：enjoyment、neutrality、confusion、fatigue、distraction。[论文 §2.2](https://openaccess.thecvf.com/content/ICCV2025/papers/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.pdf)
- 评价指标定义、类别平均方式、划分及额外实验数据集：待核实，尚未逐表整理。

## Experimental Results

原文报告 CLIP-CAER 在其学业情绪评估中优于所比较的视频表情识别方法，强调学习上下文的作用。具体比较设置、类别表现和消融待逐表核实；本笔记不填实验数值。[CVF 官方摘要](https://openaccess.thecvf.com/content/ICCV2025/html/Zhao_Context-Aware_Academic_Emotion_Dataset_and_Benchmark_ICCV_2025_paper.html)

## Strengths and Limitations

- 阅读判断：类别文本描述为表情与学习行为提供了可检查的语义接口。
- 已核实的范围：数据和方法围绕视频中的学业情绪，不能直接推断其在静态图像或一般公众情绪场景中的效果。[作者项目页](https://zgsfer.github.io/CAER/)
- 待验证关注点：移除时序信息、改变学习场景或修改文本描述时的预测变化。

## Reproduction Status

官方代码链接已核实；本地环境、权重运行、数据准备与评估状态待确认，尚未提供可验证运行记录。未完成静态图像迁移验证，不能将视频基准结果当作迁移结果。

## Potential Research Ideas

- 待验证设想：将单帧作为输入，与相同数据划分下的视频输入比较，测量时序信息的作用。
- 待验证设想：在明确标签含义和目标任务后，测试面向静态图像的上下文提示；该迁移不是论文已验证结论。

## Personal Notes

用户自述此前已阅读、讨论本论文；当前仓库没有可核对的逐篇历史笔记，精读程度待确认。后续应分别记录学业情绪、基本情绪及一般图像情感任务的区别，避免混用数据集和指标。
