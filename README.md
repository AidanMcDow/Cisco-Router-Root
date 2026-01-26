# Cisco-Router-Root

## This project is a personal project in order to practice some hardware hacking skills. 

This repo shows the process we went through in order to gain root access to a Cisco Linksys E1200 router.
### 1. Physical Inspection

Knowing what a serial connection generally looks like, this is always the go to first step for me.
After opening up the chassis there seems to be really only one area that has potential to give us a serial connection. In any serial connection you are going to see at least 4 connections, these include positive (usually 3.3 volts), ground, tx (transmit) and rx (receive).
In this case we actually see 5 total points, the 5th actually being a signal ground. This 5th pin is not important for what we are trying to do so we can ignore that connection for now.

<img width="565" height="568" alt="image" src="https://github.com/user-attachments/assets/fb14b5cb-4fd0-4d57-94af-af53a30429c8" />

Using a multimeter you can help confirm that the port in question is a serial port by checking for voltage. With the device plugged in we test to see if the contact point is producing 3.3 volts. We also test for the 2 grounded out contacts.
Confirming this increases the chances that what we are looking at, is in fact a serial port. From here we are going to want to confirm what the other 2 connecitons are for. This is where signal analysis comes into play.

### 2. Signal Analysis

As college students, an oscilloscope is much too far outside our budget. However you can find a cheap logic analyzer on amazon that will do exactly what we need it to.

<img width="1157" height="474" alt="image" src="https://github.com/user-attachments/assets/6b9d32b7-0a29-4d83-b154-6bddcb84123d" />


Connecting all of the contact points and booting up our free trial of logic 2 https://www.saleae.com/pages/downloads?srsltid=AfmBOopJTOCU2PV-4VGmJqXqi1jdSgK0Wkg6Ljopl69zwo3XhFBhTruT we see.

<img width="1699" height="893" alt="image" src="https://github.com/user-attachments/assets/a9edfce0-1884-47d0-bab4-ad592254e5db" />

Here we have 3 changes happen when the router is booted up. The top and bottom are going to be our power. The yellow connection however seems to be transmitting data, this confirms which conneciton is our tx. Through process of elimination we also now know our rx.

### 3. Bridge Connection

Now we connect everything together using the flipper zero. The flipper has GPIO pins on top and an app that creates a bridge between UART to USB. Connecting it all together we create a usb connection to our serial port on the router.

![PXL_20250721_225140893 MP](https://github.com/user-attachments/assets/2e8a7982-a86b-48b1-96d9-71629db1c7b5)

Using screen on linux we can open a shell on the device. After running sudo screen /dev/ttyACM0 115200 we get a confirmation that we have connected to the light version of linux running on the router called busybox.
![PXL_20250721_232437528](https://github.com/user-attachments/assets/d20054c1-750a-4fa2-ad77-75b493adc26c)


We now have a root access terminal for the router!



