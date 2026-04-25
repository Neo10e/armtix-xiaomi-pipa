# ARMtix Linux for Xiaomi Pad 6 (pipa)

## Troubleshooting

Below you will find a list of common issues and their solutions

> For issues specific to Artix, see https://wiki.artixlinux.org/Main/Troubleshooting

## Unbrick after using qbootctl / QBootControl

> Sometimes, when changing slots using qbootctl / QBootControl utility, you can corrupt the GPT table, which causes a brick, leaving the device stuck in an endless fastboot loop. This happens when slot isn’t marked as successful, then, after a few reboots A/B devices automatically switch to the inactive slot causing a lot of confusion and usually a soft-bricked device (it's fixed on ARMtix). Or when you mindlessly and randomly keep switching slots alternately (don’t do this!!). 

It's possible to unbrick without using EDL:
1. Download the [fastboot stock rom](https://xmfirmwareupdater.com/archive/miui/pipa) for your device
2. Decompress ROM
3. Go to the ROM folder
4. Go to the `images/` folder
5. Look for a file called `gpt_both4.bin`
6. Boot into fastboot mode (```adb reboot bootloader```)
7. Reflash 4th GPT partition
> Replace path/to/gpt_both4.bin with the actual path of file
```console
$ fastboot flash partition:4 path/to/gpt_both4.bin
```
##### Finished!

## libc++abi: terminating due to uncaught exception of type std::bad_alloc: std::bad_alloc

This is a known Fastboot issue on Windows. Make sure you are using the latest version of [Android Platform Tools](https://developer.android.com/tools/releases/platform-tools). If that doesn't help, flash the images from WSL or Linux (you can even do it from a bootable USB drive).

##### Finished!

## Sensors breaks

> [!NOTE]
> Sensors are enabled by default

### Check service status (optional)

#### OpenRC
```console
# rc-service hexagonrpcd-sdsp status
# rc-service iio-sensor-proxy-libssc status
```
#### Runit
```console
# sv status hexagonrpcd-sdsp
# sv status iio-sensor-proxy-libssc
```
#### s6
```console
# s6-svstat /run/service/hexagonrpcd-sdsp
# s6-svstat /run/service/iio-sensor-proxy-libssc
```
#### dinit
```console
# dinitctl status hexagonrpcd-sdsp
# dinitctl status iio-sensor-proxy-libssc
```

### If sensors are not working (restart services)

> Since services are enabled by default, a simple restart is usually enough. First, try simply restarting iio-sensor-proxy; if that doesn't work, then both

#### OpenRC
```console
# rc-service hexagonrpcd-sdsp restart
# rc-service iio-sensor-proxy-libssc restart
```
#### Runit
```console
# sv restart hexagonrpcd-sdsp
# sv restart iio-sensor-proxy-libssc
```
#### s6
```console
# s6-svc -r /run/service/hexagonrpcd-sdsp
# s6-svc -r /run/service/iio-sensor-proxy-libssc
```
#### dinit
```console
# dinitctl restart hexagonrpcd-sdsp
# dinitctl restart iio-sensor-proxy-libssc
```

### Monitor sensors
```console
$ monitor-sensors
```
If you see a change in value of each sensor, it means sensor is working

##### Finished!

## Audio does not work

Audio works, but not OOTB. You have to install it by yourself. I recommend using Pipewire instead of PulseAudio.

#### OpenRC
For OpenRC, assuming you installed the *-openrc packages, specifically: 
```console
# pacman -S pipewire-openrc pipewire-pulse-openrc wireplumber-openrc
```
Then enable services as user
```console
$ rc-update --user add pipewire default
$ rc-update --user add pipewire-pulse default
$ rc-update --user add wireplumber default
```

#### Runit
There are currently no official service packages for Runit. They will be added to [PKGBUILDs repo](https://github.com/Neo10e/PKGBUILDs-pipa) in the future

For now see https://wiki.artixlinux.org/Site/PipewireInsteadPulseaudio

#### s6
There are currently no official service packages for s6. They will be added to [PKGBUILDs repo](https://github.com/Neo10e/PKGBUILDs-pipa) in the future

For now see https://wiki.artixlinux.org/Site/PipewireInsteadPulseaudio

#### dinit
For dinit, assuming you installed the *-dinit packages, specifically: 
```console
# pacman -S pipewire-dinit pipewire-pulse-dinit wireplumber-dinit
```

> Also you will need dinit user services. See https://wiki.artixlinux.org/Main/Dinit#User_Services

Then enable services as user
```console
$ dinitctl enable pipewire
$ dinitctl enable pipewire-pulse
$ dinitctl enable wireplumber
```

### Reboot your device and check if audio works

For more infos or troubleshooting see Artix [wiki page](https://wiki.artixlinux.org/Site/PipewireInsteadPulseaudio) & Archlinux's [wiki page](https://wiki.archlinux.org/index.php/PipeWire)

##### Finished!

## Cracking sound

Sound is cracking sometimes, it can be fixed by rebooting device or by using headphones

##### Finished!

## Bluetooth does not work

> As of the date of writing this guide, bluetooth is working (not OOTB).

#### OpenRC
Install the init package and enable service
```console
# pacman -S bluez-openrc
# rc-update add bluetoothd default
```
#### Runit
Install the init package and enable service
```console
# pacman -S bluez-runit
# ln -s /etc/runit/sv/bluetoothd /run/runit/service
```
#### s6
Install the init package and enable service
```console
# pacman -S bluez-s6
# s6-service add default bluetoothd
# s6-db-reload
```
#### dinit
Install the init package and enable service
```console
# pacman -S bluez-dinit
# dinitctl enable bluetoothd
```
### Reboot your device and check if bluetooth works

> [!Note]
> If it still does not work, you will have to do some additional steps

In [pipa-armtix](https://github.com/Neo10e/pipa-armtix) repo, `bluez` vesrion is set to `5.86-4`. There have been instances where updating bluez caused bluetooth to break on pipa. If you want a newer version of bluetooth, install it from the [world](https://repo.armtixlinux.org/world) repo

```console
# pacman -S world/bluez
```

If this causes bluetooth to break, you can roll back bluez to the last working version from [pipa-armtix](https://github.com/Neo10e/pipa-armtix/tree/main/repo) repository

```console
# pacman -S pipa-armtix/bluez
```

For more infos or troubleshooting see Archlinux's [wiki page](https://wiki.archlinux.org/index.php/Bluetooth)

##### Finished!
