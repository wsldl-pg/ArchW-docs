---
title: "既知の問題"
parent: "日本語"
grand_parent: "Translates"
---
# Known issues

## Launcher and Common
Please see [wsldl document](https://git.io/wsldl-doc)

## glibc
The new version of glibc has compatibility issues with WSL1.

You can use WSL2 to avoid it.
<!--
Old version of `ArchWSL`(<17121600) uses patched `glibc` named `glibc-wsl`. Because old version of it has bug in `spawni.c`.

It has been fixed in the official glibc package (=> 2.26-7).

For that reason **no patched glibc is needed anymore**.
-->

## fakeroot
fakeroot is using SYSV IPC by default.
but WSL1 does not support it now.

You can use `fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp/) package instead. (WSL2 doesn't require that)

Download [fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz) and run ```pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz``` to install.

## Qt5
qt >=5.10 library doesn't work in WSL1. This is an issue with WSL.(Please see [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

Please execute this line on root:
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```

## MySQL 8/MariaDB
MySQL >=8 uses the native AIO interface by default. WSL1 does not support it, so you need to configure it.
Edit /etc/my.cnf.d/server.cnf for add `innodb_use_native_aio=0` to `[mysqld]` section.
```
[mysqld]
innodb_use_native_aio=0
```

## D-Bus
Systemd D-Bus daemon doesn't work in WSL1.
I recommend use `dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/).
Download [dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz) and run ```pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz``` to install.

For start D-Bus daemon, run:
```
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl
WSL does not supports systemd.
I recommend use systemctl alternative script or bottle.

#### WSL1 / WSL2
You can use a systemctl alternative script.
However, this is only partially compatible.

Download [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) and run ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` to install.

#### WSL2
You can use systemd bottle "[subsystemctl](https://github.com/sorah/subsystemctl)" or "[genie](https://github.com/arkane-systems/genie)".

Using it, you can run systemd completely.

##### subsystemctl
You can download [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) and build it.

[See here for how to use it.](https://github.com/sorah/subsystemctl#usage)

##### genie
You can use [PKGBUILDs from here](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[See here for how to use it.](https://github.com/arkane-systems/genie#usage)
