# ARMtix for Xiaomi Pad 6 (pipa)

## Uninstallation

### Prerequisites

- [`ADB & Fastboot`](https://developer.android.com/tools/releases/platform-tools)

- [`Fastboot Stock ROM`](https://xmfirmwareupdater.com/archive/miui/pipa)

### Notes

> [!WARNING]
> All your data will be erased! Back up now if needed.
>
> DO NOT REBOOT YOUR TABLET if you think you made a mistake, ask for help in the [Support groups](../README.md#Support-Groups)
>
> Do not run all commands at once, execute them in order!

> [!NOTE]
> If any of `adb` or `fastboot` command fails with `command not found` error check if the path to the platform-tools directory is added to the PATH environment variable

> [!NOTE]
> This guide assumes that you're using cmd on Windows and bash on Linux/macOS as your shell.

## If Singleboot

#### Download and decompress ROM
### Go to the ROM folder
- run `flash_all.bat` on Windows
- run `flash_all.sh` on Linux/macOS

### Reboot and enjoy the stock ROM


## If Dualboot

#### Download and decompress ROM
### Restore GPT table
- If you want to uninstall linux this is used instead of deleting partitions manually to avoid human error
- If you want to relock your bootloader you'll need your partition table to be stock.
#### Go to the ROM folder
- Go to the `images/` folder
> Make sure `gpt_both0.bin` file is located here
```bash
fastboot flash partition:0 gpt_both0.bin
```
### Erase userdata to avoid bootloop and restore FS size
```bash
fastboot -w
```
### Back to the ROM folder
- run `flash_all.bat` on Windows
- run `flash_all.sh` on Linux/macOS

### Reboot and enjoy the stock ROM