# Report 2 (20%) : 
> - PanZhiQing24037665g
> - Report 2 (20%) (submission date: 8 Nov)
> - Review of mitigation methods for GNSS multipath errors



> - 文献综述报告
> - 需要阅读4-10篇相关文献
> - 天线设计、信号处理方法、
> - big picture
> - 具体讲解一种方法，也可以只深入简介一种方法 Wen Duo Jie 及 Wu Chen 会阅读这些 report。

## Abstract

## Contents

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

In the past decade, machine learning algorithms have been increasingly involved in positioning-related applications, such as processing large amounts of data obtained from various complex sensors (LiDAR point clouds, high-definition photos, etc.). In general, machine learning algorithms rely on large amounts of data, especially annotated data. These algorithms first extract effective features (embedding) from the data, and then optimize the network parameters to identify these features to achieve specific tasks (classification, segmentation, and object detection, etc.). Compared with traditional algorithms based on statistics or signal processing, this data-driven method is more flexible and can adapt to different scenarios to some extent. However, there are also some problems, such as the need for a large amount of annotated data, poor interpretability of the model, and overfitting.


机器学习算法可以自动建模、提取及识别复杂数据集中的特征。GNSS 接收机的观测数据本质上是一个兼具时间维度、空间维度和频率维度的多维数据集。这种多维度数据正是机器学习算法所擅长处理的。例如经典的 CNN 网络，可以对图像数据进行特征提取和分类。若我们将 GNSS 的接收机数据格式化为类似于多通道图像数据的格式，就可以使用 CNN 网络来识别多径信号。Evgenii Munin 等人通过构建人造信号来模拟不同的GNSS接收器配置，并将输出的两个波段信号（I、Q）格式化为在地理空间分布的二维图像，然后使用 CNN 网络来识别多径信号。可以发现，在多径信号区域 CNN 被明显激活，从而实现了多径信号的检测。[$^7$](#References)

Machine learning algorithms can automatically model, extract, and identify features in complex datasets. The observation data of GNSS receivers is essentially a multidimensional dataset with time, space, and frequency dimensions. This multidimensional data is exactly what machine learning algorithms are good at handling. For example, the classic CNN network can extract features and classify image data. If we format the GNSS receiver data into a format similar to multi-channel image data, we can use the CNN network to identify multipath signals. Evgenii Munin et al. simulated different GNSS receiver configurations by constructing artificial signals and formatted the output two-band signals (I, Q) into two-dimensional images distributed in geographic space, and then used the CNN network to identify multipath signals. It can be found that CNN is significantly activated in the multipath signal area, thereby achieving multipath signal detection. [$^7$](#References)

![](./imgs/p6.png)
Figure 6: Activation map of CNN for multipath detection in GNSS receivers.

The machine learning-based GPS multipath detection method proposed by Kim et al. uses four features (i.e., C/N0, time difference of C/N0, difference between pseudorange time difference and pseudorange rate, satellite elevation angle) and one feature (i.e., double-difference pseudorange residual of dual antennas). The four machine learning algorithms used in the study are GBDT, Random Forest, Decision Tree, and K-Nearest Neighbor (KNN).[$^3$](#References)

### 2.2 3D Model-based Methods

We mentioned earlier that multipath effects are related to the local environment of the receiver and the height of the satellite position. In other words, the impact of multipath effects can be modeled by a computer. In Google Earth, more and more cities have detailed digital models. By combining these models with ray tracing techniques, we can quantify the multipath effects caused by buildings in the city and effectively reduce their impact. This method is called 3D city maps aided (3DMA) GNSS.

Through randomly selecting sampling points near the receiver (e.g., within 15m), combined with the city's digital model and ray tracing techniques, we can calculate the simulated pseudorange value of each sampling point. Combined with the real measured pseudorange, these simulated pseudoranges can be used to correct the real pseudorange observations (e.g., weighted average based on similarity) and detect outliers (e.g., multipath signals reflected two or more times).

<img src="./imgs/p4.png" width="400" />

Figure 2: Multipath detection with 3D digital maps for robust multi-constellation GNSS/INS vehicle localization in urban areas.

With the gradual maturity of technologies such as autonomous driving, the digital models of the surrounding environment can also be dynamically generated through vehicle-mounted radar. This dynamic 3D map can be fully combined with the vehicle-mounted GNSS receiver to achieve real-time detection and reduction of multipath effects, thereby improving the positioning accuracy of the vehicle-mounted GNSS in urban roads.

类似于 Google Earth 中的城市三维模型只包含了静态的城市建筑物模型，而在实际的城市道路中，动态的障碍物也会产生多径效应（例如，香港街头常见的双层大巴）。此时，如果只是依赖静态的城市建筑物模型来检测多路径效应就无法满足实际需求，甚至会带来另外的误差。使用 LiDAR 来实时生成城市道路的三维模型，结合车载 GNSS 接收机，可以实现对动态障碍物的检测和多径效应的实时消除，从而提高车载 GNSS 在城市道路上的定位精度。[$^9$](#References) 

Since the city's 3D model in Google Earth only contains static city building models, dynamic obstacles in actual city roads (e.g., double-decker buses commonly seen on Hong Kong streets) will also produce multipath effects. In this case, relying on static city building models to detect multipath effects cannot meet actual needs and may even introduce additional errors. Using LiDAR to generate real-time 3D models of city roads, combined with vehicle-mounted GNSS receivers, can achieve real-time detection of dynamic obstacles and real-time elimination of multipath effects, thereby improving the positioning accuracy of vehicle-mounted GNSS on city roads.

Weisong Wen 等人使用 LiDAR 实时获取三维点云数据，并结合 GNSS 接收机的实时观测数据，实时检测并剔除受到双层巴士遮挡的卫星信号，从而提高车载 GNSS 在香港城市道路上的定位精度。以下是具体的步骤：

Weisong Wen et al. use LiDAR to obtain real-time 3D point cloud data and combine it with real-time observation data from GNSS receivers to detect and exclude satellite signals blocked by double-decker buses in real time, thereby improving the positioning accuracy of vehicle-mounted GNSS on Hong Kong city roads. Here are the specific steps:

![](./imgs/p5.png)
Figure 3: Real-time exclusion of GNSS NLOS receptions caused by dynamic objects in heavy traffic urban scenarios using real-time 3D point cloud.

  1. First, cluster the 3D point cloud data based on Euclidean distance and identify double-decker buses through preset parameters.
  2. Centered on the vehicle-mounted GNSS receiver, project the satellites and double-decker buses onto the Skyplot for subsequent detection of blocked satellites.
  3. Exclude satellites blocked by double-decker buses based on the elevation angle, azimuth, signal-to-noise ratio of the satellite, and boundary information of the double-decker bus (elevation angle and azimuth in the Skyplot).
  4. Use satellites excluded from NLOS for GNSS positioning.

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

In the field of autonomous driving, location information can be obtained by fusing data from multiple sensors. For example, vehicle-mounted GNSS receivers, IMUs, LiDARs, cameras, etc. These sensor data can provide different information, such as the vehicle's position, attitude, speed, three-dimensional point cloud data of the surrounding environment, high-definition photos, etc.

Weisong Wen et al. proposed a dataset UrbanLoco based on a full sensor suite, which includes LiDAR, 360-degree view cameras, inertial measurement units (IMUs), and global navigation satellite systems (GNSS). Considering that densely built-up urban areas will significantly block GNSS signals and have associated multipath effects and NLOS problems, they evaluate the reliability of GNSS positioning by estimating the urbanization rate of a point. The urbanization rate refers to the proportion of the sky blocked by buildings around a point. [$^{10}$](#References)

They use the Skymask method to generate a polar coordinate map showing the outline of buildings by combining images taken by a fisheye camera installed on the roof of the vehicle with image segmentation algorithms. The gray area in Skymask represents the sky blocked by buildings, and the white area represents the clear sky. The generation of Skymask can be based on a 3D building model or using a fisheye camera and image segmentation algorithm on the top of the vehicle. To quantitatively analyze Skymask, two parameters are further defined: the mean elevation angle of the mask (µMEA) and the standard deviation of the elevation angle of the mask (σ²MEA). They are defined as follows:

- The formula for calculating the mean elevation angle $\mu_{MEA}$ of the mask:
$$
\mu_{MEA} = \frac{1}{N} \sum_{\alpha=1}^{N} \theta_{\alpha} \tag{2.1}
$$

- The formula for calculating the standard deviation of the elevation angle of the mask $\sigma^2_{MEA}$:

$$
\sigma^2_{MEA} = \frac{\sum_{ \alpha=1}^{N} (\theta_{\alpha} - \mu_{MEA})^2}{N-1} \tag{2.2}
$$

Where $\theta_{\alpha}$ represents the elevation angle at a specific azimuth $\alpha$, which is closely related to the building height, and $N$ represents the number of azimuths with uniform intervals from Skymask. Typically, $N$ is set to 360, which means that the resolution of the azimuth is 1 degree.

When the vehicle is in a densely built-up urban area, Skymask is usually dominated by high-rise buildings, resulting in a larger $\mu_{MEA}$ and a relatively smaller $\sigma^2_{MEA}$. In rural areas, both $\mu_{MEA}$ and $\sigma^2_{MEA}$ are relatively small. In areas with a mix of high and low buildings, $\sigma^2_{MEA}$ will be relatively large.

Through the above urbanization measurement method, the dataset evaluates the urbanization rate of the current mapping/positioning dataset. The results show that the urbanization levels of the three datasets are significantly lower than that of Hong Kong. By measuring the urbanization rate, the urbanization rate of the current positioning dataset can be evaluated, thereby evaluating the reliability of GNSS positioning. At the same time, other positioning methods, such as IMUs, LiDARs, etc., can also be selected in these areas.



### 2.4 Receiver Design
GPS Antenna Design is one of the key factors in eliminating multipath interference. In most cases, the direct GPS signal comes from above horizontally, while the multipath signal comes from below horizontally; the GPS signal is right-handed circularly polarized, while the multipath signal may be left-handed circularly polarized. Therefore, under the premise of ensuring a clear view from above horizontally, the antenna design should minimize the reception of signals from below horizontally. In addition, side radiation and back radiation are also important sources of multipath interference.

A choke ring antenna is a directional antenna designed for reception of GNSS signals from satellites. It consists of a number of concentric conductive cylinders around a central antenna.

For example, the classic choke ring antenna, which is designed to reduce ground reflection and low-angle multipath interference. Some well-designed choke ring antennas installed in ground stations can provide millimeter-level accuracy, making GPS positioning information useful for geodetic and geophysical measurements.

<img src="./imgs/p2.png" width="300" />

Figure 4: A choke ring antenna (real photo).

Also, there are some small antenna designs, such as the Dual-Band GPS-RSW Antenna. The Dual-Band GPS-RSW Antenna is a patch antenna designed for dual-frequency GPS (L1 and L2) with reduced surface wave. It has a compact dual-layer concentric ring structure (inner and outer rings correspond to L1 and L2, respectively). This antenna performs well in the horizontal plane and back radiation, significantly reducing ground reflection and low-angle multipath interference, suitable for high-precision positioning applications.[$^2$](#References)

<img src="./imgs/p3.png" width="400" />

Figure 5: A dual-band reduced-surface-wave patch antenna (top view).

<div STYLE="page-break-after: always;"></div>

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


