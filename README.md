# IC 741 Operational Amplifier Behavioral Model in Verilog

## Overview

This repository contains a behavioral Verilog/SystemVerilog model of the classic **IC 741 Operational Amplifier**. The model approximates the open-loop behavior of a 741 op-amp by applying a large voltage gain to the differential input voltage and limiting the output swing according to the supply rails.

The design is intended for educational purposes, simulation studies, and introductory analog behavioral modeling using hardware description languages.

---

## Features

* Differential input stage (`V+` and `V−`)
* High open-loop gain approximation
* Output saturation near supply rails
* Configurable gain and output headroom parameters
* Suitable for analog behavior demonstration in simulation environments

---

## Model Description

The output voltage is computed as:

Vout = Aol × (V+ − V−)

where:

* `Aol` = Open-loop gain
* `V+` = Non-inverting input
* `V−` = Inverting input

The output is then limited to:

* Maximum output: `VCC − Vdrop`
* Minimum output: `VEE + Vdrop`

This mimics the inability of a real 741 op-amp to swing completely to its supply rails.

---

## Parameters

| Parameter      | Description                       | Default Value |
| -------------- | --------------------------------- | ------------- |
| OPEN_LOOP_GAIN | Open-loop voltage gain            | 200000        |
| v_drop         | Output headroom from supply rails | 1.5 V         |

---

## Port Description

| Port    | Direction | Description                 |
| ------- | --------- | --------------------------- |
| v_plus  | Input     | Non-inverting input voltage |
| v_minus | Input     | Inverting input voltage     |
| v_cc    | Input     | Positive supply voltage     |
| v_ee    | Input     | Negative supply voltage     |
| v_out   | Output    | Amplifier output voltage    |

---

## Example

Supply voltages:

* VCC = +15 V
* VEE = −15 V

Inputs:

* V+ = 1.0001 V
* V− = 1.0000 V

Differential voltage:

Vdiff = 100 μV

Ideal output:

Vout = 200000 × 100 μV = 20 V

Since the output exceeds the positive swing limit:

Maximum output = 15 − 1.5 = 13.5 V

Final output:

Vout = 13.5 V

---

## Compilation and Simulation

Compile the design and testbench using Icarus Verilog:

```bash
iverilog -o ic_sim ic_741.v ic_741_tb.v
```

Run the simulation:

```bash
vvp ic_sim
```

If waveform generation is enabled in the testbench, open the generated VCD file using GTKWave:

```bash
gtkwave dump.vcd
```

## Applications

* Analog circuit simulation
* Comparator demonstrations
* Op-amp fundamentals
* Control systems education
* Behavioral HDL modeling
* Verification environments

---

## Limitations

This is a simplified behavioral model and does not include:

* Frequency response
* Slew rate limitations
* Input bias currents
* Input offset voltage
* Noise effects
* Common-mode limitations
* Output current limitations

---

## Future Improvements

* Finite bandwidth modeling
* Slew-rate limiting
* Input offset voltage
* Noise modeling
* Closed-loop examples
* Testbench library
* Comparator mode examples

---

## License

This project is released under the MIT License.

---

## Author

Developed as an educational Verilog/SystemVerilog implementation of the IC 741 operational amplifier.
