---
layout: default 
title: Fysetc H36
parent: Hardware Configurations
---


# USB Mode

To put the H36 board into USB mode (instead of CAN mode) you simply need to make sure the Katapult and Klipper firmware settings (further down below) have the 
"GPIO pins to set at micro-controller startup" set correctly. For CAN mode this needs to be `PA2`



# DFU Mode

To put the H36 into DFU mode, connect it via USB to the Pi using the USB-C port then hold the BOOT0 button, press and release the RESET button, then count to 5 and release the BOOT0 button.

![image](https://github.com/user-attachments/assets/a1a101a7-bfba-4d49-aaa6-bb22278ca1f3)




# Katapult Config

![image](https://github.com/user-attachments/assets/cb1d9e0b-1e78-492a-9dda-eb0f8ea8f967)



# Klipper Config

![image](https://github.com/user-attachments/assets/adc41c64-aac8-4cae-82d6-ad12fc3602f2)


# Sample Config

A sample config file can be found at [https://github.com/FYSETC/H36_Combo/tree/main
](https://github.com/FYSETC/H36_Combo/tree/main)

# More Info

More information can be found at the [H36 wiki](https://wiki.fysetc.com/docs/H36-Combo)
