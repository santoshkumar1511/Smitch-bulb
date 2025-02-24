

# Smitch Bulb Control and Firmware Update

This repository provides a method to control Smitch bulbs that have become unusable after the company shut down. The steps below will guide you on how to control the bulb's brightness and temperature using Termux, as well as how to update the bulb's firmware to Tasmota for better functionality.

---

## Prerequisites

1. **Termux**: Install Termux from the [Google Play Store](https://play.google.com/store/apps/details?id=com.termux) or [F-Droid](https://f-droid.org/packages/com.termux/).
2. **Telnet**: Ensure Telnet is installed in Termux. Run the following command to install it:
   ```bash
   pkg install telnet
   ```
3. **Smitch Bulb**: Ensure the bulb is connected to your Wi-Fi network and accessible at `192.168.4.1`.

---

## Controlling the Bulb Using Termux(Only work With white light bulb) 

### Adjust Brightness
To adjust the brightness of the bulb, use the following command in Termux:
```bash
(echo -ne "0001xx020600\r"; sleep 2; echo -ne "KEEPALIVE\r"; sleep 2) | telnet 192.168.4.1 80
```
- Replace `600` with the desired brightness percentage. For example:
  - `600` for 60% brightness.
  - `800` for 80% brightness.

### Adjust Temperature
To adjust the color temperature of the bulb, use the following command:
```bash
(echo -ne "0001xx016000\r"; sleep 2; echo -ne "KEEPALIVE\r"; sleep 2) | telnet 192.168.4.1 80
```
- Replace `6000` with the desired temperature value. For example:
  - `6000` for 6000K (cool light).
  - `3000` for 3000K (warm light).

---

## Updating the Bulb Firmware

If you want to flash custom firmware (e.g., Tasmota) to the bulb, follow these steps:

### Step 1: Access the Firmware Update Page
1. Open a browser and navigate to:
   ```
   http://192.168.4.1:1336/update
   ```
2. Enter the following credentials:
   - **Username**: `admin`
   - **Password**: `c21pdGNo`

### Step 2: Flash Tasmota Minimal Firmware
1. Download the Tasmota minimal firmware from the [official Tasmota repository](https://github.com/arendst/Tasmota).
2. Upload the firmware file on the update page.

### Step 3: Update to Full Tasmota Firmware
1. After flashing the minimal firmware, navigate to:
   ```
   http://192.168.4.1/up
   ```
2. Upload the full Tasmota firmware file.

---

## Notes
- Ensure your device is connected to the same network as the bulb.
- Flashing custom firmware may void any remaining warranty and carries some risk. Proceed with caution.

---

## Contributing
If you have improvements or additional methods to control the bulb, feel free to open an issue or submit a pull request.

---

