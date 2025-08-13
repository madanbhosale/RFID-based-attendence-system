# RFID-Based Attendance System (LPC2148)

## Overview
This project is an **RFID-based attendance system** using the **LPC2148 ARM7 microcontroller**.  
It can read RFID cards, log attendance with date & time, and send the data to a **Linux-based PC** for storage in a `.csv` database.

## Features
- Reads RFID cards via UART1.
- Differentiates between **Admin** and **User** cards.
- Stores Admin card in **EEPROM** (non-volatile memory).
- Displays messages and date/time on **16x2 LCD**.
- Allows Admin to:
  - Change Admin card.
  - Update RTC (time/date).
- Communicates with PC via UART0 for database updates.

## Hardware Used
- LPC2148 microcontroller
- RFID Reader + RFID Cards
- 16x2 LCD
- 4x4 Keypad
- AT25LC512 SPI EEPROM
- MAX232 Level Converter
- USB-to-UART Converter
- Push Button (Admin menu trigger)

## Software Used
- Keil uVision (Embedded C)
- Flash Magic (Programming LPC2148)
- Linux (C program for database integration)

## How It Works
1. On startup, the system loads the Admin card number from EEPROM.
2. In idle mode, it shows `"RFID ATTENDANCE"` and real-time clock.
3. When a card is scanned:
   - **Admin card** → Sends `A<card_number>$` to PC for user management.
   - **User card** → Sends `U<card_number>,<date>$` to PC for attendance logging.
4. PC updates a `.csv` file and sends back a response to display on the LCD.
5. Admin menu can be accessed via a button press + password.
