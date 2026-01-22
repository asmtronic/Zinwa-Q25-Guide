# Zinwa Q25 Complete Guide

**Zinwa Q25** is a BlackBerry Q20 modified by Zinwa with modern hardware and Android operating system, bringing classic keyboard design into the modern era.

---

## Table of Contents

1. [Backup Methods](#backup-methods)
2. [Unlocking and Rooting](#unlocking-and-rooting)
3. [Customization](#customization)
4. [System Tweaks](#system-tweaks)
5. [Keyboard Controls](#keyboard-controls)
6. [Recommended Apps & Modules](#recommended-apps--modules)
7. [Useful Resources](#useful-resources)

---

## Backup Methods

### Backup Without Root

Backup your data before making any modifications:

- **Google Backup**: Use Google's built-in backup for apps and settings
- **App List**: Create a list of installed applications for reference
- **Per-App Backup**: Use each app backup & restore method if possible
- **Export Contacts**: Save contacts to local storage or cloud
- **ADB File Transfer**: Use `adb pull` commands to copy important files
- **Swift Backup**: Cloud backup solution for app data

### Backup With Root Access

Once rooted, you can perform full system backups:

#### Swift Backup
- Perform complete cloud backups of your entire system
- Requires root access for full functionality

### SP Flash Tool V6 Backup (Full Backup)
*Create system images for each device partition*

⚠️ **IMPORTANT**: The device must be powered OFF before using SP Flash Tool V6

1. Connect your powered-off device to PC
2. Open SP Flash Tool V6
3. Use the **Readback** function in automatic mode
4. Wait for the full system backup to complete

---

## Unlocking and Rooting

### Step 1: Unlock Bootloader

⚠️ **WARNING**: This will erase all data on the device!

**Prerequisites:**
- Install required drivers and Android platform-tools
- USB cable connected to PC

**Process:**

1. **Enable Developer Options** on device:
   - Go to Settings > About Phone
   - Tap "Build Number" 7 times
   - Go back to Settings > System > Developer Options

2. **Enable USB Debugging**:
   - Turn on "USB Debugging"
   - Authorize your PC when prompted

3. **Enable OEM Unlocking**:
   - In Developer Options, enable "OEM Unlocking"

4. **Boot into Bootloader**:
   ```bash
   adb reboot bootloader
   ```

5. **Unlock Bootloader**:
   ```bash
   fastboot flashing unlock
   ```

6. **Complete Unlock**:
   - Quickly press **VOLUME UP** when prompted
   - Wait for confirmation message
   - Device will reboot

7. **Reboot Device**:
   ```bash
   fastboot reboot
   ```

### Step 2: Root with KernelSU-Next

**Method:** KernelSU-Next kernel patching

**Prerequisites:**
- Unlocked bootloader (see Step 1)
- `boot.img` file from your device's OS package

**Process:**

1. **Obtain boot.img**:
   - Extract from the OS package provided by Zinwa
   - Copy to your device

2. **Download KernelSU**:
   - Download from [KernelSU-Next GitHub](https://github.com/KernelSU-Next/KernelSU-Next/releases/)
   - Follow their patching instructions to create the batched boot.img
   - Transfer patched `boot.img` back to your PC

5. **Flash Patched Boot Image**:
   ```bash
   fastboot flash boot boot-patched.img
   ```

6. **Reboot**:
   ```bash
   fastboot reboot
   ```


---

## Customization

### Change Boot Animation

1. Install the **meta-overlayfs** module
   - Available at: https://github.com/KernelSU-Modules-Repo/meta-overlayfs

2. Install your custom boot animation module
   - Must be in KernelSU module format

3. Reboot device to apply changes

### Change Boot Logo

Flash a custom logo using fastboot:

```bash
fastboot flash logo logo.bin
```

Replace `logo.bin` with your custom logo file.

### Remove "Orange State" Warning

The device shows an "Orange State" message due to bootloader unlock. You can remove it by editing the bootloader image:

1. **Extract and Edit lk.img** (little kernel):
   - Replace the specific bytes shown in the example with zeros
   - Refer to this example: ![Remove Orange State](/remove_orange.jpg)

2. **Flash Modified Bootloader**:
   ```bash
   fastboot flash lk lk-no-orange.img
   ```

---

## System Tweaks

### Google Play Integrity & Banking Apps

**Purpose:** Enable Google Play Integrity verification for banking apps, Google Pay NFC, RCS messaging, etc.

⚠️ **Requirement:** Bootloader must be unlocked and device must be rooted

**Installation Steps** *(Install modules one by one, reboot after each installation)*:

1. Install **ZygiskNext**
2. Install **Busybox-nkd**
3. Install **Play Integrity Fork**
4. Install **Tricky Store**
5. Install **Tricky Store Addon**

6. Go to the "Sudo User" tab and set **Google Play Services** to "Unmount Disable"

7. Install **Key Attestation App** and **Native Detector**

8. Configure Play Integrity Fork (PIF):
   - Open KernelSU-Next app
   - Click the action button for PIF

9. Configure Tricky Store:
   - Open KernelSU-Next app
   - Open Tricky Store
   - From the menu, select **"Select All"**
   - From the menu, select **"Deselect Unnecessary"**
   - Click **"Save"**
   - From the menu, select **"Valid Keystore"**
   - If "Valid" gives an error, use **"AOSP"** instead
   - Click **"Save"**
   - From the menu, select **"Set Security Patch"**
   - Click **"Get Date"**
   - Click **"Save"** on the security patch window

10. Configure Native Detector:
    - Open KernelSU-Next app
    - Set **Native Detector** as "Unmount Disable" (same as Play Services)

11. **Reboot device**

12. **Verify Installation**:
    - Open Key Attestation app
    - Verify all checks show as valid/passed (the important ones)

**Ongoing Maintenance:**
- When installing or updating apps that require Play Integrity, ensure they're checked in Tricky Store
- Or select "Select All" → "Deselect Unnecessary" → "Save" again

### Trackpad Mode Control

**Purpose:** Advanced trackpad controls with per-app settings

**Installation:**

1. Install **Q25TPMT.apk**
2. Grant superuser permissions
3. Grant accessibility permissions
4. Configure per-app settings as needed

**Usage:**
- Launch from KeyMapper
- Customize trackpad behavior per application

### Resolution Changer

**Purpose:** Adjust screen resolution for better app compatibility

**Installation:**

1. Install **q25-res-changer.apk**
2. Grant superuser permissions

**Configuration:**
- Default resolution: **720x720**
- Alternative for some apps: **720x960**
- Access quick settings button in System Settings for easy switching

---

## Keyboard Controls

### Useful Key Combinations

| Combination | Function |
|-------------|----------|
| **SYM + K/L** | Volume adjustment |
| **SYM + Y/B/G/J** | Screen scrolling |
| **SYM + $** | Toggle Mute |
| **SYM + 0** | Toggle keyboard backlight |

---

## Recommended Apps & Modules

### Essential

- **KernelSU** - Root solution with modules
- **Niagara Launcher** - Minimalist Android launcher
- **KeyMapper** - Advanced key remapping

### Integrity & Security

- **ZygiskNext** - Zygisk implementation
- **Play Integrity Fork** - Play Integrity verification
- **Tricky Store** - Advanced spoofing solution
- **Key Attestation App** - Verify device attestation
- **Native Detector** - Check for root detection

### Customization

- **meta-overlayfs** - System-wide modifications overlay
- **Trackpad Mode Control App** - Q25 trackpad manager
- **Resolution Changer** - Screen resolution adjustment

### Utilities

- **Swift Backup** - Cloud backup solution
- **MTK Client** - MediaTek device tools

---

## System Updates

### Updating Device Firmware

**Using SP Flash Tool V6:**

⚠️ **IMPORTANT**: Device must be powered OFF

1. Power off the device completely
2. Connect USB cable to PC (device still off)
3. Open SP Flash Tool V6
4. Select firmware package
5. Click Download
6. Wait for completion

**Troubleshooting:**

- **Device enters bootloop**: Repeat the download process
- **Device won't connect**: Try disconnecting and reconnecting USB cable

---

## Useful Resources

### Official & Community Resources

- **Q25 Tutorials (Notion):** https://duc1607.notion.site/Q25-Tutorials-2a5709b7d17c8086a351c999e13f5551
- **Q25 Files (Google Drive):** https://drive.google.com/drive/folders/1dQ3V04yze6P7fXzjs7HB1Plg4L-vDGyQ
- **KernelSU Metamodules:** https://kernelsu.org/guide/metamodule.html#what-is-a-metamodule

### GitHub Repositories

- **meta-overlayfs:** https://github.com/KernelSU-Modules-Repo/meta-overlayfs/releases/tag/v1.3.1
- **MTK Client:** https://github.com/bkerler/mtkclient
- **Native Root Detector:** https://github.com/reveny/Android-Native-Root-Detector/releases/tag/v7.6.1
- **TypeQ25:** https://github.com/sriharshaKanukuntla/TypeQ25
- **KernelSU-Next:** https://github.com/KernelSU-Next/KernelSU-Next/releases/
- **Q25 Apps Collection:** https://github.com/AidenWTF/Q25-Apps
- **Resolution Changer:** https://github.com/mybabysexy/q25-res-changer

### Additional Resources

- **Shizuku:** https://shizuku.rikka.app/
- **MTK Boot Time Optimization:** https://github.com/JamiKettunen/droidian-zinwa-q25/wiki#make-rebooting-5-seconds-faster

---

**Last Updated:** January 2026

For more information and community support, refer to the linked resources above.
