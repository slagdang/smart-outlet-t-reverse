# Teardown of a smart switched outlet I bought in 2025

This is a KiCAD 9.X project. KiCAD is a free electronic design tool [available at kicad.org](https://kicad.org/).

## Product overview
The switched outlet is sold by Tapo.
They describe it as a Matter smart plug, but it is a switched outlet on a small box which plugs into your wall outlet.
It uses WiFi over IPv6 over WiFi. It does not use Thread.
This is for US voltage and outlets. It was purchased in July 2025.
The device allows switching of the outlet.

## Design outline
The product contains a transformerless switching power supply to generate a neutral-referenced
5V supply.
It contains a sub-module which has a RealTek Bluetooth radio and controller which uses the 5.0V supply.
It uses a 277V/16A-rated relay on the hot side to turn the connected device on and off.
The board has about 2mm of creepage clearance to components on the hot (switched) side.
The protective ground pin is not connected to anything inside except the output receptacle.
The controller uses a GPO to turn the relay on and off through an NPN transistor.
The power input is fused for the controlling circuitry with a fusible resistor. The fusible resistor
is sleeved in polyolefin heat shrink to protect against a fuse explosion causing further internal
damage like producing a short across the AC. Power through the unit to the attached device is
not protected with a fuse or similar.
The controller board appears to use a 5-pin switching power supply to cut the provided 5V voltage down
to that required by the RealTek MCU. This is more expensive than an LDO but produces less heat. It saves
up to 700mW continuosly. If left plugged in all year it would save about 4kWh per year. This could be
up to one US dollar per year compared to the other unit with the LDO. It may be less depending on how
far below its peak draw the processor idles at. The power lost in the fusible resistor is probably
several times larger than these savings and thus more than wipes them out.

## Design quirks

Each of these are small deviations from expected. Not every one may matter.

The used power supply chip suggests using a full-bridge rectifier for its AC input.
However this design uses half-wave. It does however put two diodes in series so that
a single diode failing short does not produce a short. This is probably a reasonable design
choice. The switching power supply does not have an English language datasheet so it is
hard for me to determine if it is used correctly. Nor is it possible to tell the power
rating other than likely being under 1A due to the output capacitor being 10µF. It is
hard to understand how this chip could be designed with a current sense input which
requires a sense resistor so small even for these low current levels that the required
resistance is such that 4 resistors in parallel are needed.

The device contains no X-class capacitor at all. Also this device is relying
on your wall circuit's protection for protection against overcurrent draw by the attached
device.

The device does not have a MOV for inrush limiting however the metal film fusible
resistor is 10Ω so this prevents large draws.

The single button on the controlling board is gasketed against the case for some
protection against materials ingress through the button slit.
The ingressing material can still reach the
controlling board but not the high voltage areas. The device of course also has the
receptacle on the front and those are not sealed so water could ingress there also
as it could on any similar device.

The board is laid out in a very straightfoward way using traces for all the controlling
circuity. 3 floods do exist for the current to the controlled device. There are also
strange areas of bumps in the high current floods. I do not know what these are for.

This device uses no components smaller than an 0603.

This device puts the button on the controller board. This means pressing the button is
torquing the controller board in its socket. It is soldered in with a single shear
(attached only at one end) arrangement. Is this a problem? Probably not. It also puts
the LED on the controller board which mostly just means it is smaller and perhaps less
bright.

## Device identification
The device is approximately 60mm wide by 35mm high by 35mm deep not including prongs).
It has a NEMA 5-15P on the back to plug into a US outlet. It has
a NEMA 5-15R on the front for plugging in the device you wish to switch.
It is rated for 15 amps out and 100-125V (presumably rms) in general use
(resistive load). It is rated for 8A (1kW!) incandescent load and 1/6HP motor load.

On the bottom it is identified as:

Mini Smart WiFi Plug

Model: Tapo 125M

It lists as FCC ID 2AXJ4P125
