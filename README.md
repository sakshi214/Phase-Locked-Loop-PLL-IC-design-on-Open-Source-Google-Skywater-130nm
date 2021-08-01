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
- first git clone the repository
![image](https://user-images.githubusercontent.com/69634738/127761238-60b60e01-c691-45be-a74a-e31f282585af.png)
- A spice file is the one with .spice or .cir extension
- The frequency divider circuit file is shown below
- this is the circuit diagram
![image](https://user-images.githubusercontent.com/69634738/127761397-3e5667d2-32b5-4ead-8a0c-88bde7d56a99.png)

-the sky130 library is included with 'include' command.
- xm1 is the pmos and the numbers 3 2 1 1 represents drain gate source body respectively.
- pmos length is 150 and width is 720 taken
- pmos width is taken double for the transistor sizing purpose.
- xm3 & xm4 are the transmission gates.
![image](https://user-images.githubusercontent.com/69634738/127761508-855ab22b-791e-46cb-a882-fd89c0986d33.png)
- v1 voltage source is connected to provide the 1.8V.
- v2 is the pulse source i.e, the clock signal.
- .control block is used to keep the simulation instructions.
![image](https://user-images.githubusercontent.com/69634738/127761459-9333ea10-7d04-4d6c-a9bb-b8e6a63ed5ac.png)

## PLL components circuit simulations
To start the simulation of the circuit just created
- The transient analysis block is shown
- the output is having half the frequency of input
![image](https://user-images.githubusercontent.com/69634738/127763361-21eb22ed-319a-4681-aab8-b9cfd39c2ced.png)

- This is the charge pump CP.cir file 
![image](https://user-images.githubusercontent.com/69634738/127763619-8f1134f6-740c-4cd4-9f8e-07ab1bec0a8d.png)
- on simulating this we get the below waveform.
- the current leakage is very small for charge pump
- the slope represents the charging happening
![image](https://user-images.githubusercontent.com/69634738/127763770-10483a9c-c32c-49c2-af0a-6f15ebb8ffc8.png)

- the response when actual pulse signal given to v2 is 
![image](https://user-images.githubusercontent.com/69634738/127765476-f8d851c9-5742-433f-aafa-c338e84b02f3.png)
![image](https://user-images.githubusercontent.com/69634738/127765489-29089879-640a-4bea-9990-9a60e1fc878f.png)

- This is the VCO.cir file and its simulation
- the oscillations are full swing 
![image](https://user-images.githubusercontent.com/69634738/127765786-697ead65-ec91-446a-ab6b-de5798fd25e8.png)
![image](https://user-images.githubusercontent.com/69634738/127765811-4a27acdd-3021-4fb9-849b-cfc5670da748.png)

- This is the phase frequency detector PD.cir and its simulation
![image](https://user-images.githubusercontent.com/69634738/127765902-a68bf773-ae9e-4cef-9594-b6beb4efda3f.png)
![image](https://user-images.githubusercontent.com/69634738/127765923-937be01a-0052-487c-aa81-c0af672afbaf.png)
- the circuit is able to detect the slight change in the phase.
![image](https://user-images.githubusercontent.com/69634738/127765965-7bead0ec-d71b-427f-81d4-87a972619b3d.png)

### Steps to combine PLL sub-circuits and PLL full design simulation
- This is the pre-layout file combining all the circuits
![image](https://user-images.githubusercontent.com/69634738/127767883-59f37567-22ba-4914-89f1-4c6f4464d7b6.png)
![image](https://user-images.githubusercontent.com/69634738/127767903-f7841d03-cc67-4615-a034-2121ae79591e.png)
- It is specifying
![image](https://user-images.githubusercontent.com/69634738/127767919-d4e600e8-91b3-430f-97a4-b480b648f557.png)
![image](https://user-images.githubusercontent.com/69634738/127767943-83438919-4782-47e8-9ee6-d91557badc8f.png)
- the final simulation output is as shown
![image](https://user-images.githubusercontent.com/69634738/127770865-cdb03a7e-b014-4bc7-a53b-92ed239b435a.png)

### Troubleshooting steps
- when the output doesnot show or it crashes, it is necessary to look if the connections are made properly.
![image](https://user-images.githubusercontent.com/69634738/127771268-61e446bf-b6a9-4b19-84d8-a97476ad7951.png)

### Layout Design
- The command "magic -T sky130A.tech" is used to open the magic window.
- On the right hand side there is tray of materials present.
- green section represents nmos.

![image](https://user-images.githubusercontent.com/69634738/127771476-26c13391-41e1-412a-964e-be3ce29305db.png)

### Layout walkthrough
- The following is the frequency divider layout circuit
- The components are kept close together to fit in minimum area, hence layout looks complicated.
![image](https://user-images.githubusercontent.com/69634738/127772509-7b2ff90b-5ea2-4179-8923-ff01dcfd09ac.png)

- The below is the layout of PFD circuit.
- in this design additional buffers are used to get full swing.
![image](https://user-images.githubusercontent.com/69634738/127772625-87a1cc52-a094-4345-81ad-5f5ee8a18811.png)

- The below is the charge pump layout:
![image](https://user-images.githubusercontent.com/69634738/127773445-6c92d832-acfc-4369-b091-4c142a329215.png)
- The below is the vco layout:
![image](https://user-images.githubusercontent.com/69634738/127773616-b958369d-415b-4e6d-9e02-acc23ad75db1.png)

### Parasitics Extraction
- To extract the capacitance effect information parasitics extraction.
![image](https://user-images.githubusercontent.com/69634738/127773909-7310cf74-bf65-40cb-b124-a87d1742e208.png)
- press i button to select the whole design and then after giving command extract all
![image](https://user-images.githubusercontent.com/69634738/127774082-4dea9498-df03-4e97-97dd-0d9584a31df7.png)
- this converts the connectivity information to .ext file
- "cthresh 0 and rthresh 0 " this setting is given to tell the magic to extract any amount of capacitive or resistive effect.
![image](https://user-images.githubusercontent.com/69634738/127774245-e1f15bc2-7bc5-4afb-be4f-93fa8f7ef3f2.png)
- The generated spice file is in subckt format
- in the bottom there are additional capacitances, these are the capacitances extracted by magic.
![image](https://user-images.githubusercontent.com/69634738/127774981-9c42ed3d-5507-429c-bb37-f3afdf7bf12d.png)


### Post Layout simulations
- 















