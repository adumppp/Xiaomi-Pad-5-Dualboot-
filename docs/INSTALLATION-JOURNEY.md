# Installation Journey: HyperOS + Windows 11 on Xiaomi Pad 5

This is the process I used on a Xiaomi Pad 5 (`nabu`). Tool behavior and compatible driver/UEFI versions can change, so use this page as a checklist alongside the latest upstream documentation—not as a replacement for it.

## 1. Read this before starting

Expect the following:

- Unlocking the bootloader performs a factory reset.
- Repartitioning the internal storage can erase Android and Windows data.
- A wrong image or interrupted operation can make the tablet unbootable.
- Unlocking can reduce device security, affect DRM-protected content, and affect warranty or support.
- The process needs a reliable USB cable, a charged tablet, a Windows 10/11 PC, and stable internet.

Back up photos, documents, authenticator recovery codes, and anything else you need. Keep a copy of the stock firmware and recovery resources for the exact device and region.

> [!IMPORTANT]
> Confirm the tablet is `nabu` before flashing or repartitioning anything. Pad 5 Pro variants are different devices.

With Android running and USB debugging enabled:

```powershell
adb devices
adb shell getprop ro.product.device
```

The second command should return `nabu`. In fastboot mode, also check:

```powershell
fastboot devices
fastboot getvar product
```

Stop if the device is not detected or the reported product is not `nabu`.

## 2. Unlocking the bootloader

This was the longest part for me—about two weeks from the first attempt to a completed unlock.

### Normal Xiaomi preparation

1. Sign in to the Xiaomi account that will be used for the unlock.
2. Insert a working SIM and make sure mobile data is available.
3. Enable Developer options by repeatedly tapping the OS/MIUI version in **Settings**.
4. In Developer options, enable **OEM unlocking** and **USB debugging**.
5. Open **Mi Unlock status** and try to bind the account and device.
6. Back up the tablet before continuing.

The official Xiaomi unlock flow should be tried first. The Mi Unlock tool may impose a waiting period; do not remove the SIM, change Xiaomi accounts, or repeatedly rebind the device during that wait.

### What worked for my HyperOS binding problem

HyperOS prevented the normal binding step in my case. I used `HyperSploit-Windows.exe`, obtained from the [HyperSploit project](https://github.com/TheAirBlow/HyperSploit), while the tablet was connected with USB debugging enabled. After it completed the binding workaround, I used Xiaomi's official Mi Unlock tool to finish the bootloader unlock.

Important limitations:

- HyperSploit does **not** remove Xiaomi's normal waiting period.
- The upstream project is archived and says newer HyperOS releases patched the method.
- Only download it from the upstream project/release page; do not trust random mirrors.
- Read the upstream requirements and warnings before running it.
- The final unlock still uses Xiaomi's official Mi Unlock tool and wipes the tablet.

After the unlock and factory reset, complete Android setup and re-enable USB debugging. Confirm the bootloader is actually unlocked before moving on.

## 3. Prepare for won-deployer

I used [ArKT-7's won-deployer](https://github.com/ArKT-7/won-deployer), an installer designed specifically for Windows on the Xiaomi Pad 5.

Prepare these items:

- An unlocked Xiaomi Pad 5 (`nabu`)
- A Windows 10 or Windows 11 PC
- Working Android platform tools/ADB drivers
- A Windows ARM64 ESD or WIM image
- The current Xiaomi Pad 5 Windows driver package requested by won-deployer
- Enough free tablet storage for the Android and Windows sizes you choose
- A stable cable, internet connection, and a well-charged tablet

For a first-time installation, the upstream guide recommends starting from working stock MIUI or HyperOS. Use the newest compatible drivers and UEFI from the maintained guide; old packages can contain serious storage-related bugs.

Do not reuse a random `boot.img`, `recovery.img`, driver archive, or UEFI file merely because its filename looks correct. Match every artifact to the device and the current upstream guide.

## 4. Install and run won-deployer

1. Open the [official won-deployer preparation guide](https://github.com/ArKT-7/won-deployer/blob/main/guide/English/prepare-en.md).
2. Obtain won-deployer using the current method documented there. If the guide offers a command that downloads and immediately runs a script, inspect the linked script/source first.
3. Open a new Administrator PowerShell window and verify the installation:

   ```powershell
   won-deployer -h
   ```

4. Boot the tablet into fastboot mode by holding **Volume Down + Power**, or from Android:

   ```powershell
   adb reboot bootloader
   ```

5. Confirm the PC sees it:

   ```powershell
   fastboot devices
   fastboot getvar product
   ```

6. Start the installer:

   ```powershell
   won-deployer
   ```

7. Follow the prompts carefully. Provide the Windows ARM64 ESD/WIM path, select the intended Windows edition, provide the requested driver archive, and choose the Android/Windows partition sizes.
8. Do not disconnect the cable, close the window, allow the PC to sleep, or force-restart the tablet while partitioning or deployment is running.
9. Save the partition sizes and tool version you used. They are useful if recovery or resizing is needed later.

If deployment fails, do not blindly repeat flashing steps. Return the tablet to the state requested by the guide, then collect a detailed log with:

```powershell
won-deployer --debug
```

Use that log when asking the upstream maintainers for help, but remove serial numbers, account details, local usernames, and file paths before sharing it publicly.

## 5. Finish the dual-boot setup

After won-deployer finishes and Android boots:

1. Complete Android setup and connect the tablet to the internet.
2. Restart the tablet once.
3. Open the preinstalled **Won-deployer Setup** app.
4. Run each setup button in order and follow its prompts.
5. Open **Magisk**, accept the requested additional setup, and allow it to reboot. If Magisk asks again after reboot, repeat the additional setup once more.
6. Open **WOA Helper** and grant root access.
7. In WOA Helper, select **BACKUP BOOT IMAGE**, then **Windows**, then confirm.
8. Use **QUICKBOOT TO WINDOWS** to start Windows.

To switch back:

- **Android to Windows:** use WOA Helper's **QUICKBOOT TO WINDOWS** action or its Quick Settings toggle.
- **Windows to Android:** use the **Android** shortcut created on the Windows desktop.

These app names and steps reflect the won-deployer workflow I used. Check its current guide in case a later version changes them.

## 6. Verification checklist

Before treating the setup as finished, test both operating systems:

- [ ] Android boots normally
- [ ] Windows boots normally
- [ ] Android can quick-boot to Windows
- [ ] Windows can return to Android
- [ ] Touchscreen and display rotation work in Windows
- [ ] Wi-Fi and Bluetooth work
- [ ] Audio works
- [ ] Charging and battery reporting work
- [ ] Sleep, wake, and shutdown behave normally
- [ ] Important personal data is backed up again

## 7. Recovery notes

- Keep stock firmware and known-good recovery resources offline.
- Keep device-specific partition backups private. They may contain identifiers or personal data.
- If fastboot still detects the tablet, stop and consult the current troubleshooting guide before flashing more images.
- If Windows works but dual boot does not, check the current UEFI, driver, Magisk, and WOA Helper instructions rather than repartitioning immediately.
- Never flash a Pad 5 Pro image onto a regular Pad 5 (`nabu`).

The maintained [community troubleshooting guide](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5) should be treated as the current reference for recovery, driver updates, and UEFI changes.

## 8. My outcome

The end result was a usable Xiaomi Pad 5 with HyperOS/Android and Windows 11 ARM64 dual boot. The unlock stage was the biggest obstacle; after the account binding finally succeeded, won-deployer handled the installation and dual-boot setup.

I will add a YouTube demonstration link to the main README later.
