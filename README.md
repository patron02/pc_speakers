# PC Speakers Build

This project consists of building 2 speakers that will output the audio from my PC. I am limited in circuit options since I would like to use only parts that I already have at home. It would be simple to buy an audio amp board off Amazon or use op amps but I don't have those; what I do have are transistors, capacitors, diodes, and resistors. The speakers I will be using are rated at 8 Watts and 4 Ohms.

The impedence of my speaker will not matter much because it is in series with a 220 uF coupling capacitor. At 440 Hz (roughly middle C frequency) the capacitor will have an impedence of 1.6 Ohms. If the speaker has an impedence of 4 Ohms it will still represent about 70% of the load seen by the output transistor. 

> Info on coupling capacitors: https://www.icrfq.net/coupling-capacitor/

## First Circuit
<img height="300" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/a808d26c-09ab-4580-a93c-b49b6fdaea58"> <br>
Q1 provides an initial signal gain as a common emitter amplifier. R1, R2, R3, and R4 form a 4-resistor bias network to ensure Q1 is in the linear amplification region. C2 raises the AC gain of that stage by providing a low impedence path to ground for AC signals. 

> Info on 4-resistor bias networks: https://www.youtube.com/watch?v=Ua7cZ63PlOk <br>
> Info on transistor biasing configurations: https://www.electronics-tutorials.ws/amplifier/transistor-biasing.html

Q2 and Q3 are arranged as a darlington pair, performing as a single high beta transistor. R5, C3, and SP1 make the last stage an emitter follower configuration (also called common collector configuration). 

> Info on darlington pair: https://www.electronics-tutorials.ws/transistor/darlington-transistor.html <br>
> Info on common collector configuration: https://rb.gy/c1q3d

The 330 Ohm resistor provides a DC current path for Q3 and raises the emitter voltage above ground. C3 blocks DC from flowing to the speaker and gives a low impedence path for AC signals to go to the speaker. Based on EasyEDA simulations I ran, this circuit would not provide enough power to my speaker so I decided to try a second design.

## Second Circuit 
<img height="300" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/7590ae61-89c3-447a-99ba-5c8df126c627"> <br> 


This configuration is arranged as a push pull amplifier. It may provide a litter higher power output and run more efficiently than the second circuit but power is limited by the fact that 2N3904 and 2N3906 transistors are small-signals transistors with very limited current carrying capability. This could be fixed by using transistors with higher ratings. This circuit can deliver about 10x more power to the speaker, but it is a more complex circuit to build. 

Usually a push-pull audio amplifying circuit looks as pictured below, but the one above has a a third transistor in the first stage. The complement transistor is not used to drive a transformer but to discharge the dc decoupling capacitor to give full wave alternating current to the speaker. 

<img height="300" alt="image" src="https://circuitdigest.com/sites/default/files/circuitdiagram/Class-AB-Amplifier.png">

To maximize the potential voltage of the output, the junction between the emitters of transistors 2 and 3 should be set at half of the supplyA  voltage. This setup should produce the proper voltage at transistor 1's base than causes it to be in active mode. 



> Info on push pull amplifiers: https://tinyurl.com/mry72ubs <br>
> Info on push pull amplifiers: https://circuitdigest.com/electronic-circuits/push-pull-amplifier-circuit-diagram

This circuit had audio coming out of the speaker but it was a lot of static. I was supplying the circuit with 3 [V] which provided a nice volume but the static could possibly be caused by faulty wires/breadboard. The next step is to find out the source of the static and how I can remove it. I want the circuit to fit in a small box which I will make for the speaker so I had to make it all fit onto one breadboard.

<img height="350" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/928896f2-b29f-46df-ab11-0688e0d89906"> <img height="350" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/816449ee-3075-4307-9860-950453c184d2"> <br>

## Calculations

The voltage regulator I had available was a LM2596. I have to do some calculations on the circuit I have built to see what maximum input voltage I can use without damaging the transistors, capacitors, and diodes. <br> 

> 1N4001 Datasheet: https://cdn-shop.adafruit.com/datasheets/1N4001-D.PDF <br>
> LM2596 Datasheet: https://www.ti.com/lit/ds/symlink/lm2596.pdf <br>
> 2N3904/2N3906 Datasheet: https://www.digikey.com/en/htmldatasheets/production/95776/0/0/1/2n3904-datasheet <br>


## Reducing the Static
Filter WIP

## Voltage Regulator 


## Casing Design
WIP
The initial design for the case had an open back: <br>
<img height="400" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/c04a5a2e-64c9-48ed-9734-8ccbb336083f">

3D model stl link:


