# Linear Guides

3D printers are instruments of precision motion, so they rely on linear guides to serve as a reference for their motions.

If a printer's linear guides are not accurately guiding motion, then anything it prints cannot be accurate.

There are several aspects to this:

* Rotational stiffness of the carriage in each axis relative to the guide
* Bending stiffness of the guide in each axis
* Straightness of the guide
* Friction
* Resistance to wear and/or damage

Additionally, other aspects of performance to consider include temperature resistance, maintainability, and mass of components.

## Rotational Stiffness

If the carriage is moved by the linear guide perpendicular to the guide's travel, such as in the case of the Y direction in CoreXY, or for both X and Y for cross gantry, if the center of mass of the load is not aligned with the linear guide, that will apply a rotational moment (torque) on the bearing carriage.

Even if the carriage is not moved by the linear guide, such as with bedslingers, Z axes, and pure X motion on CoreXY, there can still be a moment applied if the center of mass does not align with the drive mechanism (belts or leadscrews).

It's ideal to balance toolheads and rails such that these center-of-mass misalignments are as small as possible, but they often cannot be eliminated entirely (such as for the cross guides on cross gantry).

For this, you want high stiffness.

## Bending Stiffness of the Guide

If you are moving the linear guide itself, then the guide (and/or what it attaches to) also must be rigid enough to avoid deflecting enough to affect print quality.

If it is too flexible, that can cause ringing due to low resonant frequencies (must be compensated for with strong input shaping) and overall lag behind the intended position while accelerating hard.

## Straightness of the Guide

There are two aspects to this: straightness of the guide itself and smoothness of the carriage rolling on the guide.

Any deviation here can have strong impacts on print accuracy.

## Friction

For any motion in the direction of the guide's travel, the guide will resist that motion due to friction.
It's up to the motion system's rigidity to force it to move as close as possible to the desired position.

Often higher rigidity motion systems (e.g. high preload rails) have more friction, and they must be matched with more rigid motion systems (wider, high-tension belts) to prevent issues.

If the friction is too high compared to the motion system stiffness, the motion will exhibit hysteresis, where the toolhead error will vary depending on the direction of approach.

On 3D prints, asymmetric friction often results in oval holes.
Nobody likes oval holes.

Additionally, infill may not reach perimeters, and any direction reversals for perimeters will have noticeable positional offsets.

## Resistance to Wear/Damage

No matter how good a linear guide is in the other aspects, if it wears quickly and loses the above properties, then it will require frequent maintenance.

This is undesirable.

# Types of Linear Guides

## V-Wheels

On many cheaper, older 3D printers, linear motion is guided by plastic wheels running in slots on aluminum extrusion.

Three V-wheels, two on one side and one on the other side of a rail, can be used to constrain linear motion, but for heavier loads 4 has more load capacity due to equal tension on each side's wheels..

V-wheels must be tensioned upon installation in order to achieve any sort of stiffness, but there's a tradeoff between the preload and longevity.
Tightly pretensioning v-wheels can cause flatspots when left unused for a while, and even when used regularly they will wear out.

As for their positional accuracy:

* V-wheels are not stiff in torsion, even when pretensioned. If you want to use high accelerations, everything must be precisely balanced to prevent the nozle deflecting.
* Bending stiffness depends on the extrusion size they are mounted to. This can actually work out fairly favorably for large gantries if you use a large rail sectio
* The extrusions are generally inherently straight, but damage to the wheels can result in uneven motion.
* Friction is actually extremely low with plastic v-wheels.
* V-Wheels are very susceptible to wear and damage. Replace frequently to ensure consistent, accurate movement.

Standard v-wheels are made of POM, but higher quality v-wheels exist (polycarbonate, or Kevlar-filled plastic, or even PEEK), but they are more expensive.

They don't resist high temperatures.

Depending on the printer design, they can be very easy to replace, but at the same time they require error-prone manual tensioning.

If you care about longevity, definitely use something else.
But on low acceleration printers, if you are okay with replacing them often, there isn't any quality to be gained by switching.

## Linear bearings on rods

A common type of linear guide for 3D printers is linear bearings, whether plain bushings or recirculating ball bearings, on cylindrical rods or tubes made of steel or carbon fiber.

Rods have one less axis of constraint than most linear guides, since the bearing is allowed to rotate around them.
For some applications this is technically undesirable, since you then need two rods and two bearings in order to fully constrain motion.
However, in other circumstances such as Y guides in CoreXY that don't need the extra axis of control, this can help avoid overconstraint in the motion system.

There are two common types of bearings, plain and recirculating ball.

Plain bearings are just a block of low-friction material, whether plastic as in Igus Drylins, or oil-impregnated sintered metal.
They produce a lot of friction when a moment is applied to them, but if your design can avoid that then they can run smoothly.
Plastic ones like Drylins are useful in hostile dust or corrosion-prone environments.

Recirculating ball bearings have four or more oval tracks for bearing balls to roll in, that contact the shaft on all sides.
These are relatively low friction even as the moment load goes up, but there is minor unevenness from the balls coming into and out of preload as they go around the track.
The more preload there is, the more unevenness there will be.
Preload can be controlled by choosing different shaft diameter tolerances, or to some extent it can be increased by squeezing the outside of the bearings in a block.

For positional accuracy:

* Bearings on rods are relatively stiff in the axes they do resist, but they need a little bit of preload. In the other direction, moments are actually very manageable. You must use two rods, but by spacing them far apart there's strong resistance to moments about the direction of motion.
* Bending stiffness is limited by the stiffness of the rods. This is relatively mass-inefficient because rods are round: they waste stiffness in unimportant directions.
* The straightness depends on the rod quality, but is generally good. However, balls rolling in and out of preload can affect the straightness of the guided motion.
* Friction depends on the type (plain bushing or ball bearing), on preload, and on applied moment load. Especially when using shorter bearings and plain bushings, it is key to minimize moments on the bearing to minimize friction.
* Wear resistance depends on the type. Be aware that the right grease must be applied correctly for ball bearings to maximize lifespan.

Most printers using rods as guides should be using recirculating ball bearings simply because they are lower friction when not mounted perfectly.

The main issue with bearings for rods is that it's hard to securely mount them without distorting the bearing housing and affecting the preload in a difficult-to-control way.
Some printers like the Prusa i3 clamp their bearings with rubber pads, which avoids this issue but sacrifices rigidity.
Otherwise, the bores that rod bearings fit into must either be bored to the perfect diameter, or they must be adjustable.

The second issue with rods is mass for a given stiffness.
At small sizes, 8mm diameter rods and corresponding bearings aren't too bad, but the bearings for larger rods become surprisingly massive.
This is exacerbated by two other factors.
On printers, stiffness is usually only needed in one axis but rods, being round, always have equal bending stiffness in both axes, wasting mass.
Additionally, the mounting hardware itself needs to be fairly massive in order to properly mount the bearing without distorting it.
You need to do the math to compare the deflection of the rods bending versus the deflection of the motion system loaded with the toolhead and gantry mass in order to find the best size rods.

## Profiled Rail Linear Guides

Commonly known as "linear rails", these consist of rectangular steel profiles with two grooves cut into opposite sides that correspond with two tracks of recirculating ball bearings in a linear bearing car.

The profiles are periodically drilled and counterbored for machine screws, convenient for mounting to a surface.
The bearing cars themselves are convenient for secure mounting, with tapped holes in the rectangular prism housing.

The wider the rail, the better its resistance to torques about the axis of motion.
The longer the bearing car, the better the resistance in the other two axes.
Larger rail sections come with larger balls, which increase the load capacity.
Larger rail sections also increase stiffness, of course.

Rail preload is more precisely controllable than for rod bearings, since it doesn't depend on mounting.
It is controlled by choosing specific size bearing balls to put in the cars.
There are different classes of preload, with Z0 being no preload and the highest, Z3, having a preload of roughly 30% of the bearing's load limit.

For positional accuracy:

* In rotation, Linear bearings with appropriate rail sizes preload can be easily stiff enough. But if you have torsion forces, you need to make sure that whatever you are attaching the rail to can resist that.
* For linear deflections, stiffness goes up with larger rails, but more importantly the rails are bolted to another member that can provide as little or as much stiffness as required in one or more directions to optimize mass.
* The straightness is dependent on what the rails are mounted to. On small spans rails can be used unsupported, but that's not ideal. One important issue that must be handled is differential expansion between the rail and the structural member if used at higher temperatureus
* Friction is generally pretty good for rails, but you must watch out for overconstraints, which if imperfectly aligned can cause rails to bind up strongly. And as usual, try to minimize applied moments so as to minimize the loads under acceleration.
* Lifespan is good, provided proper lubrication is applied and that the motion system isn't binding.

For most printers, Z1 preload is appropriate to improve rigidity without increasing friction too much.
Z2 is used when precision is important, and Z3 for extreme loads such as machining where friction doesn't matter as much.

Additionally, to ensure resistance against deflection, rails should be attached to a stiff structural member.
On some very small printers with light toolheads, they get away with unbacked rails by choosing a relatively beefy rail section and having short spans and loads.
On larger printers, they must be used with backers to prevent too much deflection.

On a CoreXY machine with an unbalanced toolhead, you want to maximize torsion resistance about the axis of motion and Y-direction stiffness, but Z-direction stiffness isn't that important.
Many DIY CoreXY machines use T-slotted aluminum extrusion as a structural member.
One popular "upgrade" over T-slot extrusion to minimize gantry mass is an extremely skeletonized truss.
But you have to do the math to figure out whether it's actually worthwhile.

For cross gantry, the obvious choice should be a thin plate backer to stiffen primarily in the X/Y plane only.
The rails should be placed extremely close together in the Z axis and the toolhead designed to center its mass between them to minimize torsion loads.

On bedslingers, the rails themselves do not move quickly so just slap them on beefy structural members of your choice.

Avoiding overconstraint is another concern.
It's important to ensure that if multiple parallel rails are used, that alignment in all axes is perfect, or else selective compliance must be added to avoid binding.
With proper orientation, the distance between rails can be optimized for one temperature, but thermal expansion can cause rails that are spaced correctly at room temperature to bind up at temperature.
The other issue comes when you have a very rigid motion system but the rails are no longer coplanar due to warping.
Without having massive ground-flat billet halo structures to support the motion system (expensive!), this can only reasonably be mitigated by having selective compliance in the printer motion system in order to keep the forces from building up and causing binding.

Finally, one concern for straightnesss occurs with steel rails mounted on aluminum extrusions.
Steel expands less than aluminum, so as temperatures rise, the rail-extrusion system will form a bimetallic strip and curve.
This obviously reduces accuracy, so if you want your printer to operate at even medium chamber temperatures (20-30 C over ambient) you may want to add backers on the opposite side of the extrusion to balance the forces.
One overly-expensive way would be to put an identical rail on the other side, but sometimes thinner titanium backers are used to compensate for rails.

# Conclusion

V-wheels are bad.
Don't use them unless you really know what you're doing!
Keep moments to a minimum, have robust and precise tensioning mechanisms, and replace the wheels often.

Rods are fine, and on the low end can be very economical.
As performance goes up they are no longer cheaper than rails, and at the high end rails are generally better.
But rods do let you avoid overconstraints more easily.

Rails are definitely the best, but not all rails are equal quality or equally good deals.
Ask around for recommendations on where to buy, I can't possibly keep track of that here.
If your design is particularly rigid, make sure there's enough adjustability to prevent binding.

Common to all of these is that you really want to make sure forces are balanced to minimize moments.
Put your belts in line with the driven mass when belts are moving things along the guide axes, and put the guides in line with the driven mass when moving things perpendicular to the guide axes.
This will help minimize friction and wear.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
