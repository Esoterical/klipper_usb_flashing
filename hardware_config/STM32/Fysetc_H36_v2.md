---
layout: default 
title: Fysetc H36 V2
parent: Hardware Configurations
---


# USB Mode

To put the H36 V2 board into USB mode (instead of CAN mode) you simply need to make sure the Katapult and Klipper firmware settings (further down below) have the 
"GPIO pins to set at micro-controller startup" set correctly. For CAN mode this needs to be `PA2`



# DFU Mode

To put the H36 V2 into DFU mode, connect it via USB to the Pi using the USB-C port then hold the BOOT0 button, press and release the RESET button, then count to 5 and release the BOOT0 button.

![image](https://github.com/user-attachments/assets/a1a101a7-bfba-4d49-aaa6-bb22278ca1f3)




# Katapult Config

<img width="762" height="236" alt="image" src="https://github.com/user-attachments/assets/4e118401-dc9f-431b-a984-03b673f2b6dc" />




# Klipper Config

<img width="741" height="195" alt="image" src="https://github.com/user-attachments/assets/56f180e3-db03-4cd7-a9ad-9cdb8c470c51" />



# Sample Config

A sample config file can be found at [https://github.com/FYSETC/H36_Combo_V2/tree/main
](https://github.com/FYSETC/H36_Combo_V2/tree/main)

# More Info

More information can be found at the [H36 V2 wiki](https://wiki.fysetc.com/docs/H36-Combo-V2)
