# X11-ddc-brightness-script
A small script I wrote with assistance of ChatGPT to fix the issue of multiple monitors having different brightness levels. This controls the brightness with DDC/CI, so the monitors have to support that feature.

### Dependencies

- [`ddcutil`](https://www.ddcutil.com/) – for communicating with monitors via DDC/CI  
  Installation (for example on Arch/Garuda):

  ```bash
  sudo pacman -S ddcutil
  ```

---

## How to Find Monitor Bus Numbers

1. Open your terminal
2. Run:

   ```bash
   sudo ddcutil detect
   ```

   Example output:

   ```
   Display 1
   I2C bus:  /dev/i2c-7
   DRM connector: card1-HDMI-A-1
   ```

3. Note the **bus numbers** (e.g., `7`, `9`, `10`)
4. Edit the `ddc-brightness` script and set these bus numbers in the `BUS_LIST` array

---

## Configuration

Open the `ddc-brightness` script and modify the following lines at the top:

```bash
# DDC/CI bus numbers (from "ddcutil detect")
BUS_LIST=(7 9 10)

# Optional monitor names (for display in --list)
MONITOR_NAMES=("MSI MP242" "Gigabyte M34WQ" "Samsung S24R65x")
```

---

## Usage

**Note:** Most systems require `sudo` for `ddcutil` to communicate with hardware-level interfaces.

### Set brightness for all monitors

```bash
sudo ddc-brightness --all 60
```

### Set brightness for a specific monitor

```bash
sudo ddc-brightness --monitor 2 45
```

(Sets the brightness of monitor #2 to 45%)

### List connected monitors

```bash
ddc-brightness --list
```

---

## Optional: Install System-Wide

To make the script available globally:

```bash
sudo mv ddc-brightness /usr/local/bin/
sudo chmod +x /usr/local/bin/ddc-brightness
```

Then you can run it from anywhere:

```bash
ddc-brightness --all 70
```

---
