# Report 1 (20%) : 
> Submission date: 18 Oct

- GPS Positioning algorithms
    - GPS observation Equations
- Pseudorange, carrier phase, and Doppler
    - GPS orbit coordinate computation and satellite clock error algorithms
    - Receiver positioning algorithms with Pseuorange Measurements

## Abstract

## Contents

## 1. GPS Positioning algorithms

## 2. GPS orbit coordinate computation
GPS positioning is based on the position of GPS satellites. As a result, any GPS positioning algorithm should first confirm the position of the GPS satellites before it can calculate the target location. GPS satellite motion is represented as a type of Keplerian motion, and the orbit can be defined by a set of Keplerian elements (GPS Broadcast Ephemerides) which are transmitted to the users (receivers). Similar to weather forecasts, GPS Broadcast Ephemerides cannot guarantee very high precision. Consistent observation and systematic adjustment of the GPS satellites can correct the uncertainty of the Broadcast Ephemerides, resulting in what is called Precise Ephemerides. They can be downloaded for free from several internet homepages (e.g., www.gfz-potsdam.de).

### 2.1 GPS Broadcast Ephemerides

The ECSF (Earth-Centered, Earth-Fixed) coordinate system is an inertial coordinate system, which is a valid system for representing the Keplerian motion of satellites in the vicinity of the Earth. The origin, O (0,0,0), is at the Earth's center of mass. The z-axis is parallel to the Earth's rotational axis and points towards the North Pole. The x-axis points towards the intersection of the Prime Meridian and the Equator. The y-axis is perpendicular to the xOz plane (i.e., it points towards the intersection of 90 degrees East longitude and the Equator), forming a right-handed coordinate system.

The predicted orbits are curve fitted to a set of relatively simple disturbed Keplerian elements and transmitted to
the users.

卫星星历，是人造卫星在每日各个时刻的位置数据列表，常用于卫星导航系统（GNSS）。例如，为了从GNSS观测量当中计算出点位之位置，必须获知卫星观测时刻的三维座标。卫星星历提供轨道参数之讯息，星历可以用来决定卫星之座标并包含卫星之准确度和性能状况，并透过GNSS观测量来获得地表测站之座标。

目前而言，GNSS资料之卫星资讯可分为广播星历（Broadcast ephemeris）和精密星历（Precise ephemeris）。广播星历是卫星传播之讯号内所载之卫星位置，而精密星历是全球卫星追踪站收集各站之卫星资料后经由严密平差计算，得知卫星之位置，其精度高于广播星历。

### 2.2 Precise Ephemerides

## 3. Satellite clock error algorithms

## 4. Receiver positioning algorithms with Pseuorange Measurements


## References 
1. [GPS.js](https://github.com/infusion/GPS.js/?tab=readme-ov-file) : GPS.js is an extensible parser for NMEA sentences, given by any common GPS receiver. The output is tried to be as high-level as possible to make it more useful than simply splitting the information. The aim is, that you don't have to understand NMEA, just plug in your receiver and you're ready to go.
2. https://www.movable-type.co.uk/scripts/geodesy-library.html