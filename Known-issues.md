---
title: "Known issues"
---
# Known issues

## Launcher and Common
Please see the [wsldl document](https://git.io/wsldl-doc).

## glibc
The default glibc is optimized for the new kernel and uses syscall, which is not implemented in WSL1.

If you don't use glibc with a patch that isn't the mainline, your instance won't start.

You can use `glibc-linux4`[ᴬᵁᴿ](https://aur.archlinux.org/packages/glibc-linux4) package instead.

You can install from archlinuxcn community repository (can auto-update, recommend)
```
echo "[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch" >> /etc/pacman.conf
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring && sudo pacman -S glibc-linux4
```
or you can install from AUR helper
```
yay -S glibc-linux4
```

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
We recommend using `dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/).
Download [dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz) and run ```pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz``` to install.

For start D-Bus daemon, run:
```
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl

If you're using WSL 0.67.6 and above (see `wsl --version`), systemd is natively supported. To enable it, edit `/etc/wsl.conf` and then restart the distro.
```
[boot]
systemd=true
```

If you're using an older version of WSL, we recommend using a systemctl alternative script or bottle for apps that require it.

### WSL1 / WSL2
You can use a systemctl alternative script.
However, this is only partially compatible.

Download [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) and run ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` to install.

### WSL2
You can use systemd bottle "[subsystemctl](https://github.com/sorah/subsystemctl)", "[genie](https://github.com/arkane-systems/genie)", "[wsl-distrod](https://github.com/nullpo-head/wsl-distrod)" or "[bottled-shell](https://github.com/lungothrin/bottled-shell)".

Using any of the aformentioned solutions, will allow you to run systemd completely.

#### subsystemctl
You can download [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) and build it.

[See here for how to use it.](https://github.com/sorah/subsystemctl#usage)

#### genie
You can use [PKGBUILDs from here](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[See here for how to use it.](https://github.com/arkane-systems/genie#usage)
