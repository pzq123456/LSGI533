# Report 2 (20%) : 
> - PanZhiQing24037665g
> - Report 2 (20%) (submission date: 8 Nov)
> - Review of mitigation methods for GNSS multipath errors

## Abstract

## Contents


## 1. Introduction
GPS 接收机会接收到周围环境反射的 GPS 卫星信号，相比于直达接收机的信号，这些反射信号往往会花费更长的时间到达接收机，从而带来定位误差，这种现象也被成为多路径效应。一般情况下，接收机可能会同时接收到两种（直接、多路径间接）信号（如图1.1 所示）。

GPS Receiver will receive GPS satellite signals reflected from the surrounding environment. Compared to the direct signal received by the receiver, these reflected signals often take longer to reach the receiver, resulting in positioning errors. This phenomenon is also known as multipath effect. In general, the receiver may receive two types of signals at the same time (direct, multipath indirect) (as shown in Figure 1.1).

<!-- ![](./imgs/p1.png) -->
<img src="./imgs/p1.png" width="400" />

Figures 1.1: Multipath effect on GNSS signal

正如前面提到的，多路径效应所带来的影响与接收机所处的当地环境及卫星位置高度相关。同时，还应考虑到接收机的结构因素，不同接收机采取不同的设计，因此对多路径效应的削减效果也会有所不同。考虑到卫星处于运动之中，我们可以将多路径效应建模为时间的函数。假设直达接收机的信号表示为:

As mentioned earlier, the impact of multipath effects is highly dependent on the local environment in which the receiver is located and the height of the satellite position. At the same time, the structural factors of the receiver should also be considered. Different receivers adopt different designs, so the effect of reducing multipath effects will also be different. Considering that the satellite is in motion, we can model the multipath effect as a function of time. Assuming that the signal received by the direct receiver is represented by:

$$
s(t) = A \cos(\omega t + \phi) \tag{1.1}
$$

经过多路径反射后的信号表示为:

The signal after multipath reflection is represented by:
$$
s'(t) = f \times s(t + \delta t) \tag{1.2}
$$
其中，$f$ 为反射所带来的衰减系数，$\delta t$ 为时间延迟。
Where $f$ is the attenuation coefficient brought by the reflection, and $\delta t$ is the time delay.

多路径效应本质是带来时间延迟，所以其对定位精度所带来的影响与波长成正比。例如，对于波长为30米左右的 P-code 信号，由多路径效应所带来的影响大约为 15 米； 而对于 C/A 信号，波长约为 300 米，多路径效应所带来的影响大约为 150 米。如果采用波长更短的载波观测，多路径效应所带来的影响则会缩减到厘米级别。多路径效应的另一个特性与 GPS 信号本身有关，GPS 信号 right-handed circularly polarised(RHCP)，经多路径效应反射的信号会改变这个性质，从接收机的角度来说，信号的 signal-to-noise ratio 会显著降低（1/3）。所以，我们可以尽可能地让接收机远离反射面，或者使用载波观测，以减轻多路径效应所带来的影响。在必须采用 C/A 信号的情况下，我们可以采用相位平滑后的码（phase-smoothed code）来减小多路径效应的影响。

Multipath effects essentially bring time delays, so their impact on positioning accuracy is proportional to the wavelength. For example, for P-code signals with a wavelength of about 30 meters, the impact of multipath effects is about 15 meters; for C/A signals, the wavelength is about 300 meters, and the impact of multipath effects is about 150 meters. If shorter wavelength carrier observations are used, the impact of multipath effects will be reduced to the centimeter level. Another characteristic of multipath effects is related to the GPS signal itself. The GPS signal is right-handed circularly polarized (RHCP), and the signal reflected by multipath effects will change this property. From the receiver's perspective, the signal's signal-to-noise ratio will be significantly reduced (1/3). Therefore, we can try to keep the receiver away from the reflecting surface as much as possible, or use carrier observations to mitigate the impact of multipath effects. In cases where C/A signals must be used, we can use phase-smoothed codes to reduce the impact of multipath effects.

若想要精确地消除多路径效应，就需要检测出受多路径效应影响的信号并削弱之。一般采用码与相位结合的方法来检测多路径效应。回顾前一个报告中的内容伪距测量模型（Report1 4.4）及载波相位测量模型（Report1 4.8），我们可以得出联合公式用于检测多路径效应：

If you want to accurately eliminate multipath effects, you need to detect the signals affected by multipath effects and weaken them. Generally, a combination of code and phase is used to detect multipath effects. Reviewing the pseudorange measurement model (Report1 4.4) and the carrier phase measurement model (Report1 4.8) in the previous report, we can derive a joint formula for detecting multipath effects:

$$
R_r^s(t_r,t_e) - \lambda \phi_r^s(t_r) = 2 \delta_{ion} + \lambda N_r^s + \delta_{mul} + \epsilon \tag{1.3}
$$

式中，$R_r^s(t_r,t_e)$ 为伪距观测值，$\lambda \phi_r^s(t_r)$ 为载波相位观测值，$\delta_{ion}$ 为电离层延迟，$\lambda N_r^s$ 为整周模糊度，$\delta_{mul}$ 为多路径效应对码观测的影响，$\epsilon$ 为码观测的误差。 由于载波相位观测的误差要远小于码观测的误差，因此我们可以通过载波相位观测值来检测多路径效应。

Where $R_r^s(t_r,t_e)$ is the pseudorange observation value, $\lambda \phi_r^s(t_r)$ is the carrier phase observation value, $\delta_{ion}$ is the ionospheric delay, $\lambda N_r^s$ is the integer ambiguity, $\delta_{mul}$ is the effect of multipath on code observation, and $\epsilon$ is the error of code observation. Since the error of carrier phase observation is much smaller than the error of code observation, we can detect multipath effects through carrier phase observation.

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