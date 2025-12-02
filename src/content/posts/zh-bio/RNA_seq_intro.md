---
title: scRNA-seq全流程分析的笔记
date: 2025-03-01
summary: 对于单细胞RNA-seq及数据分析的介绍
category: 生物统计
tags: [RNA-seq, biology]
---

# RNA-seq Intro

## 测序方法

主流(商业)方法
|角度|Smart-seq2 | 10x |
|---|---|---|
|Number of cells per sample| 96/800 cells | 500-**10000** cells|
|Number of read per cell|100-**1000 million** reads|5000-10000 reads|
|Sequencing|**Full**-length(96 cells)|3'-end|

![sc-seq tech development](https://s2.loli.net/2025/03/01/TjgcHCE5JBfXpan.png 'Svensson, V., Vento-Tormo, R. & Teichmann, S. Exponential scaling of single-cell RNA-seq in the past decade. Nat Protoc 13, 599–604 (2018). https://doi.org/10.1038/nprot.2017.149')

# scRNA-seq data analysis

当前最流行用于分析单细胞数据最全面的R包 [Seurat](https://satijalab.org/seurat/)

Source: [Single-cell best practices](https://www.sc-best-practices.org/preamble.html)

## Workflow

Basic Parts: **Data Pre-processing + Downstream Analysis**

## 1 Pre-processing

Pre-processing Workflow: Quality control -> Clustering & batch correction -> Cell type annotation

### 1.1 Quality Control (QC metrics)

Data acquisition 上游：比对 -> 去重 -> 定量 -> 得到(m genes,n cells)稀疏矩阵

| Gene     | Sample1 | Sample2 | ... |
| -------- | ------- | ------- | --- |
| A1BG     | 30      | 5       | ... |
| A1BG-AS1 | 24      | 10      | ... |
| ...      | ...     | ...     | ... |

筛选细胞general rule: >200 & <2500 检测基因数量 / <5% 线粒体基因比例 / ...

阈值要视情况而定 中位数 +/- n倍标准差

### 1.2 Before Clustering

聚类分析前的处理:

1. Normalize Data 标准化数据
2. Find Variable Features 筛选高变基因
3. Scale Data
4. PCA

#### 1.2.1 Normalization

原因: 不同样本之间文库大小有差异，无法通过基因在不同样本间的表达量来比较表达程度的大小。**测序深度**(测序得到的碱基总量与基因组大小的比值)不同。

技术: **CPM** (counts per million)

$$
log(\text{CPM}+1) = log( \frac{\text{counts of gene}}{\text{total counts of cell}} \times 10^6 + 1 )
$$

Notes: $10^6$: Size factor

#### 1.2.2 Find Variable Features

原因: 找到哪些基因对于细胞的聚类分析最没有用(类似管家基因?) 通过在不同类型细胞间表达量**变异程度高**的基因，这有利于区别细胞

Basic idea: 基于方差排序，选择方差高的基因作为后续分析的基因 HVGs

#### 1.2.3 Scale Data

操作：把 HVGs 在细胞间的表达缩放到均值为0，方差为1的正态分布。

目的：为下游PCA服务；给予每个基因相同的权重

#### 1.2.4 PCA 主成分分析

将 HVGs 的信息继续浓缩得到主要影响的成分，再去除后面的一些主成分(可能是没有生物学意义的一些主成分)

##### Visualization

1. `VizDimLoadings(pbmc, dims = 1:2, reduction = "pca")`

![pca_viz-1](https://s2.loli.net/2025/03/07/GdSF5oTsawWV8qc.png)

此函数显示PCA载荷图，展示:

- 对前两个主成分贡献最大的基因
- 每个基因对主成分的贡献程度（正/负相关）

这有助于理解哪些基因驱动了细胞间的主要变异。

2. `DimPlot(pbmc, reduction = "pca") + NoLegend()`

![pca_viz-2](https://s2.loli.net/2025/03/07/zr5mIXj82pVfZDH.png)

此函数绘制PCA散点图，显示:

- 每个细胞在PCA降维空间中的位置（通常是前两个主成分）
- 细胞之间的相对关系和潜在聚类
- `+ NoLegend()`部分移除了图例以简化视觉效果

这帮助你了解数据中是否存在明显的细胞群体结构。

3. `DimHeatmap(pbmc, dims = 1, cells = 500, balanced = TRUE)`

![heatmap](https://s2.loli.net/2025/03/07/apqNiQFwP4WyGAM.png)

此函数创建热图，展示:

- 第一个主成分的热图表示
- 仅包含500个细胞（随机选择或基于PCA值排序）
- `balanced = TRUE`确保选择在主成分两端的细胞

这可以帮助识别与特定主成分相关的基因表达模式。

### 1.3 Clustering

方法: SNN(shared Nearest Neighbor)
缺点: 基于PCA空间的分簇，簇之间的轮廓不明显

可视化效果：通过非线性降维把几十个PCA空间降维到2个维度。常用方法 t-SNE 和 **UMAP** (前者簇间界限更清晰，后者能展现细胞间状态的连续变化)

### 1.4 Batch correction

批次效应可能导致簇的结果不具有生物学意义。

批次效应严重时，各消除批次效应工具表现不一实际处理数据时，应多尝试不同工具的表现。

### 1.5 Cell type annotation

方法: 手动注释(查阅文献); 自动注释

实际注释时，最好考虑自动+手动

## 2 Downstream Analysis

常用分析方法:

- Differential gene expression
- Trajectory inference
- Cell-Cell communication
- Deconvolution
