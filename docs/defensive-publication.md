# Alarm Trigger RC Delay Low-Leakage Circuit for Unlocked Positioning Alarm Lock (UPAL)

**Author:** Sanathanan Uruthireswaran  
**Date of Public Disclosure:** *(set by GitHub timestamp when pushed; include tag `v1.0-prior-art`)*  
**License:** CC0-1.0 (Creative Commons Zero)


## Abstract
A two-stage alarm architecture for  **Unlocked Positioning Alarm Lock (UPAL)**: a **low-current RC trigger** creating a **user-friendly delay** after the **stand** and **key** sensors are both activated, which then **drives a high-current alarm** through a transistor switch. This topology prevents high alarm currents from flowing through mechanical sensors, reducing wear/leakage while preserving full loudness of an active piezo buzzer.

## Technical Field
Alarm and control electronics for **Unlocked Positioning Alarm Lock (UPAL) device**.

## Background
A direct series chain of (Stand sensor ∧ Key sensor) → Buzzer drives alarm current through the mechanical switches. This:
- Increases switch wear and voltage drop,
- Complicates addition of **time delay** before sounding,
- Risks **leakage** paths and reduced buzzer loudness if track resistance is increased.

## Summary
This disclosure separates **Trigger** from **Drive**:
1. **Trigger Circuit (low current):** The two sensors in series feed an **RC network** that charges only when both switches are closed, producing a delayed rising voltage.
2. **Drive Circuit (high current):** An **NPN transistor** acts as a low-side switch, supplying full current to an **active piezo buzzer** once the trigger voltage exceeds the base-emitter threshold.

This separation enables a **configurable delay** and **prevents alarm current through sensors**.

## Detailed Description

### 1. Example Implementation (3 V coin cell)
- **Supply:** CR2032 (nominal 3.0 V).
- **Sensors:** Stand sensor (NO), Key sensor (NO), wired in series.
- **RC Delay:** R_1 and C_1 arranged to charge C_1 only when both sensors are closed. The node **V_TRIG** rises as C_1 charges.
- **Switching Device:** NPN transistor (e.g., BC547 / 2N3904). Emitter at GND; collector to buzzer negative; base fed from V_TRIG via base resistor R_2 (and optional base-emitter bleed R_3).
- **Alarm Load:** Active piezo buzzer rated for 3 V connected from +V to transistor collector.
- **Optional:** A diode across C_1 for asymmetric charge/discharge if a different arm/disarm dynamic is desired.

**Operation:** When both sensors close, C_1 charges toward +V through R_1. When V_TRIG ≳ V_BE(on) (≈ 0.6–0.7 V), the transistor turns on and the buzzer sounds. Opening either sensor discharges C_1 (via R paths and/or V_BE conduction), turning the buzzer off after a short fall time.

### 2. Timing Considerations
For a simple RC charge toward V_s, the approximate delay to reach V_BE(on) is
\[ t_d \approx - R_1 C_1 \ln\left(1 - \frac{V_{BE(on)}}{V_s}\right) \]
For **V_s = 3.0 V** and **V_BE(on) ≈ 0.65 V**, \( t_d ≈ 0.244 R_1 C_1 \).  
Examples: 
- R_1 = 100 kΩ, C_1 = 100 µF → t_d ≈ 2.4 s  
- R_1 = 220 kΩ, C_1 = 100 µF → t_d ≈ 5.4 s

### 3. Example Component Values (reference only)
- R_1 = 100–330 kΩ (delay set)
- C_1 = 47–220 µF (electrolytic, low leakage)
- R_2 = 10–47 kΩ (limit base current)
- R_3 = 100–470 kΩ (bleed/base stabilizer, optional)
- Q1 = BC547 / 2N3904 (NPN general purpose)
- Buzzer: Active piezo, 3 V rated
- Diode (optional): 1N4148 across C_1 for asymmetric timing

> **Note:** Choose R_1 and C_1 to suit desired delay; verify with your specific parts’ leakage and V_BE characteristics.

### 4. Schematic
See `schematics/upal_rc_trigger_switch.png`. 

### 5. Variations (All Included in Disclosure)
- PNP high-side switch or a P-channel MOSFET high-side arrangement.
- Logic inversion so that **opening** a sensor initiates delay.
- Use of a MOSFET (e.g., 2N7002) for lower base/gate current and higher efficiency.
- Adding a **Schmitt trigger** buffer for sharper thresholding.
- Use of separate supply for buzzer vs. trigger to improve stability.
- Using a controlled discharge path to set **off-delay** independently of **on-delay**.

### 6. Statement of Public Disclosure
This document and associated files are **publicly disclosed** to place the described circuit topology and its use in UPAL-type devices into the **public domain as prior art**. The intent is to **prevent** others from obtaining patent rights on this approach or trivial variations thereof.

### 7. How to Cite
Sanathanan, U. (2025) *Alarm Trigger RC Delay Low-Leakage Circuit for Unlocked Positioning Alarm Lock (UPAL)* (Defensive Publication). Git commit/tag: `v1.0-prior-art`.


*End of defensive publication.*
