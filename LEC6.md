# High Precision Positioning with GNSS

## Real-Time Kinematic (RTK) Positioning and Network RTK

## Methods to resolve ambiguity Quickly
- Start from a know point 在第一个点测量1h
- Antenna Exchange 改变接收机的geomatry 与 等待卫星的geomatry 改变等效
- Principle of Searching 越多不同方向上的卫星越容易确定位置

## Fast Ambiguity Resolutions
- Frei Method
- LAMBAD Method 只关心最小的两个，记录一个全局最小值，遇到更小的就更新否则就不继续算下去
- Integer Least Square
  - Pull-in Region 格网化处理，落在格网内位置算作中心点。每个格网还会细分出更多的区域 Success Failure undecided，可以控制区域的大小以控制概率
  - Integer Aperture (IA) estimator
  - Ellipsoidal Integer Aperture Estimator (EIA)
  - Combining Ratio/EIA

## Network RTK

## GNSS High Precision Positioning 超长时间观测 时间序列测量值的处理'
## What Do we do with GPS Time Series -Problems just started
- Separate geophysical information from noise - "Your noise is my signal" (and vice-versa).

## Precise Point Positioning
- IGS is formed since 1994 由该组织提供轨道数据、钟差数据，只需要一个接收机就可以实现高精度定位
  - Ionosphere-free observation (phase)
  - Un-differential 
  - 但是需要考虑卫星姿态变化 Example: Phase wind-up 差分可以直接去掉，但是单点需要建模
  - 主要问题是处理 Ambiguity 因为不再是整数所以需要更多时间来确定。 Time Convergence （随着星座的运动，确定的时间也是不同的，最多会超过一个小时）
    - PPP – Ambiguity Resolution (AR) 该问题也可以通过消除 bias 来重新是的 Ambiguity 变为整数
  - PPP-RTK 与 RTK 网络结合