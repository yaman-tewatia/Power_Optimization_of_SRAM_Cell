
## Introduction

This project focuses on the design and analysis of a 6T SRAM cell at 90nm and 45nm technology nodes using Cadence Virtuoso.

### Key Highlights

- Designed and simulated 6T SRAM schematic and layout in Cadence Virtuoso.
- Performed DRC/LVS checks, ensuring design-rule compliance and schematic–layout consistency.
- Verified read, write, and hold operations using transient simulations.
- Analyzed power scaling trends across technology nodes (90nm vs. 45nm).
- Implemented stacking technique for leakage reduction in hold mode.
**Tools & Technologies:** Cadence Virtuoso, GPDK-90, GPDK-45 (Generic Process Design Kit)

## 1. Schematic
### 6T SRAM Cell

The SRAM cell consists of six transistors:

- 4 transistors (2 NMOS + 2 PMOS): Form two cross-coupled inverters responsible for storing a single bit.

- 2 NMOS transistors: Act as access transistors controlled by the Word Line (WL).

#### Connections:

- Bit Lines (BL, BL_BAR): Used for read and write operations.

- Word Line (WL): Controls the access transistors, enabling or isolating the cell.

#### Operation Principle:

- When WL = High, access transistors connect storage nodes (Q and Q̅) to the bit lines.

- When WL = Low, the cell is isolated and retains data via cross-coupled inverters.

### Precharge Circuit

A precharge circuit was implemented using two PMOS transistors:

- Gates connected to BL_EN.

- Sources connected to VDD.

- Drains connected to BL and BL_BAR.

#### Operation:

- When BL_EN = Low, PMOS devices turn ON.

- Both BL and BL_BAR are precharged to VDD prior to a read operation.
### - View the [schematics](https://your-link-here.com) for this project.



## 2. Waveforms
### Write Operation

- Inputs applied at BL and BL_BAR.

- With WL = High, access NMOS transistors turn ON.

- The input value is written into the storage nodes:

    - Q stores BL, Q̅ stores BL_BAR.

**Verification:** Waveforms confirm that Q follows BL and Q̅ follows BL_BAR, validating the write operation.

### Read Operation

- Before read, both BL and BL_BAR are precharged to VDD using the precharge circuit.

- With WL = High, storage nodes connect to bit lines.

- Depending on stored data:

    - If Q = 0, BL shows a voltage drop.

    - If Q̅ = 0, BL_BAR shows a voltage drop.

**Verification:** Waveforms show voltage drop on BL/BL_BAR depending on stored value, validating the read process.

### - View the [waveforms](https://your-link-here.com) for this project.

## 3. Layout

The 6T SRAM layout was created in Cadence Virtuoso using the GPDK90.

All devices and interconnects were drawn following **absolute design rules**.
### Design Rules Followed (GPDK90)
| Parameter | Minimum Value |
|----------|----------|
| Metal width (M1)    | 0.12 um     |
| Metal–Metal spacing    | 0.12 um     |
| Poly width   | 0.06 um     |
| Poly–Poly spacing    | 0.12 um     |
| Contact/Via size   | 0.12 um X 0.12 um     |
| N-well to N-well spacing   | 0.12um     |

### Verification

- Design Rule Check (DRC): Passed, no violations found.

- Layout vs. Schematic (LVS): Verified, layout matches schematic.

### - View the [layout](https://your-link-here.com) for this project.

## 4. Results

The 6T SRAM cell was analyzed at both 90nm and 45nm nodes, focusing on Write Power, Read Power, and Hold Power.

### Power Definitions

- **Write Power:** Dynamic power consumed during data flip (access transistor activity).

- **Read Power:** Dynamic power during read (bit-line precharge/discharge).

- **Hold Power:** Static power consumed when data is retained; dominated by leakage in OFF transistors, especially at smaller nodes.

### Technology Scaling Impact (90nm → 45nm)

- Vdd reduced → lowers dynamic power (∝ Vdd²).

- Vth reduced → increases leakage (subthreshold + gate).

- Outcome: Dynamic power decreases, but hold power increases significantly.

### Power Consumption
| Parameter | 90 nm | 45 nm | % change |
|----------|----------|----------|----------|
| Write Power (µW)    | 129.97     | 61.39     | 52.4% Reduction     |
| Write Power (µW)    | 52.20     | 23.98     | 54.1% Reduction     |
| Write Power (nW)    | 18.79     | 1510     | Drastic Increase     |

### Leakage Optimization: Stacking Effect

**Stacking Technique:** Connecting multiple transistors in series reduces leakage in hold mode.

#### Mechanisms:

- Raised Source Potential: Reduces effective Vgs.
- Voltage Division: Lowers Vds across stacked devices.
- Self-Reverse Bias: Enhances leakage suppression.
- Exponential Suppression: More OFF devices → exponentially lower leakage.

### Hold Power with Stacking
| Technology | Without Stacking(nw) | With Sracking(nw) | % Reduction |
|----------|----------|----------|----------|
| 90 nm    | 18.79     | 11.55     | 38.5     |
| 45 nm   | 1510     | 626.77     | 58.5     |

### - View the [results](https://your-link-here.com) for this project.

### Conclusion

Stacking significantly reduces leakage power, especially at smaller nodes. At 45nm, hold power was reduced by 58.5%, demonstrating the effectiveness of this technique for low-power SRAM design.



