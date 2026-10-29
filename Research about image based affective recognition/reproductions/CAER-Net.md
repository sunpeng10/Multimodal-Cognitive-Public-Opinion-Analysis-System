# CAER-Net · 复现记录

[返回复现索引](README.md) · [论文阅读记录](../papers/CAER-Net.md)

## Project Overview

CAER-Net 研究人脸与场景上下文的联合情绪识别。原论文：[Context-Aware Emotion Recognition Networks, ICCV 2019](https://openaccess.thecvf.com/content_ICCV_2019/html/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.html)；[作者项目页](https://caer-dataset.github.io/)。

官方 GitHub 地址：**待核实**。不把检索到的第三方实现自动标为官方；历史使用的实现来源和 commit 待补充。

## Reproduction Objective

计划先核验历史代码的来源与推理状态，再确认能否按原论文协议评估静态图像任务。达到何种复现目标（运行推理/重评估/重新训练）需分别记录。

## Environment

| 项目 | 该模型的已确认配置 | 待补证据 |
| --- | --- | --- |
| Python | 待核实 | 版本输出或环境导出 |
| PyTorch | 待核实 | 实际安装版本 |
| CUDA / 驱动 | 待核实 | CUDA runtime 与驱动分别记录 |
| 操作系统 | 待核实 | Windows / AutoDL Linux 与该次运行的对应关系 |
| CPU / GPU / 显存 | 待核实 | 设备型号、显存和运行设备 |

用户说明曾使用 Windows 与 AutoDL Linux；另有 Python 3.12 / PyTorch 2.5.1 / CUDA 12.4 的历史服务器配置，但尚无证据证明它属于 CAER-Net 的运行环境。

## Installation

待核实：实现来源、依赖文件、版本约束与平台兼容性。当前仓库没有 CAER-Net 专属安装记录，不能提供声称可运行的安装命令。

```bash
# 待补充：经核实的环境创建命令及依赖安装命令，注明平台与源码 commit。
```

本次未执行环境创建或依赖安装。

## Model Weights

权重来源、对应代码版本、文件校验值、是否为预训练/自行训练：均待核实。未获取权重。

## Inference

历史推理脚本、输入预处理、人脸框来源、配置、权重路径、标签顺序及实际命令待补充。当前没有可核实的本地成功推理记录，不编写假定入口命令。

## Dataset

原论文的 CAER 与静态图像 CAER-S 参见[作者项目页](https://caer-dataset.github.io/)。实际复现所用数据集、版本、划分文件、人脸裁剪与预处理均待核实，不能将视频与静态图像协议混用。

## Evaluation

待补充实际协议、指标定义、脚本版本及原始日志；论文指标数值与本地结果分别登记。

| 数据集/划分 | 指标及计算协议 | 论文值及出处 | 本地结果 | 日志/配置 |
| --- | --- | --- | --- | --- |
| 待核实 | 待核实 | 待补充 | — | 待补充 |

“—”表示无已核验结果，不代表数值为零。

## Problems Encountered

暂无可核实的报错或解决记录。后续记录原始报错、复现命令、原因、修改及验证结果；不把潜在兼容风险写成已发生故障。

## Reproduction Status

- 历史工作：用户说明曾开展代码复现相关工作。
- 仓库证据：版本 `8e32e2f` 未见 CAER-Net 专属实现、环境或日志。
- 源码就绪、环境可用、推理、评估、训练及论文结果对齐：**均待核实**；本次只补文档。

## Next Steps

1. 补历史代码地址/commit、来源性质和已修改内容。
2. 提供与该模型绑定的环境导出、实际命令及原始运行日志。
3. 核对数据划分、权重和预处理后，登记已完成阶段与尚未解决的问题。
