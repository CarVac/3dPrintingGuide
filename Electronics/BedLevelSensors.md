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
* Eddy current distance sensors: These are similar to inductive probes but are able to directly measure the distance instead of being digital on/off, and they work with nonferrous metals as well. These let you scan the bed level without repeatedly hopping in Z.
* Strain gage nozzle probing, whether with strain gages in the toolhead or in the bed mounts. These directly measure force between the nozzle and the bed.
* Rail-mounted toolhead nozzle probing. When the nozzle is resting on the bed, the toolhead slides on a rail and actuates a switch.

## Manual bed leveling

This is the most basic method of bed leveling.
This suffers from one primary issue: that beds are not necessarily flat and ones that are flat do not necessarily stay flat.
If your bed is not flat, you will never ever get good results except for very small portions of the bed.
The top surface must stay flat to within a small fraction of the intended layer height.

If you have a small printer (<180mm square, perhaps) with a relatively thick bed, this can work fine as distortions are kept to a minimum.
But with a larger bed you can end up with a significantly high or low center, or a saddle-shape.

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


