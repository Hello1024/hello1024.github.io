---
layout: post
title: Worldwide power grid with glass insulated HVDC cables.
---


Moving electricity around the world has huge financial and environmental benefits.   Unfortunately, current power transmission systems are both lossy and expensive to build.   This post explores an alternative design for cables to make undersea power transmission substantially cheaper.


# Idea

Fused silica (glass) is a really good insulator (500 MV/m, vs 150 MV/mm for XLPE plastic), and is very cheap.   By using it as cable insulation, cables can be made substantially thinner and cheaper.


Unfortunately, glass isn't known for its ability to bend, which introduces logistical challenges.    I propose these be solved by manufacturing the cable onboard a boat in a continuous process and directly laying it.

The cable would consist of an aluminium conductor surrounded by a silica insulator.   There would be no outer protection - instead, the silica would be surface hardened, rather like a [prince ruperts drop](https://en.wikipedia.org/wiki/Prince_Rupert%27s_drop).     The extreme internal tensions should be sufficient to allow the cable to be laid on the ocean floor and span lengthy crevasses without breaking, removing the need to bury the cable - more costs saved.

# What voltage??

HVDC cable voltages are chosen to trade off the cost of the conductor (thicker=more amps!) with the cost of the insulator (thicker=more volts!).

Assume that we want our cable to transmit 10 Gigawatts across the Atlantic ocean - which would make it on par with the biggest existing links.  Do [a bit of math](https://docs.google.com/spreadsheets/d/1Pwr18v2juYgfpGX553o18YlmazdwxXBZic9R5rKAo9w/edit?usp=sharing), and it turns out 14 megavolts is the sweet spot.    That's way higher than existing projects (typically 0.5 megavolts), but inverters based on MOSFETs scale with cost proportional to power (one can just stack the mosfets and [optically control them](https://ieeexplore.ieee.org/document/7468138)), so this shouldn't matter.

The convertor stations could use air as an insulator (you need 5 meters of dry air on all sides), but it might be better to do the whole thing in transformer oil (500mm on all sides), and/or encase the circuits in moulded silica glass (25mm case thickness, but you're going to have to be very careful with joint design).

# Manufacturing

The cable manufacturing itself requires new techniques to be developed.    One approach is to have a ~1800C continuously fed furnace with silica, and continuously extrude a slab.   The slab is then curled into a 'U' shape, and molten aluminium is poured into the U.  The U is then sealed at the top.   All shaping is done by steel dies which are cooled by water or air boundary layers (like an air hockey table).   The cable is then quenched in water to surface harden it, before it moves out of the back of the ship and falls to the ocean floor over a length of many kilometers (due to very low curve radius).

## Logistics

Cable manufacture would occur at a constant speed of perhaps 2 kilometers per hour - crossing the Atlantic in 4 months.

To build this cable, 80 mm diameter, at a sluggish walking pace, would require a massive 40,000 tons of sand (silicon dioxide), so it probably makes sense to resupply the manufacturing ship every ~week whilst it is producing, allowing a smaller 'furnace' boat to be used.

### Laying process

Once the cable comes out of the back of the ship, it will not have sufficient tensile strength to get to the bottom of the deepest oceans (6 kilometers!).  This can be solved by large buoys attached to rollers on the cable spaced every 50 meters or so behind the ship.  The rollers can be regulated entirely passively, since lowering a heavy object requires no energy.

## Storms

### Waves
Typical mid-ocean wave heights are 5+ meters.    As the boat rises and falls in the ocean, it will be necessary for the cable, attached to the boat, to rise and fall too.    This will exert large tensile forces in the cable.   If the cable cannot survive those forces, the whole manufacturing system must be kept at constant height despite the ship rising and falling, which adds significant complexity and cost.

Glass ovens are made of fairly delicate zircon bricks, and building a kiln that can be at 2000C whilst also surviving sloshing molten glass at sea could be a real challenge.

### Pitch, Roll, Yaw
The final stages of the manufacturing system cannot pitch, roll or yaw during deployment otherwise the cable will be formed with bends, which will dramatically weaken it.    This might be resolved by choosing a boat with an active stabilization system,  but it's also possible to stabilize just the manufacturing equipment, and/or to use the cable itself as a reaction torque for stabilization.

## Cable strength
Prince Rupert's drops appear to only fail when the exterior reaches a zero tension state (rather like prestressed concrete).  With [pressures of 700MPa possible](https://www.google.com/search?q=prince+ruperts+drop+internal+pressure), we can calculate that a span with an 80mm cable can go 64 meters before failure.    It's possible that this could be further with chemical hardening.   Choose the route such that no crevasses of more than 64 meters happen. 

One can get an intuitive sense for this in a scale model by laying a bare fiberoptic across a floor.  Whilst a fiberoptic is fragile to bending, one would not expect it to break by simply being laid across a lumpy floor, with spans perhaps thousands of times the diameter.

# Economics
The energy+material cost (which normally is the main cost for undersea cables) of this cable is a mere $5M, and it can supply power for ~20 million homes from the far side of the ocean.  Laying it requires running a custom ship for 4 months with a glass factory onboard.  The scale of the glass factory is similar to existing land-based factories, with possible simplifications because there is no need to mould beer bottles or have loading bays for outgoing product.    A crew of perhaps 30 people could supervise the factory, onboard a converted 5000 TEU container ship. Ship operating cost= $80k/day, plus $20k/day for the glass factory operating costs.  Add 10 days either end for starting/stopping too. 

Capital cost of the ship modifications: Similar size glass factories cost around $100M, so assuming a 5 year lifespan, $60k/day for the factory capital cost.

Total cost for installed trans-atlantic cable = $23M.   Which is insanely cheap compared to other cables.    Obviously you can't have one cable for that price - R&D costs will dwarf this until such cables become common.


The converter stations, grid connections, landing spot and political considerations will dominate the cost, but those are all independent of the distance and not analyzed here - but be reassured that if cables could be laid this cheaply, almost all connections make sense to build.


# Failures/repair

## Humans
The cable, if snagged by a ship anchor, would catastrophically fail.   Not only would it snap, but the internal stresses would [propagate the crack along the entire length](https://www.youtube.com/watch?v=SVSw2jvYTMw). 

While there are various approaches to preventing crack propagation and repairing the cable, the best option is likely to simply install spare cables with slightly differing routes.

## Geological movements
The cable is really un-stretchy.    That means it must be laid in a very slightly wiggling path on the seafloor to absorb a few feet of ground movements (continental drift, earthquakes, etc)

## Erosion
The prince Rupert's drop surface is super hard, so abrasion even from fast flowing sand will be slow.   There could also be chemical weathering, but the ocean is saturated already with silicon ions, so I doubt weathering will be fast.

## Electrical protection
14 megavolt fuses, switches and protection systems do not currently exist.   The cheapest approach is probably to allow the cable itself to be sacrificed in this case, and design the converter stations carefully to minimize the chances of that happening.    For inspections and maintenance, the converter stations and cable would all be taken offline together, with disconnects on the AC side.   This means there is no need to make the converter rooms human-safe whilst energised.

# Open questions

 * How pure does the silica need to be to get these high insulation properties?
   The cost goes up fairly dramatically if the insulator isn't as good as wikipedia suggests...   Various sources have wildly different figures.

 * Will it be strong enough to be tensioned across a rocky outcrop and not crack?
   The surface of the cable will be harder than nearly every rock in the ocean (except diamond), so it should crush rocks before cracking itself.  Long spans of hanging cable can be avoided by surveying the route first and avoiding such formations.

 * Are there better materials - other ceramics or glasses?
   The key thing is a material that is cheap, decent insulating properties, does not need a slow crystal growth phase, and which can be strengthened easily with the 'prince ruperts drop' effect, or some other [chemical strengthening](https://en.wikipedia.org/wiki/Chemically_strengthened_glass) approach.

 * Is a prototype feasible?
   It appears washing-machine sized continuous glass furnaces are available for [sub $3k](https://www.alibaba.com/product-detail/1200C-1400-1600-1800-Degree-Continuous_10000025754570.html).  Aluminium can also be melted and piped in steel pipes [at hobby scale](https://www.alibaba.com/product-detail/Melting-Furnace-10kg-100kg-Scraps-Iron_10000014057267.html).  This plus a small boat rental could lead to the first laid cable.    By choosing a smaller diameter the glass is more flexible, making laying easier, and lower voltages can be used for a demo.    Lay a cable a few miles out to sea and demonstrate it doesn't immediately fail (ie. hook it up to a van-de-graff generator and verify operational voltage) would show the principle is sound at least.  Maintaining a constant diameter for both the core and insulation would likely need computerized feedback system, but even adjusting gates by hand should end up with something approximately cable-shaped.


# What next?

Unless someone [drops me an email](https://omattos.com/contact) with a lot of enthusiasm or an offer of money to some R&D and build a pilot, this project is probably parked for now - it’s way out of my ‘self fund for fun’ budget!





