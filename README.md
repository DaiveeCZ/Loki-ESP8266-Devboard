# Loki ESP8266 Devboard
![3Dview](https://github.com/DaiveeCZ/Loki-ESP8266-Devboard/assets/83717170/4bbd93d6-83de-41da-8776-aaefae6c5671)

This repo was created as a remnant of a project that was never realized. It was supposed to be a device containing RGB LEDs that could be controlled with an IR controller and also with Wi-Fi.
The repo contains documentation for the prototyping board for this project. The board has actually been assembled and used and works quite well.
This repo also contains the basic test FW in .img format. In this firmware only control via IR remote is implented.

## Connectors and peripherals on the board:

- GPIO pinheader - 8x Digital I/O, 1x Analog I/O (ADC), 5V, 3V3, GND.
- UART header - TX,RX,GND,3V3 - can only be used if the DIP switch is switched in the OFF position.

### RGB LED connection:

- R - GPIO14 (D5)
- G - GPIO13 (D7)
- B - GPIO12 (D6)

### IR Receiver connection: 

- GPIO4 (D2)

### UART connection:

- TX: GPIO1
- RX: GPIO3

### Indication LEDs:

- Blue - 5V (USB) OK.
- Red - 3.3V (5V→3.3V controller or externally from UART con.) OK.
- White (RGB 5050 LED) - Flash mode
- Flashing green - Active communication via UART -TX (when flashing prog.)
- Flashing yellow - Active communication via UART -RX (when flashing prog.)

*(Flashing intensity/brightness may vary depending on the task.)*

## Flashing testing img file:

The testing firmware (loki_v15.img) has the codes programmed in it for a cheap Chinese IR remote. The codes were read directly from the remote using [LIRC](https://www.lirc.org).

![irremote](https://github.com/DaiveeCZ/Loki-ESP8266-Devboard/assets/83717170/d4ab22de-78ea-4434-bb0c-1542a8a3fbb1)

### Preparation:
- Install [CH340 USB drivers](https://github.com/HobbyComponents/CH340-Drivers) 
- Download latest [esptool](https://github.com/espressif/esptool/releases).
- Extract from esptool-vx.x.x-xxx.zip esptool to the folder of your choice.
- Copy the img file to this folder.
### Flashing:
- Press and hold the FLASH button + briefly press the RESET button. If the RGB LED turns white, the board has successfully switched to FLASH mode.
- Open command line and write:

      esptool write_flash 0x00000 loki_v15.img

- Then press enter to start the flash process.

- If the process aborts for any reason, I recommend deleting the entire memory using:

      esptool erase_flash

And then try flash again.

## Flashing board via Arduino IDE:

### Preparation:

- Install Arduino IDE and USB drivers. 
- Prepare support for ESP8266 using this tutorial: https://randomnerdtutorials.com/installing-esp8266-nodemcu-arduino-ide-2-0/

### Arduino IDE Settings:

Select the board in Tools->Board->esp8266.

The board must be selected LOLIN(WEMOS) D1 mini (clone).

If there is only Arduino AVR Boards in the Board submenu and the esp8266 entry is missing, check the procedure from the preparation section - specifically the procedure in the URL link.

### Upload the program to the board:

To load the program to the board, press and hold the FLASH button + briefly press the RESET button. If the RGB LED turns white, the board has successfully switched to FLASH mode. 

We can then load the program. After uploading, the board should reset itself, but it is recommended to press the RESET button. The board will reset itself, and should be running the currently loaded program.

### USB-UART switch:

If for any reason the USB converter on the board cannot be used, it can be hardware disconnected using the DIP switch on the board. In the basic ON position, the integrated USB-TTL converter is connected. In the opposite position, it is possible to program or monitor the serial console using the UART connector (next to the GPIO).

**Both switches in the DIP switches must always be in the same position! (i.e. either both on ON, or both in the other position - OFF.)**

### Additional information:

Some libraries require a special version compared to the classic Arduino libraries, e.g. the library for the IR receiver is IRremote.h as standard for this board but you need to select IRremoteESP8266.h for the IR receiver to work properly.



