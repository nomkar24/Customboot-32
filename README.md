<h1 align="center">CustomBoot-32</h1>

<h2 align="center">SRA Eklavya 2025</h2>

## Table of Contents
* [About the Project](#about-the-project)  
  - [Aim](#aim)  
  - [Description](#description)  
  - [Tech-Stack](#tech-stack)  
  - [File Structure](#file-structure)  
* [Getting Started](#getting-started)  
  - [Installation](#installation)  
* [Usage](#usage)  
* [Results and Demo](#results)  
* [Report](#report)
* [Troubleshooting](#troubleshooting)  
* [Contributors](#contributors)  
* [Mentors](#mentors)  
* [Resources](#resources)  
* [Acknowledgements](#acknowledgements)  

---

# About the Project

## Aim
Designing a custom PCB with OTA support and a dual-image Bootloader using ESP32 WROOM-32E and STM32F103C8T6.

## Description
The project focuses on creating a custom PCB that integrates the Blue Pill (STM32F103C8T6) with ESP32 WROOM-32E.  
The ESP32 hosts a website, receives two firmwares via OTA, creates memory partitions, and initializes a File System in one of the partitions.  

On the STM side, a dual-image Bootloader requests firmware based on user input, verifies it, allocates it in flash memory, and executes it.  
The firmware transfer is carried out via **UART**.

## Tech-Stack

### Languages & Frameworks
![Embedded C](https://img.shields.io/badge/Language-Embedded_C-FF6F3C?style=for-the-badge&logo=c&logoColor=white)
![ESP-IDF](https://img.shields.io/badge/Framework-ESP--IDF-E7352C?style=for-the-badge&logo=espressif&logoColor=white)

### Libraries & Tools
![STM32 HAL](https://img.shields.io/badge/Library-STM32_HAL-00599C?style=for-the-badge&logo=stmicroelectronics&logoColor=white)
![LibOpenCM3](https://img.shields.io/badge/Library-LibOpenCM3-410099?style=for-the-badge&logo=c&logoColor=white)
![KiCad](https://img.shields.io/badge/Hardware-KiCad-314CB6?style=for-the-badge&logo=kicad&logoColor=white)

### Protocols & File System
![UART](https://img.shields.io/badge/Protocol-UART-333333?style=for-the-badge)
![OTA Updates](https://img.shields.io/badge/Protocol-OTA_Updates-E7352C?style=for-the-badge&logo=espressif&logoColor=white)
![SPIFFS](https://img.shields.io/badge/File_System-SPIFFS-FF6F3C?style=for-the-badge)


## File Structure

```
.
├── assets  # All images and test videos
│   ├── 2WayUART.mp4
│   ├── 3D-view back.png
│   ├── 3D-view.png
│   ├── EmbedC.png
│   ├── Final_PCB.png
│   ├── HAL.png
│   ├── LibOpenCM3.png
│   ├── OTA.png
│   ├── PCBSC1.png
│   ├── PCBSC2.png
│   ├── Routing.png
│   ├── SimpleBootloader.mp4
│   ├── SPIFFS.png
│   ├── UART.png
│   ├── website.png
│   ├── Wireless_CMD_Test.mp4
│   └── WorkingVideo.mp4
├── CustomBoot-32  # All the firmwares for both ESP as well as STM
│   ├── 1. OTA
│   ├── 2. Dual_Image_Bootloader
│   ├── 3. ESP_STM_UART1
│   ├── 4. ESP_STM_UART2
│   ├── 5. ESP_TO_STM_FIRMWARE_VIA_UART
│   ├── 6. ESP_STM_FILE_CRC
│   ├── 7. Controling_ESP_GPIO_Wirelessly
│   └── 8. Wireless_Firmware_Selection_ESP_STM(Additional)
├── Documentation  # Detailed documentation of the project
│   └── Final_DOC.pdf
├── Gerber files  # Files made for fabrication of PCB  
├── README.md
└── Schematic files  # Schematics of our PCB
    ├── 4 SRA.kicad_pcb
    └── 4 SRA.kicad_sch
```

---

## Getting Started

### Installation
1. Clone the repo  
   ```bash
   git clone https://github.com/avm1234567/Customboot-32.git
   ```
2. Navigate to the project directory  
   ```bash
   cd CustomBoot-32
   ```

---

## Usage

The codes used in our project are in the `CustomBoot-32` directory. 

### 1. OTA

- From the `CustomBoot-32` directory, navigate to the `OTA` directory:
```bash
cd CustomBoot-32/1.\ OTA
```

- In the code, set your Wi-Fi SSID and password (lines 16-17):
```c
#define WIFI_SSID "Your_SSID"
#define WIFI_PASS "Your_Password"
```

- Build using ESP-IDF PowerShell:
```bash
idf.py fullclean
idf.py build
```

- Flash and open the serial monitor:
```bash
idf.py flash monitor 
```

### 2. Dual_Image_Bootloader

- To generate the binary files, open this project in STM32CubeIDE and build it.
- To flash this code, use STM32CubeProgrammer:
  1. Flash `LED_BLINK_2.bin` at start address `0x08006000`:
     `CustomBoot-32/2. Dual_Image_Bootloader/LED_BLINK_2/Debug/LED_BLINK_2.bin`
  2. Flash `LED_BLINK.bin` at start address `0x08004000`:
     `CustomBoot-32/2. Dual_Image_Bootloader/LED_BLINK/Debug/LED_BLINK.bin`
  3. Flash the Bootloader at start address `0x08000000`:
     `CustomBoot-32/2. Dual_Image_Bootloader/Learning_Bootloader/Debug/Learning_Bootloader.bin`
- Click **Start Programming** to run.

### 3. ESP_STM_UART1

- For the ESP32 code:
```bash
cd CustomBoot-32/3.\ ESP_STM_UART1/ESP_STM_COMM
idf.py fullclean
idf.py build
idf.py flash monitor 
```

- For the STM32 code, generate build files in STM32CubeIDE and flash the binary using STM32CubeProgrammer at address `0x08000000`.

### 4. ESP_STM_UART2

- For the ESP32 code:
```bash
cd CustomBoot-32/4.\ ESP_STM_UART2/ESP_STM_COMM
idf.py fullclean
idf.py build
idf.py flash monitor 
```

- For the STM32 code, generate build files in STM32CubeIDE and flash the binary using STM32CubeProgrammer at address `0x08000000`.

### 5. ESP_TO_STM_FIRMWARE_VIA_UART

- For the ESP32 code:
```bash
cd CustomBoot-32/5.\ ESP_TO_STM_FIRMWARE_VIA_UART/OTA
idf.py build
idf.py flash monitor 
```

- For the STM32 code, build in STM32CubeIDE and flash the binary found at `CustomBoot-32/5. ESP_TO_STM_FIRMWARE_VIA_UART/Learning_Bootloader/Debug/Learning_Bootloader.bin` at address `0x08000000`.

### 6. ESP_STM_FILE_CRC

- Clone `libopencm3` required for the bootloader:
```bash
git clone https://github.com/libopencm3/libopencm3.git
cd libopencm3
```

- Flash the ESP32 firmware:
```bash
cd CustomBoot-32/6.\ ESP_STM_FILE_CRC/OTA
idf.py fullclean
idf.py build flash monitor
```

### 7. Controlling_ESP_GPIO_Wirelessly

- Clean, build, and flash:
```bash
cd CustomBoot-32/7.\ Controling_ESP_GPIO_Wirelessly
idf.py fullclean
idf.py build
idf.py flash monitor
```

### 8. Wireless_Firmware_Selection

- Clone `libopencm3` required for the bootloader:
```bash
git clone https://github.com/libopencm3/libopencm3.git
cd libopencm3
```

- Flash the ESP32 firmware:
```bash
cd CustomBoot-32/8.\ Wireless_Firmware_Selection_ESP_STM\(Additional\)/OTA
idf.py fullclean
idf.py build flash monitor
```

---

## Results

**Custom PCB Views:**  

| Front | Back |
| ----- | ---- |
| ![Front](assets/PCBSC1.png) | ![Back](assets/PCBSC2.png) |

<img src="assets/Final_PCB.png" alt="Actual PCB" width="800">

## Demo

[Working Demo of Final PCB](https://drive.google.com/file/d/1Z0VfDI0KjEA28zM6vQ-hMSaG2jekwzWR/view?usp=drive_link)  

For other results and test videos, check the [Google Drive Folder](https://drive.google.com/file/d/1JogM4m4yME66ZIJGMlyX8mcmxp7ndMSk?usp=drive_link).

## Report

Refer to the detailed project [Report](https://drive.google.com/file/d/13CS2zIfVXfLGR-wP4OjCv9lpuOwN3wu8/view?usp=drive_link).

## Troubleshooting

* ERC rule check errors in PCB schematics.  
* Routing issues in compact areas while adhering to manufacturer constraints.  
* Wi-Fi SSID and password options not appearing in Menuconfig.  
* CMakeLists errors affecting SPIFFS initialization.  
* Partition table not being detected.  
* SPIFFS initialization failure at runtime.  
* Favicon loading errors.  
* OTA binaries containing unnecessary bloatware.  
* UART initialization issues.  
* Binary file transfer failures.  
* Errors in custom file protocol implementation.  
* End-byte transmission errors during communication.  
* Application jump not functioning correctly (MSP not set).  
* Correct HAL-like application jump with LibOpenCM3.  
* Schematic issues resolved through perfboard prototyping and testing.  

---

## Contributors

* [Varun Patil](https://github.com/varun05050505)  
* [Omkar Nanajkar](https://github.com/nomkar24)  
* [Archit More](https://github.com/avm1234567)  

## Mentors

* [Prithvi Tambewagh](https://github.com/rkt-1597)  
* [Shaunak Datar](https://github.com/ShaunakKDatar)  
* [Vishal Mutha](https://github.com/Vishal-Mutha)  

---

## Resources

- [Bootloader basics (EmbeTronicx)](https://embetronicx.com/tutorials/microcontrollers/stm32/bootloader/bootloader-basics/)  
- [EmbeddedInventor: Bootloader](https://embeddedinventor.com/embedded-bootloader-and-booting-process-explained/)  
- [Getting Started with STM32](https://youtube.com/playlist?list=PLNyfXcjhOAwO5HNTKpZPsqBhelLF2rWQx)  
- [Bare-metal UART STM32](https://vivonomicon.com/2020/06/28/bare-metal-stm32-programming-part-10-uart-communication/)  
- [ESP32 UART](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/peripherals/uart.html)  
- [CRC32 for STM](https://www.st.com/resource/en/application_note/an4187-using-the-stm32-hardware-crc-unit-stmicroelectronics.pdf)  
- [LibOpenCM3 documentation](https://libopencm3.org/docs/latest/stm32f1/html/modules.html)
- [SPIFFS](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/storage/spiffs.html)  
- [FreeRTOS](https://my-esp-idf.readthedocs.io/en/latest/api-guides/freertos-smp.html#tasks-and-task-creation)  
- [ESP Web Server Handling](https://esp32tutorials.com/esp32-web-server-esp-idf/)  
- [File Transfer Protocols](https://www.geeksforgeeks.org/computer-networks/xmodem-file-transfer-protocol/)

---

## Acknowledgements

We are extremely grateful to our mentors – **Prithvi Tambewagh, Shaunak Datar, and Vishal Mutha** – for their guidance and support throughout the course of this project.  

We also thank [SRA-VJTI](https://sravjti.in/) for their support in organizing [Eklavya 2025](https://sravjti.in/projects/eklavya/) and for providing us the opportunity to work on this project.  
