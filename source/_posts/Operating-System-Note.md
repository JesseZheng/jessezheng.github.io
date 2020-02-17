---
title: Operating System Note
date: 2019-10-08 15:27:58
tags:
- OS
categories: 学习
---

## C01.操作系统概念

### OS Definition

- 提供interface用来帮助用户去操作硬件，硬件和软件资源的管理者
- Resource allocator
- Control program
- **Kernel**(内核): 在全时运行的一个程序（其他的是应用）

<!-- more -->

### Development of OS
- 真空管（无OS）-> 晶体管（批处理系统）-> 集成电路（多道程序设计）-> 超大规模的集成电路（分时系统）
- 简单批处理系统(Simple Batch System), 多道程序批处理(Multiprogramming Batched Systems)
- 分时系统(time-sharing system)

### 简单批处理系统
- 真空管计算机，速度：1000次每秒
- 脱机I/O：输入输出设备通过外围机写到磁带上，CPU去读写磁带
- 作业任务先写入磁带，然后磁带分类编成作业顺序执行，每批作业由专门监督程序Monitor自动依次处理
- 优点：减少CPU空闲时间，提高CPU和I/O的使用效率，提高了吞吐量
- 缺点：I/O或者CPU设备使用忙闲不均

### 多道程序批处理
{% asset_img [多道程序批处理] multiprogramming.png %}
- 通道技术(是一个独立于CPU的专管输入/输出控制的处理机，它控制设备与内存直接进行数据交换)
- 中断技术(中断当前执行的程序去处理特殊事件的操作)
- 多道性(并发能力)，无序性，调度性
- 优点：资源利用率高
- 缺点：无用户交互能力，响应时间长

### 分时系统
- 多个用户共享一个计算机，不同时间使用

- 按**时间片time slice**分配任务，各个程序在CPU执行的轮转时间

- 作业直接进入内存，每个作业一次只运行很短的时间

- 分时技术：CPU执行时间分成时间片(很短)，多个程序用户轮转使用CPU

- 分时系统是如今很多系统的基本！

  ---------

  
