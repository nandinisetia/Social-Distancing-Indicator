# Social-Distancing-Indicator
Social Distancing and Alarming System is made in which, Arduino UNO, Ultrasonic sensor, NeoPixel 12  RGB LEDs Ring, and Buzzer are connected to implement the system. Tinkercad text programming platform is used to implement it.
## Detailed Explanation
### Ultrasonic sensor
- **Vcc** The Vcc pin powers the sensor, typically with +5V
- **Trigger**  Trigger pin is an Input pin. This pin has to be kept high for 10us to initialize measurement by sending US wave.
- **Echo** Echo pin is an Output pin. This pin goes high for a period of time which will be equal to the time taken for the US wave to return back to the sensor.
- **Ground** This pin is connected to the Ground of the system.


### Echo pin and Trigpin
For example, if the object is 20 cm away from the sensor, and the speed of the sound is 340 m/s or 0.034 cm/µs the sound wave will need to 
travel about 588 microseconds. But what you will get from the Echo pin will be double that number because the sound wave needs to travel 
forward and bounce backward. So in order to get the distance in cm we need to multiply the received travel time value from the echo pin by 
0.034 and divide it by 2.


### For 21-22
In the setup, we declare the Trig pin as an output, the Echo pin as an input, and start Serial communications.

### For 32 to 45
Here it is written leds to glow =12 which means when all the twelve leds starts glowing, buzzer should be switched on, and when less than 12 leds 
are glowing buzzer should remain silent.

### For 46 to 60
As we have seen in the circuit , first four leds are of green color, then next four are of yellow and the last four are of red. In order to create this pattern
we use setpixelcolor which gives color to the led...primary colors that are predefined in our code are RED GREEN AND BLUE , to create yellow color,we use 
red and green simultaneously.

### For 69 to 88
Now, in the loop, what we do is first set the trigPin low for 2 microseconds just to make sure that the pin in low first. Then, we set it high for
 10 microseconds, which sends out an 8 cycle sonic burst from the transmitter, which then bounces of an object and hits the receiver(Which is 
connected to the Echo Pin).When the sound waves hit the receiver, it turns the Echo pin high for however long the waves were traveling for. 
To get that, we can use a handy Arduino function called pulseIn(). It takes 2 arguments, the pin you are listening to(In our case, the Echo pin), and
 a state(HIGH or LOW). What the function does is waits for the pin to go whichever state you put in, starts timing, and then stops timing when it 
switches to the other state. In our case we would put HIGH since we want to start timing when the Echo pin goes high. We will store the time in 
the duration variable. (It returns the time in microseconds)

duration = pulseIn(echoPin, HIGH); 
Now that we have the time, we can use the equation speed = distance/time, but we will make it time x speed = distance because we have the
 speed. What speed do we have? The speed of sound, of course! The speed of sound is approximately 340 meters per second, but since the 
pulseIn() function returns the time in microseconds, we will need to have a speed in microseconds also, which is easy to get. 
A quick Google search for "speed of sound in centimeters per microsecond" will say that it is .0343 c/μS. You could do the math, but searching 
it is easier. Anyway, with that information, we can calculate the distance! Just multiply the duration by .0343 and then divide it by 2(Because 
the sound waves travel to the object AND back). We will store that in the distance variable.

distance = (duration*.0343)/2;
