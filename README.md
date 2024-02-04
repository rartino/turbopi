# TurboPi

This repo tracks software and cronicles some fun we've had with the [Hiwonder](https://www.hiwonder.com/) [TurboPi robot car](https://www.hiwonder.com/collections/raspberrypi-bionic-robot/products/turbopi).

**Disclamer:** I'm not affiliated with Hiwonder in any way. This text just describe things I've explored with this robot kit on my own. I take no responsibility for others who may try to follow this as instructions. *Do not carry out any steps you do not understand well enough yourself so that you are sure that what you do is safe and will not damage anything.* In particular lithium-ion batteries are not safe if mishandled. If you let kids or others partake, they should be closely supervised.

The TurboPI is a very nice metallic robot car kit for a Raspberry Pi (4b) with a bunch of sensors (4 motors, 4 mecanum wheels, camera mounted with two servos, line follower, ultrasonic sensor with multicolor LED lights). It comes with a set of software that allows fairly easily get started with getting the robot to do things.

# Charge the batteries

Charging the batteries may take upwards 4-5 hours, and apparently the recommendation is to not leave them too long in the charger after they are fully charged.
Hence, it makes sense to start by putting them in the charger.

Depending on what kit you have, batteries may be included or not.
I would suggest getting the kit with batteries since it can be a bit difficult to get the right ones.
The specification says 2 x 18650, but apparently 18650 can come in slightly different sizes depending on the protective circuit included.
The kit I got with batteries included also came with an everActive LC200 charger, which I didn't see specified anywhere (and it had been nice to know, since I had thought I needed to order one.)

# Prepare the Raspberry Pi system image

For this robot you need a Raspberry Pi 4b and an SD card (or maybe a mini USB stick).

Once the robot is assembled, the SD card will be placed in such a way that it cannot easily be removed.
Hence, you probably want to fully prepare the card and check that your Rasberry Pi works with it before any other assembly.
Alternatively (I guess, I didn't try this) you can set up the software on a mini usb stick, which in that case will be possible to have inserted in an accessible position.

Use the download link to the "Source code and system image" in the TurboPi documentation booklet.
It takes you to a Google drive, where you can find the crucial image file in the path `1. System Image/System Image/TurboPi20230320.zip`.
When uncompressed it results in a file `TurboPi20230320.img` 9.6 Gb file with sha256 hash: `48a343c0391433c0d10b8849fc4dd376e1a3b103555c6dc42963def2a42de7ff`.
   
There is accompanying instructions and software to burn this image onto an SD card from a Windows Computer.
I generally recommend being careful with running software delivered this way on your computer, and since I am Linux user, I simply used Ubuntu's 'Startup Disk Creator' to get the img file written to an SD card.

Once you have written the image, you can boot the Rasberry Pi standalone using a regular Rasberry Pi power adapter and check that it works as intended, as well as configure networking.

(More will be added about this).

# Assembly of the robot

HiWonder provides a [YouTube playlist](https://www.youtube.com/playlist?list=PLFbzd0m6AcmLzo53o2Tsa20BS350rWGMj) of assembly instructions. 
However, note that the videos for some reason are out of order, and, in particular, there are quite a few feature videos mixed in among the others.

The correct order of the assembly vidoes appear to be as follows:

1. **Check contents**

   TurboPi Unboxing: https://youtu.be/VeeM6eauavM?si=aWWE4Y2o0569Epr6

2. **Attach the expansion board to the Raspberry Pi**

   - Optional: check the overview of the Pi expansion board: https://youtu.be/k4s9Au3EF6Y?si=PgsI46sfaEnbTByz  
   - TurboPi Assembly: Assemble Raspberry Pi + Expansion Board: https://youtu.be/52N_oKo334s?si=4og4as8ZxAK10uI2

3. **Attach the Rasberry Pi + expansion board to the main body**

   TurboPi Assembly: Install Controller + Line Follower: https://youtu.be/F5LvTlMeYEM?si=ZsP-zIZYwazmX7WW

4. **Install motors and wheels**

   TurboPi Assembly: Install Motors + Wheels + Battery Holder Case: https://youtu.be/erCFkrZ1qKg?si=nWRbYBGvE_l8QWKt

5. **Assmble the "head" with the camera**

   TurboPi Assembly: Assemble Servo+Ultrasonic Sensor+Camera: https://youtu.be/46S2ZhOeooE?si=OvOc0oJ7FajFvmZj

6. **Last step: attach the head to the body**
  
   TurboPi Assembly: Assemble Pan Tilt + Expansion Board Cover: https://youtu.be/vKcvwtmXHYs?si=jLAC-dm6xtmcSF

   
