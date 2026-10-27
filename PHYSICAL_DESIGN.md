# PicoRV32 Physical Design — RTL-to-GDSII

## Project Overview

This project implements the open-source PicoRV32 RISC-V processor using the LibreLane RTL-to-GDSII flow with the SkyWater SKY130A process design kit.

The objective was to take the RTL through synthesis, floorplanning, placement, clock-tree synthesis (CTS), routing, timing analysis, and physical verification.

**Repository:** [PicoRV32 Physical Design](https://github.com/Akhilesh-Hemannavar/picorv32-physical-design)

## Technology and Tools

| Item | Details |
|---|---|
| Design | PicoRV32 RISC-V CPU |
| Flow | LibreLane |
| PDK | SkyWater SKY130A |
| Standard-cell library | `sky130_fd_sc_hd` |
| Synthesis | Yosys |
| Place and route | OpenROAD |
| Static timing analysis | OpenSTA |
| DRC | Magic and KLayout |
| LVS | Netgen |
| Clock period constraint | 20 ns (50 MHz target) |

## Design Configuration

| Parameter | Result |
|---|---:|
| Die dimensions | 432.025 × 442.745 µm |
| Die area | 191,277 µm² |
| Core area | 176,307 µm² |
| Standard-cell count | 12,423 |
| Sequential-cell count | 1,597 |
| Core utilization | 69.3% |
| I/O pins | 409 |

## Timing Results

The final metrics report zero setup and hold violation counts across the reported timing corners.

| Metric | Result |
|---|---:|
| Clock period constraint | 20 ns |
| Worst setup slack (WNS) | +0.741 ns |
| Worst hold slack (WNS) | +0.109 ns |
| Setup TNS | 0 ns |
| Hold TNS | 0 ns |
| Maximum slew violations | 0 |
| Maximum capacitance violations | 0 |
| Maximum fanout violations | 0 |

The worst reported setup slack is +0.741 ns at `max_ss_100C_1v60`. The worst reported hold slack is approximately +0.109 ns at `min_ff_n40C_1v95`.

## Physical Implementation Results

| Metric | Result |
|---|---:|
| Clock buffers | 312 |
| Clock inverters | 16 |
| Timing-repair buffers | 2,828 |
| Total power at nominal TT corner | 12.24 mW |
| Antenna violations | 0 |
| Power-grid violations | 0 |
| Final routing DRC errors | 0 |
| Magic DRC errors | 0 |
| KLayout DRC errors | 0 |
| LVS errors | 0 |
| XOR differences | 0 |

The routing process reduced the reported DRC count from 132 in iteration 0 to zero in the final routing result.

LVS verification reported that the extracted and reference circuits match uniquely.

**Power note:** The reported 12.24 mW is the nominal `tt_025C_1v80` corner result.

## RTL-to-GDSII Flow

The implementation follows this sequence:

1. RTL synthesis using Yosys.
2. Floorplanning and I/O placement.
3. Global placement and timing-driven optimization.
4. Clock-tree synthesis.
5. Timing repair and detailed placement.
6. Global and detailed routing.
7. Antenna repair and physical verification.
8. Static timing analysis, DRC, and LVS.

## Engineering Work and Learnings

This project provided hands-on experience with:

- Configuring a LibreLane RTL-to-GDSII flow for SKY130A.
- Evaluating placement utilization and physical-design metrics.
- Inspecting clock buffers, fanout, and capacitance constraints.
- Understanding timing-repair buffering and clock-tree implementation.
- Tracking routing DRC violations through successive routing iterations.
- Verifying the final layout using Magic, KLayout, and Netgen.
- Reviewing setup and hold slack across multiple timing corners.

## Reproducibility

The repository contains the RTL source, project files, and LibreLane configuration.

To reproduce the flow, install and configure LibreLane and the SKY130A PDK, then run:

```bash
librelane config.json
```

Exact reproduction also depends on the tool versions, PDK revision, environment, and configuration used for the reported run.

## Verification Note

The metrics report zero DRC and LVS errors, but also report 79 disconnected pins, with zero classified as critical. This metric should be investigated before making an unconditional claim of complete signoff cleanliness.

## Future Work

- Evaluate tighter clock-period constraints.
- Compare utilization and placement-density settings.
- Investigate routing and buffering trade-offs.
- Explore multi-cut vias and their impact on physical implementation.
- Document the impact of optimization changes using comparable timing and area reports.

## Licensing

PicoRV32 RTL is distributed under its original license. Refer to `COPYING` and the upstream [PicoRV32 repository](https://github.com/YosysHQ/picorv32) for licensing terms. Preserve the original license notices when redistributing the source.
