# Thinkpad-T560-Monterey (OpenCore)

![macOS Monterey](https://img.shields.io/badge/macOS-Monterey-success?style=flat-square&logo=apple)
![OpenCore](https://img.shields.io/badge/OpenCore-1.0.6-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Stable-green?style=flat-square)

Complete OpenCore EFI configuration for **Lenovo ThinkPad T560** running macOS Monterey.  
This build focuses on system stability, power management, and native-like experience.

---

## 💻 Hardware Specification

| Component | Specification | Status |
| :--- | :--- | :--- |
| **CPU** | Intel Core i7-6600U (Skylake) | ✅ Working (Native PM) |
| **iGPU** | Intel HD Graphics 520 | ✅ Working (HW Acceleration) |
| **dGPU** | NVIDIA GeForce 940MX | ⛔ Disabled (via SSDT) |
| **RAM** | 16GB DDR3L | ✅ Working |
| **Display** | 15.6" FHD IPS (1920x1080) Non-Touch | ✅ Working |
| **Audio** | Realtek ALC293 | ✅ Working (Layout ID: 28) |
| **WiFi / BT** | Intel Dual Band Wireless-AC 8260 | ✅ Working |
| **Ethernet** | Intel I219-V | ✅ Working |
| **Input** | Synaptics Trackpad & TrackPoint | ✅ Working (with Gestures) |
| **SD Reader** | Realtek RTS522A | ⚠️ Disabled (See Notes) |
| **Camera** | None (Corporate Model) | ⛔ Not present |

---

## ✅ What Works
* **Graphics:** Full hardware acceleration (Intel HD 520).
* **Audio:** Internal speakers, internal microphone, and combo jack (layout-id `28`).
* **Boot Chime:** Enabled (Classic Mac startup sound).
* **WiFi & Bluetooth:** Native-like support via `AirportItlwm` and `IntelBluetoothFirmware`.
* **Power Management:** Native CPU power management, working battery percentage.
* **Sleep/Wake:** Fully functional (no "Zombie" sleep).
* **Input Devices:** Trackpad (multi-touch gestures) and TrackPoint works.
* **Function Keys (F1-F12):** Working (Brightness, Volume, etc.). *Requires YogaSMC App.*

## ❌ What Doesn't Work / Known Issues
* **NVIDIA 940MX:** macOS does not support Optimus technology. The discrete GPU is disabled via ACPI (SSDT) to save battery.
* **SD Card Reader:** The Realtek reader is present but **disabled in config.plist** intentionally. Enabling it causes a Kernel Panic upon waking from sleep.
* **Special Keys:** Dedicated keys for Calculator, Lock, Web Browser, and File Explorer do not function.
* **Fingerprint Reader:** Not supported by macOS.
* **DRM:** DRM content (Netflix/Apple TV+ in Safari) might not work (common iGPU limitation). Use Chromium/Firefox.

* **You tell me!**
---

## ⚙️ BIOS Settings (Important)
To boot successfully, ensure your BIOS is configured as follows:

* **Config -> Network -> Wake On LAN:** Disabled
* **Config -> Intel AMT:** Disabled
* **Security -> Secure Boot:** Disabled
* **Startup -> CSM Support:** No (UEFI Only)

---

## 📝 Installation & Post-Install

### 1. Generate SMBIOS
**⚠️ DO NOT COPY THE config.plist DIRECTLY WITHOUT EDITING!** For security reasons, the serial numbers in this repo are blanked out.
1.  Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).
2.  Generate new serials for **MacBookPro13,1**.
3.  Open `config.plist` -> `PlatformInfo` -> `Generic` and check:
    * `MLB`
    * `SystemSerialNumber`
    * `SystemUUID`

### 2. Function Keys (YogaSMC)
The `YogaSMC.kext` is included in the EFI. To get the on-screen display (OSD) for volume/brightness and full function key support:
* Download and install the **YogaSMC App** (Settings pane) inside macOS.

---

## ⚠️ Disclaimer
This EFI is provided "as is". I am not responsible for any damage caused to your device. Always make a backup of your data and current EFI before applying changes.

## 👏 Credits
* [Apple] for macOS.
* [Acidanthera](https://github.com/acidanthera) for OpenCore and Kexts.
* [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for the extensive guides.
* [OpenIntelWireless](https://github.com/OpenIntelWireless) for Intel WiFi drivers.
