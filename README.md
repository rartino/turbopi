# TurboPi

This repo tracks software and cronicles some fun we've had with the [Hiwonder](https://www.hiwonder.com/) [TurboPi robot car](https://www.hiwonder.com/collections/raspberrypi-bionic-robot/products/turbopi).

**Disclamer:** I'm not affiliated with Hiwonder in any way. This text just describe things I've explored with this robot kit on my own. I take no responsibility for others who may try to follow this as instructions. *Do not carry out any steps you do not understand well enough yourself so that you are sure that what you do is safe and will not damage anything.* In particular lithium-ion batteries are not safe if mishandled. If you let kids or others partake, they should be closely supervised.

The TurboPI is a very nice metallic robot car kit for a Raspberry PI (4b) with a bunch of sensors (4 motors, 4 mecanum wheels, camera mounted with two servos, line follower, ultrasonic sensor with multicolor LED lights). It comes with a set of software that allows fairly easily get started with getting the robot to do things.

# Assembly

HiWonder provides a [YouTube playlist](https://www.youtube.com/playlist?list=PLFbzd0m6AcmLzo53o2Tsa20BS350rWGMj) of assembly instructions. 
However, note that the videos for some reason are out of order, and, in particular, there are quite a few feature videos mixed in among the others.

The correct order appears to be this:

0. **Charge the batteries.**
   
   Depending on what kit you have, they may be included or not.
   I would suggest getting the kit with batteries since it can be a bit difficult to get the right ones.
   The specification says 2 x 18650, but apparently 18650 can come in slightly different sizes depending on the protective circuit included.
   My kit with batteries also included an everActive LC200 charger, which I didn't see specified anywhere (which had been nice to know, since this led me to order another one...)
   Charging the batteries may take upwards 4-5 hours, and apparently the recommendation is to not leave them too long in the charger after they are fully charged.

2. **Check contents**

   TurboPi Unboxing: https://youtu.be/VeeM6eauavM?si=aWWE4Y2o0569Epr6

3. **Attach the expansion board to the raspberry pi**

   - Optional: check the overview of the Pi expansion board: https://youtu.be/k4s9Au3EF6Y?si=PgsI46sfaEnbTByz  
   - TurboPi Assembly: Assemble Raspberry Pi + Expansion Board: https://youtu.be/52N_oKo334s?si=4og4as8ZxAK10uI2

4. **Attach the rasberry pi + expansion board to the main body**

   TurboPi Assembly: Install Controller + Line Follower: https://youtu.be/F5LvTlMeYEM?si=ZsP-zIZYwazmX7WW

5. **Install motors and wheels**

   TurboPi Assembly: Install Motors + Wheels + Battery Holder Case: https://youtu.be/erCFkrZ1qKg?si=nWRbYBGvE_l8QWKt

6. **Assmble the "head" with the camera**

   TurboPi Assembly: Assemble Servo+Ultrasonic Sensor+Camera: https://youtu.be/46S2ZhOeooE?si=OvOc0oJ7FajFvmZj

7. **Last step: attach the head to the body**
  
   TurboPi Assembly: Assemble Pan Tilt + Expansion Board Cover: https://youtu.be/vKcvwtmXHYs?si=jLAC-dm6xtmcSF

   
