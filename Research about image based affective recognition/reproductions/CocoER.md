# CocoER · 复现记录

[返回复现索引](README.md) · [论文阅读记录](../papers/CocoER.md)

## Project Overview

CocoER 探索多层级特征间的竞争与协调。原论文：[CocoER: Aligning Multi-Level Feature by Competition and Coordination for Emotion Recognition, CVPR 2025](https://openaccess.thecvf.com/content/CVPR2025/html/Shen_CocoER_Aligning_Multi-Level_Feature_by__Competition_and_Coordination_for_CVPR_2025_paper.html)。

已核实官方代码：[bisno/CocoER](https://github.com/bisno/CocoER)。历史实际使用的代码 commit、分支、修改及其与官方实现的差异待补充；官方仓库存在不代表本地已复现。

## Reproduction Objective

计划先整理历史代码运行证据，再按原论文的数据集和指标协议建立可追溯基线，供人物/上下文贡献等后续实验使用。推理、评估与重新训练分别登记。

## Environment

| 项目 | 该模型的已确认配置 | 待补证据 |
| --- | --- | --- |
| Python | 待核实 | 实际版本或环境导出 |
| PyTorch | 待核实 | 实际版本与对应安装来源 |
| CUDA / 驱动 | 待核实 | runtime、驱动与设备对应关系 |
| 操作系统 | 待核实 | Windows / AutoDL Linux 与具体运行对应 |
| CPU / GPU / 显存 | 待核实 | 设备型号、显存与运行设备 |

用户说明曾使用 Windows 与 AutoDL Linux；一次服务器配置为 Python 3.12 / PyTorch 2.5.1 / CUDA 12.4。尚未确认该配置属于哪次 CocoER 工作，也未验证兼容性。

## Installation

待结合[官方仓库](https://github.com/bisno/CocoER)的具体 commit 与历史依赖记录核实安装步骤。当前目标仓库没有 CocoER 专属环境清单或已验证安装命令，不能据历史服务器版本生成通用安装指令。

```bash
# 待补充：该源码版本的环境创建与依赖安装命令，以及实际执行记录。
```

本次未安装依赖，也未修改运行配置。

## Model Weights

官方权重发布情况、历史权重来源、文件校验值、适用数据集与代码版本待核实。本次未下载权重，不能将“官方代码已公开”记为“权重已就绪”。

## Inference

待补历史脚本、配置、输入裁剪/预处理、权重路径、标签映射及完整命令。当前没有本仓库内可核实的成功推理日志，不假定训练脚本可直接用于推理。

## Dataset

原论文实验涉及 EMOTIC 与 CAER-S，见[论文原文 §4.1–4.2](https://openaccess.thecvf.com/content/CVPR2025/papers/Shen_CocoER_Aligning_Multi-Level_Feature_by__Competition_and_Coordination_for_CVPR_2025_paper.pdf)。实际使用的数据版本、划分、人头/身体/上下文裁剪、标签映射及访问条件待核实。本次未获取数据。

## Evaluation

原论文在 EMOTIC 使用 AP/mAP，在 CAER-S 使用 accuracy；具体任务设置和计算协议仍需逐项核对。论文结果和个人复现结果分开记录，不混用多标签与单标签指标。

| 数据集/划分 | 指标及协议 | 论文值及出处 | 本地结果 | 原始日志/配置 |
| --- | --- | --- | --- | --- |
| EMOTIC，划分待核实 | AP/mAP；具体协议待核实 | 待补充 | — | 待补充 |
| CAER-S，划分待核实 | Accuracy；具体协议待核实 | 待补充 | — | 待补充 |

“—”表示无已核验结果，不代表数值为零。

## Problems Encountered

暂无本仓库内可核实的运行报错及修复记录。后续按原始报错、命令、原因、处理和复测结果补充，不能将版本差异猜测写成已定位问题。

## Reproduction Status

- 历史工作：用户说明曾开展代码复现相关工作。
- 仓库证据：版本 `8e32e2f` 未见 CocoER 专属源码、环境清单或运行日志。
- 代码获取、环境配置、权重、推理、评估、训练及论文结果对齐：**均待核实**。本次未执行这些阶段。

## Next Steps

1. 补历史源码位置、commit 和改动说明，确认与官方实现的对应关系。
2. 提供各次 Windows / AutoDL 运行的环境、命令、原始日志和已知问题。
3. 核对实际数据划分与权重，再确定后续是补推理、评估还是训练；每阶段独立记录证据。
