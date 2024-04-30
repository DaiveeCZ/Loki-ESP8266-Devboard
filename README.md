Preparation:

    - Install Arduino IDE and USB drivers. 
    - Prepare support for ESP8266 using this tutorial: https://navody.dratek.cz/technikuv-blog/jak-nainstalovat-podporu-pro-esp8266-do-arduino-ide.html






Upload the program to the board:

To load the program to the board, press and hold the FLASH button + briefly press the RESET button. If the RGB LED turns white, the board has successfully switched to FLASH mode. 

We can then load the program. After uploading, the board should reset itself, but it is recommended to press the RESET button. The board will reset itself, and should be running the currently loaded program.

USB-UART switch:

If for any reason the USB converter on the board cannot be used, it can be hardware disconnected using the DIP switch on the board. In the basic ON position, the integrated USB-TTL converter is connected. In the opposite position, it is possible to record or monitor the serial console using the UART connector (next to the GPIO).
Note: Both switches in the DIP switches must always be in the same position! (i.e. either both on ON, or both in the other position - OFF.)

Connectors and peripherals on the board:

    - GPIO pinheader - 8x Digital I/O, 1x Analog I/O (ADC), 5V, 3V3, GND.
    - UART header - TX,RX,GND,3V3 - can only be used if the DIP switch is switched in the OFF position.

RGB LED connection:

R - GPIO14 (D5)
G - GPIO13 (D7)
B - GPIO12 (D6)

IR Receiver connection: GPIO4 (D2)

UART connection:

TX: GPIO1
RX: GPIO3

Indication LED:

Blue - 5V (USB) OK.
Lights red - 3.3V (5V→3.3V controller or externally from UART con.) OK.
Flashing green - Active communication via UART -TX (e.g. when recording prog.)
Flashing yellow - Active communication via UART -RX (e.g. when recording prog.)
(Flashing intensity/brightness may vary depending on the task.)

Additional information:

Some libraries require a special version compared to the classic Arduino libraries, e.g. the library for the IR receiver is IRremote.h as standard for this board but you need to select IRremoteESP8266.h for the IR receiver to work properly.

Arduino IDE Settings:

Select the board in Tools->Board->esp8266.

The board must be selected LOLIN(WEMOS) D1 mini (clone).

If there is only Arduino AVR Boards in the Board submenu and the esp8266 entry is missing, check the procedure from the preparation section - specifically the procedure in the URL link.

Translated with DeepL.com (free version)
