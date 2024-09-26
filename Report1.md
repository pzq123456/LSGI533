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

GPS positioning is based on the position of GPS satellites. As a result, any GPS positioning algorithm should first confirm the position of the GPS satellites before it can calculate the target location. 

In space, the position of satellites is determined using the ECSF coordinate system. The ECSF (Earth-Centered, Earth-Fixed) coordinate system is an inertial coordinate system, which is a valid system for representing the Keplerian motion of satellites in the vicinity of the Earth. The origin, O (0,0,0), is at the Earth's center of mass. The z-axis is parallel to the Earth's rotational axis and points towards the North Pole. The x-axis points towards the intersection of the Prime Meridian and the Equator. The y-axis is perpendicular to the xOz plane (i.e., it points towards the intersection of 90 degrees East longitude and the Equator), forming a right-handed coordinate system.

GPS satellite motion can be represented as a type of Keplerian motion with perturbations(disturbed satellite motion). The perturbations are caused by the gravitational forces of many factors, such as the Earth's non-spherical shape, the gravitational forces of the Sun and the Moon, and the atmospheric drag.

For engineering purposes, the satellite's orbit can be described as follows:

$$ r = r_0 + \Delta r \tag{2.1} $$

where $ r $ is the satellite's position vector(in ECSF), $ r_0 $ is the unperturbed motion, and $ \Delta r $ is the perturbed motion. 

### 2.1 GPS Broadcast Ephemerides and Precise Ephemerides
The predicted orbits are curve fitted to a set of relatively simple disturbed Keplerian elements and transmitted to the users. Similar to weather forecasts, GPS Broadcast Ephemerides cannot guarantee very high precision. 

At any given time, the satellite transmits the following parameters to the user in the form of Broadcast Ephemerides:

- SV-id : satellite number 
- $t_c$ : reference epoch of the satellite clock 
- $a_0, a_1, a_2$ : polynomial coefficients of the clock error 
- $t_{oe}$ : reference epoch of the ephemerides 
- $\sqrt{a}$ : square root of the semimajor axis of the orbital ellipse 
- $e$ : numerical eccentricity of the ellipse 
- $M_0$ : mean anomaly at the reference epoch te 
- $ω_0$ : argument of perigee 
- $i_0$ : inclination of the orbital plane 
- $Ω_0$ : longitude of the ascending node at the weekly epoch 
- $Δ_n$ : mean motion difference 
- $\dot{I}$ : rate of inclination angle 
- $\dot{\Omega}$ : rate of node’s right ascension 
- $C_{uc}, C_{us}$ : correction coefficients (of argument of latitude) 
- $C_{rc}, C_{rs}$ : correction coefficients (of geocentric distance) 
- $C_{ic}, C_{is}$ : correction coefficients (of inclination) 

In this table, we have one reference epoch for the satellite clock ($t_c$) and another for the ephemerides ($t_{oe}$), six orbital elements ($\sqrt{a}, e, M_0, ω_0, i_0, Ω_0$), and nine correction coefficients ($Δ_n, idot, \dot{\Omega}, C_{uc}, C_{us}, C_{rc}, C_{rs}, C_{ic}, C_{is}$).

Consistent observation and systematic adjustment of the GPS satellites can correct the uncertainty of the Broadcast Ephemerides, resulting in what is called Precise Ephemerides. They can be downloaded for free from several internet homepages (e.g., www.gfz-potsdam.de).

### 2.2 Steps for GPS Satellite Oribit Position Computation

1. Calculate the mean motion of the satellite $n$:
$$ n = \sqrt{\frac{μ}{a^3}} + \Delta n \tag{2.1} $$

where $μ = 3.986005 × 10^{14} m^3/s^2$ [$^{[2]}$](http://www.braeunig.us/space/constant.htm) is the Earth's gravitational constant, and $a$ is the semimajor axis of the orbital ellipse. The $\Delta n$ term is the mean motion difference transmitted by the satellite.



## 3. Satellite clock error algorithms

## 4. Receiver positioning algorithms with Pseuorange Measurements


## References
1. GPS: Theory, Algorithms and Applications, by Guochang Xu. Springer, 2007. doi: https://doi.org/10.1007/978-3-662-50367-6
2. BASIC CONSTANTS FOR ASTRODYNAMICS, http://www.braeunig.us/space/constant.htm
4. [GPS.js](https://github.com/infusion/GPS.js/?tab=readme-ov-file) : GPS.js is an extensible parser for NMEA sentences, given by any common GPS receiver. The output is tried to be as high-level as possible to make it more useful than simply splitting the information. The aim is, that you don't have to understand NMEA, just plug in your receiver and you're ready to go.
5. https://www.movable-type.co.uk/scripts/geodesy-library.html