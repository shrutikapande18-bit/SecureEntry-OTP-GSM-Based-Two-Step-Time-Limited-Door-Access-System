# 🔐 SecureEntry OTP – GSM-Based Two-Step Time-Limited Door Access System

## 📌 Project Overview

SecureEntry OTP is an embedded security system developed using the **ARM7 LPC2148 microcontroller**. It implements a two-step authentication mechanism to provide secure door access using a unique User ID, password, and a time-limited One-Time Password (OTP).

The system uses a GSM module to send OTPs to the registered mobile number of the user. Access is granted only after successful OTP verification within the specified time limit.

It also provides SMS-based remote access control, allowing registered users to remotely block or unblock their user IDs.

##  Project Objectives

-  Implement secure two-step door authentication.
-  Authenticate users using a unique User ID and password.
-  Generate and send time-limited OTPs through GSM.
-  Store user credentials in external SPI EEPROM.
-  Enable remote access blocking through SMS.
-  Allow registered users to unblock access remotely.
-  Support password and registered mobile number modification.

## ✨ Key Features

-  **Two-Step Authentication:** User ID and password verification followed by OTP verification.
-  **Time-Limited OTP:** OTP validity is limited to a predefined period (60 seconds in the example).
-  **GSM Communication:** Sends OTP messages and receives remote control SMS commands.
-  **Remote Access Blocking:** Registered users can send `BLOCK <UserID>`.
-  **Remote Access Unblocking:** Registered users can send `UNBLOCK <UserID>`.
-  **EEPROM Data Storage:** Stores user passwords and registered mobile numbers.
-  **Credential Modification:** Allows users to update passwords and registered mobile numbers.
-  **Interrupt-Based Operations:** Uses UART interrupts for GSM communication.

##  Hardware Requirements

| Component | Purpose |
|---|---|
|  LPC2148 ARM7 | Main microcontroller |
|  SIMCOM A7662 GSM Module | SMS communication |
|  16x2 LCD | Displaying system messages |
|  4x4 Matrix Keypad | User input |
|  AT25LC512 SPI EEPROM | Credential storage |
|  LED / DC Motor with L293D | Access indication / door mechanism |
|  Switch | Interrupt-based operation |

## 💻 Software Requirements

- Embedded C
- Keil C Compiler
- Flash Magic
- UART Interrupt Programming
- SPI Communication

##  Technologies & Concepts Used

- ARM7 Architecture (LPC2148)
- Embedded C Programming
- UART Communication
- UART Interrupts
- SPI Protocol
- GSM AT Commands
- External EEPROM Interfacing
- Matrix Keypad Interfacing
- LCD Interfacing
- Real-Time Clock (RTC)
- External Interrupts
- OTP Generation and Verification

## 🔄 System Working Principle

### 1️⃣ User Identification
The system prompts the user to enter a unique User ID through the 4x4 matrix keypad.

### 2️⃣ Password Verification
The entered password is compared with the corresponding password stored in external EEPROM.

### 3️⃣ OTP Generation 📲
After successful password verification, the system generates an OTP and sends it to the registered mobile number using the GSM module.

### 4️⃣ OTP Verification 🔐
The user enters the received OTP through the keypad.

- ✅ Correct OTP within the validity period: Access Granted.
- ❌ Incorrect or expired OTP: Access Denied and authentication restarts.

### 5️⃣ Remote Access Blocking 🚫
Registered users can send:

`BLOCK <UserID>`

The system validates the sender's registered mobile number and user ID before blocking access. Any pending OTP associated with that user is cancelled.

### 6️⃣ Remote Access Unblocking 🔓
Registered users can send:

`UNBLOCK <UserID>`

After successful validation, the user can request a new OTP by completing the authentication process again.

### 7️⃣ User Details Modification 🛠️
When an external interrupt occurs, the system enters user-details modification mode.

After verifying the fixed User ID and existing password, users can update:
- 🔑 Password
- 📱 Registered mobile number

Updated information is stored in predefined EEPROM locations assigned to that user ID.

## 📡 GSM AT Commands Used

| AT Command | Function |
|---|---|
| `AT` | Check GSM module response |
| `ATE0` | Disable command echo |
| `AT+CMGF=1` | Set SMS text mode |
| `AT+CNMI=2,1,0,0,0` | Configure incoming SMS notifications |
| `AT+CMGD=1` | Delete SMS from memory |
| `AT+CMGR=1` | Read SMS from memory |
| `AT+CMGS="Mobile Number"` | Send SMS |

⚡ **Important:** The system checks the GSM response after each AT command. Further commands are processed only after receiving a positive response.

GSM interfacing is implemented using UART interrupts.

## 📩 Example SMS Commands

**OTP and Access Alert**
```text
SecureEntry: Access requested for U101.
OTP: 482731. Valid for 60 seconds.
```

**🚫 Blocking Command**
```text
BLOCK U101
```

**🔓 Unblocking Command**
```text
UNBLOCK U101
```
## System Working Flow Diagram
<img width="1031" height="616" alt="Untitled - Visual 1" src="https://github.com/user-attachments/assets/87a5ef8f-d6b0-48f6-962c-b1713d8db5b1" />


## Project Modules

| File | Description |
|---|---|
| `lcd.c / lcd.h` | LCD interfacing |
| `delay.c / delay.h` | Delay functions |
| `uart.c / uart.h` | UART communication |
| `keypad.c / keypad.h` | Keypad interfacing |
| `spi.c / spi.h` | SPI communication |
| EEPROM functions | Byte write and byte read operations |
| GSM functions | GSM initialization, SMS reception and transmission |
| `projectmain.c` | Main application logic |

##  Project Implementation

The project follows a modular development approach:

1. 🖥️ LCD interfacing and display testing.
2. ⌨️ Keypad interfacing and key detection.
3. 💾 SPI EEPROM byte write and byte read operations.
4. ⚡ External interrupt testing.
5. 🕒 RTC interfacing and display.
6. 🔄 UART transmission and reception using interrupts.
7. 📡 GSM initialization and AT command testing.
8. 📩 GSM SMS transmission and reception.
9. 🔧 Integration of all peripherals into the main application.
10. 🔐 Implementation of authentication, OTP verification and remote access control.


## 📚 Learning Outcomes

Through this project, I gained practical experience in:

-  ARM7 LPC2148 microcontroller programming.
-  Embedded C development.
-  Peripheral interfacing and hardware integration.
-  UART and SPI communication protocols.
-  Interrupt-driven programming.
-  GSM communication using AT commands.
-  External EEPROM data storage.
-  Authentication and access-control logic.
-  Modular embedded software development.

SecureEntry OTP – GSM-Based Two-Step Time-Limited Door Access System LPC2148 ARM7 • Embedded C • RTC • LCD • Keypad • SPI EEPROM • DC Motor • GSM • UART
• Interrupts • Proteus 
