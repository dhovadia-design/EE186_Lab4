# EE186_Lab4

Section 2: ADC

What are the different bit resolutions can you set the ADC? What is the maximum sampling rate at each of these resolutions? Where did you find this information in the datasheet? 

You can set ADC to 6, 8, 10, and 12 bits (which is what I used). The max sampling rate is 5.33 Msps for 12 bits, 6.15 Msps for 10, 7.27 Msps for 8, and 8.88 Msps for 6 all on the fast channel. I found this information on Table 81 ADC characteristics on page 214 of the STM32L4R5 datasheet.

Why do you need a voltage divider circuit? What would happen if the photodiode is directly connected to the board? 

You need a voltage divider because the photodiode only changes its resistance in respect to light. An ADC pin can’t read resistance, so the voltage divider turns the resistance changed into voltage changed. Without a voltage divider, one leg of the photodiode would connect to the ADC pin and the other would be connected to ground causing the pin to sit at ground. It could also be connected to 3.3V which would cause the opposite effect and the pin would always sit at 3.3V no matter the light levels. When you add the voltage divider because of Vout = Vin × R_bottom / (R_top + R_bottom), with the LDR as R_top, more light lowers its resistance so Vout increases.

Submit circuit diagrams for both configurations used in this part of the lab.
(see image!)

Section 3: DAC

If B = 9, what is Vout? Express your answer in terms of Vref . Use the DAC mode that provides the best resolution available on your MCU (refer to the data sheet).
The best resolution is 12 bits (n=12), Vref = 3.3V

Vout = (B/ 2^n) * Vref
Vout = (9/(2^12)) * Vref
(Vref = 3.3V), Vout = (9/(2^12)) * 3.3V
Vout = 7.25mV
 
How does the sampling rate of the DAC affect the quality of the output waveform? What are the differences in sound perception between sine, square, and sawtooth waves? Why do we need a capacitor in the signal path when sending an audio signal to a speaker or earphones?

The sampling rate of the DAC affects the quality of the output waveform because it changes the sharpness of your stepsizes. The number of steps per cycle are the sample rate / signal frequency. With a lower sampling rate, there are fewer steps so the wave is more blocky. With a high sampling rate, the waves are much smoother. 

A sine wave sounds smooth and consistent. A square wave has a much more buzzy tone and sounds a little more video game esque. Finally, a sawtooth wave is very buzzy and aggressive sounding. In terms of harmonics, the sine has the fundamental, square adds the odd harmonics, and sawtooth adds all harmonics. This is why the sounds get more aggressive and buzzy as you go from sine to sawtooth.

We need a capacitor in the signal path because it will only pass the changing signals and will block the constant ones. The DAC outputs range from 0 to 3.3V,so the signal is centered around 1.65V (the DC offset). A DC offset causes issues because it holds the coil to one side which means it can’t swing freely which distorts sounds and also wastes power. When you add a capacitor, it blocks the constant DC bias and only passes the waves.
