---
title: 三种测序技术简介
date: 2025-04-23
summary: 第一代、第二代(NGS)和第三代测序技术的介绍
category: 生物统计
tags: [biology, sequencing]
---

# Three Generations of Sequencing Technologies

## Overview

全基因组测序 (Whole Genome Sequencing)，简称WGS，目前默认指的是人类的全基因组测序。
所谓全（Whole），指的就是把物种细胞里面中完整的基因组序列完整地检测并排列好每个基因，因此这个技术几乎能够鉴定出基因组上任何类型的突变。对于人类来说，全基因组测序的价值是极大的，它包含了所有基因和生命特征之间的内在关联性，当然也意味着更大的数据解读和更高的技术挑战。

测序技术从1977年的第一代Sanger技术发展至今，已经足有40年时间。在这个技术发展的更迭历程中，测序读长从长到短，再从短到长。虽然就当前形势看第二代短读长测序技术在全球范围内上占有着绝对的垄断位置，但第三测序技术也已在这几年快速地发展着。

## $1^{\text{st}}$ Generation: Sanger sequencing

Sanger法的核心原理是：由于ddNTP（4种带有荧光标记的A,C,G,T碱基）的2’和3’都不含羟基，其在DNA的合成过程中不能形成磷酸二酯键，因此可以用来中断DNA的合成反应，在4个DNA合成反应体系中分别加入一定比例带有放射性同位素标记的ddNTP，然后利用凝胶电泳和放射自显影后可以根据电泳带的位置确定待测分子的DNA序列。

<div style="display: flex; justify-content: center; gap: 20px; margin: 20px 0;">
  <img src="https://s2.loli.net/2025/04/24/9ONQTAjZ5BYSsFD.png" alt="Sanger1" style="max-width: 70%;">
  <img src="https://s2.loli.net/2025/04/24/zSPsdnRl1tHhQW3.png" alt="Sanger2" style="max-width: 30%;">
</div>

操作要点：

- 向四个试管中添加单链DNA序列
  Add one-stranded DNA sequence to four test tubes.
- 每个试管含有所有dNTPs + 一个ddNTP
  Each tube contain all dNTPs + one ddNTP.

特点：测序读长可达1,000bp；准确性高达99.999%；现在仍作为检验测序结果的金标准
缺点：测序成本高；通量低。严重影响了其真正大规模的应用

## $2^{\text{nd}}$ Generation: Illumina Sequencing Sequencing by Synthesis

改进：大幅提高了测序速度（以前完成一个人类基因组的测序需要3年时间，而使用二代测序技术则仅仅需要1周）；大大地降低了测序成本；保持高准确性
缺点：序列读长方面比起第一代测序技术则要短很多，大多只有100bp-150bp

![NGS.png](https://s2.loli.net/2025/04/24/XrszI9P3jLamV5n.png)

主要分为以下四个步骤：

### 1. 样本文库准备

构建DNA测序文库，简单来说就是把一堆乱糟糟的DNA分子用超声波打断成一定长度范围的**小片段**。目前除了一些特殊的需求之外，基本都是打断为300bp-800bp长的序列片段，并在这些小片段的两端加工拼接双头序列，构建出单链DNA文库，以备测序之用。

具体而言，最终产生的每条DNA单链的两端**从外向内**连有**flowcell互补引物、indces片段和测序引物结合位点片段**，这些DNA单链即组成样品文库。
作用分别是：

- flowcell互补引物：与固定在flowcell表面上的寡核苷酸序列 (oligo) 互补配对，使得DNA片段能吸附在flowcell表面
- indices片段：用于区分样品来源 & 读序方向 (如果是双端测序需要index1和index2；如果是单端测序只需要index1)
- 测序引物结合位点片段：用于测序反应的引物结合位点

测序流动槽（flowcell），flowcell是用于吸附流动DNA片段的槽道，也是核心的测序反应容器，外观像一个玻璃载玻片 —— 所有的测序过程就发生在这里。当文库建好后，这些文库中的DNA在通过flowcell的时候会随机附着在flowcell表面的槽道（称为lane）上。每个flowcell有8个lane，每个lane的表面都附有很多接头，这些接头能和建库过程中加在DNA片段两端的接头相互配对，这就是为什么flowcell能吸附建库后的DNA的原因，并能支持DNA在其表面进行桥式PCR的扩增，理论上这些lane之间是不会相互影响的。

<div style="text-align: center; margin: 20px 0;">
  <img src="https://s2.loli.net/2025/04/24/ECUdGvnpTMZwxzS.png" alt="Flowcell" style="max-width: 50%;">
</div>

### 2. 桥式PCR扩增

这是NGS技术的一个核心特点。桥式PCR以flowcell表面所固定的序列为模板，进行桥形扩增。经过不断的扩增和变性循环，最终每个DNA片段都将在各自的位置上集中成束，每一个束都含有单个DNA模板的很多分拷贝，这一过程的目的在于实现将单一碱基的信号强度进行放大，以达到测序所需的信号要求。

> 扩增的过程如下：
>
> 1. DNA片段与flowcell表面上的寡核苷酸序列互补配对
> 2. 引入DNA聚合酶和原料，进行DNA合成
> 3. 加入NaOH碱性溶液，双链分子变形分开，洗去一条链，另一条的一段由于固定在flowcell表面上而不能被洗去
> 4. 加入中性溶液后，留下的单链DNA就会与通道表面的另一个oligo结合，形成单链桥
> 5. 此时进行一次DNA合成，形成双链桥
>
> 重复步骤 $3-5$ 25-28个循环后，原来散布在流通池表面的文库DNA单链变成了DNA簇 (此时簇内包含正反序列)，为保证同一簇内只有一种DNA单链，以及为了先从index1开始测DNA的序列，因此，先把正向DNA链**切割并洗脱**，只保留反向DNA链，并化学封闭3'端以防非特异结合，这样在flow cell表面就形成了数以亿计的DNA分子簇（cluster）。
> 由于样品文库经过稀释后浓度足够低，因此可以认为各DNA单链均匀的结合在流通池表面，且相距足够远，所以每个簇是具有**数千份相同模板的单分子簇**。

### 3. 边合成边测序

向反应体系中同时添加DNA聚合酶、接头引物和带有碱基特异荧光标记的4中dNTP（如同Sanger测序法）。这些dNTP的3’-OH被化学方法所保护，当被添加到DNA末端时可阻断延伸反应，因而每次只能添加一个dNTP，这就确保了在测序过程中，一次只会被添加一个碱基。同时在dNTP被添加到合成链上后，所有未使用的游离dNTP和DNA聚合酶会被洗脱掉。接着，再加入激发荧光所需的缓冲液，用激光激发荧光信号，并有光学设备完成荧光信号的记录，最后利用计算机分析将光学信号转化为测序碱基。这样荧光信号记录完成后，再加入化学试剂淬灭荧光信号并去除dNTP 3’-OH保护基团，以便能进行下一轮的测序反应。步骤如下：

1.  Incorporate all 4 nucleotides, each label with a different dye
2.  Wash, 4-color imaging
3.  Cleave dye and terminating groups, wash
4.  Repeat cycles

最后引入index1序列，读取样本来源。根据每次得到的荧光信号就可以得到DNA的正向序列。

---

Illumina的这种每次只添加一个dNTP的技术特点能够很好的地解决同聚物长度的准确测量问题，它的主要测序错误来源是碱基的替换，目前它的测序错误率在1%-1.5%左右。并且随着复制的进行，cluster中各个DNA分子复制的协同性降低，因此，第二代测序的缺点就是读长短。为了改进这个问题，我们需要**双端测序**，来提高序列读取的长度和准确性。步骤如下：

在完成单端测序后，先将模板链的3’端去保护，然后进行桥式PCR扩增 (此次这一次会先读取index2片段)，再化学封闭3'端，然后我们将反向DNA链切割并洗脱，保留**正向DNA链**，然后进行测序得到反向序列。

### 4. Shotgun鸟枪法分析 & 表达量分析

鸟枪法是指将基因组DNA随机打断成小片段，然后对这些片段进行测序 (也就是步骤 $1-3$)，最后通过计算机程序将这些片段拼接起来，重建出原始的基因组序列。由于小片段足够随机且后期获得的数据量又足够大，因此鸟枪法的关键在于如何将这些小片段拼接起来，通常使用重叠拼接的方法，即寻找相邻片段之间的重叠区域，进而拼凑出一段**完整的DNA序列**。

---

同时利用单个片段 (read) 的重复出现的次数，我们可以通过分析判断出基因在样本中的表达量。
Illumina测序使用的是RPKM/FPKM法进行表达量的衡量。

> RPKM: Reads Per Kilobase Per Million, 每一百万条Reads中, 对基因的每1000个Base而言，比对到该1000个base的Reads数；
> FPKM: Fragments per Kilobase Per Million, 其与RPKM的差别仅在于以Fragment进行计算，双端测序一对reads称为一个fragment。

精细的分析将在后面的文章中介绍。

## $3^{\text{rd}}$ Generation Sequencing

第三代测序的目的是克服第二代测序的缺点，得到的一种“完美”的测序方法。其中最最主要的，是把读长提上去，所以它也被称作长读长测序（Long-Read Sequencing）。
目前“商业化主流”的三代测序技术是Pacific Biosciences公司的SMRT单分子实时测序技术和Oxford Nanopore Technologies公司的纳米孔单分子技术。

特点：

- 读数更少但更长：适合长序列，但不适合读数计数应用
  Fewer but much longer reads: good for long sequences, but not for read count applications.

- 无需扩增、单分子测序

- PacBio的SMRT技术：零模波导（Zero-Mode Waveguide, ZMW）的纳米结构

- Oxford：使用聚合酶和/或孔进行测序，无需DNA扩增
  Single molecule sequencing: use polymerase and/or pores for sequencing without DNA amplification.

## References

- [STAT115/215](https://www.youtube.com/watch?v=Stp1PhG8Ka8&t=8s)
- [从零开始完整学习全基因组测序数据分析](https://luohao-brian.gitbooks.io/gene_sequencing_book/content/)

---

- [BiliBili:【高中生物】次世代测序技术原理动画：illumina （上）- 第二代DNA测序】 ](https://www.bilibili.com/video/BV1PN4y1i76c/?share_source=copy_web&vd_source=107b4c6997b8d2ed6549accc94910d18)
- [知乎:你真的搞懂测序技术了吗 ——第二代测序](https://zhuanlan.zhihu.com/p/579242208)
