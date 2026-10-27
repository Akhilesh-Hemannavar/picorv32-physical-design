# PicoRV32 Physical Design using LibreLane and Sky130

This project implements the physical design flow for the PicoRV32 RISC-V processor using LibreLane and the SkyWater SKY130A process design kit. The goal is to take the RTL through the full ASIC backend flow: synthesis, floorplanning, placement, clock-tree synthesis, routing, timing analysis, and physical verification.

## Project objective

The objective of this project was to:
- configure a real RTL-to-GDSII flow for PicoRV32 in SKY130A
- implement the design in LibreLane
- evaluate area, timing, and design-rule compliance
- validate the final implementation using DRC and LVS checks
- build a clean, reproducible physical-design project suitable for a portfolio

## Why this project matters

This project demonstrates practical ASIC backend experience using industry-relevant tools and a real open-source PDK flow. It focuses on the physical implementation stage of digital design — the phase that turns synthesized logic into a manufacturable layout.

## Tools and technology

- RTL: PicoRV32 (RISC-V RV32IMC-compatible CPU core)
- Flow: LibreLane
- PDK: SkyWater SKY130A
- Synthesis: Yosys
- Place and route: OpenROAD
- Timing analysis: OpenSTA
- Physical verification: Magic, KLayout, Netgen

## Repository structure

```text
.
├── README.md                  # project overview and summary
├── PHYSICAL_DESIGN.md         # detailed physical design report
├── LICENSE                    # project license
├── Makefile                  # build and execution entry points
├── config.json               # LibreLane configuration
├── picorv32.v                # PicoRV32 RTL source
├── picorv32.core             # project metadata for OpenLane/LibreLane
├── sky130A.lyp               # layer properties for SKY130A
├── testbench.v               # standard RTL testbench
├── testbench_ez.v            # simplified testbench
├── testbench_wb.v            # Wishbone variant testbench
├── showtrace.py              # trace decoder utilities
├── COPYING                   # upstream PicoRV32 license notice
├── firmware/                 # firmware and test executables
├── dhrystone/                # Dhrystone benchmark support
├── picosoc/                  # example SoC integration
├── scripts/                  # helper scripts and utilities
├── tests/                    # software and instruction tests
└── .github/                  # CI and repository automation
```

## Physical design flow followed

1. RTL setup and project configuration
2. Logic synthesis with Yosys
3. Floorplanning and I/O placement
4. Global placement and optimization
5. Clock-tree synthesis (CTS)
6. Detailed placement and timing repair
7. Global and detailed routing
8. Antenna repair and routing cleanup
9. DRC and LVS verification
10. Final timing and physical-signoff checks

## Key results

The reported implementation metrics are as follows:

| Metric | Result |
|---|---:|
| Target clock period | 20 ns |
| Core area | 176,307 µm² |
| Die area | 191,277 µm² |
| Standard-cell count | 12,423 |
| Sequential-cell count | 1,597 |
| Core utilization | 69.3% |
| Worst setup slack | +0.741 ns |
| Worst hold slack | +0.109 ns |
| Final DRC errors | 0 |
| Final LVS errors | 0 |
| Total nominal power | 12.24 mW |

These numbers indicate a physically valid implementation with acceptable timing margins and no reported DRC/LVS violations in the final flow.

## Verification notes

The physical design report notes:
- zero final DRC and LVS errors
- zero setup and hold violations in the reported timing corners
- no critical antenna or routing violations in the final pass

There was also a mention of disconnected pins in the physical verification summary, which is a good candidate for future investigation and optimization.

## Why this is good for a portfolio

This project is valuable for a hardware or VLSI portfolio because it shows real backend ASIC workflow experience, including:
- working with a real PDK and physical implementation tools
- understanding timing, placement, and routing issues
- interpreting DRC/LVS results
- translating RTL into a manufacturable layout
- documenting engineering work and design metrics

## Reproduction

To reproduce the flow, ensure LibreLane and the SkyWater SKY130A PDK are installed and configured, then run:

```bash
librelane config.json
```

The exact results will depend on the tool versions, PDK revision, and local environment used for the implementation run.

## Learning outcome

This project strengthened understanding of:
- ASIC physical design flow setup
- floorplanning and placement behavior
- timing closure and slack analysis
- DRC and LVS validation
- open-source VLSI tooling in a full backend flow

## License

PicoRV32 is distributed under its original upstream licensing terms. Please refer to `COPYING` for the original source notice and licensing details.

## Acknowledgements

This project builds on the PicoRV32 RTL from the upstream YosysHQ PicoRV32 repository and applies it to a physical design flow using LibreLane and SKY130A.

## Project summary

This repository represents a complete RTL-to-GDS physical design exercise for PicoRV32 using open-source ASIC tooling and a real process-design kit. It is suitable as a strong example of practical VLSI and backend design work for a technical portfolio or job search.
