# Tactile-Slip-Detection-Benchmark

**基于高密度磁触觉阵列的灵巧手感知：多时空深度学习架构对比研究**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/)
[![Dataset](https://img.shields.io/badge/Dataset-Let's_DENSE-green.svg)](https://zenodo.org/records/17336134)

本仓库是论文《基于高密度磁触觉阵列的灵巧手感知：多时空深度学习架构与序列长度的对比研究》的官方代码实现。本项目面向机器人多指灵巧手的高频闭环控制需求，全面实现了基于 1D-CNN、LSTM、Temporal Transformer 与 ST-GCN 的四种多时空深度学习感知架构，并提供了完整的模型训练、评估脚本及预训练权重。

## 核心亮点 (Features)

- **多架构深度消融**：横向对比了空间特征（ST-GCN）、时序记忆（LSTM）、全局注意力（Transformer）与轻量化卷积（1D-CNN）在触觉感知中的底层机制差异。
- **序列长度物理验证**：通过严格的 $W \in \{5, 10, 15, 20\}$ 帧时间窗口消融实验，揭示了微观纹理识别对“粘滞-滑移”完整周期（约 150 ms）的物理依赖。
- **极速边缘侧部署**：经过算力与延迟帕累托权衡，最终确立的 `1D-CNN (W=15)` 方案在双任务中维持 99.3%+ 精度的同时，实现了 **0.470 ms** 的极低推理延迟，完美支持百赫兹级硬件闭环控制。
- **拓扑感知突破**：引入物理节点图邻接矩阵的 `ST-GCN (W=10)` 模型在材质分类任务上实现了高达 **99.80%** 的断层式精度领先。

## 性能基准 (Benchmarks)

在 Let's DENSE 数据集上的多任务综合评估（最佳配置，Batch Size = 1）：

| 网络架构        | 最优序列长度 ($W$) | 滑移检测准确率 (%) | 材质分类准确率 (%) | 单次推理延迟 (ms) | 模型特点与部署优势                          |
| :-------------- | :----------------: | :----------------: | :----------------: | :---------------: | :------------------------------------------ |
| **1D-CNN**      |         15         |       99.32        |       99.51        |     **0.470**     | 计算极简，极低延迟，适合严苛实时系统        |
| **LSTM**        |         15         |       99.52        |       99.57        |       0.660       | 流式推理稳定，引入 `BatchNorm` 解决模式崩溃 |
| **Transformer** |         5          |     **99.52**      |       99.30        |       1.605       | 极短序列强表征，抗长时序静态噪声能力优异    |
| **ST-GCN**      |         10         |       99.28        |     **99.80**      |       1.753       | 空间物理拓扑建模，微观纹理分类精度极高      |

*(注：详细的混淆矩阵与帕累托权衡图请见 `figures/` 目录)*

## 仓库结构 (Repository Structure)

```text
Tactile-Slip-Detection-Benchmark
 ┣ 📂 data                  # 数据集相关说明与预处理脚本
 ┣ 📂 figures               # 论文中用到的所有高清图表
 ┣ 📂 paper                 # 学术论文草稿 (Markdown/PDF 格式)
 ┗ 📜 README.md
```
