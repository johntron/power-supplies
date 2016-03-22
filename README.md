# Open Power Supplies

Designs for electronic power supplies. To limit scope, I've decided to start with only mains AC to low-voltage (less than 50V) designs.

# General design

Power supplies are a combination of:

1. Unregulated linear power supplies for bulk power conversion
* Zero or more switching mode converters for intermediate power conversion (one per output)
* Optional voltage feedback circuit for regulation

Numbers 1 and 2 may be combined for simple 1-output circuits, and number 3 can be a simple voltage regulator IC (with a heatsink to dissipate all the wasted energy). I recommend [powerEsim](http://www.poweresim.com/) to help choose appropriate designs.

#Definitions

* Input - possible input characteristics (AC/DC, low/high voltage/current/power, etc.)
* Mains - can be powered from consumer wall outlet (regardless of country)
* Isolated - no direct conduction between input and output (provides safety and eliminates ground loops)
* Regulated - changes to input and load have little/no impact on output
* Adjustable - input/output can change without soldering
* Linear - primary components operate in linear regions only
* Efficiency - percentage of input power converted to output power

# Hard truths

1. Isolation requires some kind of transformer if power will be drawn from input. Don't be fooled into thinking optoisolators are a magic bullet; they can only modulate existing voltage/current. No current flows *across* the isolator.
* Transformer sizes shrink with input frequency. The infamous iPhone charger contains a very small transformer.
* Mains power is deadly, and I'm not responsible for your ignorance. Everyone warns about this for a reason. If you're unsure, you'll only kill/maim yourself.
* p-n junction components (transistors and diodes) are inefficient in linear regions. Efficient circuits keep these in non-linear regions as much as possible.

## Linear power supply

* Mains / AC input
* Isolation by transformer
* Only adjustable if variac transformer or variable regulator
* Linear
* Can be regulated with voltage regulator
* Low (40-60%) or high (90-95%) efficiency

Consists of a transformer, rectifier, and filter components. Output can be regulated by adding a voltage regulator between output and load at the cost of efficiency.

![linear power supply diagram](https://en.wikipedia.org/wiki/Power_supply#/media/File:ACtoDCpowersupply.png)

## Switching-mode converters

The basic switching mode power supplies (SMPS) use transistors to switch input power into or out of an inductor. The inductor can be a separate component or one side of a transformer. Power conversion leverages the facts that inductors store energy in their magnetic field and also "resist" changes in current. More advanced SMPS's use both sides of the transformer as an integral component.

### Buck

Reduces voltage, increases current. See [Wikipedia's "Concept" section for functional description](https://en.wikipedia.org/wiki/Buck_converter#Concept).

### Boost

The opposite of buck. Increases voltage, decreases current.

### Flyback



## Voltage regulation

### Simple linear voltage regulator

Pick the right IC, slap a big heatsink on it, and you're done. Be aware that all voltage regulators have some amount of droput voltage, so the preceding power supply stage will need to supply slightly voltage than the desired output. To reduce droput voltage, use a low-droput (LDO) regulator.

### Voltage feedback/-forward control