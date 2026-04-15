# PicoRV32-Physical-Design-Sky130
Level 1: RTL-to-GDSII flow of a 32-bit RISC-V Core using OpenLane and Sky130 PDK.

# Project Overview
This project demonstrates a complete Physical Design flow for the PicoRV32, a size-optimized RISC-V CPU. The goal was to achieve a clean "Tape-out ready" GDSII file while meeting specific timing constraints on the SkyWater 130nm Process Design Kit (PDK).

# Repository Structure
rtl/: Contains the Verilog source code (picorv32.v).

config.json: The OpenLane configuration file used for the final run.

timing_setup_report.txt: Post-extraction (RCX) Setup timing report.

timing_hold_report.txt: Post-extraction (RCX) Hold timing report.

picorv32.zip: The final GDSII layout file (zipped).

# Final Sign-off Metrics
The design was successfully closed after 3 iterations with the following results:

Target Clock Period: 15ns

Setup Slack: 10.28ns (MET)

Hold Slack: 0.82ns (MET)

Technology: Sky130nm

Flow Tool: OpenLane

# Design Optimization Details
1. Fanout Violation Reduction:
The Problem: High fanout nets can lead to signal degradation and transition violations, especially on the clock or reset lines.

The Solution: Adjusted the FP_CORE_UTIL and utilized OpenLane's PL_MAX_FANOUT parameter to force the tool to insert buffers.

Result: Successfully reduced Max Fanout violations to zero by balancing the load across the logic paths.

2. Die Area Reduction:
The Problem: Initial runs often leave too much "white space," which increases manufacturing costs (more silicon used for the same logic).

The Solution: Iterated on the Core Utilization (e.g., moving from 30% to a more dense 40-50%) and refined the Aspect Ratio to ensure the core was tight but still routable.

Result: Minimized the total area while maintaining enough "breathing room" for the routing layers to avoid congestion.
