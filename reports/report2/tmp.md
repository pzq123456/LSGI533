# Report 2 (20%) : 
> - PanZhiQing24037665g

## Abstract

## Contents
- [Report 2 (20%) :](#report-2-20-)
  - [Abstract](#abstract)
  - [Contents](#contents)
  - [1. Introduction](#1-introduction)
  - [2. Review of GNSS Multipath Error Mitigation Methods In Recent Years](#2-review-of-gnss-multipath-error-mitigation-methods-in-recent-years)
    - [2.1 Machine Learning-based Methods](#21-machine-learning-based-methods)
    - [2.2 3D Model-based Methods(3DMA GNSS)](#22-3d-model-based-methods3dma-gnss)
    - [2.3 Multi-Device Fusion Method](#23-multi-device-fusion-method)
    - [2.4 Receiver Design](#24-receiver-design)
  - [4. Appendix](#4-appendix)
    - [1. Convolution Neural Network (CNN)](#1-convolution-neural-network-cnn)
    - [2. Long Short-Term Memory (LSTM)](#2-long-short-term-memory-lstm)
    - [3. Ray Tracing](#3-ray-tracing)
  - [References](#references)


## 1. Introduction

GPS Receiver will receive GPS satellite signals reflected from the surrounding environment. Compared to the direct signal received by the receiver, these reflected signals often take longer to reach the receiver, resulting in positioning errors. This phenomenon is also known as multipath effect. In general, the receiver may receive two types of signals at the same time (direct, multipath indirect) (as shown in Figure 1).

<!-- ![](./imgs/p1.png) -->
<img src="./imgs/p1.png" width="400" />

Figures 1: Multipath effect on GNSS signal

As mentioned earlier, the impact of multipath effects is highly dependent on the local environment in which the receiver is located and the height of the satellite position. At the same time, the structural factors of the receiver should also be considered. Different receivers adopt different designs, so the effect of reducing multipath effects will also be different. Considering that the satellite is in motion, we can model the multipath effect as a function of time. Assuming that the signal received by the direct receiver is represented by:

$$
s(t) = A \cos(\omega t + \phi) \tag{1.1}
$$

The signal after multipath reflection is represented by:

$$
s'(t) = f \times s(t + \delta t) \tag{1.2}
$$

Where $f$ is the attenuation coefficient brought by the reflection, and $\delta t$ is the time delay.

Multipath effects essentially bring time delays, so their impact on positioning accuracy is proportional to the wavelength. For example, for P-code signals with a wavelength of about 30 meters, the impact of multipath effects is about 15 meters; for C/A signals, the wavelength is about 300 meters, and the impact of multipath effects is about 150 meters. If shorter wavelength carrier observations are used, the impact of multipath effects will be reduced to the centimeter level. Another characteristic of multipath effects is related to the GPS signal itself. The GPS signal is right-handed circularly polarized (RHCP), and the signal reflected by multipath effects will change this property. From the receiver's perspective, the signal's signal-to-noise ratio will be significantly reduced (1/3). Therefore, we can try to keep the receiver away from the reflecting surface as much as possible, or use carrier observations to mitigate the impact of multipath effects. In cases where C/A signals must be used, we can use phase-smoothed codes to reduce the impact of multipath effects.

If you want to accurately eliminate multipath effects, you need to detect the signals affected by multipath effects and weaken them. Generally, a combination of code and phase is used to detect multipath effects. Reviewing the pseudorange measurement model (Report1 4.4) and the carrier phase measurement model (Report1 4.8) in the previous report, we can derive a joint formula for detecting multipath effects:

$$
R_r^s(t_r,t_e) - \lambda \phi_r^s(t_r) = 2 \delta_{ion} + \lambda N_r^s + \delta_{mul} + \epsilon \tag{1.3}
$$

Where $R_r^s(t_r,t_e)$ is the pseudorange observation value, $\lambda \phi_r^s(t_r)$ is the carrier phase observation value, $\delta_{ion}$ is the ionospheric delay, $\lambda N_r^s$ is the integer ambiguity, $\delta_{mul}$ is the effect of multipath on code observation, and $\epsilon$ is the error of code observation. Since the error of carrier phase observation is much smaller than the error of code observation, we can detect multipath effects through carrier phase observation.

## 2. Review of GNSS Multipath Error Mitigation Methods In Recent Years

<!-- ### 2.1 Combination of Computer Science Methods -->

With the development of computer technology, people's ability to model the real world is also constantly improving. Compared with traditional methods based on empirical formulas, filters, etc., it is now possible to perform more detailed modeling and analysis through computers. For example, the use of machine learning algorithms to detect multipath signals in GNSS measurements has been proposed in recent years.[$^3$](#References) In addition, the use of 3D models of cities and ray-tracing techniques to detect multipath signals has also been proposed.[$^{4,5}$](#References)


### 2.1 Machine Learning-based Methods
在过去的十来年，机器学习算法越来越多地参与到定位相关的应用中，例如处理从各类复杂传感器中获取到的大量数据（LiDAR pointclouds、高清照片等）。概括性地讲，机器学习算法依赖大量的数据，尤其是有标注的数据。这些算法首先会从数据中提取有效特征（embedding），然后优化网络参数以识别这些特征以达成特定的任务（分类、分割及目标检测等）。相较于传统的基于统计学或信号处理领域的算法，这种基于数据驱动的方法更加灵活，且在一定程度上可以适应不同的场景。但是，也存在一些问题，例如需要大量的标注数据、模型的可解释性较差及过拟合等。

机器学习算法可以自动建模、提取及识别复杂数据集中的特征。GNSS 接收机的观测数据本质上是一个兼具时间维度、空间维度和频率维度的多维数据集。这种多维度数据正是机器学习算法所擅长处理的。例如经典的 CNN 网络，可以对图像数据进行特征提取和分类。若我们将 GNSS 的接收机数据格式化为类似于多通道图像数据的格式，就可以使用 CNN 网络来识别多径信号。Evgenii Munin 等人通过构建人造信号来模拟不同的GNSS接收器配置，并将输出的两个波段信号（I、Q）格式化为在地理空间分布的二维图像，然后使用 CNN 网络来识别多径信号。可以发现，在多径信号区域 CNN 被明显激活，从而实现了多径信号的检测。[$^7$](#References)


![](./imgs/p6.png)
Figure 6: Activation map of CNN for multipath detection in GNSS receivers.




机器学习算法除了可以有效识别多路径效应外，还可以预测诸如GNSS satellite visibility、 pseudorange error 等其他 GNSS 测量的不确定性。例如，Zhang 等人使用 LSTM 网络来预测 GNSS 测量的不确定性。[$^{11}$](#References) 其中， satellite visibility 指的是卫星是否受到遮挡，pseudorange error 指的是多径效应引起的伪距误差。他们通过 FCNN 网络来提取 GNSS 信号的特征，然后通过 LSTM 网络来整合时序 GNSS 信号上下文以预测卫星可见性和伪距误差。 Fully Connected Neural Networks (FCNNs) 是一种常见的神经网络结构，主要用于特征提取及输出格式化。Long Short-Term Memory (LSTM) 通过引入记忆单元来模拟记忆及遗忘过程，从而实现对时序数据的建模。



![](./imgs/p8.png)
Figure 7: LSTM-based GNSS measurement uncertainty prediction.

### 2.2 3D Model-based Methods(3DMA GNSS)

除了匹配卫星可见性外，3DMA GNSS 射线跟踪进一步考虑了测量和基于 3D 建筑模型的预测之间的伪距延迟匹配。尽管 3DMA GNSS 可以在密集城市区域实现 10 米的定位精度。



在该领域，较早被提出的一个方法是通过城市的 3D 数字模型来检测并剔除可能会收到多路径影响的卫星(shadow matching 方法)。在此之后有基于光线追踪技术的方法来量化城市中建筑物引起的多径效应，该方法在高楼密集的区域能够达到10m的定位精度。



<!-- shadow matching 方法 -->
之所以需要通过城市的 3D 数字模型来检测多径干扰，是因为手机中安装的消费级 GNSS 接收机功率不够，难以通过信噪比（SNR）区分直射线（LOS）信号和通常的非直射线（NLOS）信号。 
Wang 等人[$^12$](#References) 使用伦敦市部分区域的 3D 建筑模型，结合星历数据使用 Shadow matching 方法对接收到的信号进行排位，仅挑选排位高的信号进行定位。


![](./imgs/p9.png)
Figure 8: 3D Model for London City.


他们使用的 Shadow matching 方法，具体来说就是将建筑物边界表示为方位角-高程对，然后投影至当地的天空图中，这样再结合星历数据计算出的卫星位置，就可以构造用于排位的指标。


![](./imgs/p10.png)
Figure 9: an example of a building boundary as azimuth-elevation pairs in a sky plot. 

通过在接收机附近（例如，15m内）随机选择采样点，结合城市的数字模型和射线追踪技术，我们可以计算出每个采样点的模拟伪距值。结合实测伪距，这些模拟伪距可以用于校正实测伪距观测值（例如，基于相似性的加权平均）并检测异常值（例如，反射两次或两次以上的多径信号）。[$^5$](#References)


<img src="./imgs/p4.png" width="400" />

Figure 10: Multipath detection with 3D digital maps for robust multi-constellation GNSS/INS vehicle localization in urban areas.



随着城市数字资产逐步增长（例如谷歌地球中的城市模型），这项技术的应用前景也越发广阔。但是，这项技术也存在若干局限性，例如某一城市的三维模型过于放大，导致计算量过大，或者某些城市的三维模型尚未建立等。此时，可以考虑使用 LiDAR 来实时生成局地区域的三维模型。



类似于 Google Earth 中的城市三维模型只包含了静态的城市建筑物模型，而在实际的城市道路中，动态的障碍物也会产生多径效应（例如，香港街头常见的双层大巴）。此时，如果只是依赖静态的城市建筑物模型来检测多路径效应就无法满足实际需求，甚至会带来另外的误差。使用 LiDAR 来实时生成城市道路的三维模型，结合车载 GNSS 接收机，可以实现对动态障碍物的检测和多径效应的实时消除，从而提高车载 GNSS 在城市道路上的定位精度。[$^9$](#References) 



Weisong Wen 等人使用 LiDAR 实时获取三维点云数据，并结合 GNSS 接收机的实时观测数据，实时检测并剔除受到双层巴士遮挡的卫星信号，从而提高车载 GNSS 在香港城市道路上的定位精度。以下是具体的步骤：



![](./imgs/p5.png)
Figure 11: Real-time exclusion of GNSS NLOS receptions caused by dynamic objects in heavy traffic urban scenarios using real-time 3D point cloud.



### 2.3 Multi-Device Fusion Method

在自动驾驶领域，获取位置信息可以通过融合多种传感器数据来实现。例如，车载 GNSS 接收机、IMU、激光雷达、摄像头等。这些传感器数据可以提供不同的信息，例如车辆的位置、姿态、速度、周围环境的三维点云数据、高清照片等。

Weisong Wen 等人提出了一种基于全传感器套件的数据集 UrbanLoco，该数据集包含一套完整的传感器信息，包括激光雷达、360度视角相机、惯性测量单元（IMU）和全球导航卫星系统（GNSS）。考虑到高层建筑密集的城市区域会显著遮挡 GNSS 信号，并有伴生的多径效应及 NLOS 问题，他们通过估算某一点位的城市化率来评估 GNSS 定位的可靠性。城市化率是指某一点位周围被建筑物遮挡的天空的比例。[$^{10}$](#References)

他们使用 Skymask 方法，通过安装在车顶鱼眼相机拍摄的图像，结合图像分割算法，生成极坐标图显示建筑物轮廓。Skymask 中的灰色区域表示被建筑物阻挡的天空，白色区域表示清晰天空。Skymask 的生成可基于三维建筑模型或使用车辆顶部的鱼眼相机及图像分割算法。为了定量分析Skymask，进一步定义了两个参数：平均掩膜高程角（µMEA）和掩膜高程角标准差（σ²MEA）。它们的定义如下：

- 平均掩膜高程角$\mu_{MEA}$计算公式：

$$
\mu_{MEA} = \frac{1}{N} \sum_{\alpha=1}^{N} \theta_{\alpha}
$$
  
- 掩膜高程角标准差$\sigma^2_{MEA}$计算公式：

$$
\sigma^2_{MEA} = \frac{\sum_{ \alpha=1}^{N} (\theta_{\alpha} - \mu_{MEA})^2}{N-1}
$$

其中，$\theta_{\alpha}$ 表示在特定方位角 $\alpha$ 下的高程角，与建筑物高度密切相关，$N$ 表示来自 Skymask 的均匀间隔的方位角数量。通常，$N$ 取 360，这意味着方位角的分辨率为 1 度。

当车处于密集城市区域时，Skymask 通常会被高层建筑主导，从而导致较大的 $\mu_{MEA}$ 和相对较小的 $\sigma^2_{MEA}$。而在农村地区，$\mu_{MEA}$ 和 $\sigma^2_{MEA}$ 都相对较小。在高低建筑混合的地区，$\sigma^2_{MEA}$ 会相对较大。

通过上述城市化测量方法，数据集评估了当前测绘/定位数据集的城市化率。结果表明，三个数据集的城市化水平明显低于香港的城市化水平。通过测量城市化率，可以评估当前定位数据集的城市化率，从而评估 GNSS 定位的可靠性。同时，也可以选择在这些区域采用其他定位方法，例如IMU、激光雷达等。




### 2.4 Receiver Design
消费级别的 GNSS 天线具有较低的增益和较少的极化区分。这使得通过信噪比（SNR）区分直射线（LOS）信号和通常的非直射线（NLOS）信号更加困难。因此，天线设计是消除多径干扰的关键因素之一。在大多数情况下，直接的 GPS 信号是从上方水平方向传来的，而多径信号是从下方水平方向传来的；GPS 信号是右旋圆极化的，而多径信号可能是左旋圆极化的。因此，在确保从上方水平方向有清晰视野的前提下，天线设计应尽量减少从下方水平方向接收信号。此外，侧向辐射和背向辐射也是多径干扰的重要来源。



<img src="./imgs/p2.png" width="300" />

Figure 12: A choke ring antenna (real photo).


<img src="./imgs/p3.png" width="400" />

Figure 13: A dual-band reduced-surface-wave patch antenna (top view).

<div STYLE="page-break-after: always;"></div>


## 4. Appendix
I will add some necessary content in this section.

### 1. Convolution Neural Network (CNN)
从工程角度讲，一个典型的 CNN 网络主要包括三个部分，即卷积层、池化层和全连接层。卷积层主要用于提取特征，池化层主要用于降维，全连接层主要用于分类。最典型的，假设我们有一个$[64 \times 64 \times 3]$的输入，经过卷积层和池化层后，最终输出一个$[1 \times 1 \times n]$的输出，其中$n$表示可能的类别数。CNN 网络的结构如图所示。

![](./imgs/p11.png)
Figure 10: An simple CNN architecture, comprised of just five layers

具体来讲，卷积层又可以按照维度分为一维卷积、二维卷积和三维卷积。对于一维卷积([Conv1d](https://pytorch.org/docs/stable/generated/torch.nn.Conv1d.html#torch.nn.Conv1d))，我们假设输入为$(C_{in},L)$，其中$C_{in}$表示输入的通道数，$L$表示输入的长度。输出为$(C_{out},L_{out})$，其中$C_{out}$表示输出的通道数，$L_{out}$表示输出的长度。卷积核的大小为$(C_{out},C_{in},K)$，其中$K$表示卷积核的长度。卷积操作的公式如下：

$$
C^{outj} = bias(C^{outj}) + \sum_{k=0}^{C_{in} - 1} Weight(C^{outj},k) \ast C^{inj} \tag{4.1}
$$

![](./imgs/p12.png)
Figure 11: An example of 2D convolution operation

其中，$C^{outj}$表示输出的第$j$个通道，$C^{inj}$表示输入的第$j$个通道，$Weight(C^{outj},k)$表示卷积核的第$j$个通道和第$k$个通道的权重，$\ast$表示互相关操作。对于互相关操作，我们有：

$$
(f * g)[n] = \sum_{m=-\infty}^{\infty} f[m] g[n + m] \tag{4.2}
$$

其中，$n$是索引变量，表示信号的平移。在卷积操作中，我们通常使用互相关操作来表示卷积操作。在数学中，互相关操作（cross-correlation）通常用于信号处理和统计学中，表示两个信号或函数之间的相似度。卷积操作和互相关操作的区别在于卷积操作会翻转卷积核。对于二维卷积和三维卷积，我们可以类似地定义卷积操作。

池化层主要用于降维，常见的池化操作有最大池化和平均池化。典型的，我们以最大一维池化([MaxPool1d](https://pytorch.org/docs/stable/generated/torch.nn.MaxPool1d.html#torch.nn.MaxPool1d))为例，假设输入为$(C_{in},L)$，输出为$(C_{out},L_{out})$，池化核的大小为$K$，池化操作的公式如下：

$$
P^{outj} = \max_{k=0}^{K-1} P^{inj+k} \tag{4.3}
$$

池化操作也就是在输入的每个通道上取一个固定大小的窗口，然后取窗口中的最大值或平均值作为输出。

![](./imgs/p13.png)
Figure 12: An example of 2D max pooling operation

### 2. Long Short-Term Memory (LSTM)

### 3. Ray Tracing
主要详细介绍
  - CNN、LSTM 等机器学习算法
  - 光线追踪技术
  - 及GPU加速计算在 GNSS 领域中的应用

## References
1. GPS: Theory, Algorithms and Applications, by Guochang Xu. Springer, 2007. doi: https://doi.org/10.1007/978-3-662-50367-6

2. Basilio, Lorena I., Richard L. Chen, Jeffery T. Williams, and David R. Jackson. "A New Planar Dual-Band GPS Antenna Designed for Reduced Susceptibility to Low-Angle Multipath." IEEE Transactions on Antennas and Propagation 55, no. 8 (2007): 2358-2366. doi: 10.1109/TAP.2007.901818

3. Kim, Sanghyun, Jungyun Byun, and Kwansik Park. "Machine Learning-Based GPS Multipath Detection Method Using Dual Antennas." arXiv preprint arXiv:2204.14001 (2022). doi: https://doi.org/10.48550/arXiv.2204.14001

4. Hsu, Li-Ta, Yanlei Gu, and Shunsuke Kamijo. "NLOS Correction/Exclusion for GNSS Measurement Using RAIM and City Building Models." Sensors 15, no. 7 (2015): 17329-17349. doi: 10.3390/s150717329

5. M. Obst, S. Bauer, P. Reisdorf and G. Wanielik, "Multipath detection with 3D digital maps for robust multi-constellation GNSS/INS vehicle localization in urban areas," 2012 IEEE Intelligent Vehicles Symposium, Madrid, Spain, 2012, pp. 184-190, doi: 10.1109/IVS.2012.6232285.

6. Paul Schwarzbach, Albrecht Michler, Oliver Michler. "3DMA Grid-based Hybrid 3DMA GNSS and Terrestrial Positioning." arXiv preprint arXiv:2309.05644 (2023). doi: https://doi.org/10.48550/arXiv.2309.05644

7. Evgenii Munin, Antoine Blais, Nicolas Couellan. "Convolutional Neural Network for Multipath Detection in GNSS Receivers." arXiv preprint arXiv:1911.02347 (2019). doi: https://arxiv.org/pdf/1911.02347

8. Ashwin V. Kanhere, Shubh Gupta, Akshay Shetty, Grace Gao. "Improving GNSS Positioning using Neural Network-based Corrections." arXiv preprint arXiv:2110.09581 (2021). doi: https://doi.org/10.48550/arXiv.2110.09581

9. Weisong Wen, Guohao Zhang, Li-Ta Hsu. "Exclusion of GNSS NLOS Receptions Caused by Dynamic Objects in Heavy Traffic Urban Scenarios Using Real-Time 3D Point Cloud: An Approach without 3D Maps." arXiv preprint arXiv:1804.10917 (2018). doi: https://doi.org/10.48550/arXiv.1804.10917

10. W. Wen, G. Zhang, L. Hsu, "UrbanLoco: A Full Sensor Suite Dataset for Mapping and Localization in Urban Scenes," 2020 IEEE International Conference on Robotics and Automation (ICRA), Paris, France, 2020, pp. 2310-2316, doi: 10.1109/ICRA40945.2020.9196526.

11. G. Zhang, P. Xu, H. Xu and L. -T. Hsu, "Prediction on the Urban GNSS Measurement Uncertainty Based on Deep Learning Networks With Long Short-Term Memory," in IEEE Sensors Journal, vol. 21, no. 18, pp. 20563-20577, 15 Sept.15, 2021, doi: 10.1109/JSEN.2021.3098006.

12. Wang, L., Groves, P. D., & Ziebart, M. K. (2015). Smartphone Shadow Matching for Better Cross-street GNSS Positioning in Urban Environments. Journal of Navigation, 68(3), 411-433. doi: 10.1017/S0373463314000836
