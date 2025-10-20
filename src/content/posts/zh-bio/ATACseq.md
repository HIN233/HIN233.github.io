---
title: scATAC-seq全流程分析的笔记
date: 2025-06-29
summary: 对于单细胞ATAC-seq及数据分析的介绍
category: 生物统计
tags: [RNA-seq, biology]
---

# scATAC-seq Intro

## 什么是ATAC-seq

Tn5 transposome 会将开放的染色质切割成小段，我们对这些小片段进行测序就知道基因组哪些片段是开放的。相对于同期其他染色质水平的测序，ATAC-seq所需的细胞数量更少，准备时间更短，信号强度高，噪音更小，可重复性强，操作更简单。近年来非常流行，可以帮助我们研究未知的基因活动。

现在常用的 ATAC-seq 测序方法是10X Genomics Chromium Single Cell ATAC

## ATAC-seq 的流程

整体结构和RNA-seq类似，分为数据预处理和下游分析两部分。数据处理主要是：建库测序，QC，构建矩阵，整合降维，聚类，注释。

### 和 RNA-seq 区别

- 高纬度：特征按照区段（元件）定义名字
- 高噪音
- 非常稀疏：基因组的数量少（一个细胞2份，而转录组的量可以很大
- 缺乏先验知识

### Pre-processing

- Demultiplexing 将测序的原始文件转化成FASTQ文件: bcl2fastq
- Adaptor Trimming 去除接头序列 : AdapterRemoval/Trimmomatic
- Alignment 比对到参考基因组: Bowtie2/BWA/STAR

整套数据处理流程（商业化）

- 10X Genomics: Cell Ranger ATAC

### Quality Control

主要是控制两个指标：一个是质量不好的细胞，一个是质量不好的片段。

下图是常见的一个细胞质量控制指标图，横轴是 Fragment 的数量，一般选取1k以上，纵轴是信噪比 (TSS enrichment Score) 的分布。其次还要去除双细胞 doublets。

![QC.png](https://s2.loli.net/2025/06/30/Ui2rOl8gaPDw6Ld.png)

去除 doublets 的方法有很多，例如 ArchR: 先构建一些模拟的 doublets ，计算enrichment scoure，然后和正常的细胞一起聚类，和这些细胞相近的细胞就很可能可以被认为是 doublets。

对于片段的质量控制，主要是去除黑名单（重复但是没有明显生物学意义的）片段 ENCODE **blacklist** regions。

### Martrix formation

构建 Cell-by-feature 矩阵: 每一列代表一个细胞，每一行代表一个基因组区段（元件），矩阵中的值表示该细胞在该区段的开放程度。
定义元件和计数的方式基本有两种: Peaks 和 Bins。一个是基于峰值的计数，另一个是基于等距划分的区段的计数。

### Normalization

现在常用的是 TF-IDF (Term Frequency-Inverse Document Frequency) 方法。TF-IDF 是一种常用的NLP文本挖掘方法，用于评估一个词在文档中的重要性。对于 ATAC-seq 数据，TF-IDF 可以帮助我们更好地理解每个细胞在不同基因组区段的开放程度。
把一个细胞当作一个文档，基因组区段当作词，TF-IDF 就是计算每个词在语料库中的重要程度。

TF-IDF 的计算公式如下：
\[
\text{tf_idf_i} = \text{tf_i} \times \text{idf_i}
\]
其中，
\[
\text{tf}_{i,j} = \frac{n_{i,j}}{\sum*k n*{k,j}}
\]

- \( n\_{i,j} \)：词 \( t_i \) 在文档 \( j \) 中的出现次数。
- \( \sum*k n*{k,j} \)：文档 \( j \) 中所有词的出现次数之和。

\[
\text{idf}\_i = \log \frac{|D|}{|\{j: t_i \in d_j\}|}
\]

- \( |D| \)：文档集合中的文档总数。
- \( |\{j | t_i \in d_j\}| \)：包含词 \( t_i \) 的文档数量。

对于TF-IDF重要的词，赋予更高的权重，这样我们成为 Normalization

### Feature Selection

> The low dynamic range of scATAC-seq data makes it challenging to perform variable feature selection, as we do for scRNA-seq. Instead, we can choose to use only the top n% of features (peaks) for dimensional reduction, or remove features present in less than n cells with the FindTopFeatures function. Here, we will all features, though we note that we see very similar results when using only a subset of features (try setting min.cutoff to 'q75' to use the top 25% all peaks), with faster runtimes. Features used for dimensional reduction are automatically set as VariableFeatures for the Seurat object by this function.
> scATAC-seq数据的低动态范围使其在进行可变特征选择时具有挑战性，就像我们为scRNA-seq所做的那样。相反，我们可以选择仅使用前n%的特征（峰）进行降维，或者使用FindTopFeatures函数移除在少于n个细胞中出现的特征。在这里，我们将使用所有特征，尽管我们注意到，当仅使用特征子集时（尝试将min.cutoff设置为'q75'以使用所有峰的前25%），我们看到非常相似的结果，且运行时间更快。用于降维的特征将自动由该函数设置为Seurat对象的VariableFeatures。

使用Top k features进行降维，或者使用所有feature都是可以的。

### Dimension Reduction

还是可以采用NLP中的降维方法，Topic models有:

- Latent Semantic Indexing (LSI) - SVD
- Nonnegtive Matrix Factorization (NMF)
- Latent Dirichlet Allocation (LDA)
  他们可以提取出一篇“文章”中的主题，对应到细胞中就是peaks。

### Data integration (Batch correction)

和RNA-seq很像，比较好的方法有：LIGER，Harmony。

### Cell type annotation

Manually annotation: based on gene activity + known marker genes

- Signac gene activity score
- Cicero co-accessibility gene activity score
- MAESTRO RP(regulatory potential) score
- ArchR gene score

Automatically annotation

- Marker gene based methods: MAESTRO, Cell WalkR
- Batch correction based methods: **Seurat**, Conos
- Multi-modality integration based methods: GLUE, scJoint

## 下游分析

### Differential analysis

差异分析主要是比较不同细胞类型之间的基因组区段开放程度的差异。可以使用一些统计方法来计算每个基因组区段在不同细胞类型之间的差异。

### Trajectory Inference

Monocle3, ArchR...

### Co-accessibility

看哪些peak有协同/互作的作用（共同开放）

- Cicero

### Motif analysis

通过转录因子结合位点Motif的富集情况，推断转录因子结合位点。

### Footprint analysis
