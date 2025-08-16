# Alarm Trigger RC Delay Low-Leakage Circuit for Unlocked Positioning Alarm Lock (UPAL) 

This repository is a **defensive publication** for an electronics topology used in the **Unlocked Positioning Alarm Lock (UPAL)** concept: 
a **low-current RC-trigger circuit** that introduces a **time delay** and **drives a high-current alarm** via a transistor switch, so the mechanical **key** and **stand** sensors do **not** carry the alarm current.

- **Author:** Sanathanan Uruthireswaran
- **Initial public disclosure date (repo creation/push):** *(set by GitHub when you push)*
- **Document:** [`docs/defensive-publication.md`](docs/defensive-publication.md)
- **Schematic:** [`schematics/upal_rc_trigger_switch.png`](schematics/upal_rc_trigger_switch.png)

## What this is
A public, timestamped disclosure to ensure the described circuit and its use in Unlocked Positioning Alarm Lock (UPAL) device is **prior art**. This makes it **unpatentable** by anyone else while keeping it usable by the author and the public.

## Context with UPAL Patent

The Unlocked Positioning Alarm Lock (UPAL) is my primary invention, where a simple series connection of the Key Sensor and Stand Sensor directly powers a buzzer to indicate unsafe bicycle conditions.

However, in practical use, the original circuit triggered the alarm immediately when both sensors were closed, leaving no time to safely park and lock the bicycle. This defensive publication documents an auxiliary improvement:

The trigger path is decoupled from the alarm path using a transistor.

An RC delay is introduced to provide the rider with a short interval (typically 1–3 seconds) before the alarm activates.

The sensors no longer carry the full buzzer current, improving reliability and reducing power loss.

This improvement is not a new invention in itself, but rather an incremental enhancement to the Unlocked Positioning Alarm Lock (UPAL) system. Publishing it here ensures that such a variation is part of the public domain and cannot be re-patented by others.



## Circuit Function

1. Both the **Key Sensor** and **Stand Sensor** must be closed for the trigger circuit to activate.
2. An **RC network** provides a delay (t ≈ R × C) before the transistor switches on.
3. The **transistor separates the low-current trigger circuit** from the **high-current alarm circuit**, reducing power loss through the sensors.
4. Once the transistor switches, the **buzzer/alarm** is powered directly from the battery for full loudness.


## Bill of Materials (BOM)

Battery : CR2032 (3V)  (Supply )                     
Key Sensor (In series with Stand Sensor)  
Stand Sensor (In series with  Key Sensor)
Resistor R1 :100k–330k ohm   (Sets delay with C1)
Capacitor C1 : 47uF - 220uF   (Sets delay with R1) 
Resistor R2	:10k - 47k ohm
Resistor R3	: 100k- 470k ohm
Diode D1	:1N4148
Transistor Q1 : BC547 / 2N3904 NPN (Acts as switch )
Buzzer BZ1: Active Piezo Buzzer (Alarm output)


## Schematic

[schematics/upal_rc_trigger_switch.png](https://github.com/epidsc/upal-defpub/blob/main/schematics/upal_rc_trigger_switch.png)



## License

This work is released under the **CC0-1.0 (Creative Commons Zero)** license to maximize visibility and protect against restrictive patents.


