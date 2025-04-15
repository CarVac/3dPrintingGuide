# Nozzles

Nozzles are where the rubber meets the road, so to speak.

To some extent, almost any nozzle *can* be made to print well, but better nozzles can help you print faster or have more consistent extrusion or last longer without maintenance.

## Geometry

### Orifice Size

The key parameter of any nozzle is the orifice size.
This sets your tradeoff between detail and print speed.

Most product lines of nozzles are available in a range of sizes, so you get to pick what you need.

But you'll mostly never find hardened nozzles in small sizes below 0.4mm, because the fiber-filled filaments that need the wear resistance would clog the orifice, and you'll likewise never find high-flow nozzles in small sizes because filament melt rate is not a bottleneck in small sizes.

If you want to use a very small nozzle, you need to make sure that your hotend is particularly good at avoiding heat creep.

### Tip Geometry

Around the orifice, before the taper begins, there is a small flat that helps maintain surface quality.

If you buy premium nozzles, this will always be nicely machined, but cheap nozzles with uneven flats may tear up the surface and cause bad print quality.

### Wear

Eventually, as a nozzle gets oodles of filament squeezed through it and has its tip rubbed all over the top surface of a print.

This causes both orifice size to change and the tip flat to become worn.

You can adjust for the different orifice diameter, but sometimes the wear on the flat is enough to cause unevenness that impacts prints.

Choosing harder materials helps avoid this wear.

## Material

The choice of nozzle material presents performance tradeoffs for printing.

### Single-Material 

#### Brass

Brass nozzles are the cheapest you can get.
Brass itself is inexpensive, is easy to machine, and has good thermal conductivity.
Additionally, it has good thermal expansion matching with hotends that have copper heater blocks.
However, it is prone to wear and not great at high temperatures above 300°C.

That said, if your filament isn't abrasive, there's not too much reason to use any other materials.

#### Copper

Copper is an excellent upgrade over brass because it has higher temperature resistance.
It also has higher thermal conductivity, but that's not so impactful as it's far from a limiting factor.

However, it's not much more wear-resistant, and it costs more.

#### Hardened Steel

For entry level printing of abrasive filaments, a nozzle made of hardened tool steel is an inexpensive way to minimize wear.

However, this has much lower thermal conductivity than brass, to a degree that significantly impacts printing.
Even for non-abrasive filaments, hardened steel nozzles may need the hotend temperature set as much as 10-15 degrees C higher than for brass nozzles.

It's wear-resistant, but not impervious to wear, so many people don't like solid steel nozzles.

#### Tungsten Carbide

Some higher-end nozzles are made entirely from cemented tungsten carbide.

Tungsten carbide is extremely hard and strong, and has almost as good thermal conductivity as brass.

Additionally, they have enough temperature resistance to withstand direct flames, letting you clean them out using a blowtorch if you really need to.

Because they're sintered from powder, solid tungsten carbide nozzles can be made with unique geometries that would be extremely difficult to produce in a normal metal, such as the fins in Bozzle or the narrow slot in Nanoflow nozzles.

If they're available for you and the cost is acceptable, tungsten carbide nozzles can be a good investment as a "forever" nozzle.

However, you have to be careful when using it with aluminum heat blocks because the thermal expansion mismatch is particularly large.

### Multi-Part Nozzles

Sometimes it's not possible to manufacture an entire nozzle in the primary material you want.
To get around this, many nozzles are actually assemblies of a brass or copper threaded portion for machinability and thermal conductivity, and some other material insert specifically for hardness.

These can work really, well, but they add a failure point where a leak may occur.

#### Hardened Steel Insert

The most basic form of these multi-part nozzles is a hardened steel tip mounted in a brass or copper body.

They are still somewhat vulnerable to wear, but the tip is harder than an all-brass nozzle and it's better thermally than an all-steel nozzle.

#### Tungsten Carbide Insert

Carbide inserts are more economical than full-carbide nozzles, but they lose the benefit of blowtorchability, and the thermal expansion differences can cause leaks.

#### Sapphire Insert

Sapphire (or ruby, which is just a particular color of sapphire) inserts offer extreme hardness, even better than tungsten carbide.

But they have worse thermal performance, and the monocrystal tip is vulnerable to cracking if there's a bed crash.

These are fairly expensive.

#### Silicon Carbide Insert

Silicon carbide is even harder than sapphire, and has better thermal conductivity than tungsten carbide.
The only reason it's not used for entire nozzles is that it isn't sintered the way tungsten carbide is.

The main disadvantage is that, like sapphire nozzles, the tip is vulnerable to cracking.

These are also very expensive.

#### Polycrystalline Diamond (PCD) Insert

On the top of the heap for nozzle tips is polycrystalline diamonds, the hardest possible material.

On top of the hardness, they have incredibly high thermal conductivity and very low friction, reducing the amount of plastic that sticks to the nozzle.

The polycrystalline nature of the diamond also makes it more resistant to fracture than sapphire and silicon carbide inserts.

The main issue is they are extremely expensive, and you don't have the blowtorchability of a solid tungsten carbide nozzle..

## Heat Transfer Enhancements

When trying to print quickly, one of the limiting factors in how fast you can print is how fast you can get heat to the center of the filament.
There are several approaches for enhancing the performance relative to a straight cylindrical bore, that involve reducing the distance to the center.

### Flow Splitters (CHT)

One prominent high flow geometry involves splitting the flow of plastic into two or more narrower passages that reduce the distance to the center of the filament.

This is what Bondtech calls Core Heating Technology, as it heats the filament from the core outward,

If the filament is fully melted, if not at the desired temperature yet, before it reaches the splitter, this can greatly improve the heat transfer to the melt pool.

However, on short hotends you can run into what I call the "cold core" issue: when the flowrate gets hot enough, the still-solid core of the filament will run into the splitter and produce a lot of backpressure, reducing the effectiveness of the hotend.

### Projections

Bozzle, a cemented tungsten carbide nozzle, tries to improve heat transfer to the core of the filament by having fins protrude inward from the walls of the nozzle.
Even at high flow rates, this allows the cold core to pass by the fins, picking up heat from their proximity without hitting any obstruction.

### Narrowing to slot

Nanoflow, another cemented cemented carbide nozzle, simply narrows the entire melt chamber to a narrow slot.
This results in a very short distance between the coldest part of the filament and the hot walls.

## Coatings

Low-end brass nozzles are often uncoated, but higher-end nozzles are coated to mildly improve wear resistance and to help reduce the tendency for filament to stick to the nozzle.

Some manufacturers claim that the coatings are enough to provide significant wear resistance, but it's difficult to verify their claims.

Most tungsten carbide nozzles are uncoated, but Nanoflow has a nonstick coating.

## Tip Shape

Most nozzles have a fairly blunt conical tip to maximize heat transfer in the presence of cooling air, but some are specifically designed to be pointier for nonplanar printing or belt printer use.

## Hotend Compatibility

The most comprehensive selection of nozzles is currently available in the V6, volcano, and Mk8 form factors.
More proprietary shapes are usually only catered to by a handful of third-party manufacturers, if at all.
The FIN standard is promising, but hasn't achieved wide adoption yet.

See the [nozzle compatibility section of the hotend document](Hotends.md#nozzle-compatibility) for more detail.

---

This work is licensed under Creative Commons Attribution-ShareAlike 4.0 International
