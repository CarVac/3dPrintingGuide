# Stepper Motors

99% of 3D printers use open-loop stepper motors to drive all motion, because they are economical, fast, and precise.

Here's what I think is important to keep in mind when selecting them and designing things around them.

## Overview

There are many types of stepper motors, but those used in 3D printing are almost all of one type: 2-phase bipolar hybrid.

## Construction

Hybrid steppers are made of a stator housing surrounding a rotor.

The rotor hase banks of toothed wheels around an axially-oriented permanent magnet, with each pole's wheel angularly offset by half a tooth pitch.

They are surrounded by toothed rotors with a slight tooth count mismatch such that when a stator phase's north pole's teeth are aligned with the rotor's south pole teeth and misaligned with the rotor's north pole teeth, while the stator phase's south pole is perfectly misaligned with the south pole rotor teeth and aligned with the rotor's north pole teeth.
When one phase is aligned, the other is half-aligned in opposite directions on each side, allowing that to produce torque.

The ends of the stator are attached to endcaps that house bearings that support the rotor.

# Specifications

There are several specifications you need to consider when choosing a motor or designing for an existing motor

## Size and Weight

Motors come in various sizes.
In 3D printers you'll see NEMA 14 motors, NEMA 17 motors, and NEMA 23 motors.

Larger motors generally have more torque, but have more resistance and inductance thus reducing their high speed performance, and more rotational inertia.

Longer motors generally have more torque too, as well as more inertia.

Motor inertia counts towards moving mass when you compute the amount of torque required to drive your gantry, which is bad.

Additionally, if you have your motors mounted on moving parts of your gantry, then they straight up add mass there as well.

## Shaft Size

Many Nema 17 stepper motors use 5mm shafts with a flat cut in one side.

When you just slap a timing belt pulley on them and tension it as a cantilever, that produces heavy bending stress in the shaft that can cause it to fatigue and snap off as the motor rotates.

It's a bad idea to use more than 6mm wide GT2 belts in "single shear" cantilevered configuration.

Lately (mid-late 2024), there have been more printers designed for motors with wider 8mm shafts without the flat for better strength, while also making the shafts longer so that the far side can be supported by a bearing ("double shear" configuration).

This opens up the use of wider 9mm and 12mm belts, as well as GT3 belts that are stiffer but require very high tensions.

## Torque

The very reason motors exist is to produce torque to move things around, so torque is important.
But datasheets have several kinds of torque that you need to understand.

### Detent Torque

Detent torque is how much torque it takes to spin the motor with all phases disconnected.
This is often unimportant but occasionaly can be if you have a belt-driven Z axis.
When the steppers are unpowered, the detent torque is the only thing stopping the Z axis from falling.

### Holding Torque

Holding torque is the torque required to cause the motor to skip a step when holding at a full stepping position at nominal drive current.
This correlates pretty well with low speed torque, at least up until the speed where the motor's back EMF is high enough in comparison to the drive voltage to reduce the flow of drive current.

### Pull-In and Pull-Out Torque 

Pull-Out Torque is the torque required to cause a motor to skip a step when rotating at any given speed.
This is usually shown in the form of a graph.

This is the closest information to what you want to know when speccing out motors for a printer and calculating how much acceleration you can expect from it, but you have to realize that the test conditions (particularly the motor driver) are not going to be the same.

## Precision and Accuracy

### Step size

In NEMA 17 sizes, motors have two common full step angles available: 1.8 degrees (200 steps per revolution) and 0.9 degrees (400 steps per revolution).

### Step Accuracy

There are several limits to accuracy.

Motors have a step size error in their specifications.
For most hobby printers, this is +/- 5%.
Higher end motors may be 3% or even better, but those are rarely used.

What is this from?
This is somewhat conjecture, but it's likely mainly due to imperfections in the anti-alignment of the north and south rotor teeth, which would cause errors that sinusoidally repeat every 4 whole steps.
The next source might be imperfections in the stamped teeth themselves of the rotor and stator, and those errors will be random but repeating every full revolution.
Beyond that it's probably down to bearing inaccuracy which is probably not integer-multiple periodic with rotation, though it can be repeatable.

## Inertia

Larger and torquier motors tend to have higher rotor inertia.
When you gear down a motor or when the mass of the object being moved is small, the inertia of the motor can be the main resistance to acceleration.

Lower inertia is basically always better, all else equal.
Just be aware that not all else will be equal.

## Current Rating

Stepper motors come with a rated current.
Because the current flowing into motors varies sinusoidally as the motor rotates around, this can be given in two ways: RMS or peak current.

The RMS value will be lower, while the peak current value is 1.414 (the square root of 2) times the RMS value.

Make sure not to use too high of a current by mixing up RMS and peak current in your printer configuration, or your motor can overheat and melt the insulation inside the coils.

If you want to run the motor in a higher temperature environment, you may need to derate the current to reduce temperature rise.
This will reduce the amount of torque available.
Likewise, you may want to derate your motors if they are mounted to non-temperature-resistant plastic motor mounts.

Conversely, it's not necessarily a good idea to over-current your motors even if you have a lot of cooling available.
There can be magnetic saturation inside the rotor and stator materials, limiting any additional torque you may get.

## Resistance

Phase resistance is a specification that affects chopper configuration.
Consult your stepper driver documentation to tune the driver parameters based on your motor specs.

Resistance is also somewhat related to current rating: lower resistance motors can have more current flowing at the same amount of heat output.
But this doesn't really matter to you, the end user.

## Inductance

Phase inductance is a measure of how resistant the coils are to changing current.
It's also related to how much back EMF the motor produces at any given rotation speed.

Lower inductance of the phases means that you can go faster before the back EMF overwhelms the drive voltage and reduces current flow.

So lower inductance motors are generally good if top speed is important.

However, if inductance gets *too* low (less than 1 millihenry) then it makes chopper configuration extremely troublesome, particularly at high drive voltages.

## Insulation Rating

Make sure that the insulation on the motor is rated for voltages well above what you will be applying.

# Other Design Considerations

## Stiffness

As you deflect a stepper from its current equilibrium position, the reaction torque gradually rises in roughly a sinusoid until you reach the holding torque.

The higher the holding torque, the greater this stiffness is.
Additionally, the more steps a stepper has, the stiffer it gets for a given holding torque, although finer steps usually result in lower holding torques.

Greater motor step stiffness results in better positioning accuracy, because the motion system will be held closer to the desired position given a specific friction force.

## Resonances

Some motors make lots of audible noise, and some motors are prone to making vibrations in the motion system that become visible in the print as "VFA".

I don't know what actually goes into mitigating noise and vibrations in the motors themselves, so suffice it to say: ask people about the motors you are planning on buying and get ones with a track record for being good.

Or go out on a limb and try various ones yourself.

Note that different printers behave differently with different motors.
This depends on the belt lengths and belt stiffnesses.

## Heat Resistance and Dissipation

Stepper motors generate heat while operating.
Most of the heat is caused by current flowing through the coils, with a power equal to the resistance times the square of the RMS current.
Some of the heat is generated in the steel of the rotors and stators due to hysteresis as the magnetic fields change rapidly.

If the heat builds up too much without proper dissipation, the main issue is that the coils can heat up to above the temperature of their insulation, causing the potential for short-circuits.
Additional points of failure include the grease in the bearings, or the connection to the outside whether that be a JST connector or PVC-insulated wires.
Higher-temperature-rated steppers often use PTFE-insulated wire that resists somewhat higher temperatures before softening.

The heat in the coils has a hard time making it out of the stepper.
First, the coil must conduct heat through the plastic winding guides to the stators.
Then the stators, which are made of stacks of magnetic steel that isn't very thermally conductive, must transfer the heat to the outside.
Some attempt to cool motors by attaching heatsinks to the ends, but that is even more poorly connected to the stack of laminated steel.

How hot do things actually get?
Without heatsinking, LDO 2504s at 2.5 amps hit coil temperatures of more than 120 C over ambient. (source: deadlock)
Most of the temperature drop came from the poor convection, as the sides of the stepper were about 90 C over ambient.

So the best way to cool steppers without modification of the housing is to draw heat away from the sides of the laminations.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
