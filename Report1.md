# Report 1 (20%) : A Guideline for Implementing GPS Positioning Algorithms Using Pseudorange Measurements
> Submission date: 18 Oct

## Abstract

## Contents

## 1. Introduction
   - Briefly introduce GPS technology and its applications.
   - Explain the purpose of the report: to describe algorithms and equations that a programmer can use to write a program for GPS positioning.

## 2. GPS Positioning Algorithms
   - Overview: Explain what GPS positioning algorithms are and their significance.
   - GPS Observation Equations: 
     - Provide the detailed mathematical models that describe how GPS measurements are related to the position of the receiver and the satellites.
     - Include specific equations for pseudorange, carrier phase, and Doppler measurements.
     - Clearly label variables and constants to make it easy for a programmer to implement.

## 3. Pseudorange, Carrier Phase, and Doppler
   - Pseudorange: 
     - Define the pseudorange and explain how it is computed based on the time difference between the signal sent by the satellite and the signal received by the GPS receiver.
     - Include necessary equations and explain time adjustments (e.g., satellite clock errors).
   - Carrier Phase: 
     - Explain carrier phase measurements, how they improve accuracy, and provide equations.
   - Doppler Effect: 
     - Provide a mathematical explanation of how Doppler measurements give insight into the velocity of the receiver relative to the satellite.

## 4. GPS Orbit Coordinate Computation and Satellite Clock Error Algorithms
   - Orbit Calculation: 
     - Explain how to calculate satellite positions based on broadcast ephemeris data.
     - Provide relevant orbital equations that allow a programmer to compute satellite coordinates at any given time.
   - Satellite Clock Error: 
     - Provide equations for compensating satellite clock errors, ensuring the programmer understands how to account for this in their implementation.
  
## 5. Receiver Positioning Algorithms with Pseudorange Measurements
   - Introduction to Positioning Algorithms: 
     - Explain the concept of trilateration and how the pseudorange measurements from multiple satellites are used to determine the receiver's position.
   - Algorithm Outline: 
     - Provide step-by-step instructions for implementing a positioning algorithm using pseudorange measurements.
     - Include any iterative methods like least squares, which are often used to refine the position estimate.
  
## 6. Algorithm Implementation Guidelines
   - Algorithm Breakdown: 
     - Break down each algorithm into smaller steps or pseudocode so a programmer can easily follow the logic.
   - Key Challenges: 
     - Point out any potential challenges a programmer might face, such as handling multiple solutions in the positioning algorithm or dealing with clock drift.

## 7. Conclusion
   - Summarize the key points and emphasize how each part of the report connects to the final objective of GPS receiver positioning.