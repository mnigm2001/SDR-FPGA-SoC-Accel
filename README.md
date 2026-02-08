
# SDR FPGA/SoC Acceleration (FM Mono/Stereo + RDS)

Hardware-accelerated SDR project that evolves a working **Raspberry Pi + RTL-SDR (C++)** receiver into an **FPGA/SoC-accelerated DSP pipeline** using **RTL + HLS**, verified against **golden models**, and demonstrated over progressively harder system interfaces (**simple link → Ethernet → PCIe**).

---

## Project goals
- Keep an end-to-end receiver working at every stage
- Add **measurable** acceleration (throughput, latency, CPU offload)
- Practice industry skills: **DSP, RTL/HLS, AXI/DMA, timing/CDC, SystemVerilog verification, system integration**

---

## Roadmap (high level)

### Stage A — Reproduce baseline on Raspberry Pi
- Rebuild and run the receiver end-to-end
- Verify RTL-SDR health (`rtl_test`) and basic RF capture

### Stage B — Finish the “full RDS” milestone
- Complete RDS chain: carrier recovery → demod → timing recovery → frame sync → parsed fields  
- Targets: PS name, RadioText, time/date (as available)

### Stage C — Hardware acceleration (hero blocks, easy → hard)
- **Hero A (easiest):** FIR/decimation or polyphase resampler (streaming)
- **Hero B (medium):** FFT / waterfall / spectral features
- **Hero C (hardest):** RDS helpers (demod + timing recovery + frame sync acceleration)

### Stage D — Real interface demo (easy → hard)
- Simple link (UART/SPI-style bursts)
- Ethernet control/streaming
- PCIe DMA (stretch)

---

## Repo layout
- `sw/` : C++ receiver, profiling, optional SIMD (NEON) path
- `model/` : MATLAB/Python golden models + test-vector generation
- `hw/` : RTL + HLS accelerators, AXI wrappers, constraints
- `dv/` : SystemVerilog testbenches (UVM-lite), assertions, coverage
- `docs/` : architecture diagrams, timing reports, integration notes
- `data/` : small IQ captures + expected outputs (kept minimal)

---

## Quick start (Raspberry Pi + RTL-SDR)
1. Update/upgrade packages
2. Plug in RTL-SDR and confirm it enumerates (`lsusb`)
3. Blacklist the default kernel driver if needed
4. Install `rtl-sdr` and run `rtl_test`
5. Build and run the receiver

---

## Key architecture notes
- DSP is organized as a streaming block pipeline from IQ input to audio/RDS outputs
- Threading plan: RF front-end thread + audio thread + RDS thread (optionally split RDS further)
- Hardware blocks target clear boundaries with golden-model equivalence tests

---

## Milestones (portfolio-friendly)
- Baseline FM mono working
- Stereo path working
- RDS: bitstream + frame sync + parsed fields
- Hero A accelerated + verified vs golden
- Hero B accelerated + live waterfall demo
- Hero C accelerated + robust RDS decode
- Ethernet demo
- PCIe demo (stretch)

---

## License
TBD

## Status
Work in progress
