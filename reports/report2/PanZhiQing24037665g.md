# Report 2 (20%) : 
> - PanZhiQing24037665g
> - Report 2 (20%) (submission date: 8 Nov)
> - Review of mitigation methods for GNSS multipath errors

## Abstract

## Contents


## 1. Introduction
GPS 接收机会接收到周围环境反射的 GPS 卫星信号，相比于直达接收机的信号，这些反射信号往往会花费更长的时间到达接收机，从而带来定位误差，这种现象也被成为多路径效应。一般情况下，接收机可能会同时接收到两种（直接、多路径）信号（如图1.1 所示）。

![](./imgs/p1.png)
Figures 1.1: Multipath effect on GNSS signal

正如前面提到的，多路径效应所带来的影响与接收机所处的当地环境及卫星位置高度相关。同时，还应考虑到接收机的结构因素，不同接收机采取不同的设计，因此多路径效应的影响也会有所不同。考虑到卫星处于运动之中，我们可以将多路径效应建模为时间的函数。假设直达接收机的信号表示为:
$$
s(t) = A \cos(\omega t + \phi) \tag{1.1}
$$

经过多路径反射后的信号表示为:
$$
s'(t) = f \times s(t + \delta t) \tag{1.2}
$$
其中，$f$ 为反射所带来的衰减系数，$\delta t$ 为时间延迟。



### 1.1 Causes of Multipath Errors

### 1.2 GNSS Multipath Error Sources

### 1.3 GNSS Signal Interference

## 2. Review of GNSS Multipath Error Mitigation Methods

### 2.1 Multipath Eliminating Delay Lock Loop (MEDLL)
从时间延迟的角度来看，多路径效应可以被视为一个延迟的信号，因此我们可以通过延迟锁相环（Delay Lock Loop, DLL）来消除多路径效应。延迟锁相环的基本原理是通过延迟输入信号，使得输入信号与延迟信号之间的相位差保持在一个固定的范围内，从而实现信号的同步。在 GPS 接收机中，延迟锁相环被广泛应用于消除多路径效应。

### 2.2 Observation Environment Optimization

### 2.3 Signal Filtering and Data Processing

### 2.4 Multi-frequency GNSS Receiver

### 2.5 Multipath Error Post-processing Algorithm

## 3. Comparative Analysis of GNSS Techniques
## 4. Multipath Effects can be useful

<div STYLE="page-break-after: always;"></div>

| 大纲内容                     | 英文关键词                                      |
|------------------------------|------------------------------------------------|
| **1. 引言：GNSS多路径效应概述**        | GNSS multipath error, GNSS positioning error, GNSS signal interference, Introduction |
| **2. 多路径效应的产生原因**             | Causes of multipath errors, Multipath effect origin, GNSS signal reflection, Signal propagation error |
| **3. 多路径效应对定位精度的影响**       | GNSS accuracy degradation, Positioning accuracy, Impact of multipath on GNSS accuracy, GNSS error sources |
| **4. 减轻多路径效应的方法综述**         | Mitigation methods for multipath, GNSS multipath reduction, GNSS error correction techniques |
| &nbsp;&nbsp;&nbsp;&nbsp;**4.1. 使用多路径抑制天线**  | Multipath suppression antenna, GNSS antenna technology, High-precision GNSS antenna |
| &nbsp;&nbsp;&nbsp;&nbsp;**4.2. 优化观测环境**       | Observation environment optimization, GNSS multipath-free environment, Site selection for GNSS |
| &nbsp;&nbsp;&nbsp;&nbsp;**4.3. 信号滤波和数据处理** | Signal filtering, GNSS data processing, Kalman filtering, GNSS signal filtering |
| &nbsp;&nbsp;&nbsp;&nbsp;**4.4. 应用多频接收器**     | Multi-frequency GNSS receiver, Dual-frequency GNSS, GNSS multi-band |
| &nbsp;&nbsp;&nbsp;&nbsp;**4.5. 多路径效应的后处理算法** | Multipath error post-processing, GNSS multipath mitigation algorithm, Post-processing techniques |
| **5. 不同技术的对比与适用性分析**       | Comparative analysis of GNSS techniques, Performance comparison GNSS, Suitability of GNSS methods |
| **6. 未来研究方向**                  | Future research GNSS multipath, Emerging technologies in GNSS, GNSS advancements |
| **7. 总结**                        | GNSS multipath review, Summary of GNSS mitigation methods, Overview of multipath techniques |

## References
1. GPS: Theory, Algorithms and Applications, by Guochang Xu. Springer, 2007. doi: https://doi.org/10.1007/978-3-662-50367-6