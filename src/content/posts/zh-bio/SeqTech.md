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

特点：测序读长可达1,000bp；准确性高达99.999%
缺点：测序成本高；通量低。严重影响了其真正大规模的应用

## $2^{\text{nd}}$ Generation: Illumina Sequencing Sequencing by Synthesis

改进：大幅提高了测序速度（以前完成一个人类基因组的测序需要3年时间，而使用二代测序技术则仅仅需要1周）；大大地降低了测序成本；保持高准确性
缺点：序列读长方面比起第一代测序技术则要短很多，大多只有100bp-150bp

![NGS.png](https://s2.loli.net/2025/04/24/XrszI9P3jLamV5n.png)

主要分为以下四个步骤：

1. 构建DNA测序文库，简单来说就是把一堆乱糟糟的DNA分子用超声波打断成一定长度范围的小片段。目前除了一些特殊的需求之外，基本都是打断为300bp-800bp长的序列片段，并在这些小片段的两端添加上不同的接头，构建出单链DNA文库，以备测序之用；

2. 测序流动槽（flowcell），flowcell是用于吸附流动DNA片段的槽道，也是核心的测序反应容器——所有的测序过程就发生在这里。当文库建好后，这些文库中的DNA在通过flowcell的时候会随机附着在flowcell表面的槽道（称为lane）上。每个flowcell有8个lane，每个lane的表面都附有很多接头，这些接头能和建库过程中加在DNA片段两端的接头相互配对，这就是为什么flowcell能吸附建库后的DNA的原因，并能支持DNA在其表面进行桥式PCR的扩增，理论上这些lane之间是不会相互影响的。

<div style="text-align: center; margin: 20px 0;">
  <img src="https://s2.loli.net/2025/04/24/ECUdGvnpTMZwxzS.png" alt="Flowcell" style="max-width: 50%;">
</div>

1. 桥式PCR扩增与变性：这是NGS技术的一个核心特点。桥式PCR以flowcell表面所固定的序列为模板，进行桥形扩增。经过不断的扩增和变性循环，最终每个DNA片段都将在各自的位置上集中成束，每一个束都含有单个DNA模板的很多分拷贝，这一过程的目的在于实现将单一碱基的信号强度进行放大，以达到测序所需的信号要求。

2. 测序 (边合成边测序)
   向反应体系中同时添加DNA聚合酶、接头引物和带有碱基特异荧光标记的4中dNTP（如同Sanger测序法）。这些dNTP的3’-OH被化学方法所保护，当被添加到DNA末端时可阻断延伸反应，因而每次只能添加一个dNTP，这就确保了在测序过程中，一次只会被添加一个碱基。同时在dNTP被添加到合成链上后，所有未使用的游离dNTP和DNA聚合酶会被洗脱掉。接着，再加入激发荧光所需的缓冲液，用激光激发荧光信号，并有光学设备完成荧光信号的记录，最后利用计算机分析将光学信号转化为测序碱基。这样荧光信号记录完成后，再加入化学试剂淬灭荧光信号并去除dNTP 3’-OH保护基团，以便能进行下一轮的测序反应。步骤如下：
   1. Incorporate all 4 nucleotides, each label with a different dye
   2. Wash, 4-color imaging
   3. Cleave dye and terminating groups, wash
   4. Repeat cycles

Illumina的这种每次只添加一个dNTP的技术特点能够很好的地解决同聚物长度的准确测量问题，它的主要测序错误来源是碱基的替换，目前它的测序错误率在1%-1.5%左右。并且随着复制的进行，cluster中各个DNA分子复制的协同性降低，因此，第二代测序的缺点就是读长短。

## $3^{\text{rd}}$ Generation Sequencing

特点：

- **单分子测序**：使用聚合酶和/或孔进行测序，无需DNA扩增
  Single molecule sequencing: use polymerase and/or pores for sequencing without DNA amplification.

- 读数更少但更长：适合长序列，但不适合读数计数应用
  Fewer but much longer reads: good for long sequences, but not for read count applications.

- 技术仍在积极发展中
  Technology still under active development
