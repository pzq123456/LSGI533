
## 
目前检测脉冲星的方式主要分为两种，一种是借助直径数十米至数百米的大型地面射电望远镜来持续观测脉冲星的微波信号。

There are currently two main ways to detect pulsars, one is to continuously observe the microwave signals of pulsars using large ground-based radio telescopes with diameters ranging from tens of meters to hundreds of meters.

## 

XNAV 技术的主要优势在于其成本效益，通过较低的成本实现了较高的定位精度和自主性。随着紧凑型 X 射线天线的发展，XNAV 技术得以广泛应用于深空探测任务，并可以搭载于各类航空器上，其推广意义可与 GPS 相提并论。此外，XNAV 技术的定位精度也非常出色。例如，使用脉冲星 PSR B1937+21 时，航天器在距离最大可达 30 天文单位的范围内，经过 10 小时的观测，可以实现约 2 公里的定位精度；而经过 1 小时的观测，定位精度可达到 5 公里。

The main advantage of XNAV technology is its cost-effectiveness, which achieves high positioning accuracy and autonomy at a lower cost. With the development of compact X-ray antennas, XNAV technology has been widely used in deep space exploration tasks and can be carried on various types of aircraft, with its promotion significance comparable to GPS. In addition, the positioning accuracy of XNAV technology is also very good. For example, when using the pulsar PSR B1937+21, the spacecraft can achieve an accuracy of about 2 kilometers after 10 hours of observation within a range of up to 30 astronomical units; and after 1 hour of observation, the accuracy can reach 5 kilometers.

## 

我们的系统由三部分组成：VLBI 观测网络、脉冲星数据库和 XNAV 系统。VLBI 观测网络负责持续搜索和观测脉冲星，脉冲星数据库则负责处理观测数据，建立并存储脉冲星信号模型。对于 VLBI 观测网络来说，既可以利用地球上现有的观测网络，也可以是未来在宇宙空间中部署的观测网络。XNAV 系统则类似于 GPS 接收机，安装在需要导航的目标航天器上，负责实时定位。

Our system consists of three parts: VLBI observation network, pulsar database, and XNAV system. The VLBI observation network is responsible for continuously searching and observing pulsars, while the pulsar database processes the observation data and establishes and stores pulsar signal models. For the VLBI observation network, it can use the existing observation network on Earth or the observation network deployed in space in the future. The XNAV system is similar to a GPS receiver, installed on the target spacecraft that needs navigation, and is responsible for real-time positioning.

## 
同时观测多个脉冲星信号，可以得到多个观测方程，从而可以通过非线性最小二乘法求解航天器的位置。虽然脉冲信号的周期会引入整数模糊性，但在航天器已有精度优于300公里的初始导航解的情况下，可以忽略这种影响。在每一个计算周期内，系统除了观测脉冲星信号外，还需要不断更新自身的位置向量。

这样不断借助观测到的脉冲星信号来更新自身的位置向量，可以有效控制 inertial navigation system (INS) 的误差累积[@WANG_2023]，从而实现长时间的高精度导航。

与GPS观测原理类似，XNAV 系统通过同时观测多个脉冲星信号，可以得到多个观测方程，从而利用非线性最小二乘法求解航天器的位置。尽管脉冲信号的周期可能引入整数模糊性，但在航天器的初始导航解精度超过 300 公里的情况下，这种影响可以忽略不计。在每个计算周期内，除了观测脉冲星信号外，系统还需要不断更新自身的位置向量。通过不断借助观测到的脉冲星信号来更新位置向量，可以有效控制惯性导航系统（INS）的误差积累。

Similar to the GPS observation principle, the XNAV system can obtain multiple observation equations by simultaneously observing multiple pulsar signals, and then solve the position of the spacecraft using the nonlinear least squares method. Although the period of the pulsar signal may introduce integer ambiguity, this effect can be ignored when the initial navigation solution of the spacecraft has an accuracy of more than 300 kilometers. In each calculation period, the system needs to continuously update its position vector in addition to observing the pulsar signal.


多个航天器同时观测同一脉冲星，通过比较它们接收的脉冲星到达时间（TOA），可以计算相对投影距离，并构建星座的观测向量，从而提高星座整体定位精度，支持协同导航。融合地面测量、星座观测和恒星数据等多种数据源，可进一步提升定位精度。这也就意味着，我们可以构建一个基于XNAV的深空协同导航网络。

Multiple spacecraft simultaneously observe the same pulsar, and by comparing the pulsar arrival times (TOAs) received by them, the relative projection distance can be calculated, and the observation vector of the constellation can be constructed to improve the overall positioning accuracy of the constellation and support collaborative navigation. The integration of various data sources such as ground measurements, constellation observations, and star data can further improve the positioning accuracy. This means that we can build a deep space collaborative navigation network based on XNAV.