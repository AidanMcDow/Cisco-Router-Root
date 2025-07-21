# Cisco-Router-Root

# This project is a personal project in order to practice some hardware hacking skills. 

This repo shows the process we went through in order to gain root access to a Cisco Linksys E1200 router.
1. Physical Inspection

Knowing what a serial connection generally looks like, this is always the go to first step for me.
After opening up the chasis there seems to be really only one area that has potential to give us a serial connection. In any serial connection you are going to see at least 4 connections, these include positive (usually 3.3 volts), ground, tx (transmit) and rx (recieve).
In this case we actually see 5 total points, the 5th actually being a signal ground. This 5th pin is not important for what we are trying to do so we can ignore that connection for now.

Using a multimeter you can help confirm that the port in question is a serial port by checking for voltage. With the device plugged in we test to see if the contact point is producing 3.3 volts. We also test for the 2 grounded out contacts.

Confirming this increases the chances that what we are looking at, is in fact a serial port. From here we are going to want to confirm what the other 2 connecitons are for. This is where signal analysis comes into play.

2. Signal Analysis

As college students, an osciliscope is much too far outside our budget. However you can find a cheap logic analyzer on amazon that will do exactly what we need it to.

Connecting all of the contact points and booting up our free trial of logic 2 https://www.saleae.com/pages/downloads?srsltid=AfmBOopJTOCU2PV-4VGmJqXqi1jdSgK0Wkg6Ljopl69zwo3XhFBhTruT we see.

Tracing back these connections we can see that one is sending out data. This pin is going to be our tx pin, and the only other pin left will in turn be our rx connection. 

Bridge Connection

Connected Flipper Zero to the UART header (TX/RX/GND only, avoiding VCC).

Connected Flipper to a computer as a USB serial interface.

Accessing the Interface

Used screen on Linux to connect to the serial port (e.g., screen /dev/ttyACM0 115200).

Sent ? to the interface, which triggered a debug or diagnostic shell.
