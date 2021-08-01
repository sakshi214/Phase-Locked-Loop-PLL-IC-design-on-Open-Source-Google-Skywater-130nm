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
- On incresing the voltage, the speed of the oscillator increases.
- The main issue of charge pump is charge leakage.
- charge leakage-> it keeps charging the capacitor even when inputs are off.
- This is tackled by using low pass filter in the output, which also helps inj stabilizing the PLL.

### Introduction to VCO and frequency divider
- VCO is the onchip oscillator.
- The frequency depends on delay and delay depends on current supplied.
- Frequency divider is used to convert the whole system into frequency multiplier.
Lock Range ->the range of frequencies for which PLL can maintain lock, already in locked state.
Capture range -> The frequencies for which PLL is able to lock-in from unlocked state.

### Tool setup and Design flow
Two tools are used:
- Ngspice: it is used for the transistor level circuit simulations.
- Magic: it is used for the layout design.

Development flow steps:
- SPICE level circuit development
- Pre layout simulation
- Layout development
- Parasitics extraction
- Post layout simulation



# DAY 2
## PLL Components circuit design
To make circuit description in ngspice:
first git clone the repository
![image](https://user-images.githubusercontent.com/69634738/127761238-60b60e01-c691-45be-a74a-e31f282585af.png)
![image](https://user-images.githubusercontent.com/69634738/127761237-68ce4caf-a607-4ce5-9c72-a48ea6fe73d4.png)


