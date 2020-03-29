---
layout: post
title: Arduino on a rechargable battery - how to self-switch off.
---


Battery powered things with a lithium battery are always a little complex.  You have to handle not draining the battery when your device isn't in use, not overdischarging the battery, and still being able to do whatever you wanted to do.   A lot of usecases can be handled by a sensor turning the circuit on, and the circuit turning itself off again when it's done doing whatever needs doing.


Here's a trick to make that simpler and cheaper.

## Abuse the DW01 battery protection chip to power off your circuit.

Your battery likely already has a DW01 and a pair of mosfets inside to protect it, or if you're using a [$1 battery charging and protection board](https://amzn.to/2UEzf6E),  it has one built in.

You can trick the DW01 into turning your circuit off by raising it's CS pin to high (specifically above 0.15 volts for 30 milliseconds).  It will then turn your whole circuit off till either you disconnect your circuit, start charging the battery, or the CS pin goes low again.   To make sure you don't loose the overload protection of the DW01, you should drive the pin through a resistor between 3k and 20k.

The CS pin can be accessed here on the common charging/protection boards: ![](images/dw01-highlight.jpg)

And this is the typical circuit wiring ![](images/dw01-wiring.png).

## To turn things back on

Either disconnect your circuit momentaraly (for example through a push-to-break button), or pull the CS pin low (to the battery- pin, not to the ground of the rest of the circuit - they aren't connected!).    Bear in mind, if you want to pull the CS pin low, whatever circuitry you use to do that will not be protected by the DW01 - that means you won't get the overdischarge protection , so things like switches are probably okay, but devices that use real power are probably a no-no.

Hope that helps!
