# Cisco Linksys E1200: UART Exploitation and Root Access

## Project Overview
This project demonstrates the process of identifying, analyzing, and exploiting a physical serial interface on a Cisco Linksys E1200 router. The goal was to gain low-level system access through hardware-level debugging interfaces.

### 1. Physical Reconnaissance
The first step involved opening the chassis to inspect the PCB for potential debug headers. I identified a 5-pin layout commonly used for serial communication. Using a multimeter, I mapped the pinout by:

- Identifying Ground (GND) through continuity testing.
- Locating the VCC (3.3V) rail.
- Isolating potential TX/RX pins for signal analysis.

<img width="565" height="568" alt="image" src="https://github.com/user-attachments/assets/fb14b5cb-4fd0-4d57-94af-af53a30429c8" />

### 2. Logic Analysis & Signal Validation
To confirm the data pins without the risk of blind trial-and-error, I used a logic analyzer. By capturing the boot sequence in Logic 2, I observed:

- Periodic signal bursts on the TX (Transmit) line, confirming the router was sending bootloader data.
- Voltage levels consistent with 3.3V TTL logic.


Here we have 3 changes happen when the router is booted up. The top and bottom are going to be our power. The yellow connection however seems to be transmitting data, this confirms which conneciton is our tx. Through process of elimination we also now know our rx.

### 3. Establishing the Bridge
I utilized a Flipper Zero as a UART-to-USB bridge to interface the router's hardware with my workstation.

- Connection: Wired the router’s GND, TX, and RX to the Flipper Zero’s GPIO.
- Interface: Used the screen utility on Linux to establish a connection.

![PXL_20250721_225140893 MP](https://github.com/user-attachments/assets/2e8a7982-a86b-48b1-96d9-71629db1c7b5)

### Result: Root Access
Upon successful connection, I gained access to the BusyBox environment. Sadly, this router is not powerful enough to run OpenWRT. However this provided a full root terminal, allowing for deep-system inspection and the ability to analyze the router's internal firmware operations in real-time.



