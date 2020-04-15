---
layout: post
title: Ebike Chain motion sensor with a broken inductor
---


Making an ebike is easy enough, but controlling the motor speed is tricky.  You want a bit of regen for braking (so a sensor on the brake lever?), and power when pedalling (A crank rotation sensor?), and it would be nice if the bike was only putting a lot of effort in when you were, which is really the product of the speed the pedals are turning times the force on them (A force sensor on the pedals?).

Is this sounding like a lot of effort and fragile sensors to buy, fit and maintain?

Try a new approach...


## A broken inductor for a sensor!

 * **Step 1**:  Accidentally stand on an inductor so the ferrite breaks.
   ![](/images/ebike-inductor-broken.jpg)
 * **Step 2**:  Put the chain near the break in the ferrite.
   ![](/images/ebike-chain.jpg)
 
And you're done.  You can now measure the rate of movement of the chain, the direction the chain is moving, and the tension in the chain.  As a bonus, the circuit doesn't mind getting wet, has no moving parts, and is non-contact.

Here's how:

 *  The inductance of the inductor can be measured by putting any old capacitor across it and hooking it up to an arduino to measure the frequency of oscillation.   The easiest way is to give it a voltage for a few microseconds, then use the [comparator](https://forum.arduino.cc/index.php?topic=158657.0) to see how long till the voltage becomes negative.
    
    ![](/images/ebike-inductor-capacitor.jpg)
 
 * As each link of the chain passes, the inductance will vary a lot up and down.  Count the oscillations, and you know how far the chain has moved.
 
 * When there is a lot of tension on the chain, the chain rises up by a fraction of a millimeter (on my bike at least).  That has a big impact on the DC level of the signal.  This is your tension feedback.   It's a noisy signal, because it also picks up bumps in the road, so filter it a lot.
 
 * When the chain moves, the combination of the broken inductor not being perfectly symmetric, together with the chain possibly not being perfectly symmetric means the sine wave you see is slightly more of a sawtooth wave.  Look which way the teeth face (by looking at the phase of the 2nd harmonic), and that tells you the direction the chain is moving.   This only works after 5 or 6 links of then chain have passed, but it turns out that's fine for backpedal e-braking :-)
 ![](/images/ebike-inductor-broken-diagram.png)
 
![](/images/ebike-chain-sensor-raw.png)
