# ESP32 TTGO T-Display + LVGL v9.3 Demo

This project demonstrates a simple "Hello LVGL 9.3!" interface on a TTGO T-Display v1.1 (ESP32 with ST7789 SPI display), using **ESP-IDF v5.4.1** and **LVGL v9.3**. It directly integrates LVGL without `esp_lvgl_port`, using only timers for rendering and ticking.

## 🎓 Educational context
This project is used in the first-year Embedded Systems course for Applied Computer Science at The Hague University of Applied Sciences. It helps students understand how to directly drive an SPI-based TFT display and integrate LVGL without extra abstraction layers.

## 🔧 Hardware

- **Board**: [TTGO T-Display v1.1 (ESP32-WROOM-32)](https://lilygo.cc/products/lilygo%C2%AE-ttgo-t-display-1-14-inch-lcd-esp32-control-board)
- **Display**: 240×135 ST7789 (16-bit color via SPI)
- **Wiring** (display is hard wired to the T-display PCB):
  - MOSI → GPIO19
  - SCLK → GPIO18
  - CS   → GPIO5
  - DC   → GPIO16
  - RST  → GPIO23
  - BL   → GPIO4 (backlight)

---

## 📦 Installation

### 1. Install ESP-IDF

You probably installed Visual Studio Code (VSC) and ESP-IDF before.
If you didn't do that yet, follow the official guide:  
https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/

## 🪜 Steps

1. **Open ESP-IDF terminal from VSC**  
   Launch the "ESP-IDF Command Prompt" (Press Ctrl+E T) or use your configured shell with `idf.py`.

2. **Clone this repository**

```bash
git clone https://github.com/gdnztm/ESP32_ST7789V_DEMO.git
cd ESP32_ST7789V_DEMO
```

3. **Add LVGL v9.3**
Do NOT use `main/idf_component.yml` to configure the lvgl dependency, instead install it manually using `git clone`.
I assume you use Windows. If you use Linux, you will probably know which commands to use below.
From the "ESP-IDF Command Prompt" enter:

```bash
mkdir components
cd components
git clone -b master https://github.com/lvgl/lvgl.git
```
This will download 600+ MB of data, so building the repository for the first time (or after `idf.py reconfigure`) will take some time.

To check if you have the correct lvgl version:
```bash
cd lvgl 
type lv_version.h
```
This should show:
```
/**
 * @file lv_version.h
 * The current version of LVGL
 */

#ifndef LV_VERSION_H
#define LV_VERSION_H

#define LVGL_VERSION_MAJOR 9
#define LVGL_VERSION_MINOR 3
#define LVGL_VERSION_PATCH 0
#define LVGL_VERSION_INFO ""

#endif /* LV_VERSION_H */
```
Enter `cd .. ` twice to return to the project directory.

Configure ESP-IDF for using an ESP32 (`idf.py set-target esp32`), select UART as the method of programming and select the correct serial/COM port.
From the "ESP-IDF Command Prompt" enter:

```bash
idf.py reconfigure
idf.py build
idf.py flash monitor
```
The code should now run, displaying "Hello LVGL 9.3!" as white text on an blue background.

Below is short explanation of files and folders in the project folder.

```
ESP32_ST7789V_DEMO/
├── CMakeLists.txt
├── components/                This is the directory you need to create to put lvgl in.
│   └── lvgl/                  lvgl will end up here (do not create this directory manually!)
├── main
│   ├── CMakeLists.txt         This contains files and directory that need to be included.
│   └── main.c                 This contains the program code.
└── README.md                  This is the file you are currently reading.
```
