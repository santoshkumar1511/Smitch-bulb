# Smitch Smart Bulb Control and Firmware Update (B22)

This repository provides a method to control Smitch bulbs that have become unusable after the company shut down. The steps below will guide you on how to control the bulb's brightness and temperature using Termux, as well as how to update the bulb's firmware to Tasmota for better functionality.

---

## With termux 

1. **Termux**: Install Termux from the [Google Play Store](https://play.google.com/store/apps/details?id=com.termux) or [F-Droid](https://f-droid.org/packages/com.termux/).
2. **Telnet**: Ensure Telnet is installed in Termux. Run the following command to install it:
   ```bash
   pkg install telnet
   ```
3. **Smitch Bulb**: Ensure the bulb is connected to your Wi-Fi network. The bulb's IP address can be any IP (`<ip>`), but most of the time, it is `192.168.4.1`.

---

## Controlling the Bulb Using Termux / Terminal (Only Works For White Light Bulbs)

### Adjust Brightness
To adjust the brightness of the bulb, use the following command in Termux:
```bash
(echo -ne "0001xx020600\r"; sleep 2; echo -ne "KEEPALIVE\r"; sleep 2) | telnet <ip> 80
```
- Replace `600` with the desired brightness percentage. For example:
  - `600` for 60% brightness.
  - `800` for 80% brightness.

### Adjust Temperature
To adjust the color temperature of the bulb, use the following command:
```bash
(echo -ne "0001xx016000\r"; sleep 2; echo -ne "KEEPALIVE\r"; sleep 2) | telnet <ip> 80
```
- Replace `6000` with the desired temperature value. For example:
  - `6000` for 6000K (warm light).
  - `3000` for 3000K (cool light).

---

## Updating the Bulb's Firmware

If you want to flash custom firmware (e.g., Tasmota) to the bulb, follow these steps:

### Step 1: Access the Firmware Update Page
1. Open a browser and navigate to:
   ```
   http://<bulb ip>:1336/update
   ```
   You can figure out the bulb's IP by looking into your router's connected devices list.


3. Enter the following credentials:
   - **Username**: `admin`
   - **Password**: `c21pdGNo`

### Step 2: Flash Tasmota Minimal Firmware
1. Download the Tasmota minimal firmware from the [official Tasmota repository](http://ota.tasmota.com/tasmota/release/tasmota-minimal.bin.gz).(if downloading not working tap and hold, copy link paste in search box) 
2. Upload the firmware file on the update page. [You might see 2 fields labelled firmware and file system upgrade, choose the one which says "firmware"]

### Step 3: Update to Full Tasmota Firmware
1. After flashing the minimal firmware, navigate to:
   ```
   http://<bulb ip>/up
   ```
      **Note:** The IP you were using in the previous step will no longer work as, if the flash was successful, your smart device will be reset and you will need to scan for a new WiFi device on the network. Generally, this would look like the name of the pattern "ESP****" or something similar. Connect to the said SSID and follow the rest of the steps.
   
3. Upload the full Tasmota firmware file.
  Download the full Tasmota firmware from the [official Tasmota repository](http://ota.tasmota.com/tasmota/release/tasmota.bin.gz).
<br>
  **Note:** If you encounter an error indicating “Not enough space” while uploading the entire firmware, try using the compressed “tasmota.bin.gz” file instead of the uncompressed one. If you haven’t enabled automatic extraction (for instance, when downloading via Safari), this shouldn’t be an issue that you encounter.
   
---

## Notes
- Ensure your device is connected to the same network as the bulb for step 1.
- Flashing custom firmware may void any remaining warranty and carries some risk. Proceed with caution.

---

## What's Next?

- Once the device is flashed with custom firmware, the world is your oyster. Ideally, we would want to configure a working pin configuration and template. If using Tasmota, you can refer to [Tasmota Templates](https://templates.blakadder.com/bulb-socket.html) for a starting point on how to configure your newly flashed device.
- Once a template is loaded, you might have to fine-tune the module and / or template configuration. This will require manual tinkering with the modules. Below is an example of a working example of Smitch 10W 6500K Dimmable Bulb (SB0110 - B22) post-tweaking from a base template. 

<img width="452" alt="image" src="https://github.com/user-attachments/assets/65727427-9219-49dc-aba0-17a241680253" />


---
## Contributing
If you have improvements or additional methods to control the bulb, feel free to open an issue or submit a pull request.

---

