# Bed Level Sensors

When 3D printing, it is vitally important to accurately know where the nozzle is relative to the bed in order to control the thickness of the first layer.
If the nozzle is too high, the filament will not stick well, often causing the print to detach or for corners to warp.
If the nozzle is unexpectedly low, the filament will bulge, causing the first layer to be larger than desired and potentially catching and building up on the nozzle during travels if not using Z-hop.

There are various methods for ensuring bed leveling:

* Manual bed leveling: This relies on the bed being perfectly flat, and the user must manually tram the bed so that it is level and at the right height.
* Extending touch probes: These retract above the nozzle height for printing and extend below the nozzle for probing the bed height relative to the toolhead.
* Docking touch probes: These slot into a dock beside the bed and attach temporarily to the print head with magnets.
* Inductive probes: These detect whether ferrous metal is closer than specific distance below them, making retraction or docking unnecessary.
* Optical probes: These shine light at an angle and register a reflection when a reflective glass surface is at a specific distance.
* Eddy current distance sensors: These are similar to inductive probes but are able to directly measure the distance instead of being digital on/off, and they work with nonferrous metals as well. These can scan the bed level without repeatedly hopping in Z.
* Force sensor nozzle probing, whether with force sensors in the toolhead or in the bed mounts. These directly measure force between the nozzle and the bed.
* Rail-mounted toolhead nozzle probing. When the nozzle is resting on the bed, the toolhead slides on a rail and actuates a switch.

## Manual bed leveling

This is the most basic method of bed leveling.
This suffers from one primary issue: that beds are not necessarily flat and ones that are flat do not necessarily stay flat.
If your bed is not flat, you will never ever get good results except for very small portions of the bed.
The top surface must stay flat to within a small fraction of the intended layer height.

If you have a small printer (<180mm square, perhaps) with a relatively thick bed, this can work fine as distortions are kept to a minimum.
But with a larger bed you can end up with a significantly high or low center, or a saddle-shape.

It is possible to manually perform mesh bed level measurements to compensate for beds that aren't flat, but this is tedious and less consistent, and can't account for changes in bed shape over time.

## Extending touch probes

The best known extending touch probe is the BLTouch, but there are several clones such as the CR Touch available.

Extending touch probes enable touch probing of the bed surface without interfering with printing by having the probe extend using a solenoid.
They detect the probe contact by having a hall effect sensor measuring the magnetic field of a magnet in the deployed probe.

While they can measure the contour of a bed, they need a separate measurement to determine the relative Z position of the sensor and the nozzle, known as a Z-offset.
This must be re-measured every time the nozzle is changed, or if you swap between bed surfaces with different thicknesses.
The z-offset can also change with bed and hotend and chamber temperature too.

These are generally considered to be best used under 50 degrees C chamber temperature, as they are reportedly unreliable at higher temperatures.

To fully probe the entire bed surface, you need a bit of extra travel since the probe cannot be centered at the nozzle.

Finally, extending touch probes require an output pin on your printer motherboard.
Some may directly include a port for a BLTouch, that provides power as well as an input and output.

## Docking touch probes

These include the Klicky and Euclid probes.

Instead of having the probe always attached to the toolhead and deployed by a solenoid, these mount a pair of magnets to the toolhead to serve as attachment and electrical contacts for corresponding magnets on a dockable probe with a microswitch.

The probe itself normally sits in a slot just off the edge of the bed.
When the toolhead approaches the probe perpendicular to the slot and leaves parallel to it, will attach the probe to the toolhead and carry it away.
Approaching along the slot puts the probe back in the dock, and leaving perpendicular to it shears apart the magnets, leaving it behind.

These can operate at higher temperatures than extending touch probes, and don't require separate power or deployment pins.

However, they also need the toolhead to be able to have travel extend off the bed in order to reach the dock, have the same thermal expansion issues, and need Z-offset calibration.

## Inductive probes

These are often unbranded but one particular model is the SuperPINDA.

Inductive probes are binary sensors that detect whether ferrous metal is within a certain distance of the end of the sensor.
They do not require contact with the bed, so they do not need to extend or retract or dock.

However, they only work with ferrous metal under them, typically a spring steel plate coated in PEI.
The PEI steel plate limitation is usually not something to worry about, but it can cause crashes if the plate is removed and Z is homed.

These can sometimes be highly sensitive to temperature.
Some have internal temperature sensors for compensation in software.
Others are internally compensated, like the Prusa SuperPINDA.

As for all these auxiliary sensors, inductive probes need Z-offset calibration, and you need a little extra travel to cover the entire bed.

## Optical probes

Optical probes detect bed proximity by bouncing light off the bed surface.
They require a polished glass surface to function.

As glass beds are not too commonly used these days, so too are optical probes seldom seen.

The Positron printer makes use of one, however, since its upside down printing is made visible with a completely transparent glass bed.

Optical probes need Z-offset calibration, they need a little extra travel to cover the whole bed, and thermal expansion effects them just like everything.

## Eddy current distance sensors

The original eddy current distance sensor is the Beacon, with alternatives such as the Cartographer and the BTT Eddy.

Eddy current distance sensors are somewhat similar to inductive probes, but they can actually measure analog distance from the bed.
This lets them rapidly scan the bed without stopping and moving up and down in Z, merely zigzagging back and forth across the bed.
You can get many more samples much more quickly than any other bed leveling method.

This distance detection gives some of them another trick: nozzle probing.
When driving the nozzle into the bed, the distance closes continuously until the nozzle makes contact, and the resulting deflection of the bed and or toolhead abruptly changes the rate of change of distance.
This can eliminate the need for Z-offset calibration, and it lets them probe beds that don't have a uniform steel surface, as long as metal is close under the surface (such as an aluminum bed structure under a glass bed surface).

However, nozzle probing is vulnerable to solidified plastic that oozed out of the nozzle.

They need a little extra travel to cover the whole bed, but with contact probing simply having the steel bed plate extending past the edge of the physical bed can let you probe the entire bed.

They need thermal compensation due to hotend expansion, but with non-PEI steel plates, nozzle probing can be performed at full printing temperature.
Additionally, not all models are fully thermally compensated for non-contact scanning.
Beacon in particular is rated up to 115 degrees C.

## Force sensor nozzle probing

Becoming common in commercial printers, it is available for DIY printers from Precision Piezo and recently from E3D as PZ Probe.

These are piezoelectric sensors placed under the bed or above the hotend, to measure the force between the bed and nozzle.

The signal to noise ratio is stronger from bed probing but for printers with bed that move in Z, the inertia of the bed can cause false triggers while Z is accelerating.

This eliminates z-offset calibration, but like all nozzle probing it is vulnerable to solidified nozzle ooze.

## Rail mount toolhead nozzle probing

Commonly known as TAP for Voron printers, this mounts the entire toolhead on a very short Z-oriented linear rail.

When the nozzle contacts the bed, the whole toolhead mass rests on the bed and the carriage slides until a switch is actuated.

This has the disadvantage of decreasing motion system rigidity and applying much greater forces on the nozzle tip and bed, increasing the chance of damage.

# Recommendations

For room temperature printers that will be printing with a limited range of nozzle temperatures, a BLTouch is generally okay on a budget.

At higher temperatures, a dockable probe is an economical option.

If you care about speed of bed mesh measurement, an eddy current sensor is incredibly capable.
Beacon is the gold standard, good to high temperatures, but it's fairly expensive.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
