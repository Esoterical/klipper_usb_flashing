---
layout: default 
title: BigTreeTech EBB42 Gen2
parent: Hardware Configurations
---

# USB Mode

To put the EBB36 Gen2 into CAN mode (instead of USB mode) make sure to **remove** any jumper on the USB/CAN header

<img width="655" height="478" alt="image" src="https://github.com/user-attachments/assets/6d3c9f5d-413d-4588-b8c5-5804552e4c3c" />


# DFU Mode

To put the EBB42 Gen2 into DFU mode first power off the printer then connect the main CAN/Power cable from the EBB42 Gen2 to the breakout board that goes in your electronics bay.

Then make sure you have power connected to this breakout board as well, and then connect a USB cable from your Pi to the breakout board. 

Then power up the system and on the EBB42 Gen2 board hold the BOOT button, press and release the RST button, then count to 5 and release the BOOT button.

<img width="715" height="402" alt="image" src="https://github.com/user-attachments/assets/6085f87d-8462-4454-a477-e9b3f02263b0" />


# Katapult Config

<img width="754" height="274" alt="image" src="https://github.com/user-attachments/assets/af504c9a-43db-487f-b018-64ebe42ab554" />


# Klipper Config

<img width="717" height="238" alt="image" src="https://github.com/user-attachments/assets/a6c27dec-c665-49af-b764-c8d7ccc1b10f" />


# Sample Configuration

A sample configuration file can be found at [https://github.com/bigtreetech/EBB/blob/master/EBB_GEN2/EBB42_GEN2/sample-bigtreetech-ebb42-gen2-v1.0.cfg](https://github.com/bigtreetech/EBB/blob/master/EBB_GEN2/EBB42_GEN2/sample-bigtreetech-ebb42-gen2-v1.0.cfg)
