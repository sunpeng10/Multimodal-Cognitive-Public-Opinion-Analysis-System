# CAER-Net-S 单图推理与可视化前端验证报告

[返回实验索引](README.md) · [模型复现记录](../reproductions/CAER-Net.md) · [论文阅读记录](../papers/CAER-Net.md) · [研究主页](../readme.md)

> 已完成并留有证据的是：真实公开权重的严格加载、CPU 单图推理、模型内部可视化及 Gradio 前端功能验证。没有进行 CAER-S 数据集性能评估或重新训练，不能据此声称复现了论文准确率。

## 1. Experiment ID

- 记录编号：`CAERS-FRONTEND-001`（本次归档编号）。
- 类型：模型推理复现与前端工程验证，不是方法性能对比实验。
- 对象：CAER-Net-S 静态图像版的**第三方 PyTorch 实现**，不包含视频版 CAER-Net 的完整官方复现。
- 本地工程：`D:\CAER-Net`；本仓库只收录整合报告，截图、原始 JSON、原报告、开发源码、权重、虚拟环境和数据集均未随本次推送上传。仅克隆本仓库不能直接启动该本地前端。
- 来源聊天：**复现 CAER-Net-S 并开发前端**。本次读取原聊天历史，并交叉核对本地报告、源码、环境元数据和已有输出；未将聊天中的计划直接写成完成项。

## 2. Experiment Date

| 阶段 | 日期（Asia/Shanghai） | 依据 |
| --- | --- | --- |
| 初始推理复现与 Dashboard 记录 | 2026-10-23 | 初始复现报告快照（本地证据 E1） |
| 奶油色双页面工作空间重构与验收 | 2026-10-30 | 前端交付报告快照（本地证据 E2）、原聊天 |
| 本次核验与 GitHub 文档归档 | 2026-10-31 | 核验清单及文件 SHA256（本地证据 E0） |

本次仅整理已有材料，没有重新启动前端、运行推理/测试、安装依赖或训练。历史服务地址不代表服务目前仍在线。

## 3. Research Question

能否在 Windows 本地、不依赖官方数据集目录的条件下，使用原有 CAERSNet 和指定公开 checkpoint 完成单图推理，并通过前端检查 Face、Masked Context、空间注意力、融合权重和分类输出？

这一阶段建立后续研究的操作与检查入口，不回答“上下文是否提升准确率”“是否跨域泛化”等性能问题。

## 4. Hypothesis

工程验收假设：若权重与原模型完整匹配，预处理与上游静态图像路径一致，且前端展示真实推理输出，则应能完成上传、目标人脸选择、CPU 推理、可视化及结果导出。

对应检查是参数匹配、张量形状、概率/权重归一化、回调接线与状态清理；不能以单张图的类别或高 Softmax 值判定识别性能。

## 5. Baseline

- 原论文：[Context-Aware Emotion Recognition Networks，ICCV 2019](https://openaccess.thecvf.com/content_ICCV_2019/html/Lee_Context-Aware_Emotion_Recognition_Networks_ICCV_2019_paper.html)。
- 实际实现：[ndkhanh360/CAER](https://github.com/ndkhanh360/CAER)，属于第三方实现。
- 上游 commit：[`93d25828ce2ea050fb379d85258ba3fdbf59d2a6`](https://github.com/ndkhanh360/CAER/tree/93d25828ce2ea050fb379d85258ba3fdbf59d2a6)。本次只读核对 commit 一致，上游工作树干净。
- 模型类：`CAERSNet`；本地使用独立推理和展示模块，没有以新网络替换原模型。
- 没有训练或评估新的对照模型，不能称为已完成 baseline 性能复现。

## 6. Dataset and Split

- 没有下载或使用 CAER/CAER-S 的完整训练、验证、测试划分。
- 初始文件链路验证使用本地生成的 `320×240` PNG 与固定手动人脸框；对应原始推理 JSON（本地证据 E4）。该图没有情绪真值。
- 前端完整流程使用本机 Matplotlib 自带 `grace_hopper.jpg`；工作台样例为 `512×600` 图像，对应原始工作台 JSON（本地证据 E5）。双人检测测试使用该样例的横向拼接，不是新采集的多人数据集。
- 样例只用于输入处理、检测、选框、推理与导出检查，没有建立带情绪真值的评测集，也没有样本级准确率统计。

## 7. Environment

以下以原任务报告和本次只读文件核验为依据；设备型号与内存等未留存项目不作推断。

| 项目 | 已记录/核验的配置 | 证据范围 |
| --- | --- | --- |
| 操作系统 | Windows | 本地工程与原报告 |
| Python | 3.10.11，独立 `.venv` | `.venv/pyvenv.cfg`，禁用全局 site-packages 继承 |
| PyTorch / torchvision | 2.4.1+cpu / 0.19.1+cpu | 历史报告、本地包元数据 |
| Gradio | 5.49.1 | 历史报告、本地包元数据 |
| NumPy / OpenCV | 1.26.4 / 4.11.0.86 | 本地包元数据、依赖文件 |
| Pillow | 依赖文件和 `PIL/_version.py` 均为 11.3.0 | 另存在 12.3.0 的重复包元数据，见限制 |
| 推理设备 / CUDA | 历史验收为 CPU；原报告记录 CUDA 不可用 | 推理 JSON 的 `device=cpu`；本次不重新探测 CUDA |

原依赖文件快照（本地证据 E3）保留历史锁定配置；核验清单（本地证据 E0）单列本次观察。不要把其他 AutoDL 项目的 Python/PyTorch/CUDA 配置套用到本记录。

## 8. Experimental Settings

### 权重与加载

- 来源：第三方仓库 README 指向的[公开 Google Drive 文件](https://drive.google.com/file/d/1HxHZQmWnXbhYV0_HU2q-2fcC3twtGJZp/view)。
- 文件：`weights/caers.pth`，大小 **19,171,379 字节**。
- SHA256：`45E58E7D93852089361C396B287949FA63EBF39567745B0F863F6D07DD7BCA9A`，本次重新计算文件哈希，与既有记录一致。
- checkpoint 记录：`arch=CAERSNet`、`epoch=61`、106 个 state-dict 键；`strict_load=true`，missing/unexpected keys 均为空。`epoch=61` 是上游 checkpoint 字段，不是本人训练轮数。
- 原加载器为固定 SHA 的已知 legacy checkpoint 保留兼容读取路径，最终使用 `strict=True`；这不表示可任意加载其他 pickle 权重。

### 输入与真实中间量

1. 自动人脸检测采用 OpenCV Haar；多人脸必须选择目标，检测失败时提供手动框。支持原图像素坐标与两点选框。
2. Face：从原始 RGB 图像按框裁剪，Resize 至 `96×96`。
3. Context：在原图遮黑人脸，Resize 至高 128、宽 171，再 CenterCrop 为 `112×112`。
4. 两路均使用 ImageNet mean `(0.485, 0.456, 0.406)` 和 std `(0.229, 0.224, 0.225)`；本次已核对上游变换与本地预处理源码。
5. 推理路径使用 `model.eval()` 和 `torch.inference_mode()`；预览中的网格、刻度和人脸框不进入模型输入。
6. 通过原模型 hooks 捕获上下文注意力及融合 logits，按原 forward 的 softmax 规则还原空间注意力与 Face/Context 权重，不使用随机可视化填充。

类别顺序为 `Angry, Disgust, Fear, Happy, Neutral, Sad, Surprise`。Attention 是内部空间注意力，不是 Grad-CAM 或经过因果验证的解释；融合权重也不是经消融测得的“人脸/场景贡献百分比”。

### 前端实现与本地入口

当前版本采用 **Gradio Blocks + 自定义 HTML/SVG/CSS**，奶油米杏色、白色与珊瑚橙风格。原深色 Dashboard 是早期版本，不能与最新界面混写。

- 首页概览、图像分析、运行日志、结果导出四个导航入口；核心页面是 Dashboard 与三列分析工作台。
- 三列依次展示输入及人脸定位、Face/Context 与注意力、七类情绪输出。原始 logits、JSON、耗时和融合权重可进一步查看。
- 页面切换保留当前图像、选框与预测；换图或开始新分析时清除旧结果和当前导出链接，避免旧结果被当成新图结果。
- 首页统计来自已留存的本地分析/导出事件，重复分析也会计次；趋势可按 7/30/90 天筛选。这些是运行记录统计，不是准确率或独立评测样本数。
- 支持 JSON、五联分析图及完整 ZIP；ZIP 含 `original.png`、`face_crop.png`、`masked_context.png`、`attention.png`、`overlay.png`、`prediction.json`、`analysis.png`。

实现文件包括 `app.py`、`workspace_ui.py`、`ui_components.py`、`style.css`、`local_history.py` 及推理/可视化模块。它们仍位于本地工程，没有在本次文档上传中迁入系统仓库。

在**已具备原本地工程及环境**的电脑上，可双击 `D:\CAER-Net\start_test.bat`，或使用：

```powershell
Set-Location D:\CAER-Net
.\.venv\Scripts\python.exe app.py --device cpu --port 7861
```

历史启动入口为 `http://localhost:7861`，监听 `127.0.0.1`，`share=False`。端口曾从 7860 调整为 7861 以避免与另一项目冲突；本次没有启动或停止任何服务。

## 9. Evaluation Metrics

本阶段检查：权重严格匹配、七类 logits、概率和近似 1、Face/Context 尺寸、空间注意力归一化、融合权重和近似 1、回调与导出、页面状态及水平溢出。

**没有 Accuracy、F1、Recall、mAP 等数据集性能结果。** 单图 Softmax 值不是识别正确率；单次耗时也不是经重复测量和硬件控制得到的速度基准。

## 10. Results

### 已有证据与验证结论

| 检查项 | 历史结果/本次核验 | 可核查证据 | 能证明的范围 |
| --- | --- | --- | --- |
| 源码版本与权重身份 | commit 一致、上游工作树干净；大小和 SHA 一致 | 核验清单（本地证据 E0） | 本次归档时的来源与文件身份 |
| 真实权重严格加载 | 106 键；missing/unexpected 均为空 | 合成图 JSON（本地证据 E4）、工作台 JSON（本地证据 E5） | 已有两次输出记录的加载状态 |
| 单图与前端完整流程 | CPU 推理、真实 attention/fusion、选框和三类导出已有验证 | 两份原始报告、原聊天、输出文件 | 历史运行链路可用，不证明分类正确 |
| 自动化回归 | 原交付报告记载 `54 passed in 27.16s`；原聊天对应命令退出码 0 | 前端报告（本地证据 E2）、历史命令定位（本地证据 E0） | 历史测试结果，本次未重跑 |
| 桌面布局 | 两页面在 1920×1080、1600×900、1366×768 均记录无水平溢出 | 六组视口测量（本地证据 E6） | 当时内置 Chromium、约 100% 缩放的测量 |

### 两份已有推理记录

| 输入/用途 | Top-1 模型输出 | Softmax 值 | Face 融合权重 | Context 融合权重 |
| --- | --- | --- | --- | --- |
| 生成 PNG，验证文件链路 | Neutral | 0.933575 | 0.039121 | 0.960879 |
| Matplotlib 本地样例，验证工作台与导出 | Surprise | 0.952837 | 0.929704 | 0.070296 |

数值直接摘自本地原始 JSON（E4、E5），表中作了小数舍入。两份记录均没有情绪真值，不能判断预测正确与否；也不是同一图像的受控对照。

### 已留存的界面截图（仅本地）

**首页可见区域预览**：统计数字是截图时已留存的运行事件，含验收样例和重复分析，不是实验性能指标。

本地截图：`outputs/ui_review/dashboard_1600x900.jpg`（E7，未随报告上传）。

**工作台阶段截图**：来自真实样例推理，之后又修正了图片工具栏大小及按钮样式。本图保留阶段证据，不代表最后一轮工具栏样式，也不是本次重新截图。

本地截图：`outputs/ui_review/analysis_real_result_stage.jpg`（E8，未随报告上传）。

## 11. Ablation Study

未进行模型消融。没有 Face-only、Context-only、去注意力、固定融合或跨数据集对照结果。前端重构与功能测试不构成模型方法的消融实验。

## 12. Observations

- 原 checkpoint 可在兼容加载路径下与 CAERSNet 严格匹配，已有 CPU 推理输出包含七类 logits 和真实中间量。
- 上下文注意力只对应模型所见的裁剪 Context；不能把插值热图当成原图每个像素的因果贡献。
- 前端状态清理与结果关联对研究记录可靠性有直接影响：新图必须清空旧预测、热图和下载链接。
- 初始复现报告只记录了合成图链路；后续前端报告和现存导出补充了本地照片样例。不能把早期“只有合成图”的说明当作后续阶段的完整状态。

## 13. Limitations

1. 未训练模型、未按 CAER-S 标准划分评估，尚无论文性能复现、泛化或新方法有效性结论。
2. 自动 Haar 人脸框与原数据标注可能不同；检测误差会改变两路输入，研究比较需固定人脸框和预处理。
3. 原聊天与报告给出历史测试结果；未发现独立保存的完整 pytest stdout 日志，因此保留来源定位，不将其描述为本次重新通过的测试。
4. 本地环境同时存在 Pillow 11.3.0、12.3.0 的 `.dist-info`；依赖锁定与 `PIL/_version.py` 声明为 11.3.0。元数据有歧义，不能声称已验证当前环境完全一致；本次未安装、修复或重测环境。
5. Edge 原生窗口控制当时授权超时，不能把内置 Chromium 验收写成 Edge 实测。最后一轮工作台截图工具报错，故明确保留阶段截图。
6. 本地前端源码及原始附件尚未随本报告上传，无法仅凭本仓库从零重建前端；当前交付是研究记录与证据，不是完整可分发应用包。

## 14. Conclusion

现有材料支持将本阶段登记为：**CAER-Net-S 第三方静态图像实现的真实权重单图推理与 Gradio 前端工程验证已完成并有留存记录**。本次还核对了源码版本、权重身份、关键预处理、环境元数据及原始输出。

这满足建立可操作研究入口的阶段目标；不代表完成视频版官方复现、数据集性能复现、注意力因果解释或模型创新验证。

## 15. Next Experiment

1. 核查并整理本地环境一致性；若后续需要重新验收，单独保存完整命令、环境导出和 stdout 日志。
2. 按明确授权与数据访问条件确定标准评测协议，固定数据划分、人脸框、标签顺序和预处理，再报告真实指标。
3. 在可追溯 baseline 上分别设计人物/上下文、注意力与融合消融；预先写明对照、指标和计算预算。
4. 如需要发布可运行前端，另行整理源码版本和授权说明；补最终工作台截图及必要的浏览器实测，不将当前文档上传等同于应用发布。

### 本地证据清单

以下材料已只读核对，但未随本次推送上传。正文的 E 编号指向此表；表中路径相对于 `D:\CAER-Net`，SHA256 为原文件哈希。E0 为本次本地核验清单，记录读取日期、来源聊天、上游 commit、权重身份与附件哈希。

| 编号 | 本地原始文件 | SHA256 |
| --- | --- | --- |
| E1 | `REPRODUCTION_REPORT.md` | `94d18ced971e95a01926887d3484b44c4defe391bd22d7bffceba8cfdcadddd2` |
| E2 | `FRONTEND_REFACTOR_REPORT.md` | `6cb61d109979877bbbc50cd8149a3d7fcf9f656859aab776a8a4126854290141` |
| E3 | `requirements-local.txt` | `b6d1e947067b914193997e65d995eea7d959843d46953f255c238929cd776368` |
| E4 | `outputs/final_cli/json/caers_20261023_152545_647839.json` | `ef3f673b831f6df1db52dd57129030128893f341587f64d22749aa2fb9339170` |
| E5 | `outputs/bundles/caers_20261030_102349_740884/prediction.json` | `58929079c798ea6d06d98018bcd463327afe95089c13d9c38e83e6de3ef3ed08` |
| E6 | `outputs/ui_review/viewport_checks.json` | `14f57e1603255e70f38849061d42e630bde2c62f04a92d4bcd04f70ecf1ad60b` |
| E7 | `outputs/ui_review/dashboard_1600x900.jpg` | `d673da92ed50b1041a24cb17133a9d17ead0620ab45e30561ff89cd010a0dc4d` |
| E8 | `outputs/ui_review/analysis_real_result_stage.jpg` | `0b6177f86d48892b13d5fb3aae9913d9721ec8e57141ce04fd82d36e524e4c75` |

原始报告保留各自日期和历史语境；本报告整合其阶段差异。截图、推理 JSON、依赖文件和历史报告仅在本地留存，本次 GitHub 变更不含附件。
