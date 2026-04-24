# Waveshare ESP32-S3-Touch-LCD-2: Precision Current Monitor & Logger

A professional-grade, high-visibility directional current monitoring instrument and data logger built for the Waveshare ESP32-S3-Touch-LCD-2 development board and the INA219 sensor.

## 🚀 Key Features

### 📊 Advanced Dashboard
*   **Calibrated Analogue Gauge**: A central circular scale (0-2000mA) with a smooth-motion indicator arc.
*   **Directional Color Coding**:
    *   🟢 **Green**: Charging / Power Source (> 1mA).
    *   🔴 **Red**: Discharging / Power Load (< -1mA).
    *   ⚪ **White**: Neutral Deadband (-1mA to 1mA) for visual stability.
*   **High-Visibility Readout**: Uses **Montserrat 48** bold font for the central numeric display and **Montserrat 24** for units.
*   **Auto-Scaling Units**: Automatically switches from **mA** (integer) to **Amps** (2 decimals) when current exceeds 999mA.

### 💾 Data Logging System
*   **On-Demand Setup**: Prompts for Date & Time setup only when logging is first initiated, ensuring meaningful timestamps.
*   **Manual Control**: Dedicated **START/STOP** touch button to control logging sessions.
*   **Reliable Timestamps**: Uses a hardware-backed `millis()` offset to ensure precisely incrementing records even without an active internet connection.
*   **Automatic File Rotation**: Generates CSV files named by timestamp and automatically starts a new file every **5,000 records**.
*   **Configurable Intervals**: Integrated **Settings Menu** (Gear icon) to change logging frequency from **1 second** to **10 minutes**.

## 🛠️ Hardware Configuration

### Pin Mapping
| Component | Function | Pins |
| :--- | :--- | :--- |
| **LCD (ST7789)** | SPI (HSPI) | CS: 45, DC: 42, RST: 0, MOSI: 38, SCK: 39, BL: 1 |
| **SD Card** | SPI (Shared) | CS: 41, MISO: 40, MOSI: 38, SCK: 39 |
| **I2C Bus** | Shared | SDA: 48, SCL: 47 |
| **Touch (CST816D)**| I2C | INT: 46, RST: 0 |
| **INA219 Sensor** | I2C | Address: 0x40 (Default) |

### Board Settings (Arduino IDE)
*   **Board**: `ESP32S3 Dev Module`
*   **USB CDC On Boot**: `Enabled` (Required for Serial Debugging)
*   **Flash Size**: `16MB`
*   **PSRAM**: `OPI PSRAM`

## 📦 Software Requirements

The following libraries must be installed via the Arduino Library Manager:
*   `lvgl` (v9.x)
*   `Adafruit_ST7789`
*   `Adafruit_GFX`
*   `Adafruit_INA219`
*   `CST816S` (by fbiego)

### LVGL Configuration
Ensure your `lv_conf.h` has the following fonts enabled:
```c
#define LV_FONT_MONTSERRAT_14 1
#define LV_FONT_MONTSERRAT_24 1
#define LV_FONT_MONTSERRAT_34 1
#define LV_FONT_MONTSERRAT_48 1
```

## 📖 Usage
1.  **Boot**: The device starts directly into the real-time monitoring dashboard.
2.  **Monitor**: View the live current flow on the analogue gauge and digital readout.
3.  **Log**: Press the green **START** button. If the time is not set, use the rollers to select the current Date/Time and press **START LOGGING**.
4.  **Configure**: Press the **Gear Icon** in the top right to adjust the logging frequency.
5.  **Retrieve Data**: Insert the SD card into a computer to access the `.csv` log files.
