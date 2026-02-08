# SDR-FPGA-SoC-Accel

readme:
  title: "SDR FPGA/SoC Acceleration (FM Mono/Stereo + RDS)"
  summary: >
    This repo evolves a working real-time RTL-SDR receiver into a hardware-accelerated DSP pipeline.
    Baseline runs on Raspberry Pi (C++). Acceleration targets FPGA/SoC hero blocks (RTL + HLS),
    verified against golden models, with progressive system interfaces (simple link → Ethernet → PCIe).

  goals:
    - "Keep an end-to-end receiver working at every stage"
    - "Add measurable acceleration (throughput, latency, CPU offload)"
    - "Practice skills: DSP, RTL/HLS, AXI/DMA, timing/CDC, SV verification, integration"

  roadmap:
    stage_a_reproduce_baseline:
      - "Rebuild and run the Raspberry Pi receiver end-to-end"
      - "Verify RTL-SDR health (e.g., rtl_test) and basic RF capture"
    stage_b_finish_rds_milestone:
      - "Complete RDS chain: carrier recovery → demod → timing recovery → frame sync → parsed fields"
      - "Targets: PS name, RadioText, time/date (as available)"
    stage_c_hardware_acceleration_hero_blocks:
      hero_a_easiest:
        - "FIR/decimation or polyphase resampler (streaming)"
      hero_b_medium:
        - "FFT / waterfall / spectral features path"
      hero_c_hardest:
        - "RDS helpers: demod + timing recovery + frame sync acceleration"
    stage_d_real_interface_demo:
      - "Simple link (UART/SPI-style bursts)"
      - "Ethernet control/streaming"
      - "PCIe DMA (stretch)"

  repo_layout:
    sw: "C++ receiver, profiling, optional SIMD"
    model: "MATLAB/Python golden models + test-vector generation"
    hw: "RTL + HLS accelerators, AXI wrappers, constraints"
    dv: "SystemVerilog testbenches (UVM-lite), assertions, coverage"
    docs: "Architecture diagrams, timing reports, integration notes"
    data: "Small IQ captures + expected outputs (kept minimal)"

  quick_start_raspberry_pi:
    - "Update/upgrade packages"
    - "Plug in RTL-SDR and confirm it enumerates (lsusb)"
    - "Blacklist the default kernel driver if needed"
    - "Install rtl-sdr and run rtl_test"
    - "Build and run the receiver"

  key_architecture_notes:
    - "Signal-processing is organized as a streaming block pipeline from IQ input to audio/RDS outputs"
    - "Threading plan: RF front-end thread + audio thread + RDS thread (optionally split RDS further)"
    - "Hardware blocks target clear boundaries with golden-model equivalence tests"

  milestones:
    - "Baseline FM mono working"
    - "Stereo path working"
    - "RDS: bitstream + frame sync + parsed fields"
    - "Hero A accelerated + verified vs golden"
    - "Hero B accelerated + live waterfall demo"
    - "Hero C accelerated + robust RDS decode"
    - "Ethernet demo"
    - "PCIe demo (stretch)"

  references:
    - "Project spec + DSP chain and threading notes (local docs)"
    - "Raspberry Pi + RTL-SDR setup notes (local docs)"
