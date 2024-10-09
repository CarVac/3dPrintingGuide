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

Leadscrews that aren't perfect can cause artifacts, known as Z-banding, if the nut is rigidly mounted.
When the leadscrew axis tilts relative to the nut, it binds, affecting the layer uniformity.
This can be mitigated with an Oldham coupler at the expense of some backlash, or a WobbleX which can correct for more axes of nut wobble motion with less backlash.
It also be good to use a separate motion carriage from the bed carriage to decouple any forces.

## Belted Z

The next most common Z drive mechanism is using timing belts, similar to XY motion.

Belts offer immunity from Z wobble, but at the expense of additional complexity.

Because of the precision and torque requirements of Z, this most often involves reduction gearing.

Reduction can be implemented via intermeediate closed loop belts with pulleys, or with planetary gearboxes attached directly to the motors.

CoreXZ will be described in detail later, but it implements Z motion using belts and motors shared with the X axis, and simply makes do without gear reduction at all.

Especially if there is no gear reduction, but even if there is, the z axis can fall under gravity.
Some printers use counterweights, retracting keychain holders, or constant-force springs to support the weight of the bed or gantry and prevent it from creeping downward.

## Ballscrew Z

Ballscrews are fancy leadscrews, but they're different enough in practice because they are far more precise, lower-friction, and commonly larger diameter.

The larger diameter and greater precision makes them generally no problem for Z banding, and the larger diameter increases the speed at which you can spin them before they go unstable and wobble.

They operate by having recirculating balls rolling in the nut instead of having sliding interfaces between the threads and the nut.

The downside is that these are much more expensive than either normal leadscrews or belts.

If you cheap out on ballscrews, though, they can be no better than ordinary leadscrews.

# Z Motion Arrangements

## Bedslingers

Bedslingers move the bed in the Y axis, and the toolhead in X and Z.
The X gantry moves up and down, and the toolhead moves along the gantry.

This reduces the amount of structure needed to build a printer, and simplifies Z.

Kinematically, belt printers are bedslingers, and so this section applies to them as well.

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

Printers that are not bedslingers either move their beds purely vertically, or move ther x/y motion systems vertically.
This leads to an entirely different set of Z motion systems.

### Single Z Cantilevered

The simplest way to drive a bed purely vertically is to support it from a drive system on only one side of the bed.

This works very well for small beds but larger ones will shake up and down as the printer toolhead vibrates the machine, unless the cantilever and the linear guides it is built on are extremely rigid.

Tramming (alignment to the x/y motion system) must be done manually.

### Dependent Double Z

To reduce cantilever issues, some printers straddle the bed with a pair of Z drives linked together, usually a pair of leadscrews belted together.

This is okay, but it also relies on the rigidity of the linear motion guides to prevent rocking in some circumstances.

Bed tramming must be done manually.

### Dependent Triple Z

Triple Z drives that are controlled as one are completely immune to bed tilting.
These are often implemented with one motor driving three leadscrews through a belt.

This provides excellent Z motion rigidity while keeping costs relatively low, but it still requires manual tramming.

### Independent Double Z

Some printers use two Z leadscrews but drive them with two indepedendent motors to automatically tram in one axis.

You still need linear motion rigidity in one direction to prevent rocking, but you need compliance in the other direction to prevent jamming.
On top of that, you still need manual tramming in one axis, and it needs an additional motor and stepper driver.

Why would you do this?
Why wouldn't you just use dependent or independent triple Z?

There are some questions we may never know the answers to.

### Independent Triple Z

With three independent Z drives, bed tilt can be fully computer-controlled, eliminating the need for manual tramming with an appropriate bed probe.

This specifically requires a compliant bed support mechanism, ideally a kinematic mount for the bed or a bedframe, but this comes with the risk of dropping the bed if the drives go significantly out of sync.

If you do have a kinematic coupling (perfect constraints, fully flexible) between motion system and bed mount, make sure that the supports are not cantilevered too far out from the linear motion guides, to improve the rigidity of the system.
Additionally, preload on kinematic mounts is important if you intend to have fast Z acceleration.

If the bed to linear guide connection is not a kinematic coupling, then it must be made compliant enough to overload the linear motion guides.

Independent triple Z does need three separate Z motors and drivers, which adds to costs.

### Flying Gantry

By fixing the bed to the bottom of the print chamber and moving the entire x/y gantry up and down, you can reduce the mass of the Z system.
The gantry in other sorts of printers would ordinarily require mechanical adjustment to ensure flatness, but with flying gantry, *Quad Gantry Leveling* can be employed to automatically ensure that the X/Y system is free of twist and is parallel to the bed.

Compared to independent triple Z, this requires an additional motor and stepper driver, and resonances can change dramatically as the toolhead moves up and down in Z.
Additionally, you really need to have a semi-compliant gantry structure, which sacrifices stiffness.
Finally, you have to make your X/Y wiring is carefully routed to account for motion.

These compromises are something worthwhile with large format (>500 mm on a side) printers, where bed plate weight can be immense and it is far easier to move the gantry.

However, it also sees some use with smaller printers such as the Voron 2.4 and derivatives.

Why?
Maybe they just think the design is neat.

It is neat, I guess.

### Delta

Delta kinematics are unique because with they are parallel manipulators, allowing both the bed and all of the motors to remain stationary, yet only requiring three motors for all of X, Y, and Z.

This is potentially ideal for simple construction and fast printing.

However, they have complex nonlinear interactions between each actuator's position and the toolhead position that must be calibrated, ideally with nozzle bed probing.
This nonlinearity also results in non-uniform precision and motion capabilities across the build volume, which itself is not necessarily conveniently shaped.
The Z axis shares its drive mechanisms with X and Y, so like CoreXZ you usually cannot fit multiple full steps per layer height, reducing Z precision.
Additionally, if a stepper motor loses steps and moves afterwards, this can potentially cause damage to the mechanism by driving it into an improper configuration.

# Recommendations

For actuators, leadscrews are fine, but you need to be careful to decouple them properly to avoid banding issues.

Belted Z is good, but you have to either balance the forces with a spring or gear them down strongly to avoid creeping when power is removed.

Ballscrews can be great, but ones that are actually good are really expensive.
Use these if you must have the best.

On a bedslinger, use dual Z actuators, whether linked or independent.

On non-bedslingers, if your printer is small (say, 150mm bed or smaller), you can use a cantilevered bed with single Z, as long as you build it robustly.
For midsized printers, just use triple Z, whether linked or independent.
For large printers, you should consider flying gantry.

Most things should use triple Z with a moving bed.

If you're making a delta printer, you're making a delta printer.
There's no other Z motion to worry about.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
