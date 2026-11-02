# Wireless Expansion & Processing Module (TIE2023 Contest Subject)

## General Description

This hardware project is a high-performance **wireless communication expansion module**
designed as a plug-in card with a 75-pin card-edge interface (compatible with M.2/PCI standards). 

Built around an advanced wireless SoC (referred to in the schematic as **TIE2023**), the module is engineered for 
compact applications requiring wireless connectivity, high-speed data storage, and efficient power management.

---

## Architecture & Functional Blocks

The board integrates several major functional sections:

1. **Central Processing & Wireless Unit (SoC - TIE2023):**
   * Dedicated chip for embedded applications and wireless protocols.
   * Integrated high-speed peripherals, including USB lines (`USB_D+`, `USB_D-`) and PCI differential pairs (`PERP0`/`PERN0`, `PETP0`/`PETN0`).
   * External antenna support through two dedicated RF ports with U.FL connectors (`J1`, `J2`) and optimized impedance matching networks.

2. **Non-Volatile Storage (QSPI Flash):**
   * Features the **MX25R6435F** (64Mb Serial Multi-I/O Flash) memory connected via a high-speed QSPI bus for firmware storage, file systems, or configuration data.

3. **Power Management System:**
   * **DC-DC Regulator:** Based on the Texas Instruments **TPS562810-Q1** step-down regulator, generating a stable internal supply voltage (`VDD`) from the main input rail (`VIN`).

4. **Interface (Card-Edge / Bus - J3):**
   * A 75-pin card-edge connection providing power rails, high-speed data buses (USB/PCIe), and control/status signals (`W_DISABLE1`, `W_DISABLE2`, alert lines)

---

## PCB Layout & Design Guidelines
The printed circuit board (PCB) was routed following various good practices such as:

* **4-Layer Stackup Strategy:**
  * **Layer 1 (Top):** Primary component placement, critical RF traces leading to U.FL connectors, and high-speed signals.
  * **Layer 2 (Inner 1 - Ground Plane):** A solid, continuous internal ground plane (`GND`) ensuring a low-impedance return path for high-speed signals and effective electromagnetic shielding (EMI).
  * **Layer 3 (Inner 2 - Power Plane):** Split power planes dedicated to distributing various supply voltages cleanly across the board.
  * **Layer 4 (Bottom):** Secondary routing layer.
* **High-Speed Routing:** Differential pairs (such as USB and PCIe lines) were routed with controlled impedance and matched lengths to preserve signal integrity (Within the limits of the footprints and pads dimensions).
* **Component Placement & Decoupling:** 
  * All decoupling capacitors were placed as close as possible to the power pins of their respective ICs to minimize parasitic inductance and noise (Especially on the bottom right of the board where the converter sits).
  * Quartz crystal oscillators (`Y1`, `Y2`) were positioned directly adjacent to their target chips to ensure clean clock generation.
* **Test Points:** Dedicated test points (`TP1`, `TP3`, `TP4`, `TP5`) were strategically placed on the board to facilitate hardware debugging, signal probing, and manufacturing verification.

---

## Technical Specifications

* **Power Input:** `VIN` converted internally to `VDD` via the `TPS562810-Q1` buck regulator.
* **Storage:** 64Mb Serial Flash (`MX25R6435F`).
* **Connectivity & Interfaces:** 
  * High-speed USB and PCIe links.
  * Dual U.FL RF ports for external antennas.
  * Integrated NFC capability.
* **Status Indication:** 3 status LEDs (`LED1`, `LED2`, `LED3`).
