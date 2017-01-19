+++
date = "2017-01-19T12:48:10+10:30"
title = "12v-to-5v-switching-regulator-v0.1"
description = "A ~80% efficient power supply!"
categories = ["electronics"]
tags = ["electronics","success"]
draft = false

+++

After the failure of my initial linear regulator design for the power supply of my fan control board, I have created a new switching power supply using the LM2678 "Simple Switcher" step-down regulator.

The design of this supply was based almost entirely on the example given in the [datasheet for the LM2678 regulator](http://www.ti.com/lit/ds/symlink/lm2678.pdf).

![Schematic Image](/images/switch-mode-ps-schematic.jpg)

A circuit board was designed based on this schematic:

![Board Design Image](/images/switch-mode-ps-board.jpg)

I tested this design on a breadboard prior to etching a circuit board and soldering everything together this time, as it was hugely frustrating to have wasted time etching the previous failed design only to have it overheat almost instantly.

![Breadboard image](/images/switch-mode-ps-breadboard.jpg)

This new supply has no such problems, and when breadboarded none of the components had any issues with heat generation when tested when an incredibly scientific "touch it and see if it's warm" test.

Having proven there should (hopefully) be no problems with the new design, I etched a new circuit board, drilled the required holes, and mounted all the components for the power supply. Testing again, it was generating five volts and not heating up substantially.

Given that the power supply seemed to be working OK, I hooked up an ESP8266 development board and measured the current from the 12v supply to the board, and from the board to the ESP8266.

![Photo of new control board](/images/switch-mode-ps-board-closeup.jpg)

The supply to the board was 190mA @ ~12V, while the supply from the board to the ESP8266 was 400mA @ 5V

Some rough calculations were done to work out how efficient the new board is:
```
Power in = 0.19A * 12V = 2.28W
Power out = 0.4A * 5V = 2W
Efficiency = Power out / Power in = 2 / 2.28 = 87.7%
```

I am entirely happy with this result, and so am proceeding with this power supply setup.

I then connected up a PN100 transistor to control one of the fans so I could test the full setup. There were two problems with this:

1. The transistor I connected is the one linked to D3 in the schematic. D3 on the NodeMCU boards matches up with GPIO0 on the ESP8266 which takes the ESP8266 into "flash" mode when it is pulled low during boot, which is exactly what happens as it is connected to the base pin of one of the fan control transistors which provides a path to ground. I'm still not sure how to get around this problem, so for now I'm just manually disconnecting D3 to boot the ESP8266, and reconnecting it after the board has started.
2. As I was lazy, and used a different kind of transistor when designing the board in Eagle, the collector and emitter pins were reversed. This meant I had to install the PN100 transistors I'm using "backwards". Luckily the base pin is in the middle or it would have been a lot more difficult to fix.

Those two points aside, everything is currently working very well. I have been running the board and one fan on a "fan on, 10s wait, fan off, 10s wait" loop for the last hour with no fires, minor burns, magic-smoke escapes, or other concerning incidents.

Without wanting to jinx it, it looks like this project might finally be coming to a workable build!


![Photo of testing control board](/images/fan-control-board-testing.jpg)


I also managed to blow the fuse in my multimeter by accidentally attaching the probes to +12V and GND while it was set to 200ma current measurement, so "new fuse" is now on my shopping list. Another reason to go back to Jaycar!

The full design for this board is available on my [GitHub](https://github.com/nicholasnelson/FancyFan-CircuitBoard)