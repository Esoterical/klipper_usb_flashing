---
layout: default 
title: Fysetc SB Combo V2
parent: Hardware Configurations
---

# Safety

The Combo V2 board (at the time of writing, 12th of October 2024) doesn't ship with any protection board for the USB connection to your Pi. If you plug it directly in to the USB ports of your Pi there is a risk that 
if something goes wrong with your wiring (it gets caught up or damaged or cracks or whatever) then there could be a voltage spike that has the potential to damage the USB circuitry on the Raspberry Pi, stopping the 
USB from working or destroying the Pi outright.

A simple solution I've found is an isolation board using the [ADUM3160](https://www.aliexpress.com/w/wholesale-ADUM3160.html) usb isolator chip. They are pretty cheap (around 9 Australian dollars) and no doubt they
can be found in all the usual online marketplaces.

![image](https://github.com/user-attachments/assets/a7699202-c086-445f-bf38-3eba58d2868e)

The only tweak needed for this particular ADUM-based board is to bridge the GND pins from the Pi side to the ComboV2 side. This is because the cable supplied with the Combo V2 board isn't connecting the shield wire
(which is at the JST that connects to the USB adapter) to the rest of the DC GND. So you need to provide this connection yourself.
It's simple to do, and doesn't stop the ADUM board from doing its job. You can solder a wire from the outside casing of the USB ports themselves, or from the USB GND pins (just test first to make sure you have the 
correct pins).

![image](https://github.com/user-attachments/assets/dc7af9cb-456d-484a-8e65-3551f0dcf131)


# USB Mode

To put the SB Combo V2 board into USB mode (instead of CANBUS mode) make sure the two switches are in the "down" position.

![image](https://github.com/user-attachments/assets/a5be3ceb-fa40-41a5-a245-058a7c04f866)



# DFU Mode

To put the SB Combo V2 into DFU mode, connect it via USB to the Pi (either by the main cable, or by the USB-C port) then hold the BOOT0 button, press and release the RESET button, then count to 5 and release the BOOT0 button.

![image](https://github.com/user-attachments/assets/922c0f4f-9b4a-44d5-b636-77b9678f62f1)



# Katapult Config

![image](https://github.com/user-attachments/assets/1b74e630-9896-4240-b50e-49419b0b0982)



# Klipper Config

![image](https://github.com/user-attachments/assets/07166d06-09c7-46aa-8448-3f5f27e415df)


# Sample Config

A sample config file can be found at https://github.com/FYSETC/SB_Combo_V2/tree/main/Config

# More Info

More information can be found at the [SB Combo V2 wiki](https://wiki.fysetc.com/SB_Combo_V2/)
