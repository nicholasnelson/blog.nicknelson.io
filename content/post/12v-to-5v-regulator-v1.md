+++
categories = ["electronics"]
date = "2017-01-09T11:54:32+10:30"
title = "12v-to-5v-regulator-v0.1"
draft = false
description = "A 12.5% efficient power supply"
tags = ["electronics","derp"]

+++

For a stupidly over-the-top personal cooling fan project I’m currently working on, I need both ~1A @ 12v for three 12v fans, as well as ~0.5A @ 5v for the control circuit.

The best way to do this that I have been able to work out with my extremely limited knowledge of electronics is to use a 12v wall-wart powering the fans directly, and some kind of regulator to bring that voltage down to the 5v required for my control board.

![Breadboard regulator](/images/bb-reg.jpg)

I settled on the LM2940CT 5v voltage regulator as a starting point, and set about breadboarding a test of the regulator.
This worked really nicely, and gave a stable output voltage close enough to 5v to suit the needs of this project when tested with a multimeter with no load.

The flaw with this plan, I found after burning myself on the regulator, is that linear regulators such as the LM2940CT work by dissipating excess power as heat.

The power dissipation of the regulator follows the formula:

```
P = (Vin – Vout) * I
```

This meant that in my setup assuming a current draw of 500mA, the regulator needs to dissipate (12-5)*0.5 watts as heat, or 3.5W.

The datasheet for the LM2940CT shows that this level of power dissipation would be acceptable with an ambient temperature anywhere up to 90°C… as long as I have a 10°C/W heatsink attached. Without this heatsink, I was hitting almost 200% of the maximum power dissipation.

While it’s certainly possible to obtain a heatsink, I’ve decided against pursing that for now as even with a heatsink attached, with that much power being dissipated as heat for a working current of 0.5A, we have a power supply with 12.5% efficiency.

To try to increase efficiency, I’ve started looking at switching regulators. Currently I’m planning on going with the MC34063. This will make the power supply more complex, however research suggests I should be able to get efficiency over 90%.

A 77.5% increase in efficiency easily seems worth the added complexity of using a switching regulator.