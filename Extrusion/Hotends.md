# Hotends

A FFF 3D printer's purpose in life is to melt plastic and lay it down in a controlled manner.

The hotend is the part of the printer that actually performs the melting.
It consists of a "cold side" keeping the filament, which is under compression, as solid as possible right up until the moment that it reaches the "hot side", where the filament is melted in a heater block.
Below the hotend (or sometimes integrated into it), is the nozzle that sets the final diameter of the filament prior to extrusion.

Ideally, hotends deliver uniform, constant-temperature liquid plastic to the nozzle at all desired flowrates, but there are many considerations for doing this well.

I do not intend to recommend specific hotends, but to teach the basics for what to look for when selecting a hotend.

# Issues to Avoid

The following are common issues that occur in hotends.

## Heat Creep

Heat creep occurs when filament is allowed to reach its softening temperature before reaching the heatbreak.

As it gets pressed from behind by the extruder, the softened filament bulges and jams against the walls of the filament path.
No matter how hard it is pushed, flow will completely stop.

Inexperienced 3D printer users might think this is a "nozzle clog", but it actually has nothing to do with an obstruction in the nozzle opening.

Heat creep happens when the cold side isn't cooled well enough, or when the transition from cold to hot is too long and gradual.

Other factors for heat creep that come from printer settings instead of physical configuration is that heat creep is often worse at low flow rates (when you'd expect backpressure to be lower) because the heat on the cold side gets more time to diffuse into the filament, and that it's worse at higher hotend temperatures (which you'd expect to reduce viscosity and thus backpressure) because the cold side near the heatbreak gets hotter.

## Leaks

The pressures that exist inside a hotend can be absolutely monstrous.
If the interfaces sealing the molten plastic in are not pressed closely enough, this can cause filament to leak out and form large blobs of plastic that can destroy hotends.

When nozzles and heater blocks are made of materials with significantly different thermal expansion ratios, then it's important to tighten them at operating temperature so that you can be sure they do not loosen up.

Softer materials are easier to deform and create tight seals with, but they can also completely fail.
You don't want to rip off a nozzle in your hotend.

Make sure to use a torque wrench or torque screwdriver when tightening nozzles, as there can be a fine line between leaking from insufficient tightening, and damaging the heater block or nozzle.

## Poor Heating Control

If the heater or temperature sensor (or both) is poorly coupled to the heater block, then the printer controller's ability to tightly regulate the temperature is going to be impacted.

There are several aspects to this.

If the coupling is bad, it can result in difficulty actually controlling the heater, resulting in fluctuations and overshoots which will lead to unpredictable results.
Alternatively, if it's stable but the response time is poor enough, the response of the hotend to changing conditions such as cooling air or filament flow can be delayed enough to cause significant temperature excursions.

The next aspect is that the thermistor location affects where the temperature is controlled.
Some hotends have worse control of the final temperature when the measurement takes place at the top, due to the cooling environment being very different from the nozzle.

## Structural Rigidity

Most basic hotends only support the heater block and nozzle via the filament path heatbreak, which leads to more flexing under high acceleration and damage upon nozzle crashes.

Better hotends add structural reinforcement, but these differ dramatically in rigidity as well as whether they in turn impact heat creep due to increased heat transfer.

## Temperature Limits

The materials that make up the hotend and heater, as well as the type of temperature sensor, determine how hot a temperature the hotend can achieve.
If you intend to print more advanced materials, ensure that the hardware you select is capable of reaching the required temperatures.

# Structure

This section goes into more detail about what actually make up hotends and how they actually affect the performance.

## Heatbreaks

Heatbreaks refer to parts that connect the hot and cold parts of the hotend, with the goal of reducing heat transfer between the two as much as possible.

These come in two varieties: filament passage heatbreaks, and structural heatbreaks.

### Filament Heatbreaks

#### Radial Heatbreaks

In the past, many low-end printers used heatbreaks that effectively isolated temperature radially using PTFE tubing that goes all the way through the metal heatbreak to the hotend.

The PTFE has extremely low thermal conductivity, greatly reducing heat creep into the filament on the cold side.

Additionally, the material has the advantage of very low friction, which can be extremely useful when using long retraction lengths on Bowden extruders, as long retractions can get molten plastic stuck to the cold side.

However, the PTFE lining limits the maximum operating temperature of the printer, as it decomposes and releases toxic gases above around 240 C.

It also degrades over time, requiring occasional replacement.

#### Axial Heatbreaks

Commonly called "all-metal hotends", these use a thin-walled tube of a low-conductivity material to constrain the filament between the cold side and the hot side.

Usually this is metal such as stainless steel or titanium for strength, rigidity, and relatively low thermal conductivity.

Occasionally these are made out of zirconia for hardness and even lower thermal conductivity, though this cannot serve on its own to support the heater block.
When zirconia is used, there are structural heatbreaks used to support the heater block.

These can be somewhat less suitable for Bowden use, because a long retraction might pull molten plastic stuck to the cold side.

### Structural Heatbreaks

Older hotends used to use only the filament heatbreak to support the heater block, but this reduces the strength and stiffness of the hotend, increasing deflection of the nozzle tip under high acceleration and making the hotend susceptible to damage when tightening nozzles.

To mitigate this issue, some hotends are designed with additional structural reinforcement.
On the plus side, this allows the filament heatbreak be thinner and conduct less heat.
However, the structural supports themselves conduct heat from the hotend, potentially heating up the cold side of the filament.

Ideally, these are as long and/or thin as possible, made from material with as low a thermal conductivity as possible.

There are many ways that these are implemented. 

Sometimes, they can put the filament heatbreak under compression so that simple tension screws may be used for structure, though this risks damage to the filament heatbreak.
Example: Phaetus Rapido V1, Micro-Swiss Flowtech

Other times, the filament heatbreak is used under tension to compress the structural heatbreak, reducing the risk of damage to the thin filament heatbreak.
Example: DropEffect neXtG

The best structural heatbreaks use a truss-like structure to make the heat path longer and thinner while remaining rigid.
Examples: v9 (extremely thin members), Chube (extremely long distance to conduct)

## Cold Side

Even with an extremely effective heatbreak, the cold side of the heatbreak needs some way to dissipate any heat that makes it through.

### Standalone heatsink

Typically, this is done with a finned aluminum heatsink located coaxially around the filament path.

These are very simple and effective.

They only need a very small fan, or can even be operated passively with a good enough heatbreak setup thanks to the toolhead moving through the air.

### Separate heatsinks for structural reinforcement

One method to reduce the amount of heat transferred from structural heatbreaks into the filament on the cold side is to attach the structural heatbreak to a heatsink separate from the filament heatsink.

With separate heatbreaks, the filament heatbreak can be thinner and weaker and so transfer even less heat, minimizing heat creep.

However, often this could be better implemented by simply eliminating the structural heatsink and increasing the length of the structural heatbreak to reduce its conduction.

Examples: Slice Mosquito, Phaetus Dragon, Triangle Lab Rapido Ace

### Integrated into extruder

Some extruders use the extruder's structure itself as a heatsink to enable extremely compact packaging.
They put pins, fins, or grooves in the structure and mount a fan on it.

This is very neat and works well in open printers but the front face is less effective as a heatsink than more conventional coaxial finned heatsinks and heat creep can become an issue with some filaments at high chamber temperatures.

This issue is compounded by the fact that the extruder motor is also a source of heat.

Examples: E3D Hemera and Roto, Biqu H2, Smart Orbiter V3

### Conduction into toolhead

If the hotend's heatbreak is good enough and it is mounted to a large-enough aluminum toolhead, it may not need a dedicated heatsink at all.

The main example of this is Chube Conduction.

### Liquid Cooling

High performance hotends intended for extremely high temperature use are often available with liquid cooling instead of finned heatsinks, because it removes the need for a fan on the toolhead.

This makes them extremely resistant to heat creep, though of course with a corresponding complexity increase in requiring a pump, reservoir, and radiator for the printer.

On the other hand, that enables knock-on benefits such as allowing for liquid cooling of motors.

## Heater Block

### Meltzone Length

The longer the filament path between the heatbreak and the nozzle tip, the greater a hotend's capacity to fully melt filament at high flowrates.

The V6 heater block is 11.5mm long, or 17.5mm to the nozzle tip, a fairly short length by today's standards.

This can go all the way up to 52mm without the nozzle for the Chube Conduction, or even longer than that for crazy custom designs.

In addition to pushing higher peak flowrates, longer meltzones let you use a lower hotend temperature at the same flowrate, which can be good for high temp engineering plastics.

On the other hand, longer meltzones are harder to control flow in, requiring more PA and oozing more at rest.

### Heaters

Heaters are what actually produce the heat to melt the plastic.

#### Cartridge Heater

Cartridge heaters are usually nichrome wire embedded in ceramic inside of a stainless-steel tube.

These are simultaneously the most bog-standard heater type but also the most performant, with some available that are capable of extremely high temperatures.

Hotends that use 6mm diameter cartridge heaters are very friendly for repair/replacement, since you can get cartridges of many different power levels and maximum temperatures to suit your needs from many different places.

Cartridge heaters can be affixed in heater blocks either by being held in place by a setscrew or by having a screw clamp a flexible section of the heater block around the cartridge.
The important thing to keep in mind when installing a heater is that overtightening can cause the heater to break due to thermal expansion.
Tighter is not better.

#### PTC Ceramic Heater

Ceramic heaters have a heater element inside that increases in resistance at higher temperatures, causing the effective wattage to drop off.

They are very small and light, enabling faster heat-up times, but the decrease in wattage at the top end limits how hot they can feasibly heat a hotend.

They come in two varieties: planar and cylindrical.

Cylindrical heaters were often used because they allow a simple round hotend that heats the filament from all sides, but due to thermal expansion issues they often have poor contact with the heater block and are relatively prone to failure.

Planar heaters in the shape of a small rectangle are growing more common.
They don't have contact issues due to the use of simple steel spring clips that hold them to the heater block, allowing them to expand while still having a good thermal connection.

Compared to cartridges, ceramic heaters are harder to source and basically lock you in to a particular size, but the resulting hotends can be extremely small, which is helpful for very fast printing.

#### Nichrome or Kanthal Wire

Some hotends, notably the Goliath, use Kanthal wire as a heating element.
This forms an electrically insulating aluminum oxide layer on the outside so it can be directly wrapped around a metal heater block.

This allows for the heater to fully surround a block without the risks of cracking from a cylindrical ceramic heater.

However, it means that if the heater breaks, the entire heater block must be replaced.

### Materials

The material of the heater block affects the performance of the hotend to a moderate extent.

The important parameters (besides cost) are density, thermal conductivity, and coefficient of thermal expansion (CTE).

A denser material increases the mass of the hotend, which is worse for the motion accuracy of the toolhead.

A more conductive material helps transfer heat better.
This is often relatively unimportant, but it can have impacts on how quickly changes in temperature are detected by the temperature sensor and thus affects how well the temperature can be regulated.

Finally, coefficient of thermal expansion is important because it determines whether to expect loosening or overstressing of the block due to a mismatch with the nozzle.

The three common materials in use are aluminum, copper, and non-stainless steel.

Aluminum is inexpensive and lightweight with good thermal conductivity, but it has a low maximum service temperature, low hardness, and a high CTE of 23 microstrain per degree C.
**Be careful when operating aluminum above 270°C, as its strength drops off dramatically and hot tightening at E3D's recommended torque specs (2 Nm) can strip the threads.**

Copper has great thermal conductivity and enough maximum service temperature for any filament, but it has a high density, is expensive, and doesn't have great hardness.
Its CTE is 17 microstrain per degree C, which is similar to that of brass nozzles and obviously the same as copper nozzles.

Steel has great hardness and maximum service temperature, but it has a lower thermal conductivity which can make thermal regulation slightly more challenging.
Its CTE is around 11 microstrain per degree C, which pairs better than other materials with tungsten carbide nozzles (around 5.5 microstrain per degree C).

### Temperature measurement

One of the keys to consistent extrusion is proper control of the temperature of the plastic extruded through the nozzle.

If the temperature drops momentarily, the flow may drop and the layer adhesion could be reduced.

#### Placement

Ideally the entire heater block has enough material and thermal conductivity for the entire heater block, including nozzle, to be a uniform and constant temperature.
However, in reality, the heat is coming from a localized spot (for a 6mm cartridge or planar ceramic heater) and heat is being lost to the heatbreak(s), cold filament feeding in, and convection at the nozzle tip.

Most hotends only measure one location, which is fine on smaller hotends, but on long hotends it is often near the top.
This is able to deal with heat lost to incoming filament and the heatbreaks, but it is poor at responding to heat loss from part cooling air blowing on the nozzle.

A sensor near the nozzle will be worse at handling incoming filament, but model-predictive control of the hotend can compensate for that.

#### Sensor type

Temperature sensors have different behaviors that lend themselves to different uses.

NTC thermistors are commonly used for their low price, but they are only barely usable up to 300 C, leading to hotend temperature limits being set to 280 C.
They are made from semiconductors to have large drops in resistance with increasing temperature, roughly exponential.
However, most of these give up a lot of precision at the high end, where the thermistor resistance is very small compared to the usually 4700 ohm pullup resistor on the ADC measuring it.
Additionally, the semiconductors themselves are vulnerable to drift as they get temperature cycled.
This causes temperatures to vary over time, requiring settings changes.

Resistance Temperature Detectors, or RTDs, are an alternative.
Made of a simple metal, usually platinum, these have much smaller resistance changes for a given temperature change, but they are much more stable than thermistors, and platinum RTDs are capable of much higher temperatures than thermistors.
These come in two common resistances: 100 ohm and 1000 ohm.
100 ohm ones are much more affected by lead resistance if not measured using 3-wire or 4-wire sensing.
Additionally, their resistance is much lower than the typical 4700 ohm pullup resistor, leading to worse resolution without an RTD-specific ADC.
1000 ohm sensors can be used with conventional 4700 ohm pullup thermistor ports on common 3d printer motherboards, but if the microcontroller ADCs aren't good (for example the RP2040) then the results can be relatively poor.

Thermocouples are also usable, with an extreme temperature range, but these have their own quirks such as aging over time and absolutely requiring an amplifier.

#### Sensor form factor

Just as a note for compatibility, different hotends use different form factors for their temperature sensors.

Low-end hotends simply use a screw to hold a thermistor's glass bead in a cavity in the heater block.
This sucks and is vulnerable to damage.

Other than that, the two common sensor form factors are 3mm cylindrical and M3 thread-in sensors.

## Sock/Draft Shield

To improve the temperature uniformity across the heater block, reduce the power to maintain temperature, and reduce the cooling effect of part cooling air, heater blocks are usually covered with insulation.

On almost all hotends for sub-300°C temperatures, this is a "sock" made of silicone that tightly fits around the heater block and usually attempts to cover at least some of the nozzle.
The lifespan of silicone is basically unlimited at lower temperatures, but it gradually degrades at temperatures approaching 300°C.

For higher temperatures, the hotend can be wrapped in fiberglass or mineral wool and that can be secured with Kapton or aluminum tape or silicone tubing.
There is also premade fiberglass insulation tape that can work.

Ultra high temperature hotends often have provisions for a low-conductivity draft shield made of stainless steel or (ideally) titanium. Chube, in particular, uses the titanium structural heatbreak as part of its draft shield.

# Nozzle Compatibility

You do want to make sure the nozzles you want exist in the form factor of your chosen hotend.

Some hotends can accept multiple types of nozzles, though often with overall length changes.

## V6

E3D's V6 nozzle is basically the standard for enthusiast printers, and it's available in many basically any variety you'd like.

12.5mm overall length.
7.5mm M6 threaded section to the back of the hex.
5mm hex+tip length.

### Volcano

The E3D Volcano nozzle is a V6 nozzle with a longer threaded section to extend the meltzone.
All volcano-compatible hotends are longer than the minimal v6 hotends, but some v6 hotends have longer meltzones than a minimal volcano hotend.
Volcano nozzles can be used in a V6 hotend with a nut to help heat transfer, though with a longer overall length.

21mm overall length.
16mm M6 threaded section to the back of the hex.
5mm hex+tip length.

#### Volcano-like

Some manufacturers made similar nozzles to the volcano.
Their hotends can fit volcano nozzles, though there are compatibility issues around cooling ducts.
The lengths are slightly longer so you may need to adjust part cooling ducts or bed leveling hardware if you want to use standard volcano nozzles.

##### Creality K1 Volcano-Like

23mm overall length.
15mm M6 threaded section to the back of the hex.
8mm hex+tip length.

##### Sovol SV06+ SV07 Volcano-Like

This is just like an E3D volcano but with a longer tip to provide room for better airflow around the heater block.

23.5mm overall length.
14.5mm from the back to the end of the M6 threads.
16mm M6 threaded section to the back of the hex.
8.5mm-ish hex+tip length.

### Supervolcano

This E3D standard, a ridiculously lengthened version of the V6, never really caught on because the original hotend for it severely lacked rigidity due to a lack of structural support.
But you can use these nozzles in a Chube with a meltzone adapter.

51.5mm overall length.
46.5mm M6 threaded section to the back of the hex.
5mm hex+tip length.

## Mk8

Many basic hotends, such as those on the original Creality Ender 3, use this nozzle.

This has a shorter threaded section and a longer tip than a V6 nozzle, and is overall 0.5mm longer.

Mk8 hotends can usually function fine with a V6 nozzle, but V6 hotends cannot work with a Mk8 nozzle.

13mm overall length.
5mm M6 threaded section to the back of the hex.
8mm hex+tip length.

## FIN

A newer standard designed by Slice in collaboration with Bondtech and Micro-Swiss with a prescribed tip geometry to allow the hotend socks to cover most of the nozzle, reducing the unwanted nozzle cooling from part cooling fans.

It also uses a shorter threaded section to reduce the effects of differential thermal expansion between nozzle and heater block.

Not many hotends are available for it, but hopefully more are coming.

## And many others...

## Integrated Heatbreak

Some hotends use nozzles that have the heatbreak installed directly into the nozzle.

This eleminates user-error in tightening the nozzles, whether that be undertightening and leaking or overtightening and snapping the nozzle.

### E3D Revo

The original integrated heatbreak standard, Revo has the nozzle thread into the heatsink and uses a spring-loaded heater block to transfer heat to the nozzle.

It is toolless, but has been known to come unscrewed on its own in some circumstances.

### Prusa Nozzle (for Nextruder)

Prusa's take is sorta v6 compatible, and it involves snugly screwing the heater block onto the nozzle, then holding the heatbreak in the heatsink using a setscrew.

You can use V6 heater blocks with it, but the cold side is different.
You can also use V6 nozzles with an adapter (which is basically just a heatbreak with the appropriate cold side).

### Triangle Lab TUN

It is similar to Prusa's, except it doesn't have a copper ring around the cold side of the heatbreak to improve heat transfer, instead using a grub screw on a force spreader in the hotend to prevent buckling of the heatbreak.

This is compatible with V6 heater blocks, just like Prusa.

### Micro-Swiss Flowtech

These nozzles thread into the heater block, which is loosely retained using two structural screws.
The heatbreak is placed in compression and the structural screws are in tension.

### Creality Unicorn nozzle

This nozzle is generally like the Prusa Nozzle but uses a rigidly mounted heater block that the nozzle is snugly screwed into. 

### QIDI Plus4 nozzle

This nozzle is generally like the Prusa Nozzle but uses a rigidly mounted heater block that the nozzle is snugly screwed into.
It additionally uses a zirconia filament heatbreak to better prevent heat creep, taking advantage of the rigid heatblock mount.

## Integrated Heater Block

Some printers have a single unit heatsink, heatbreak, heater block, and nozzle, which the heater and thermistor are attached to.

### Bambu Lab

The X1 and P1 series hotends have the nozzle integrated in the hotend, with a steel clip holding the heater and thermistor on.
Changing nozzles involves swapping the cold side cooling fan, heater, and thermistor over.

The A1 series hotends eliminate much of the hassle by hard-mounting the heater and temperature sensor, and having the hotend nozzle assembly simply clip in.

### Sovol SV08

The Sovol SV08 only integrates the heatbreak, heater block, and nozzle.
Changing nozzles is similar to on the X1 and P1 except the heatsink is a separate piece that is not replaced.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
