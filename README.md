# TurboPi

This repo tracks software and cronicles some fun we've had with the [Hiwonder](https://www.hiwonder.com/) [TurboPi robot car](https://www.hiwonder.com/collections/raspberrypi-bionic-robot/products/turbopi).

**Disclamer:** I'm not affiliated with Hiwonder in any way. This text just describe things I've explored with this robot kit on my own. I take no responsibility for others who may try to follow this as instructions. *Do not carry out any steps you do not understand well enough yourself so that you are sure that what you do is safe and will not damage anything.* In particular lithium-ion batteries are not safe if mishandled. If you let kids or others partake, they should be closely supervised.

The TurboPI is a very nice metallic robot car kit for a Raspberry Pi (4b) with a bunch of sensors (4 motors, 4 mecanum wheels, camera mounted with two servos, line follower, ultrasonic sensor with multicolor LED lights). It comes with a set of software that allows fairly easily get started with getting the robot to do things.

## Charge the batteries

Charging the batteries may take upwards 4-5 hours, and apparently the recommendation is to not leave them too long in the charger after they are fully charged.
Hence, it makes sense to start by putting them in the charger, and check on them now and then during the rest of the process.

Depending on what kit you have, batteries may be included or not.
I would suggest getting the kit with batteries since it can be a bit difficult to get the right ones.
The specification says 2 x 18650, but apparently 18650 can come in slightly different sizes depending on the protective circuit included.
The kit I got with batteries included also came with an everActive LC200 charger, which I didn't see specified anywhere (and it had been nice to know, since I thought I needed to order one.)

## Prepare the Raspberry Pi with the system image

For this robot you need a Raspberry Pi 4b and an SD card (or maybe a mini USB stick).

Once the robot is assembled, the SD card port is placed in such a way that it cannot easily be accessed.
Hence, you probably want to start with preparing the card and check that your Rasberry Pi works with it before any other assembly.
Alternatively (note: I didn't try this yet) you can set up the software on a mini USB stick that can be inserted in a position that is accessible after the assembly.

In the documentation booklet you should have received with kit there is a download link/QR code to the "Source code and system image".
It takes you to a Google drive, where you can find the crucial image file in the path `1. System Image/System Image/TurboPi20230320.zip`.
**Note:** *the "tutorial" link includes a series of "Lessons", where Lesson 2 has info and files related to preparing the card with a system image, but the system image itself is NOT included there - you have to find the specific system image link.* 
When uncompressed it results in a file `TurboPi20230320.img` 9.6 Gb file with sha256 hash: `48a343c0391433c0d10b8849fc4dd376e1a3b103555c6dc42963def2a42de7ff`.

There is accompanying instructions and software to burn this image onto an SD card from a Windows Computer.
I generally recommend being careful with running software delivered this way on your computer, and since I am Linux user, I simply used Ubuntu's 'Startup Disk Creator' to get the img file written to an SD card.

Once you have written the image, you can boot the Rasberry Pi standalone using a regular Rasberry Pi power adapter and check that it works as intended and configure networking.

You can now decide whether to connect a keyboard and screen to the Rasberry Pi to do the configuration, or whether to do it completely over the network.
I did the latter, which worked fine.
Note that since the Rasberry Pi is essentially a "real computer" you should, as far as you can, avoid just cutting power to it as that can corrupt the system image if you are unlucky.
Always shut it down by logging in and issuing `shutdown -h now` or equivalent, or (see below) once the HiWonder board is mounted, use the 'shutdown' button on that board.

Out of the box the image sets up its own WIFI hotspot named something like `HW-XXXXXXXX`.
You can connect to it from your computer with the default password `hiwonder`.
Once connected, the official documentation suggest connecting via VNC viewer, whereas I suggest simply using `ssh` (available as a terminal command on Linux, MacOSX and [recent versions of Windows](https://learn.microsoft.com/en-us/windows/terminal/tutorials/ssh#access-windows-ssh-client)).
The default login info is:

- host: 192.168.149.1
- username: pi
- password: raspberry

So, e.g., connect using `ssh pi@192.168.149.1` and enter the password.
Once logged in, I did the following setup:

* Change the default password for the `pi` user using `passwd`.
* Change the timezone to your own: `sudo timedatectl set-timezone Europe/Stockholm`.
* Enable Enable eth0 networking so we can always connect via network cable if we have trouble with the wifi.
  Use, e.g., `nano /etc/network/interfaces.d/eth0` to edit that file to contain the following:
  ```
  auto eth0
  allow-hotplug eth0
  iface eth0 inet dhcp
  ```
  
* After scratching my head a bit over HiWonder's networking setup, I decided to disable the HiWonder network setup script and re-do networking the "normal" way:

  ```
  systemctl disable hw_wifi
  echo "denyinterfaces eth0 wlan0 >> /etc/dhcpcd.conf"
  sudo apt-get purge isc-dhcp-client isc-dhcp-common
  sudo apt-get install dhcpcd5
  ```
  Now use e.g., `nano /etc/network/interfaces.d/wlan0` to contain:
  ```
  auto wlan0
  iface wlan0 inet dhcp
      wpa-ssid "ssid"
      wpa-psk "password"
  ```
  with the "ssid" and "password" for the network you want the robot to use.
  I use our low-sequrity 'internet of things' WIFI network for this.

At this point, try rebooting without a network cable attached, and see if the Raspberry PI connects as intended
(check your WIFI router logs/info section to see what IP number it gets).
Otherwise connect an ethernet cable, log in using ssh again using the new, changed, password and debug the network setup.
(again, after connecting the cable you need to check the IP number it gets from your WIFI router to know what to connect to).

## Assembly of the robot

HiWonder provides a [YouTube playlist](https://www.youtube.com/playlist?list=PLFbzd0m6AcmLzo53o2Tsa20BS350rWGMj) of assembly instructions. 
However, note that the videos for some reason are out of order, and quite a few feature videos are mixed in among the others which can make it difficult to work out precisely what to watch and in what order.

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

## First startup and shutdown

1. Make sure both the HiWionder board power switch and the battery compartment switch both are OFF.
2. Insert the, now charged, batteries. Make sure to insert them correctly - Li-ion batteries can be dangerous if used/mounted incorrectly.
3. Turn on the battery compartment power switch.
4. Turn on the HiWonder board power switch.
5. You should see LEDs coming on, and after a quite long while an audiable BEEP, indicating that the bootup process is done.

There are two tiny buttons marked "KEY1" and "KEY2" on the HiWonder board that can be reached through the hole in the top cover.

- "KEY1" runs a self test on all the motors and servos.
- Holding down "KEY2" for a couple of seconds gracefully (well, semi-gracefully - we will get to fixing that) shuts down the Pi.
  Regrettably there is no clear way to determine that it has worked, e.g., like turning off the LEDs.
  For now I suggest using `ssh <ip>` or `ping <ip>` from your computer to verify sure the Raspberry Pi computer has shut down.

Hence, to shut down the robot:

1. Press and hold "KEY2". Try to verify in some way that the robot actually has shut down (at least press "KEY1" to make sure that does not trigger a self-test).
2. Shut off the power switch on the HiWonder Pi board.
3. Shut off the power switch on the battery compartment.

## Installation and use of the mobile app

Our ultimate intent may be to build our own software for the robot, it is nice to verify that the functions work as intended using the official software.

Install the [WonderPi Android app published by Hiwonder](https://play.google.com/store/apps/details?id=com.Wonder.Pi)
(Perhaps overly cautious, I would suggest running this not on your main device but, e.g., one used for mobile gaming, etc.)

Connect your phone to the same WIFI network the TurboPi is connected to, start the app, and select "Turbo PI".

Note that the app doesn't work very relibably, especially if the network connection to/from the phone and the robot is not robust.
It is very easy for the robot to get stuck in a "moving" mode.
I wouldn't regard that as an issue with the product, just that this is demo software is meant to showcase the possibilities of this kit, and wasn't written as a fully robust production-level robot controller.

