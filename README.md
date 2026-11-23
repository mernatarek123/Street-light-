# Street-light-
# Smart Automatic Street Light with Adjustable Sensitivity

An analog light-controlled automatic street light circuit built around a **BC547 (NPN) BJT** acting as a saturated switch, paired with an **LDR**, **potentiometer**, **Zener diode voltage reference**, and **delay capacitor**.

---

## Circuit Schematic

```text
                       +VCC (e.g., 9V - 12V DC)
                         │
          ┌──────────────┼──────────────┬──────────────┐
          │              │              │              │
         [R1]           [R2]           [R3]           [R4]
        (1kΩ)         (10kΩ)          (330Ω)         (330Ω)
          │              │              │              │
          │         ┌────┴────┐        ─┴─            ─┴─
          │         │  [POT]  │        ╲ ╱ LED1       ╲ ╱ LED2
          │         │ (50kΩ)  │        ─┬─            ─┬─
          │         └────┬────┘         │              │
          ├──────┬───────┴──────────────┼──────────────┘
          │      │                      │
         ─┴─     │                     │/  C
         /▲\ ZD  ├───[R_base 1kΩ]─────┤   BC547 (NPN)
         ─┬─     │                     │\  E
          │      │                      ▼
          │     [LDR]                  [C1] (10µF–100µF)
          │      │                      │
         ─┴─    ─┴─                    ─┴─
         GND    GND                    GND
```

*(Note: Connect the delay capacitor `C1` between the **BC547 Base** and **GND**, and connect the **BC547 Emitter (E)** directly to **GND**.)*

---

## System Block Diagram

```mermaid
flowchart LR
    VCC(["+VCC Supply"]) --> Zener["Zener Diode Reference<br/>(Prevents Voltage Drift)"]
    Zener --> Divider["Potentiometer + LDR<br/>(Voltage Divider)"]
    Divider --> Delay["RC Delay Capacitor<br/>(Prevents False Triggers)"]
    Delay -->|"V_base > 0.7V"| BJT["BC547 NPN Transistor<br/>(Saturated Switch)"]
    BJT --> LEDs["Multiple LED Outputs<br/>(Street Lights ON)"]
```

---

## Components List

| Component | Role in Circuit | Suggested Value |
| :--- | :--- | :--- |
| **BC547 (NPN)** | Main light-controlled switch (cut-off & saturation) | 1x BC547 |
| **LDR** | Senses ambient light (resistance rises in darkness) | 5mm Photoresistor |
| **Potentiometer** | Adjusts the darkness trigger threshold | 10kΩ – 50kΩ |
| **Zener Diode** | Holds a stable reference voltage across the divider | 5.1V Zener (e.g., 1N4733A) |
| **Capacitor** | Creates an adjustable turn-on delay | 10µF – 100µF Electrolytic |
| **LEDs** | Street light output indicators | 2–4x White/Yellow LEDs |
| **Resistors** | Current limiting for Zener, base, and LEDs | 1kΩ, 10kΩ, 220Ω–330Ω |

---

## How It Works

1. **Voltage Reference:** The Zener diode clamps the voltage feeding the sensing divider so the switching threshold stays consistent even as the battery or power supply fluctuates.
2. **Light Sensing & Sensitivity:** The **LDR** and **potentiometer** form a voltage divider connected to the base of the **BC547**. Adjusting the potentiometer sets the exact ambient light level required to trigger the circuit.
3. **Turn-On Delay:** When darkness falls, the LDR's resistance increases, raising the voltage at the divider node. The **capacitor** charges gradually through the divider resistance, creating a brief delay before the base reaches **~0.7 V** so passing shadows do not flicker the lights.
4. **Switching Action:** Once the base-emitter voltage exceeds **0.7 V**, the BC547 enters **saturation**, completing the path to ground and turning **ON** all connected LEDs.

---

## Key Features & Concepts Learned

* **Features:**
  * Automatic ON/OFF switching based on ambient light
  * Adjustable light sensitivity threshold
  * Adjustable turn-on delay against transient shadows
  * Multi-LED lighting output
* **Core Electronics Concepts:**
  * BJT cut-off and saturation regions
  * Base biasing with a resistive voltage divider
  * Zener diode voltage regulation / reference
