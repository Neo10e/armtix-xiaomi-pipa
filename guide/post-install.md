# ARMtix for Xiaomi Pad 6 (pipa)

## First boot

### Prerequisites

- `Wired keyboard (USB-C / OTG Cable / HUB)` or `Official Xiaomi Pad 6 Keyboard`

- `Brain (Very important)`

### Notes

> [!IMPORTANT]
> These are pure images and you need to setup all by yourself.

> [!CAUTION]
> PROCEED WITH CAUTION!!! Don't touch other partitions than userdata / linux and boot until you know what you're doing because you can PERMANENTLY brick your device!!!

> [!IMPORTANT]
> hwclock replaced with pre-installed swclock-offset
>
> That's because hardware clock is not writable on pipa
>
> On the first boot after connecting to the internet, we need to wait ~2 min for the date & time to be synchronized. Next time we boot up, we won't have to wait anymore

> [!NOTE]
> Login & password:
>
> User name is "armtix", user and root password both are "armtix". User can run any program with sudo.

### Setting up 
Log in as root with password armtix

#### Resize the image you flashed to span the entire partition 
> You can't install packages without
```bash
resize2fs /dev/disk/by-label/armtix
```
#### Connect to the Internet
Network Manager is pre installed.
Use nmtui to connect to your wifi
```bash
nmtui
```
> now wait ~2 minutes

#### Initialize the pacman keyring:

```bash
pacman-key --init
```
> No need to populate artix keyring; currently packages in ARMtix don't have signatures

#### Kernel updates
Kernel updates are handled via pacman
- to enable automatic kernel updates run
```bash
touch /boot/.autoflash
```
- to flash kernel manually, run 
```bash
/usr/bin/flashkernel.sh
```

### Configure the base system

Continue configuring ARMtix as usual and customize ARMix to your needs

Images include a helper script that can be used to setup and install KDE Plasma
```bash
~/setup.sh
```
Do not install GNOME on ARMtix because for now “GNOME Desktop Environment No Longer Supported” (read more [here](https://artixlinux.org/news.php#GNOME_Desktop_Environment_No_Longer_Supported)) Blame GNOME devs for depending heavily on systemd

Feel free to refer artix guide from this point onwards **(skip bootloader section!!)**
https://wiki.artixlinux.org/Main/Installation#Configure_the_base_system


