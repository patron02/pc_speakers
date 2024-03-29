# PC Speakers Build

This project consists of building 2 speakers that will output the audio from my PC. I am limited in circuit options since I would like to use only parts that I already have at home. It would be simple to buy an audio amp board off Amazon or use op amps but I don't have those; what I do have are transistors, capacitors, diodes, and resistors. The speakers I will be using are rated at 8 Watts and 4 Ohms.

I thought the impedence of my speaker would not matter much because it is in series with a 220 uF coupling capacitor. At 440 Hz (roughly middle C frequency) the capacitor will have an impedence of 1.6 Ohms. If the speaker has an impedence of 4 Ohms it will still represent about 70% of the load seen by the output transistor. But later on I measured the impedance of my speaker and it was about 3.4 [Ohms] and I ended up needed to impedance match the speaker. 

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

To maximize the potential voltage of the output, the junction between the emitters of transistors 2 and 3 should be set at half of the supply voltage. This setup should produce the proper voltage at transistor 1's base than causes it to be in active mode. 

To maximize the output the Q1 and Q3 should be set at haf the input voltage. Based on some research I chose the input to be 3 [V], I later tested it below to make sure it was outputting the correct values. We need the voltage at Q2's base to 0.6 [V] so it can be in active moed, this means that the voltage across R4 will set the base voltage.

VR4 = 1.5V * R4/(R4 + R3 + R2) = 0.63 [V] <br> 

The current coming in through the diodes needs to be enough to to give proper idle current. 

Ic = (VCC - 2*Vdiodes)/2R1 = 0.9 [mA]

> Info on push pull amplifiers: https://tinyurl.com/mry72ubs <br>
> Info on push pull amplifiers: https://circuitdigest.com/electronic-circuits/push-pull-amplifier-circuit-diagram

## Voltage Regulator

The voltage regulator I had available was a LM2596. I have to do some calculations on the circuit I have built to see what maximum input voltage I can use without damaging the transistors, capacitors, and diodes. <br> 

> 1N4001 Datasheet: https://cdn-shop.adafruit.com/datasheets/1N4001-D.PDF <br>
> LM2596 Datasheet: https://www.ti.com/lit/ds/symlink/lm2596.pdf <br>
> 2N3904/2N3906 Datasheet: https://www.digikey.com/en/htmldatasheets/production/95776/0/0/1/2n3904-datasheet <br>

Measured Values: <br>
<img alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/a92225d1-c8fe-4cc7-9398-6889a81c4b2e"> <br>

All the values were within the correct parameters when the LM2596 was set to output 3 [V]. This circuit had audio coming out of the speaker but it was a lot of static. I was supplying the circuit with 3 [V] which provided a nice volume but the static could possibly be caused by faulty wires/breadboard. The next step is to find out the source of the static and how I can remove it. I want the circuit to fit in a small box which I will make for the speaker so I had to make it all fit onto one breadboard. I soldered 1 of the speaker circuits and there was still static so it wasnt the breadboard, I will try to reduce static by checking the transient function in LTSpice and possibly building an audio filter if needed.  

<img height="350" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/928896f2-b29f-46df-ab11-0688e0d89906"> <img height="350" alt="image" src="https://github.com/patron02/pc_speakers/assets/69320369/816449ee-3075-4307-9860-950453c184d2"> <br>

## Reducing the Static
The static coming out of the speaker could be due to multiple things including noise from the power supply, EMI, and lack of impedance matching. I started with double checking that the impedance was matched. The speaker has a 3.4 [Ohm] impedance and the circuit has an 8.3 [Ohm] impedance at 440 Hz (which is the average frequency of muscial audio signals). I added A 4 [Ohm] resistor in series with the speaker to have it match up. This mattered because at 440 Hz the impedance of the capacitor is 1.64 [V] and the speakers is about 3.4 [V] (should be 4). This means that it only represents about 70% of the load to the output transistor. I also increased the input to 9 [V] so I could use an easily replaceable battery and added some resistance to the discharge transistor's emitter to increase the bias, linearize the gain, and prevent saturation. The signal was also clipping because I set my input too high, the maximum Vpp coming from my phone was 4 [V] which I measured with an oscilloscope. There was still some distortion and not that much amplification. 

Before changes: <br>
<img height="300" src="https://github.com/patron02/pc_speakers/assets/69320369/517f1bcd-80cb-4eb4-ae40-7804a7e14f5a"> <br>

After changes: <br>
<img height="300" src="https://github.com/patron02/pc_speakers/assets/69320369/93033e9f-a469-41ce-993c-e2ac20587653"> <br>

The new circuit on LTSpice: <br>
<img height="350" src="https://github.com/patron02/pc_speakers/assets/69320369/869f0177-0e30-4baa-96dd-2b34fe8af641"> <img height="350" src="https://github.com/patron02/pc_speakers/assets/69320369/8102d5ce-c85a-45fa-9367-c846ad695277"> <br>

Using LTSpice I noticed that there was some crossover distortion, it was very small but still noticeable. <br>

<img height="250" src="https://github.com/patron02/pc_speakers/assets/69320369/50dcb967-2af4-42af-afdc-49316c1d6afb"> <img height="250" src="https://github.com/patron02/pc_speakers/assets/69320369/73f49079-b687-4be0-8132-205a1f4c9f5d">

I tried to add resistors between the transistors so that the emitters wouldnt fight for the voltage at the junction but that reduced the amplification significantly so I chose to leave it for now. The pushpull amplifier output will always be roughly be 0.7 [V] less than the input so the LTSpice is showing the correct signal output. There is still some small distortion on the bass notes so I will try adding a high pass filter or potentiometers at the emitters of Q3 so that the BJT biasing can be slightly altered for different songs and not clip the signal.

> Info on crossover distortion: http://tinyurl.com/bdh88hz9

The final circuit: <br>
<img height="400" src="https://github.com/patron02/pc_speakers/assets/69320369/da0b0b22-7236-45f5-91d9-faa9b73da3b4">

Video: <br>
https://youtu.be/_dIUI8IVlO8

## Casing Design
Fusion 360 Model: <br>
<img height="350" src="https://github.com/patron02/pc_speakers/assets/69320369/293553f8-9291-4113-93c0-e1e41be9a23e"> <img height="350" src="https://github.com/patron02/pc_speakers/assets/69320369/d116a2c9-ee97-4e98-b6f6-350f43383b07"> 

## Final Product
<img height="300" src="https://github.com/patron02/pc_speakers/assets/69320369/b783bc04-3471-4cf0-995c-fc31b2381e8c"> <img height="300" src="https://github.com/patron02/pc_speakers/assets/69320369/3b7c3905-e050-43f9-9b39-f44d62cc075e"> <img height="300" src="https://github.com/patron02/pc_speakers/assets/69320369/3aedfd76-24ba-4f2b-bb3d-0608f177df08"> <br>

Video: <br>
https://youtu.be/L6ErmH1Rq8c




