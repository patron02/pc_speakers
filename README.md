# PC Speakers Build

This project consists of building 2 speakers that will output the audio from my PC. I am limited in circuit options since I would like to use only parts that I already have at home. It would be simple to buy an audio amp board off Amazon or use op amps but I don't have those; what I do have are transistors, capacitors, diodes, and resistors. The speakers I will be using are rated at 8 Watts and 4 Ohms.

I started off with two circuits that I found online:

<img height="300" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/a8e7eec6-bb4c-415e-a268-96df13e557f5">
<img height="300" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/a808d26c-09ab-4580-a93c-b49b6fdaea58">

The impedence of my speaker will not matter much because it is in series with a 220 uF coupling capacitor. At 440 Hz (roughly middle C frequency) the capacitor will have an impedence of 1.6 Ohms. If the speaker has an impedence of 4 Ohms it will still represent about 70% of the load seen by the output transistor. 

> Info on coupling capacitors: https://www.icrfq.net/coupling-capacitor/



## How the coloured circuit above works:

Q1 provides an initial signal gain as a common emitter amplifier. R1, R2, R3, and R4 form a 4-resistor bias network to ensure Q1 is in the linear amplification region. C2 raises the AC gain of that stage by providing a low impedence path to ground for AC signals. 

> Info on 4-resistor bias networks: https://www.youtube.com/watch?v=Ua7cZ63PlOk <br>
> Info on transistor biasing configurations: https://www.electronics-tutorials.ws/amplifier/transistor-biasing.html

Q2 and Q3 are arranged as a darlington pair, performing as a single high beta transistor. R5, C3, and SP1 make the last stage an emitter follower configuration (also called common collector configuration). 

> Info on darlington pair: https://www.electronics-tutorials.ws/transistor/darlington-transistor.html <br>
> Info on common collector configuration: https://rb.gy/c1q3d

The 330 Ohm resistor provides a DC current path for Q3 and raises the emitter voltage above ground. C3 blocks DC from flowing to the speaker and gives a low impedence path for AC signals to go to the speaker. 



## DC Analysis:



## AC Analysis:



## Configuration with Diodes
The configuration above with diodes has the output arranged as a push pull amplifier. It may provide a litter higher power output and run more efficiently than the coloured circuit. Power is limited by the fact that 2N3904 and 2N3906 transistors are small-signals transistors with very limited current carying capability. The coloured circuit could deliver at maz 10 mW to the speaker, while the push pull amplifier configuration could maybe get up to 100 mW.

Calculations: 

Info on push pull amplifiers: 


## Prototype 1
First build had some audio but it was very quiet and mostly static. The capacitors were rated for a maximum of 10 V and the diodes were also different thn the circuit above so some analysis needs to be done on if that is what is causing some issues. I aso am only supplying the circuit with 2.4 V. I will add in a 12 V power supply and attempt to modify the components for maximum gain by doing some calculations on excel. 
![gg_10](https://github.com/patron02/pc_speakers/assets/69320369/5b49ef03-c8c6-4ac2-a4cc-eef4e9326e03)

## EasyEDA Build and Analysis



## Physical Circuit Design



## Casing Design
3D model stl link: 
CNC wood cuttin
Filter


