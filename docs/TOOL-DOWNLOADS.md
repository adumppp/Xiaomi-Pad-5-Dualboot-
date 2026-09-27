# Tool downloads, versions, and checksums

This page records the tools used during my Xiaomi Pad 5 setup and explains where to get them safely.

## HyperSploit for Windows

The binary from my working folder was compared byte-for-byte with the official HyperSploit v1.0.0 GitHub release. The SHA-256 values matched.

- Version used: **1.0.0**
- Repository release: [Download `HyperSploit-Windows.exe`](https://github.com/adumppp/Xiaomi-Pad-5-Dualboot-/releases/download/setup-tools-v1/HyperSploit-Windows.exe)
- Original upstream asset: [TheAirBlow/HyperSploit v1.0.0](https://github.com/TheAirBlow/HyperSploit/releases/tag/1.0.0)
- Source code: [TheAirBlow/HyperSploit](https://github.com/TheAirBlow/HyperSploit/tree/1.0.0)
- License: [Mozilla Public License 2.0](https://github.com/TheAirBlow/HyperSploit/blob/1.0.0/LICENCE)
- SHA-256: `E71A1E0372A8D7F8B1A60A8DA8D0EAFDDAF8CA92781AA87AED8F0C139F98839F`

> [!WARNING]
> HyperSploit is archived and unsigned. Its maintainer says the method was patched on newer HyperOS 2 releases and completely patched on HyperOS 3. The v1.0.0 file is preserved because it is the version that worked in this setup—not because it is recommended for every device.

## Xiaomi Mi Unlock

My local folder contains Xiaomi Mi Unlock **v6.5.406.31**. Its main executable has a valid digital signature from Beijing Xiaomi Intelligent Technology Co., Ltd.

- Version used: **6.5.406.31**
- `miflash_unlock.exe` SHA-256: `28A1623FF8AAF65D2A7BD34ED1644270896B7B7080E8DA2D9CA0A6C9750B24AE`
- Official Xiaomi entry point: [Mi Unlock](https://en.miui.com/unlock/download_en.html)
- Current community unlock instructions: [Bootloader unlocking guide](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/blob/main/guide/English/unlock-bootloader-en.md)

The Mi Unlock package is not mirrored here because the package does not include permission to redistribute Xiaomi's proprietary program. Download the current Xiaomi-signed version from Xiaomi instead of using an old repackaged copy.

## Android SDK Platform-Tools for Windows

My setup folder contains Platform-Tools **35.0.2**. The local `adb.exe` and `fastboot.exe` both have valid Google signatures.

- Version used: **35.0.2**
- `adb.exe` SHA-256: `0E606318957BAAC81B997CCD8EE4BCDFF79964A9921DA07C716AEA3E8D856AF7`
- `fastboot.exe` SHA-256: `E1B1537A9F5E73C746A96F6F2FE3461477320867A4206B7ECE138AC1AEEF5300`
- Official download and release notes: [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools)

Google recommends using the latest Platform-Tools because they are backward compatible. The old local package is not mirrored here; use Google's official download so you receive the current signed binaries and license notices.

## Verification on Windows

Check the checksum of a downloaded file in PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath '.\HyperSploit-Windows.exe'
```

Check a file's Windows digital signature:

```powershell
Get-AuthenticodeSignature -LiteralPath '.\adb.exe' | Format-List Status,SignerCertificate
```

For signed Google or Xiaomi tools, stop if the signature status is not `Valid`. HyperSploit v1.0.0 is not Authenticode-signed, so compare its SHA-256 value instead.
