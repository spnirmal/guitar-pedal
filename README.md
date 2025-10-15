# 🎸 Analog Guitar Distortion Pedal

An analog **guitar distortion pedal** designed and simulated using LTSpice and Falstad.
This project demonstrates audio signal conditioning, op-amp gain stages, and diode-based hard clipping for creating a warm, saturated distortion effect.
the falstad text file can be directly imported to the website and bring the distortion to life.

---

## ⚙️ Overview

This project focuses on building a complete **analog signal chain** for a guitar pedal, including:

* Input biasing and protection
* Op-amp voltage follower (buffer stage)
* Non-inverting amplifier with hard clipping using LEDs
* Single-supply biasing for 9V operation
* Output stage compatible with speakers or amplifier input

The design was verified in **LTSpice** and **Falstad** simulators before hardware prototyping on a breadboard.

---

## 🔧 Circuit Stages

### 1. Input Stage

Handles signal coupling, protection, and biasing:

* 3.5 mm or ¼″ guitar input jack
* 1 kΩ series resistor for current limiting
* TVS or Zener diode pair for ESD and surge protection
* 47 nF coupling capacitor to block DC offset
* 1 MΩ resistor for biasing via a 4.5 V virtual ground (voltage divider from 9 V supply)
in the falstad simulation we have given the audio inout as a file. the 1K ohm resistor is a current limiting resistor which is connected to a tvs diode to ground this suppresses the transient voltage.
the input audio signal could have DC offset wlthough in most cases this is not the situation it is better to have that in consideration. the capacitor has a basic porperty of letting AC signal pass while not allowing DC current to pass through
this property of capacitor is used to remove the DC offset in the audio. we connect the capacitor to a 1M ohm resistor for biasing via a 4.5V derived from the voltage divider from teh supply this voltage is suitable for 
feeding it to a ADC pin of an MCU. if it operates at 3.3V the resistor values in the voltage divider can be changed accordingly.

### 2. Buffer Stage

An **op-amp voltage follower** isolates the high-impedance guitar input from the next stage.

* Configured as unity gain (non-inverting input fed, output tied to inverting input)
* Prevents signal loading
* Provides clean signal reference to bias point
the output from the opamp ideally has zero loss. this is fed to the ADC pin although that is not the case in the falstad simualtion. the EQ section or the distortion effect can be made in the firmware itself without having
to use an opamp gain stage with diodes.

### 3. Distortion Stage

Implements **hard clipping** using an op-amp gain stage with diodes:

* Non-inverting amplifier with gain:
  [ Gain = 1 + \frac{R_f}{R_g} ]
  Typical values: Rf = 50 kΩ, Rg = 1 kΩ
* Two red LEDs connected anti-parallel between output and inverting terminal for clipping
* Produces characteristic square-like distorted waveform
diodes are used for the clipping part of the circuit but the reason i chose LEDs is to bring an visual appeal to the circuit. using LEDs to do teh ahrdclipping of the audio input seems not only functional but also decorative.
seeing your audio processed by a functional part of the circuit iin visuals seemed like a cool idea.

### 4. Output Stage

* Optionally includes RC low-pass filter for smoothing
* Output can drive an amplifier or powered speaker

---

## 🔋 Power Supply

* Single 9 V supply (battery or DC adapter)
* Voltage divider generates 4.5 V virtual ground for biasing

---

## 🖊️ Design & Simulation Tools

* **LTSpice** – for detailed circuit simulation and waveform analysis
* **Falstad Circuit Simulator** – for quick prototyping and visual understanding
* **KiCad** – for schematic capture and PCB design (optional hardware layout)

---

## 🔌 Bill of Materials (BOM)

| Component  | Value / Type            | Quantity |
| ---------- | ----------------------- | -------- |
| Op-Amp     | TL072 / LM358           | 2        |
| Resistors  | 1 kΩ, 50 kΩ, 1 MΩ, etc. | Various  |
| Capacitors | 47 nF, 100 nF           | 2        |
| Diodes     | Red LEDs (clipping)     | 2        |
| TVS/Zener  | 5.1 V (optional)        | 1        |
| Input Jack | 3.5 mm TRS / 6.35 mm    | 1        |
| Power      | 9 V Battery / DC supply | 1        |

---

## 🔬 But how is this anywhere related to an actual guitar pedal
 an actual guiatr pedal must work in real time opposed to our falstad simulation which takes input as an audio file. the real porduct is not very far from this project.
 when a guitar pickup signal is connected to an aux or a 3.5mm jack this is the actual processing going on within the pedal. after teh impedance matching we could feed the audio signal to the ADC of an 
 efficient MCU and process teh signal in firmware. allowing us to discard any extra hardware that might be needed to produce the Effects. through firmware we could actually to mixing of effects and switch between presets
 all through the firmware which is going to be the next step from this project.


---

## 👨‍💻 Author

**Nirmal S P**
[GitHub: spnirmal](https://github.com/spnirmal)

---

## 🔖 License

This project is released under the **MIT License**.
