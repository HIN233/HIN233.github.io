---
title: 给新手的 Slurm 作业调度系统使用教程
date: 2025-06-01
summary: 本文介绍 Slurm 的基本概念、常用命令和配置方法，帮助新手快速上手。
category: 生物统计
tags: [Slurm, 作业调度系统, HPC]
---

## 简介

[Slurm](http://slurm.schedmd.com/) (Simple Linux Utility for Resource Management) 是开源的、具有容错性和高度可扩展的 Linux 集群超级计算系统资源管理和作业调度系统。超级计算系统可利用Slurm对资源和作业进行管理，以避免相互干扰，提高运行效率。所有需运行的作业，无论是用于程序调试还是业务计算，都可以通过交互式并行 `srun` 、批处理式 `sbatch` 或分配式 `salloc` 等命令提交，提交后可以利用相关命令查询作业状态等。

![slurm1.png](https://s2.loli.net/2025/05/30/v3VdbyFrYKktWnR.png)

![slurm2.png](https://s2.loli.net/2025/05/30/jLYCsOi7NIRhMZ1.png)

## 常用指令

### 概览

| Slurm    | 功能               |
| -------- | ------------------ |
| sinfo    | 集群状态           |
| squeue   | 排队作业状态       |
| sbatch   | 作业提交           |
| scontrol | 查看和修改作业参数 |
| sacct    | 已完成作业报告     |
| scancel  | 删除作业           |

### 1. sbatch 提交作业

将整个计算过程，写到**脚本**中，通过sbatch指令提交到计算节点上执行：

```bash
sbatch cpu.sh
```

这是一个名为cpu.sh的作业脚本，该脚本向cpu队列申请1个节点40核，并在作业完成时通知。在此作业中执行的命令是/bin/hostname。

```bash
#!/bin/bash

#SBATCH --job-name=hostname
#SBATCH --partition=cpu
#SBATCH -N 1
#SBATCH --mail-type=end
#SBATCH --mail-user=YOU@EMAIL.COM
#SBATCH --output=%j.out
#SBATCH --error=%j.err

/bin/hostname
```

以下是常用的参数：

| 参数                         | 含义               |
| ---------------------------- | ------------------ |
| `-n [count]`                 | 总进程数           |
| `--ntasks-per-node=[count]`  | 每台节点上的进程数 |
| `-p [partition]`             | 作业队列           |
| `--job-name=[name]`          | 作业名             |
| `--output=[file_name]`       | 标准输出文件       |
| `--error=[file_name]`        | 标准错误文件       |
| `--time=[dd-hh:mm:ss]`       | 作业最大运行时长   |
| `--exclusive`                | 独占节点           |
| `--mail-type=[type]`         | 通知类型           |
| `--mail-user=[mail_address]` | 通知邮箱           |
| `--nodelist=[nodes]`         | 偏好的作业节点     |
| `--exclude=[nodes]`          | 避免的作业节点     |
| `--depend=[state:job_id]`    | 作业依赖           |
| `--array=[array_spec]`       | 序列作业           |

用以下方式提交作业：

```bash
sbatch cpu.slurm
```

输出将实时更新到文件[jobid] .out和[jobid] .err。

### 2. salloc 交互式分配

申请计算节点，然后登录到申请到的计算节点上运行指令；salloc的参数与sbatch相同。

以下是一个GPU节点的使用案例：申请一个GPU节点，6个核心，1块GPU卡，并跳转到节点上运行程序。

```bash
salloc -p GPU -N1 -n6 --gres=gpu:1 -q low -t 24:00:00
# salloc 申请成功后会返回申请到的节点和作业ID等信息，假设申请成功后返回的作业号为1078858，申请到的节点是gpu05
ssh gpu05 # 直接登录到刚刚申请到的节点gpu05上调式作业
scancel 1078858  # 计算结束后结束任务
squeue -j 1078858 # 查看作业是否还在运行，确保作业已经退出，避免产生不必要的费用
```

### 3. sinfo 查看集群状态

通过sinfo可查询各分区节点的空闲状态。

| 命令                     | 功能             |
| ------------------------ | ---------------- |
| `sinfo -N`               | 查看节点级信息   |
| `sinfo -N --states=idle` | 查看可用节点信息 |
| `sinfo --partition=cpu`  | 查看队列信息     |
| `sinfo --help`           | 查看所有选项     |

节点状态包括：

drain(节点故障)，alloc(节点在用)，idle(节点可用)，down(节点下线)，mix(节点部分占用，但仍有剩余资源）。

`sinfo`提供以下信息：

| Header Column | Definition                                                                                    |
| ------------- | --------------------------------------------------------------------------------------------- |
| **PARTITION** | 一组节点                                                                                      |
| **AVAIL**     | 节点是否启动、关闭或处于其他状态（up/down/other）                                             |
| **TIMELIMIT** | 用户可以请求给定分区中的节点的时间量（格式：days-hours:minutes:seconds）                      |
| **NODES**     | 给定分区中的节点数                                                                            |
| **STATE**     | 节点状态（如：维护（drain）、混合（mixed）、空闲（idle）、停机（down）、分配（allocated）等） |
| **NODELIST**  | 具有给定状态的节点名称（列出符合条件的节点）                                                  |

通过sinfo查看指定分区的空闲状态：

例如：指定显示C032M0128G和C032M0256G分区的空闲状态；

```bash
sinfo -p C032M0128G,C032M0256G
```

最后是sinfo的一些常用参数。

| Option           | Description                              |
| ---------------- | ---------------------------------------- |
| `--help`         | 显示 sinfo 命令的使用帮助信息            |
| `-d`             | 查看集群中没有响应的节点                 |
| `-i <seconds>`   | 每隔指定的秒数刷新分区节点信息           |
| `-n <name_list>` | 显示指定节点的信息（多个节点用逗号隔开） |
| `-N`             | 按每个节点一行的格式显示信息             |
| `-p <partition>` | 显示指定分区的信息（多个分区用逗号隔开） |
| `-r`             | 只显示响应的节点                         |
| `-R`             | 显示节点不正常工作的原因                 |

### 4. squeue 查看作业状态

默认情况下`squeue`输出的内容如下，分别是作业号，分区，作业名，用户，作业状态，运行时间，节点数量，运行节点(如果还在排队则显示排队原因)

```bash
 JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
```

如何在队列中显示自己的作业；

```bash
# 注意whoami前后不是单引号
squeue -u `whoami`
```

介绍squeue的常见参数；
| Option | Description |
|--------|-------------|
| `--help` | 显示 squeue 命令的使用帮助信息 |
| `-A <account_list>` | 显示指定账户下所有用户的作业（多个账户用逗号隔开） |
| `-i <seconds>` | 每隔指定的秒数刷新作业信息 |
| `-j <job_id_list>` | 显示指定作业号的作业信息（多个作业号用逗号隔开） |
| `-n <name_list>` | 显示指定节点上的作业信息（多个节点用逗号隔开） |
| `-t <state_list>` | 显示指定状态的作业信息（多个状态用逗号隔开） |
| `-u <user_list>` | 显示指定用户的作业信息（多个用户用逗号隔开） |
| `-w <hostlist>` | 显示指定节点上运行的作业（多个节点用逗号隔开） |

### 5. sacct 查看作业相关信息

通过`sacct`和`scontrol show job`显示作业信息。

`scontrol show job` 只能显示正在运行或者刚结束没多久的作业信息；

```bash
# 查看作业7454119的详细信息
scontrol show job 7454119
```

通过`sacct`查询已经结束作业的相关信息，如下所示：

```bash
sacct -j 7454119
```

输出内容会包括，作业号，作业名，分区，计费账户，申请的CPU数量，状态，结束代码

```
JobID    JobName  Partition    Account  AllocCPUS      State ExitCode
```

```bash
# 添加 -a 参数将提供有关所有帐户的信息。
sacct -a

# 下面的命令可以提供更多有用的列信息。
sacct -a --format JobID,Partition,Timelimit,Start,Elapsed,NodeList%20,ExitCode,ReqMem,MaxRSS,MaxVMSize,AllocCPUS
```

### 6. scancel 删除作业

取消指定作业；

```bash
# 取消作业ID为123的作业
scancel 123
```

取消自己上机上号上所有作业；

```bash
# 注意whoami前后不是单引号
scancel -u `whoami`
```

取消自己上机账号上所有状态为PENDING的作业；

```bash
scancel -t PENDING -u `whoami`
```

scancel常见参数;

| Option                | Description                                             |
| --------------------- | ------------------------------------------------------- |
| `--help`              | 显示 scancel 命令的使用帮助信息                         |
| `-A <account>`        | 取消指定账户的作业（未指定job_id时取消该账户所有作业）  |
| `-n <job_name>`       | 取消指定作业名的作业                                    |
| `-p <partition_name>` | 取消指定分区的作业                                      |
| `-q <qos>`            | 取消指定QoS的作业                                       |
| `-t <job_state_name>` | 取消指定状态的作业（"PENDING"、"RUNNING"或"SUSPENDED"） |
| `-u <user_name>`      | 取消指定用户的作业                                      |

## References

- [快速入门：Slurm资源管理与作业调度系统](https://zhuanlan.zhihu.com/p/571973164)
- [上海交大超算平台用户手册](https://docs.hpc.sjtu.edu.cn/job/slurm.html#id2)
- [北京大学高性能计算平台用户使用文档](https://hpc.pku.edu.cn/_book/guide/slurm/slurm.html)
- [Slurm 作业调度系统使用指南](https://zhuanlan.zhihu.com/p/356415669)
