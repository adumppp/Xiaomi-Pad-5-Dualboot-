# Xiaomi Pad 5 Dualboot Journey

Personal notes from my successful Xiaomi Pad 5 (`nabu`) dual-boot setup with **HyperOS/Android and Windows 11 ARM64**.

My hardest step was unlocking the bootloader. It took me about two weeks. I used [HyperSploit](https://github.com/TheAirBlow/HyperSploit) to get past the HyperOS account-binding restrictions, completed the unlock with Xiaomi's official Mi Unlock tool, and then followed [ArKT-7's won-deployer](https://github.com/ArKT-7/won-deployer) workflow to install Windows and configure dual boot.

> [!WARNING]
> This procedure erases data and modifies the tablet's partition table, boot images, and firmware. A mistake or an incompatible file can leave the device unbootable. This is a record of what worked for me, not a guarantee. Read the current upstream instructions completely before starting.

## Documentation

- [My installation journey and checklist](docs/INSTALLATION-JOURNEY.md)
- [Files intentionally excluded from this repository](docs/LOCAL-FILES.md)
- [Official won-deployer guide](https://github.com/ArKT-7/won-deployer/blob/main/guide/English/prepare-en.md)
- [Community Xiaomi Pad 5 Windows guide](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5)

## Result

- Android/HyperOS remains available.
- Windows 11 ARM64 boots on the tablet.
- WOA Helper provides quick boot from Android to Windows.
- The Windows desktop shortcut returns the tablet to Android.

## Video demonstration

YouTube link: **coming soon**

## Important scope

This repository is for the **Xiaomi Pad 5, codename `nabu`**. Do not apply its images or partition instructions to another Xiaomi device, including the Pad 5 Pro models.

Third-party executables, Windows images, drivers, and device-specific boot/recovery images are not mirrored here. Download current files from their original maintainers and verify them before use.

## Credits

- [ArKT-7/won-deployer](https://github.com/ArKT-7/won-deployer) — automated Windows-on-Nabu installation and dual-boot setup
- [erdilS/Port-Windows-11-Xiaomi-Pad-5](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5) — maintained community guide, drivers, UEFI, and troubleshooting references
- [TheAirBlow/HyperSploit](https://github.com/TheAirBlow/HyperSploit) — the HyperOS binding bypass that worked during my unlock attempt

All linked projects belong to their respective authors. This repository only documents my experience.
