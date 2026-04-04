# ARMtix for Xiaomi Pad 6 (pipa)

This project is an unofficial port of Artix Linux to aarch64 for Xiaomi Pad 6 (pipa)

## ⚠️ Warning

ALL YOUR DATA WILL BE LOST!!! PROCEED WITH CAUTION!!! 

Note that ARMtix does NOT use systemd - it uses OpenRC, Runit, s6 or dinit (depending on the RootFS image you choose). If you have only ever used systemd-based distros, expect differences in service management, logging, and boot process. You are expected to be comfortable with non-systemd inits.

This guide assumes you know how a linux distro works and are capable of installing a gui yourself

**NO ONE IS NOT RESPONSIBLE FOR ANY DAMAGE YOU HAVE MADE TO YOUR DEVICE!!! YOU HAVE BEEN WARNED, IF YOU AREN'T COMFORTABLE MODDING YOUR TABLET OR YOU ARE PARANOID OF BRICKING YOUR DEVICE CLICK AWAY NOW!!! AGAIN! YOU HAVE BEEN WARNED!!!**

## Get Started

- [Installation](guide/install.md)

- [Post-Installation](guide/post-install.md)

- [Project status](guide/status.md)


## Miscellaneous

- Troubleshooting (TO DO)

- Tips & Tricks (TO DO)

- [Uninstallation](guide/uninstall.md)

## Support Groups
* [xiaomi_pipa](https://t.me/xiaomi_pipa) - Telegram group Xiaomi Pad 6 | Android/Linux Mainline/Windows
* [pipa_mainline](https://t.me/pipa_mainline) - Telegram group Xiaomi Pad 6 Mainline Linux

## Credits
- [PKGBUILDs-pipa](https://github.com/maakiopus/PKGBUILDs-pipa) for original pkgbuilds for alarm (Arch Linux ARM), by maakiono (thank you!!), forked and adapted for ARMtix
- [ARMtix](https://armtixlinux.org/) for port of Artix Linux to aarch64
- [Kernel port](https://github.com/pipa-mainline/linux) by adomerle, V1p0ll, Lukapanio, domin746826 and others
- [pmaports](https://gitlab.postmarketos.org/postmarketOS/pmaports) from which the pkgbuilds are loosely based on
- [Void templates](https://github.com/pipa-mainline/void-pipa) by adomerle
- [Artix gitea](https://gitea.artixlinux.org/packages) for pkgbuilds showing how init packages are built

## See Also
- [postmarketOS](https://wiki.postmarketos.org/wiki/Xiaomi_Pad_6_(xiaomi-pipa)) - pmOS for pipa
- [void-pipa](https://github.com/pipa-mainline/void-pipa) - Void Linux for pipa (EOL?)
- [void-linux-pipa](https://github.com/userg0d/void-linux-pipa) - Another Void Linux for pipa.
- [pipa-alarm](https://t.me/pipa_mainline/32978) - alarm (Arch Linux ARM) for pipa.
- [pocketblue](https://github.com/pocketblue/pocketblue) - Fedora Silverblue for pipa
- [pipa-fedora-builder](https://github.com/timoxa0/pipa-fedora-builder) - Non Atomic Fedora for pipa (EOL?)
- [pipa-fedora-builder-43](http://github.com/rr1111/pipa-fedora-builder-43) - Another Fedora for pipa.
- [xiaomi-pipa](https://github.com/TheMojoMan/xiaomi-pipa) - Ubuntu for pipa (EOL)