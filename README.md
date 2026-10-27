# PicoRV32 Physical Design — RTL to GDSII

Physical implementation of the open-source **PicoRV32 RISC-V processor** using LibreLane and the SkyWater SKY130A process design kit (PDK).

This project covers the ASIC backend flow from RTL synthesis through floorplanning, placement, clock-tree synthesis (CTS), routing, static timing analysis (STA), and physical verification.

## Key Results

| Metric | Final Result |
|---|---:|
| Target clock period | 20 ns (50 MHz) |
| Core area | 176,307 µm² |
| Die area | 191,277 µm² |
| Standard-cell count | 12,423 |
| Sequential-cell count | 1,597 |
| Core utilization | 69.3% |
| Worst setup slack (WNS) | +0.741 ns |
| Worst hold slack (WNS) | +0.109 ns |
| Nominal power (TT corner) | 12.24 mW |
| Final routing DRC errors | 0 |
| Magic DRC errors | 0 |
| KLayout DRC errors | 0 |
| LVS errors | 0 |

**Timing:** The reported timing results show positive worst setup and hold slack, with zero setup and hold violations across the reported timing corners.

**Physical verification:** The final reports show zero routing DRC, Magic DRC, KLayout DRC, and LVS errors.

> Power is the reported nominal result at the `tt_025C_1v80` corner. Results depend on the implementation configuration, PDK revision, and tool environment.

## Technology Stack

| Stage | Tool / Technology |
|---|---|
| RTL design | PicoRV32 RISC-V CPU |
| RTL-to-GDSII flow | LibreLane |
| Process design kit | SkyWater SKY130A |
| Logic synthesis | Yosys |
| Placement and routing | OpenROAD |
| Static timing analysis | OpenSTA |
| Design-rule checking | Magic and KLayout |
| Layout-versus-schematic | Netgen |

## Physical Design Flow

The design follows this implementation sequence:

1. RTL setup and LibreLane configuration
2. Logic synthesis using Yosys
3. Floorplanning and I/O placement
4. Global placement and timing-driven optimization
5. Clock-tree synthesis (CTS)
6. Detailed placement and timing repair
7. Global and detailed routing
8. Antenna repair and routing cleanup
9. DRC and LVS verification
10. Final timing and physical-design checks

## Engineering Work

The project involved hands-on analysis of the physical implementation, including:

- Configuring an RTL-to-GDSII flow for SKY130A.
- Evaluating floorplan area, placement utilization, and standard-cell statistics.
- Inspecting clock buffers, fanout, and capacitance constraints.
- Investigating clock-tree implementation and timing-repair buffering.
- Tracking routing DRC violations across routing iterations.
- Reviewing setup and hold slack across multiple timing corners.
- Checking the final layout with Magic, KLayout, and Netgen.

The routing report records a reduction from 132 DRC errors in iteration 0 to zero in the final routing result.

## Repository Structure

```text
.
├── README.md
├── PHYSICAL_DESIGN.md
├── config.json
├── picorv32.v
├── picorv32.core
├── sky130A.lyp
├── results/
│   └── final/
│       └── reports/
│           └── final_metrics.md
├── scripts/
├── src/
├── tests/
├── firmware/
├── dhrystone/
├── picosoc/
├── Makefile
└── COPYING
```

- `config.json` — LibreLane configuration.
- `PHYSICAL_DESIGN.md` — detailed physical-design report.
- `results/final/reports/final_metrics.md` — summarized final implementation metrics.
- `scripts/` — supporting scripts and utilities.
- `tests/` — PicoRV32 test programs and test-related files.
- `COPYING` — upstream PicoRV32 license notice.

## Reproducing the Flow

Install and configure LibreLane and the SKY130A PDK first.

From the repository root, run:

```bash
librelane config.json
```

Reproduction depends on the installed tool versions, PDK revision, configuration, and environment. The reported results describe the documented implementation run; they are not a guarantee that every environment will produce identical metrics.

## Future Work

Potential next steps include:

- Comparing placement density and utilization settings.
- Evaluating tighter clock-period constraints.
- Studying clock-tree and buffering trade-offs.
- Comparing implementation changes using consistent timing, area, and power reports.
- Extending the work toward low-power physical design techniques.

## License and Attribution

This project uses the open-source PicoRV32 RTL from [YosysHQ/PicoRV32](https://github.com/YosysHQ/picorv32). Refer to `COPYING` and the upstream repository for the original licensing terms. Preserve applicable source notices when redistributing the RTL.

## Detailed Report

See [`PHYSICAL_DESIGN.md`](PHYSICAL_DESIGN.md) for the detailed implementation report, timing results, physical-design metrics, and engineering notes.
