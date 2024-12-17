# 3D Printing Guide

A (hopefully) up-to-date repository of best practices for FFF/FDM 3D printer design.

Much of the written knowledge on the internet is either outdated, or locked up in videoes and chatrooms, or worse, both.

I've absorbed a lot and I hope to convey as much of what I have learned as possible.

There is a limit to the depth I will go into.
To some extent once you are armed with the knowledge from here you should be better prepared to do your own research and know what the right questions are. But if you're working on esoteric motion systems or extreme high temperatures for exotic materials, you will need to do more work on your own.

# Motion

XY Motion Systems (CoreXY vs Bedslinger vs Delta vs Cross Gantry)

[Z Motion Systems](/Motion/ZMotionSystems.md)

[Linear Guides](/Motion/LinearGuides.md)

[Stepper Motors](/Motion/StepperMotors.md)

Drive Mechanisms (belts, leadscrews, ballscrews)

# Where the Plastic Hits the Plate

Filament extrusion overview

Extruders (single, dual gear, hob size, runout etc)

Direct drive vs Bowden

Hotends (heatbreak, meltzone, structural support)

Nozzles (materials, coatings, form factor, high flow geometries)

Part cooling

Beds (surfaces and surface treatments)

# Structure

Frame design

Frame assembly (straightening)

Toolhead structure (particularly regarding balance)

Bed structure

# Software, Electronics, Power, and Sensors

MCUs

Motor Drivers

Toolhead Boards

Limit Switches

[Bed Probes](/Electronics/BedProbes.md)

Bed Heaters

Chamber Heaters

Wires

Temperature Measurement (thermistors, thermocouples, RTDs)

Input Shaping overview

Temperature Control overview

Klipper, Marlin, RRF specifics

# Printing Materials

Primary materials

Reinforcement/Fill Materials (glass, CF, metal, inhomogeneous plastic "silk")

Support materials

Filament dryers

Material switchers (MMU/AMS vs IDEX vs toolchanger)

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
