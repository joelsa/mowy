# Mowy
A truly automated lawn mowing robot using RTK localization

## Introduction

### Background
In recent times, robots have increasingly found their way into households to facilitate housework. Especially two areas have proven to be particularly well suited for automation: vacuuming and lawn mowing. 

A clear downward trend in costs has emerged in these two areas of robot application in the 2010s. At the same time, vacuum cleaner robots have also become more and more intelligent. With a few fortunate exceptions, this development has not yet reached lawn mower robots.

Most, if not all, lawnmower robots need a perimeter coil and drive around randomly within it. This is not primarily due to software, the required algorithms do not differ much between vacuum cleaner and lawnmower applications. Instead, it is more the sensors that are responsible, as they have to be much more robust and reliable in the field than indoors, for example due to the sun's influence on LIDARs.

However, a major advantage of robotics in the open is the availability of the Global Positioning System (GPS), especially in combination with the latest market maturity of low-cost real-time kinematics systems (RTK).
For example, there is the ZED-F9P from uBlox, which has virtually no systematic errors and, with correction data via [NTRIP][1] in measurements, achieves a standard deviation of less than 7 millimeters.

The thesis of this project is that a robot with such a system can already be built cost-effectively today, functions reliably enough and manages without a perimeter coil.
The aim of this project is to demonstrate this with a prototype and thus contribute to maximally automated - and therefore more efficient, faster and more elegant - lawnmower robots.
### Problem
As of 2019 almost all lawn mowing robots drive around randomly within the perimeter coil:
![alt text][random]
The idea is to have a human supervisor define a map in a xml-like format, which contains keep-in and keep-out zones:
![alt text][regions]
The robot then generates an optimized path using algorithms used for gcode optimization (think of the robot as a lawn cnc)
and drives via GPS:
![alt text][structured]

### Setup
Since the focus of this project is intended to be on software, rather than hardware, a commercially available lawn mowing robot (R800EASY) will be modified and serve as the basic platform.
I intend to add several peripherals to the robot, including a Raspberry Pi for path calculation, a LoRa module to receive correction data and an IMU to do some basic kalman sensor fusion for improved accuracy.
The simpleRTK2B Board from Ardusimple will be used as a ZED-F9P breakout.

Since the electronic control system of the R800EASY consist mainly of a single large PCB, modifying the control system is not easily possible. Due to this reason a custom motor driver and power management PCB has to be designed, built and programmed.

An (extremely) simplified system overview can be seen here: 
![alt text][generalsetup]

The robot gets correction data via LoRa from a base station inside the house:
![alt text][rtksetup]

[1]: https://en.wikipedia.org/wiki/Networked_Transport_of_RTCM_via_Internet_Protocol

[random]: ./documentation/images/book/random_paths.png "Random Paths"

[regions]: ./documentation/images/book/region_definitions.png "Region definitions"

[structured]: ./documentation/images/book/structured_paths.png "Structured Paths"

[generalsetup]: ./documentation/images/book/general_setup.png "General Setup"

[rtksetup]: ./documentation/images/book/rtk_setup.png "RTK Setup"