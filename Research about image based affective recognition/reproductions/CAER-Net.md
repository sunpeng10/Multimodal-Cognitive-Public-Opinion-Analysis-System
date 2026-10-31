# CAER-Net · 复现记录

[返回复现索引](README.md) · [论文阅读记录](../papers/CAER-Net.md)

> 2026-10-31 更新：已读取原聊天与 `D:\CAER-Net` 中的材料，确认存在 CAER-Net-S 静态图像版第三方实现的推理和前端验证记录。完整来源、环境差异及原始 JSON/阶段截图的本地位置见[工程验证报告](../experiments/CAER-Net-S-Frontend.md)。没有标准数据集性能评估或训练结果。

## Project Overview

CAER-Net 研究人脸与场景上下文的联合情绪识别。原论文：[Context-Aware Emotion Recognition Networks, ICCV 2019](https://openaccess.thecvf.com/content_ICCV_2019/html/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.html)；[作者项目页](https://caer-dataset.github.io/)。

本次实际使用 [ndkhanh360/CAER](https://github.com/ndkhanh360/CAER) 的第三方实现，commit 为 `93d25828ce2ea050fb379d85258ba3fdbf59d2a6`，已只读核对本地上游工作树干净。官方 GitHub 地址仍待核实，不能将该实现称为作者官方代码或完整视频版复现。

## Reproduction Objective

已核对历史单图推理与前端工程验证。下一阶段再确认能否按原论文协议评估静态图像任务；推理、数据集评估、重新训练分别记录。

## Environment

| 项目 | 该模型的已确认配置 | 待补证据 |
| --- | --- | --- |
| Python | 3.10.11，独立 `.venv` | 本地 pyvenv.cfg 与原报告 |
| PyTorch | 2.4.1+cpu；torchvision 0.19.1+cpu | 本地包元数据与原报告 |
| CUDA / 驱动 | 历史验收为 CPU；原报告 CUDA 不可用 | 本次未重测 CUDA，驱动待补 |
| 操作系统 | Windows | 本地工程与原报告 |
| CPU / GPU / 显存 | CPU 推理有记录；具体硬件待补 | 已有推理 JSON |

Gradio 5.49.1。依赖快照与 Pillow 重复元数据问题见[完整环境说明](../experiments/CAER-Net-S-Frontend.md)。此前提及的 AutoDL Python 3.12 / PyTorch 2.5.1 / CUDA 12.4 不用于本次已确认的 Windows CPU 记录。

## Installation

原本地工程已有环境；本地 `requirements-local.txt` 和 `REPRODUCTION_REPORT.md` 已核对，来源见[工程报告](../experiments/CAER-Net-S-Frontend.md)。尚未在另一台机器重新验证从零安装流程，保留环境元数据一致性待核查项。

```bash
# 环境重建步骤参见原本地 README；本次不执行安装，不宣称跨机器安装已验证。
```

本次未执行环境创建或依赖安装。

## Model Weights

已核对第三方仓库指向的公开 `caers.pth`：19,171,379 字节，SHA256 为 `45E58E7D93852089361C396B287949FA63EBF39567745B0F863F6D07DD7BCA9A`。已有 JSON 记录 `strict_load=true`、106 键、无 missing/unexpected keys。是上游预训练权重，不是本人训练；本次未重新下载或加载。

## Inference

已有 CPU 单图推理 JSON、`infer_image.py` 和 Gradio 回调验证记录。Face 为 96×96；遮黑人脸的 Context 经 Resize 后 CenterCrop 为 112×112；使用 ImageNet Normalize。自动 Haar 检测与手动框两种入口、七类顺序、启动命令见[工程验证报告](../experiments/CAER-Net-S-Frontend.md)。

## Dataset

原论文的 CAER 与静态图像 CAER-S 参见[作者项目页](https://caer-dataset.github.io/)。本地工程没有下载完整数据集；历史链路验证使用生成 PNG 与 Matplotlib 自带照片，均无情绪真值。没有标准数据划分评估结果。

## Evaluation

已归档工程验证结果，不填数据集性能指标。后续仍需补标准评估协议、数据划分、指标定义和原始评估日志；论文结果与个人结果分开登记。

| 数据集/划分 | 指标及计算协议 | 论文值及出处 | 本地结果 | 日志/配置 |
| --- | --- | --- | --- | --- |
| 待核实 | 待核实 | 待补充 | — | 待补充 |

“—”表示无已核验结果，不代表数值为零。

## Problems Encountered

已记录 legacy checkpoint 兼容、端口冲突、换图旧结果清理、Gradio 样式冲突和最终截图工具失败等历史问题，见[工程验证报告](../experiments/CAER-Net-S-Frontend.md)。本次另观察到 Pillow 重复包元数据，尚未修复或重测环境。

## Reproduction Status

- 已有证据：第三方静态图像实现、真实权重严格加载、CPU 单图推理、真实中间量展示和前端/导出验证。
- 原前端报告记录 54 项测试通过；本次未重跑，完整 stdout 未单独留存。
- 未完成范围：标准数据集性能评估、重新训练、论文指标对齐、视频版复现，以及可分发前端源码归档。

## Next Steps

1. 核查环境一致性，下一次验收保留完整命令与 stdout 日志。
2. 明确数据访问条件、标准划分与人脸框协议，再开展数据集评估。
3. 按[实验记录](../experiments/CAER-Net-S-Frontend.md)中的后续计划设计受控消融，区分工程验证与科研结论。
