# ARMtix for Xiaomi Pad 6 (pipa)

## Installation

### Prerequisites

- `Unlocked bootloader`
- `PC/Laptop with Windows 10-11/Linux/macOS`
- [`Android platform tools`](https://developer.android.com/tools/releases/platform-tools)

- [`Kernel & RootFS image`](https://github.com/armtix-xiaomi-pipa/releases)
- `Brain (Very important)`

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

> [!NOTE]
> Make sure rootfs is decompressed before flashing.


## Singleboot

### Flashing
  

#### Reboot your tablet into bootloader mode by holding `Volume Down` and `Power` buttons

#### Flash kernel image to boot paritions
> Replace path/to/armtix-pipa-boot.img with the actual path of boot image
```bash
fastboot flash boot_ab armtix-pipa-boot.img
```

#### Flash rootfs image to userdata partition
> Replace path/to/armtix-pipa-&lt;init.img&gt; with the actual path of rootfs image and &lt;init&gt; with your chosen init (openrc, runit, s6 or dinit)
```bash
fastboot flash userdata path/to/armtix-pipa-<init>.img
```

#### Erase dtbo partitions
```bash
fastboot erase dtbo_ab
```

#### Reboot your tablet
```bash
fastboot reboot
```

</details>

## Dualboot
### Repartitioning

> [!NOTE] TO DO
>
> For now, ask in the [Support groups](../README.md#Support-Groups)
---

### Flashing

> [!WARNING]
> Repartition required!

> [!NOTE]
> Recommended slots configuration: 
> - Slot A: Android
> - Slot B: Linux

> [!TIP]
> To switch slot from linux use `qbootctl -s [a|b|0|1]` or [QbootControl](https://github.com/khairul169/qbootctrl-gui) or `fastboot set_active <a|b>` (safest, but need second device)
>
> To switch slot from android use [Boot Control](https://github.com/capntrips/BootControl) app (root required) or any custom recovery
>
> Disable Android OTA updates in settings. Otherwise it will override linux boot with android boot on the second slot

#### Reboot your tablet into bootloader mode by holding `Volume Down` and `Power` buttons

#### Flash kernel to boot b
> Replace path/to/armtix-pipa-boot.img with the actual path of boot image
```bash
fastboot flash boot_b path/to/armtix-pipa-boot.img
```

#### Flash rootfs image to linux partition
> Replace &lt;linux&gt; with the name of your linux partition, path/to/armtix-pipa-&lt;init.img&gt; with the actual path of rootfs image and &lt;init&gt; with your chosen init (openrc, runit, s6 or dinit)
```bash
fastboot flash <linux> path/to/armtix-pipa-<init>.img
```

#### Erase dtbo partition in slot b
```bash
fastboot erase dtbo_b
```

#### Reboot your tablet
```bash
fastboot reboot
```

## [Next step: Post-install](./post-install.md)
