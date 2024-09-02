# Satellite Positioning and Navigation Systems
## Lecture 1
### Position
1. Positioning Methods
    • Landmarking
    • Celestial Positioning
    • Intersection with distance and angle

2. What does a single measurement tell us about our Position? (a single measurement can not measure position, 3D) 
    • Surface of Position (SOP, 3D)
    • Line of Positioning (LOP, 2D)

3. 3 points of GNSS
   1. orbit control points
   2. measurement 
   3. remove errors 

4. Positioning Error
    • Reference Station Errors
    • Distance Measurement Error
        – Systematic
        – Random
    • Positioning Geometry (e.g. 3 points are on a line)


propose a new positioning system --> good 

### Navigation
1. DEF(key): Navigation is a *process* of monitoring and controlling the movement of an object **from one place to another**. 
2. Navigating Process (feedback control): Determine Position -> Check Velocity -> Change Accelearte -> Determine Position
3. Performance Indicators

### Position Information for other users
- GNSS is also a Remote Sensing tool. (e.g. usage in Atmosphere Science )

### Introduction of Global Navigation Satellite Systems (GNSS)
1. GPS SYSTEM: 
   • Three segments
        – Space Segment
            •Satellites in Space
        – Ground Segment
            •5 monitor station and one master control centre (using atmoic clock, 5 measurements to calaulate the GPS satellites position)
        – User Segment
            •Any users with GPS receivers
   1. Monitor Stations, Space Segment, User Segment
   2. A KEY TO GPS SUCCESS : Atomic clocks no error (receiver has error), the delta_t(PSEUDORANGE) has error.

2. PSEUDORANGE MEASUREMENT: have receiver clock error
   - Time shift = PSEUDORANGE MEASUREMENT (in principle, time between transmission and reception is measured) Pseudorange = delta_t · c
   - Pseudo-range Pure geometrical range corrupted by :
     - Clock offsets 
     - Atmospheric errors 
     - Other error sources

3. at least 4 satellites necessary. more measurements can detect wrong
4. Differential GPS: 
   1. 2 receivers : DGPS reference receiver & user receiver
   2. removes most ephemeris, atmospheric and satellite clock errors
5. GPS Carrier Phase Surveying 载波相位跟踪

### Resilient and Seamless PNT Infrastructure


