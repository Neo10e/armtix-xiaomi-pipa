# ARMtix Linux for Xiaomi Pad 6 (pipa)

## Tips & Tricks

Below you'll find a list of useful tips & tricks for ARMtix on pipa

For general tips & tricks for pipa, we should make a separate wiki/repo/channel in our free time. If one is created, it will be linked here

## Enable Arch / ALARM repos

> [!WARNING]
Any unofficial repositories (including mine, Arch, ALARM repositories and the AUR) are not supported by ARMtix. Use them at your own risk. Packages in these repositories get updated at a different rate than the official ones and may break your system. If you have any problems with your system after installing packages from these repositories, you will have to solve them yourself. If you need assistance, you can ask in the forum or [Support groups](../README.md#Support-Groups), but don't demand any help from the developers.

### Do I need this?

Arch / ALARM repos provide packages missing from ARMtix, but they may lack init scripts (you'll have to write them yourself) or cause dependency conflicts. Enable only if you're comfortable troubleshooting on your own.

### Installation 

#### All Arch / ALARM repositories are disabled by default. To enable them install the following package
```console
# pacman -S artix-archlinux-support
```
Follow the on-screen instructions to activate Arch / ALARM repositories you want which contain packages not yet in ARMtix repositories. Make sure the ARMtix repositories are listed above the Arch / ALARM repositories

Your enabled repos in `/etc/pacman.conf` can, for example, look like this:
```shell
#
# PIPA
#

[pipa-armtix]
SigLevel = Optional
Server = https://neo10e.github.io/pipa-armtix/repo/

#
# ARMTIX
#

[system]
SigLevel = Never
Include = /etc/pacman.d/mirrorlist

[world]
SigLevel = Never
Include = /etc/pacman.d/mirrorlist

[galaxy]
SigLevel = Never
Include = /etc/pacman.d/mirrorlist

[armtix]
SigLevel = Never
Include = /etc/pacman.d/mirrorlist

#
# ARCHLINUX
#

[extra]
Include = /etc/pacman.d/mirrorlist-arch

[community]
Include = /etc/pacman.d/mirrorlist-arch

[alarm]
Include = /etc/pacman.d/mirrorlist-arch

[aur]
Include = /etc/pacman.d/mirrorlist-arch
```

#### Then populate archlinuxarm keyring
```console
# pacman-key --populate archlinuxarm
```

- If you get an prompt about the package's signature marginal trust, add `SigLevel = Never` to the repo (at your own risk!)

- If your Arch downloads are slow, try enabling other mirrors near you in `/etc/pacman.d/mirrorlist-arch`. For ARMtix, all of them are enabled

#### Next synchronize the repositories
```console
# pacman -Sy
```

##### Finished!

## Using ZRAM for better multitasking

ZRAM creates a compressed swap space in RAM. It's faster than  swapping to your internal UFS storage and reduces its usage. Especially useful on pipa with 6-8GB RAM.

We'll use `zramen` – a lightweight utility that manages ZRAM swap space.

### Installation 

#### OpenRC
Install the init package and enable service
```console
# pacman -S zramen zramen-openrc
# rc-update add zramen default
```
> Config file is located in `/etc/conf.d/zramen`

#### Runit
Install the init package and enable service
```console
# pacman -S zramen zramen-runit
# ln -s /etc/runit/sv/zramen /run/runit/service
```
> Config file is located in `/etc/runit/sv/zramen/conf`
#### s6
Install the init package and enable service
```console
# pacman -S zramen zramen-s6
# s6-service add default zramen
# s6-db-reload
```
> Config file is located in `/etc/s6/config/zramen.conf`
#### dinit
Install the init package and enable service
```console
# pacman -S zramen zramen-dinit
# dinitctl enable zramen
```
> Config file is located in `/etc/dinit.d/config/zramen.conf`

### Configuration (optional)

Default config should be fine. If you want to increase the zram size or change the compression algorithm, edit the config file

> [!Note]
> Config path depends on your init, see above

<details>
<summary>Example config</summary>
<pre><code>ZRAM_SIZE=100
ZRAM_COMP_ALGORITHM=lz4
ZRAM_PRIORITY=32767
</code></pre>
</details>

### Check if ZRAM is active
```console
$ zramctl
```

##### Finished!

## Power & session management

ARMtix uses `elogind` (see [here](https://wiki.artixlinux.org/Main/Elogind)). The `loginctl` command lets you manage sessions and power from the terminal.

> Remember to add your user to the `power` group

### Enable lingering
Keep user services after logout

```console
$ loginctl enable-linger $USER
```

### Power commands
Manage power commands without needing root access
```console
$ loginctl suspend
$ loginctl reboot
$ loginctl poweroff
```

### Execute script at suspend

Put your script in `/lib/elogind/system-sleep/` and make it executable. An example of a custom sleep script: 

```sh
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "Going to $2..."
    ;;
  post/*)
    echo "Waking up from $2..."
    ;;
esac
```

##### Finished!
