# using-LTspice-analyze-the-same-diode-circuits-using-two-different-diode-model
A simple circuit with a single series diode and a resistor and a DC source. The diode is connected in series with the resistor and the DC source. This single series diode circuit has a resistor to limit the current, from the DC source. The single series. The resistor work together with the DC source.

V1 (DC source) -> D1 (diode) -> R1 (1 kΩ) -> GND

To get the information we need we have to measure the current that is going through the diode, which is called current ID. We also need to check the voltage at the diode so we will measure it at the anode and the cathode of the diode. We will do this as needed.

LTspice: ideal-diode schematic (how to approximate an “ideal” diode)

Place a voltage source (F2 → “voltage”) named V1 between node VIN and ground.

Place a diode (component “D”) between VIN and node NOUT.

Place R1 = 1k between NOUT and ground.

Create an “ideal-like” model. In the schematic text, add: .model DIDEAL D(Is=1e3 N=1 Rs=1e-6 Cjo=1e-12 M=0.5)

The thing about large Is and really small Rs is that they make the forward turn-on happen at a very small voltage. This is pretty close, to a step behavior. You can adjust the Is and Rs to see what happens make sure to keep the values the same each time you try something.

Set the diode attribute “Value” to DIDEAL.

Add DC sweep directive: .dc V1 0 5 1m

Run simulation. Plot I(D1) and V(NOUT) vs V1.

LTspice: real-diode schematic (1N4148)

To start make a copy of the circuit we already have. Then we need to change the diode. The diode "Value" should be set to 1N4148. This is a choice because LTspice has a model, for the 1N4148 diode.

Use same .dc V1 0 5 1m directive.

Run simulation. Plot I(D1) and V(NOUT) vs V1.

What to capture (screenshots to include)

Schematic files: ideal.asc and real_1N4148.asc

Simulation plot: I(D1) vs V1 (0–5 V) for ideal case (screenshot).

Simulation plot: I(D1) vs V1 (0–5 V) for 1N4148 (screenshot).

Optionally: V(NOUT) vs V1 for both cases.

Notes on plotting

When you are looking at the plot window you can click on the diode trace.. You can use the expression I(D1) to do the same thing with the diode current.

To make it easier to compare we should put both traces on the plot. We can do this by running one simulation then running the one and adding the traces to the first one. Alternatively we can use the.step parameter if we like to run simulations with parameters. This way we can look at both traces on the plot and see the differences between the two simulations the traces from the first simulation and the traces, from the second simulation.

Short README (200–300 words)

(Use this verbatim in README.md — currently ~220 words)

Comparison of Ideal vs. Practical Diode (1N4148)

This repository looks at how a diode model and a real 1N4148 diode work when you change the voltage in LTspice.

The circuits are pretty simple: you have a voltage source, the diode, then a resistor that is one thousand ohms and finally ground.

The voltage source is changed from zero volts, to five volts to see what happens to the diode.

Difference in turn-on voltage

The ideal model is set up with a big saturation current and almost no series resistance. So it acts like a switch: it turns on at a low voltage and starts conducting a lot even when the voltage is very small.

The 1N4148 is different. It has an exponential current and voltage relationship: it starts conducting a lot, around 0.6 to 0.8 volts depending on the current. This happens because it gradually moves from leaking a little to conducting.

Difference in current behavior

The perfect model makes a sharp change and gives a lot more forward current when you apply the same voltage. This is because Is is really big and Rs is really small. The 1N4148 diode works according to a rule that says the current is equal to Is times a big exponential thing (I = Is times the exponential of V divided by some constants). So when you increase the voltage the current goes up really fast over a big range. At first when the voltage is low the current is really tiny a few nano or microamps. Then as the voltage gets closer to, around 0.6 to 0.8 volts the current starts to get bigger going from microamps to milliamps.. When the current gets really high you start to see the effects of the series resistance.

The thing is, ideal models are still used because they are simple and easy to understand. Ideal models are still used in fields.

They help us get an idea of how something works.

Ideal models are still used to make things easier to learn.

For example ideal models are still used in schools to teach people about things.

Ideal models are still used to help people understand things better.

* They are simple

* They are easy to use

Ideal models are still used because they are good, for making decisions.

We still use models because they are easy to work with.

Ideal models are still used every day.

Diodes that are idealized make it easier to understand things. They help us get an idea of what is going on right away. Idealized diodes also make it easier to figure out how a circuit is going to behave when it is first turned on. We can use diodes when we do not need to know everything exactly like when we are teaching or looking at big parts of a circuit. This makes it faster to simulate. It is not as complicated. For example idealized diodes are good, for switching thresholds or when we are making block-level models and we do not need a lot of detail.

When the ideal models we have become inaccurate it is a problem. The ideal models are supposed to be correct and help us understand things.. What happens when the ideal models become inaccurate? This is something that can cause a lot of trouble. The ideal models are used to make predictions and decisions so if they are not correct then the predictions and decisions will not be correct either. We have to be careful when we use the models and make sure they are accurate. If the ideal models become inaccurate we have to find out why and fix the problem. The ideal models are important. We need them to be accurate.

Ideal models fail when precise voltage drop, leakage, temperature dependence, reverse recovery, dynamic capacitances, or series resistance matter—e.g., analog precision circuits, RF switching, fast switching where reverse recovery matters, power diodes carrying high currents, or thermal analyses. In those situations, use manufacturer SPICE models or tuned diode parameters.
