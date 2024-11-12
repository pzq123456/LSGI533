# System Desigh
> PanZhiQing | 2024-11-11 23:00

## 0. 背景及引入
> - 1 l.y = 9.461e+12 km = 9.461e+15 m = 63240 AU

比邻星距离地球约**4.24光年**，即 268,137 AU，是距离我们最近的恒星系统。假设我们以目前最快的无人探测器（如“旅行者1号”约17 km/s）的速度，并考虑加速和减速操作来完成前往比邻星的旅程，可以进行以下估算。旅行者1号的速度为**17 km/s**，约为**0.000057倍光速**。不考虑加速和减速的理想情况下，前往比邻星的时间计算如下：

$$ T = \frac{4.24 l.y}{0.000057 c} \approx 74,386 y $$

其中，$l.y$表示光年，$c$表示光速，$y$表示年。

这意味着仅保持目前的速度不变，就需要**约74,000年**才能抵达比邻星，在这样长的航程中，如何提供可靠的定位和授时服务，是一个极具挑战性的问题。现在假设我们从比邻星出发，那么在最终进入太阳系时，最大允许误差可以做如下估算。

从空间角度来讲，太阳系八大行星大致位于半径 100 天文单位的球体内。**比邻星到太阳系的距离**：4.24 光年 ≈ 268,137 AU。**太阳系行星分布的范围**：太阳系八大行星主要分布在距太阳 100 AU 以内的球体中。为了确保进入太阳系且不与八大行星擦肩而过，我们可以假设目标精度是使得误差不超过 100 AU 的范围，即最终到达太阳系时的允许偏差半径。

$$
\Delta\theta = \frac{\delta}{r} = \frac{100 AU}{268137 AU} \approx 3.73 \times 10^{-4} rad = 76.9 arcsec
$$

Where: $\Delta\theta$ is the angular deviation, $\delta$ is the deviation distance, $r$ is the distance from the target.

![](../imgs/p4.png)

**我们需要在抵达太阳系附近时将定位精度控制在约 76.9 角秒以内，或者约 $3.73 \times 10^{-4}$ 弧度，以保证进入太阳系的行星分布范围内。**

注意，这样的定位精度并非总是需要，在航程的初期阶段只需要保持一个大致的方向即可，但在接近目标时，定位精度就变得至关重要。因此，我们需要一个系统，能够在整个航程中提供不同精度的定位服务，以满足不同阶段的需求。类似于瓦片地图，随着航程的推进，我们需要逐渐细化定位精度，以确保探测器能够准确进入目标星系。

![](../imgs/p5.png)

## 1. 系统框架

The X-ray pulsar-based spacecraft positioning system mainly consists of an X-ray
detector, spacecraft-borne atomic clock, spacecraft-borne computational device, nav-
igation model algorithms database and pulsar model database. The workflow of the
whole system is given in Fig.

### 1.1 时空框架

重力场与相对论效应
- gravitational environment 
- correcting time delay caused by the geometrical and general relativistic effect.

The X-ray pulsar-based navigation method works by comparing the pulse TOA at the spacecraft and that at the SSB. As the solar system is a Riemannian space, the relationship between the measured and the predicted TOA has to consider the general relativistic effect.

### X-Ray Pulsar-Based Spacecraft Time Keeping

### Traditional Celestial Measurement Model
The so-called stellar angle measurement refers to the angle between the direction vector of a reference planet and of a star with respect to the satellite.

## 2. 脉冲星的特性
![](../imgs/p6.png)
## 3. 特殊的应用环境（宇宙尺度）