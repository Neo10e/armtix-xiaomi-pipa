# ARMtix Linux for Xiaomi Pad 6 (pipa)

## Troubleshooting

Below you will find a list of common issues and their solutions

> For issues specific to Artix, see https://wiki.artixlinux.org/Main/Troubleshooting

## Unbrick after using qbootctl / QBootControl

> Sometimes, when changing slots using qbootctl / QBootControl utility, you can corrupt the GPT table, which causes a brick, leaving the device stuck in an endless fastboot loop. This happens when slot isn’t marked as successful, then, after a few reboots A/B devices automatically switch to the inactive slot causing a lot of confusion and usually a soft-bricked device (it's fixed on ARMtix). Or when you mindlessly and randomly keep switching slots alternately (don’t do this!!). 

It's possible to unbrick without using EDL:
- Download the [fastboot stock rom](https://xmfirmwareupdater.com/archive/miui/pipa) for your device
- Decompress ROM
- Go to the ROM folder
- Go to the `images/` folder
- Look for a file called `gpt_both4.bin`
- Boot into fastboot mode (```adb reboot bootloader```)
- Reflash 4th GPT partition
> Replace path/to/gpt_both4.bin with the actual path of file
```bash
fastboot flash partition:4 path/to/gpt_both4.bin
```
##### Finished!

## Audio does not work

Audio works, but not OOTB. You have to install it by yourself. I recommend using Pipewire instead of PulseAudio.

#### OpenRC
For OpenRC, assuming you installed the *-openrc packages, specifically: 
```bash
pacman -S pipewire-openrc pipewire-pulse-openrc wireplumber-openrc
```
Then enable services as user
```bash
rc-update --user add pipewire default
rc-update --user add pipewire-pulse default
rc-update --user add wireplumber default
```

#### Runit
There are currently no official service packages for Runit. They will be added to [pipa-armtix](https://github.com/Neo10e/pipa-armtix) repo in the future

For now see https://wiki.artixlinux.org/Site/PipewireInsteadPulseaudio

#### s6
There are currently no official service packages for s6. They will be added to [pipa-armtix](https://github.com/Neo10e/pipa-armtix) repo in the future

For now see https://wiki.artixlinux.org/Site/PipewireInsteadPulseaudio

#### dinit
For dinit, assuming you installed the *-dinit packages, specifically: 
```bash
pacman -S pipewire-dinit pipewire-pulse-dinit wireplumber-dinit
```

> Also you will need dinit user services. See https://wiki.artixlinux.org/Main/Dinit#User_Services

Then enable services as user
```bash
dinitctl enable pipewire
dinitctl enable pipewire-pulse
dinitctl enable wireplumber
```

### Reboot your device and check if audio works

For more infos or troubleshooting see Artix [wiki page](https://wiki.artixlinux.org/Site/PipewireInsteadPulseaudio) & Archlinux's [wiki page](https://wiki.archlinux.org/index.php/PipeWire)

##### Finished!

## Bluetooth does not work

> As of the date of writing this guide, bluetooth is working (not OOTB).

#### OpenRC
Install the init package and enable service
```bash
pacman -S bluez-openrc
rc-update add bluetoothd default
```
#### Runit
Install the init package and enable service
```bash
pacman -S bluez-runit
ln -s /etc/runit/sv/bluetoothd /run/runit/service
```
#### s6
Install the init package and enable service
```bash
pacman -S bluez-s6
s6-service add default bluetoothd
s6-db-reload
```
#### dinit
Install the init package and enable service
```bash
pacman -S bluez-dinit
dinitctl enable bluetoothd
```
### Reboot your device and check if bluetooth works

> [!Note]
> If it still does not work, you will have to do some additional steps;

Downgrade Bluez to an older version, for example:
```bash
pacman -U /var/cache/pacman/pkg/bluez-5.86-4-aarch64.pkg.tar.xz
```
> If you don't have any older version in your cache, try [this](../files/bluez-5.86-4-aarch64.pkg.tar.xz) version

For more infos or troubleshooting see Archlinux's [wiki page](https://wiki.archlinux.org/index.php/Bluetooth)

##### Finished!

