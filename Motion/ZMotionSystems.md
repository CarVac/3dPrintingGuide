# Z Motion Systems

The key third dimension of a 3D printer, the Z axis of motion must be controlled with immense precision and stability, with much less emphasis on speed.

Consistency of Z motion is of utmost importance to getting clean layer stacking and consistent part strength.
Thinner layers than expected will cause the extrusions to bulge out and potentially stick up and snag the nozzle while printing.
Meanwhile, thicker than expected layers will reduce layer adhesion and thus part strength.

This will cover both drive mechanisms and various arrangements of those drive mechanisms.

# Drive Mechanisms

There are three main drive systems used for Z, leadscrews, belts, and ballscrews, each with their own advantages and disadvantages.

Additionally, there are various ways to adjust the gear ratio for more precision, or to prevent or reduce backdriving.

Generally, you want the drive mechanism to have your standard layer height (often 0.2mm) be an exact multiple number of whole steps of your Z stepper motors. This ensures that any microstepping angular error, which typically repeats with every whole step, is the same for every layer.

## Leadscrews

Leadscrews are by far the most common method to convert a stepper motor's rotary motion to linear Z motion.

Leadscrews are convenient because they are difficult to backdrive. When the printer is off, the weight of the bed will be unable to spin the motors and cause it to fall.

Typically, you will find an 8m diameter Acme threaded rod with 2mm teeth but either 2 or 4 thread starts leading to either 4 or 8mm of linear motion per revolution of the leadscrew.

Acme threads are trapezoidal, which offer lower friction compared to triangular threadforms while being easier to cut than square threads.

Fewer starts gives more motion precision, but this limits the speed of Z motion, which can potentially take a while..
If a leadscrew spins too fast, "centrifugal force" will cause unsupported lengths to bend and whip around wildly, potentially causing permanent damage.

Leadscrews that aren't perfectly straight can cause artifacts, known as Z-banding, if the forces they apply to the nut deflect the carriage they are driving in the X/Y direction.
This can be mitigated with an Oldham coupler at the expense of some backlash, a WobbleX which can correct for more axes of nut wobble motion with less backlash, or by using a separate carriage from the bed carriage to interface with the leadscrew.

## Belted Z

The next most common Z drive mechanism is using timing belts, similar to XY motion.

Belts offer immunity from Z wobble, but at the expense of additional complexity.

Because of the precision and torque requirements of Z, this most often involves reduction gearing.

Reduction can be implemented via intermeediate closed loop belts with pulleys, or with planetary gearboxes attached directly to the motors.

CoreXZ will be described in detail later, but it implements Z motion using belts and motors shared with the X axis, and simply makes do without gear reduction at all.

Especially if there is no gear reduction, but even if there is, the z axis can fall under gravity.
Some printers use counterweights, retracting keychain holders, or leaf springs to support the weight of the bed or gantry and prevent it from creeping downward.

## Ballscrew Z

Ballscrews are fancy leadscrews, but they're different enough in practice because they are far more precise, lower-friction, and commonly larger diameter.

The larger diameter and greater precision makes them generally no problem for Z banding, and the larger diameter increases the speed at which you can spin them before they go unstable and wobble.

They operate by having recirculating balls rolling in the nut instead of having sliding interfaces between the threads and the nut.

The downside is that these are much more expensive than either normal leadscrews or belts.

# Z Motion Arrangements

## Bedslingers

Bedslingers move the bed in the Y axis, and the toolhead in X and Z.
The X gantry moves up and down, and the toolhead moves along the gantry.

This reduces the amount of structure needed to build a printer, and simplifies Z.

### Single Z

On cantilevered bedslingers where there is only one vertical column, a single Z motion system is the only choice for controlling the height of the X gantry.
This requires a lot of bending stiffness for the mount of the X gantry onto the Z axis for consistent vibration-free motion.

Single Z also comes up occasionally on very low budget two-column bedslingers such as the original Ender 3, still relying on the X gantry mount's in-plane bending stiffness to ensure that the X axis remains level.
With soft v-wheels like the stock Ender 3, this is a recipe for high wear and low resistance to damage such as wheel flatspotting.

### Single dependent Z, dual drive

On two-column bedslingers, each side of the X gantry can be driven by one motor, with a linkage connecting two drive mechanisms.

When leadscrews are used as drive mechanisms, they can simply have pulleys attached at the top, with a belt running between them to synchronize their motion.

When belted Z is used, a shaft can run across the top of the machine to synchronize the belts.

This isn't so easily adjustable but it doesn't often need adjustment, mostly relying on manual bed adjustment for tramming.

### Dual Z

If the joints between the X axis gantry and Z axis columns are allowed to be a little flexible, then two independent actuators can each drive one side of the X gantry.

This allows for automatic tramming of the X axis, whether by using two limit switches at the top of the travel, or by using a bed probe to compare height of the toolhead over the bed at different X positions.

However, this requires an extra motor and stepper driver.

### CoreXZ

One unique way to control the Z axis of a bedslinger is by sharing two stationary motors with the X axis, and using CoreXY-style belt routing to move the toolhead in a vertical plane.

This has several advantages:

* The X axis motor is relocated to the bottom of the machine, simplifying wiring
* Z motion can be extremely rapid, since it shares the motion system with X which is necessarily fast
* X motions are driven by two motors together, giving slightly increased torque

It also has several disadvantages:

* The gantry does require high in-plane bending stiffness to prevent racking (axis skew) in the case of uneven belt tensions
* Long belt paths can reduce motion system stiffness, resulting in more corner rounding from input shaping at any given acceleration
* The Z resolution is comparatively poor
* The gantry *will* fall when the stepper drivers are disabled, so this requires countermeasures to stop the nozzle from smacking into the bed.

## Non-Bedslingers

### Single Z Cantilevered

### Dependent Double Z

### Dependent Triple Z

### Independent Double Z

### Independent Triple Z

### Flying Gantry

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
