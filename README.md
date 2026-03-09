# Hiveton H5000M DDR4 4GB 3200Mbps Modification Guide

This repository provides a comprehensive guide to upgrading the RAM of the **Hiveton H5000M (MT7987A)** from the stock 1GB to **4GB DDR4 3200Mbps**. This mod achieves stable operation at the default frequency without the need for downclocking.

## Environment & Hardware Specifications
* **Device Model:** Hiveton H5000M
* **SoC:** MediaTek MT7987A (Filogic 830)
* **RAM Chip:** SK Hynix **H5ANBG6NAMR-XNC** (DDR4 16Gb, x16 DDP High-Density Package)
* **Final Frequency:** **3200Mbps** (Stable at default clock)
* **Bootloader Source:** [hanwckf/bl-mt798x](https://github.com/hanwckf/bl-mt798x) (ATF/BL2)

---

## Core Solution

Successfully supporting 4GB RAM on the MT7987 at high frequencies requires a combination of **Hardware Strapping Adjustment** and **Software Configuration**.

### 1. Hardware Resistor Modification (Critical)
Based on the **MT7988 (BPI-R4)** 8GB upgrade reference, the MT7987 requires hardware resistor changes to correctly set the logic levels for the **E9 (BG1)** and **M9 (UZQ)** pins. These pins are essential for bank grouping and impedance calibration in high-density chips.

#### Detailed Steps:

**A. Top Side Modification:**
Locate the cluster of resistors next to the DDR4 chip as shown in the image below. There are five resistors aligned in a row. 
* **Action:** Identify the **second resistor from the right**. Replace the original 0-ohm resistor with a **240-ohm** resistor.



**B. Bottom Side Modification:**
Flip the PCB to the back, directly behind the DDR4 chip.
* **Action:** **Remove** the resistor circled in the reference image.

#### PCB Revision Warning:
* **V2 PCB:** The layout is compatible with larger 4GB chip footprints.
* **V1 PCB:** The resistor placement physically obstructs the larger 4GB chip, preventing it from sitting flush on the pads. Verify your PCB version before desoldering.



---

### 2. Software Configuration (ATF/BL2)

In the `bl-mt798x` source code, follow these steps:

1. Run `make menuconfig`.
2. Navigate to the memory settings.
3. Enable: `Support DDR4 4GB (16-bits)`.
4. Compile and flash the **BL2** image.

---
