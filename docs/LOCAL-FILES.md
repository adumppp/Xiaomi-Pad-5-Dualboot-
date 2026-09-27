# Local files and repository policy

My working folder contained tools and images used during the setup, including Android platform tools, USB/fastboot drivers, Xiaomi Mi Unlock files, `HyperSploit-Windows.exe`, `boot.img`, `recovery.img`, and other installer packages.

Most of them are intentionally **not included** in Git history because:

- executables and drivers can become outdated;
- boot and recovery images must match the exact device and software version;
- redistribution rights and original provenance are not confirmed for every file;
- device-generated images and logs can contain identifiers or private data;
- large Windows images do not belong in Git history.

The exact HyperSploit v1.0.0 binary I used was verified byte-for-byte against its official upstream release and is available as a GitHub Release asset. See [Tool downloads, versions, and checksums](TOOL-DOWNLOADS.md). Xiaomi Mi Unlock and Google Platform-Tools are linked to their official publishers instead of being repackaged here.

## Where to get current resources

- [HyperSploit upstream repository](https://github.com/TheAirBlow/HyperSploit)
- [ArKT-7/won-deployer](https://github.com/ArKT-7/won-deployer)
- [Xiaomi Pad 5 Windows community guide](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5)
- [Google Android platform tools](https://developer.android.com/tools/releases/platform-tools)

Download tools from their original maintainers, check the release notes, and verify published hashes or signatures when available. Do not use files from this project's local working folder as a universal bundle.

Screenshots that do not reveal serial numbers, Xiaomi account details, Wi-Fi information, or other personal data may be added later under an `assets/` directory.
