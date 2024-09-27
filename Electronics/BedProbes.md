# Bed Probes

Bed probes, also known as Z probes, or less precisely as bed level sensors, are used to measure the height of the toolhead above the bed.

When 3D printing, it is vitally important to accurately know where the nozzle is relative to the bed in order to control the thickness of the first layer.
If the nozzle is too high, the filament will not stick well, often causing the print to detach or for corners to warp.
If the nozzle is unexpectedly low, the filament will bulge, causing the first layer to be larger than desired and potentially catching and building up on the nozzle during travels if not using Z-hop.

To correct for these errors, there are several steps that must be performed in order.

1. Bed tramming: physically adjusting the bed to be as level as possible
2. Mesh compensation: measuring a grid of points across the bed and correcting for measured height variations caused by bed curvature or motion system alignment or sagging.
3. Z offset adjustment: correcting for the difference in height between the probe's trigger point and the nozzle

# Bed Tramming

Bed tramming can be done manually, on machines without the ability to control the bed tilt, or automatically, when the machine can tilt the bed or gantry.

## Manual Tramming

On many machines, this is done by having the printer place the nozzle at each height-control screw and either visually or using feeler gages under the nozzle to check for equal nozzle height, adjusting the screws as needed.

On smaller bedslingers, this often involves 3 or 4 adjustment screws on the bed carriage.

Some commercial machines have triple Z leadscrews but no ability to automatically adjust them independently, requiring manual tramming again with three or four adjustment screws. Machines like this include Bambu Labs X1C.

Some machines have single-axis automatic tramming, such as bedslingers with two independent Z motors. These would still need tramming for the other direction.

Some commercially-made printers do not provide for any tramming at all, relying on the machine being assembled properly at the factory.

## Automatic Tramming

When the machine can adjust the relative orientation of the gantry and the bed in two axes, a bed probe can allow automatic tramming at the beginning of every print.

### Triple Z Bed Leveling

Machines with three independent Z motors can control the bed tilt in both axes.
There are many machines like this, because it is more or less optimal in most circumstances.

Bed leveling can be accomplished by probing the bed near the actuators and adjusting until they all have the same relative probed height.
It may take a few iterations for the measurements to converge.

### Quad Gantry Leveling

On CoreXY machines where the gantry is moved up and down and the bed is fixed, like the Voron 2.4 and derivatives, the gantry itself must be leveled relative to the bed as well as de-skewed.

These machines use four independent Z motors, one on each corner, and have slightly flexible gantry attachments.

Similar to triple Z bed leveling, quad gantry leveling involves probing the bed height with the nozzle near the corners of the bed and adjusting the Z motors relative to each other until the measurements are all equal.

# Mesh Leveling

Once the bed is level, any error in flatness can only be compensated by making a grid of measurements across the bed and using these to adjust Z based on the X and Y coordinates.

Mesh compensation can be done manually, but usually a bed probe is used to perform the measurements more quickly and consistently.

There are various sensors for producing bed meshes.

## Manual bed measurement

This involves tweaking Z up or down using the printer's interface until the Z height is a fixed distance above the bed, often judged by feeling friction when sliding a shim between the bed and the nozzle.

This is not a very effective way to ensure consistency, because of the subjective nature of the measurement.

Additionally, it is time-consuming, annoying, and potentially painful if doing it on a hot bed.

But it's by far the cheapest option and can work with any machine.

## Extending touch probes

In order to probe the bed without getting in the way of a print, an extending touch probe will use a solenoid or servo to extend its tip past the nozzle while probing the bed, and retract to be shorter than the nozzle while printing.

The best known extending touch probe is the BLTouch, but there are several clones such as the CR Touch.

These are cheap, easy to fit onto a toolhead, well-supported by firmware, and there are printer motherboards with a dedicated port available for them.
But if your motherboard doesn't have a dedicated port, these probes require an extra output pin as well as an input pin.

To fully probe the entire bed surface, you need a bit of extra travel beyond the printable area in one axis since the probe must have an X/Y offset.
Or you can make do not probing the whole bed.

Generally, BLTouch and similar probes should not be used over 50 degrees C chamber temperature, as they are reportedly unreliable in hotter conditions.

In the past, there were DIY extending probes using microswitches mounted on arms attached to servos, but this method has been generally been superseded.

## Docking touch probes

These are known by various names such as Quickdraw, Euclid, and Klicky.

Docking touch probes reach below the toolhead by having the probe only temporarily attach via magnets while measuring the bed.
When printing, they are held out of the printing area in a dock.

The probe itself sits in a slot just off the edge of the bed.
When the toolhead approaches the dock perpendicular to the slot and leaves parallel to the slot, it will pick up and carry away the probe using the magnets, which conveniently also act as electrical contacts.
To deposit the probe back in the dock, approach along the slot and leave perpendicular to the slot, shearing apart the magnetic connection.

These can operate at higher temperatures than extending touch probes, and don't require separate power or deployment pins.

However, since the dock must be located off the bed, dockable probes require extra travel beyond the printable area in order to function.

## Inductive probes

Inductive probes are on/off sensors that detect whether ferrous metal (in the case of printers, steel build plates) and only ferrous metal is within a certain distance of the end of the sensor.
Because they do not require contact with the bed, they do not need to extend/retract or dock.

However, because they only work with ferrous metal and only over a very short distance, this makes them incompatible with glass, garolite, and carbon fiber print surfaces.
Additionally, if the spring steel build plate is removed, accidentally triggering z homing can cause a crash.

Some of these are temperature sensitive, others are provisioned with thermistors for external compensation, and others are internally compensated.

These probes are quite compact and can be placed close to the hotend, but you still need a little extra travel if you want to be able to probe the whole bed.

## Optical probes

Optical probes, also known as differential IR height sensors, detect bed proximity by bouncing light off the bed surface.
They require a polished glass surface to function.

These are fairly uncommon because polished glass surfaces are not often used.
Some variants of the Positron do use it.

These require a little extra travel to cover the entire bed, and they may fail from adding bed adhesion agents.

## Eddy current distance sensors

The original eddy current distance sensor is the Beacon, with alternatives such as the Cartographer and the BTT Eddy.

Eddy current distance sensors are somewhat similar to inductive probes, but they can actually measure analog distance from the bed.
This lets them rapidly scan the bed without stopping and moving up and down in Z, merely zigzagging back and forth across the bed.
You can get many more samples much more quickly than any other bed leveling method.

For rapid scanning, they work with a uniform steel surface over a magnetic sticker.
They have artifacts from probing over discrete magnets embedded in the bed plate.

They require a decent amount of extra travel to cover the entire bed, because the sensing coil is relatively large and can't be too close to the nozzle.

Additionally, the models currently on the market only work with Klipper firmware, and they have significant metal keepout zones above the coil to ensure consistent results, making it slightly harder to integrate this into printers.

Some of these are capable of nozzle probing, which can function with any bed material as long as there is metal (ferrous or not) under the sensing coil.
With nozzle probing, you don't need any extra travel to cover the whole bed since you can just get a slightly larger spring steel sheet to extend under the coil.

Nozzle probing is vulnerable to solidified nozzle ooze if not probing at printing temperature.

The Beacon in particular is rated for high chamber temperatures up to 115 degrees C.

## Force sensor nozzle probing

Becoming common in commercial printers, it is available for DIY printers from Precision Piezo and recently from E3D as PZ Probe.

These consist of piezoelectric sensors placed under the bed or above the hotend, to measure the force between the bed and nozzle.

The signal to noise ratio is stronger from bed probing but a printer with a bed that moves in Z, the inertia of the bed can cause false triggers while Z is accelerating.

Force sensor probing doesn't need any extra travel to cover the entire bed.

But like all nozzle probing, it is vulnerable to solidified nozzle ooze.

They may have limited chamber temperature compatibility, though PZ Probe goes to 75C which is solid.

## Rail mount toolhead nozzle probing

Commonly known as TAP for Voron printers, this mounts the entire toolhead on a very short Z-oriented linear rail.

When the nozzle contacts the bed, the whole toolhead mass rests on the bed and the carriage slides until a switch is actuated.

This doesn't require extra travel to cover the entire bed.

However, it has the severe disadvantage of decreasing motion system rigidity and applying much greater forces on the nozzle tip and bed, increasing the chance of damage.
With insufficiently secured beds, this can tip the bed over.

Do not use this if one of the other nozzle probe options is available to you.

# Z Offset Calibration

Once the bed mesh has been measured, the Z-offset, the actual zero point where the nozzle touches the bed, must be determined.

This usually stays the same as long as the nozzle and bed surface are unchanged, but it also changes depending on operating temperature of the hotend, bed, and chamber.

Note that there is no one true best zero point, so even in ideal situations with automatic Z-offset setting, there may need to be an additional manual offset applied depending on the needs of the filament and bed surface.
For example, powder-coated PEI surfaces need slightly lower offsets than smooth surfaces, and different filaments might need more or less squish to achieve the desired amount of adhesion.

There are several ways that Z offset can be set.

## Manual Z offset

The old-fashioned way, you use a shim or observe with your own eyes to tweak Z until it's the right height.

This requires practice and experience, and even then it can be somewhat inconsistent. But if you don't change your bed material or nozzle often, this can be just fine for daily use, and because it's only done manually you don't have to worry about keeping the nozzle as clean.

This doesn't compensate for temperature.

## Separate strain gage nozzle probe

Some printers use an external Z-offset sensor that the nozzle is moved over to check nozzle length.

This can handle nozzle changes but any bed surface changes must be adjusted manually, and it doesn't account for changes in bed temperature.

And like all nozzle probing, this is vulnerable to solidified nozzle ooze so that must be cleaned off either manually or automatically if not probing at printing temperature.

## Bed leveling sensor nozzle probe

Whether done by eddy current sensor, in-bed force sensors, in-hotend force sensors, or rail mount toolhead, nozzle probing can eliminate the need for tweaking Z offset when changing bed material or nozzles.

If not probing at the printing nozzle temperature, Z offset will need to be tweaked depending on the hotend temperature.

These are vulnerable to hardened nozzle ooze, but with certain bed materials (particularly plain spring steel with adhesives) you can safely nozzle probe at full printing temperature and then you will always get a perfect Z offset.

# Recommendations

For room temperature printers that will be printing with a limited range of nozzle temperatures, a BLTouch or similar is generally good on a budget and easy to integrate.

For higher temperature use, a dockable probe is an economical option.

If you care about speed of bed mesh measurement, an eddy current sensor is incredibly capable.
If you have a large bed, meshing on a normal sensor can take quite a long time so this can be very desirable.
Beacon is the gold standard, good to high temperatures, but it's fairly expensive.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
