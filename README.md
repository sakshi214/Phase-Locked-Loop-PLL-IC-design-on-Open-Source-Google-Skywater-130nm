# Phase-Locked-Loop-PLL-IC-design-on-Open-Source-Google-Skywater-130nm

# DAY-1
## Introduction to PLL
- PLL stands for phase locked loop.
- It is a control system that tracks the output frequency and synchronises it with the reference signal.
- It is used to get a precise clock signal without frequency or phase noise.

### PLL Components
- Phase frequency detector
- charge pump -> it converts the digital comparision into anolog signal.
- Low pass filter -> it is used to smoothen the charge pump output signal.
- voltage controlled oscillator-> it is the onchip oscillator.
- frequency divider ->it is used to convert the whole system into frequency multiplier.

### Introduction to phase frequency detector (PFD)
- It is used to compare output signal with reference signal.
- The width of the pulse is used to determine the phase of the signal.
- As width increases, phase also increases.
- The main issue with PFD is deadzone.
- Deadzone-> it is the zone within which the PFD is insensitive to phase difference. it is mainly when signals fall close to each other hence the output doesn't get enough time to rise. this introduces a dealay.
- A more precise PFD enables better stability for the PLL.

### Introduction to Charge Pump
- It converts the digital comparision from PFD into anolog signal.
- 
