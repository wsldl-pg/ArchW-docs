---
title: "Known issues"
---
# Known issues （已知问题）

## 快捷方式
请查看 [wsldl 的文档](https://git.io/wsldl-doc)。

## glibc
新版的 glibc 和 WSL1 有兼容问题。

你可以用WSL2规避此问题。
<!--
Old version of `ArchWSL`(<17121600) uses patched `glibc` named `glibc-wsl`. Because old version of it has bug in `spawni.c`.

It has been fixed in the official glibc package (=> 2.26-7).

For that reason **no patched glibc is needed anymore**.
-->

## fakeroot
fakeroot 默认使用 SYSV IPC，
但是WSL1目前还不支持它。

你可以使用转而使用 `fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp/) 包。 (WSL2 无此问题)

下载 [fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz) 然后运行 ```pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz``` 以安装。

## Qt5
qt >=5.10 库在WSL1不能使用，这是WSL的问题。(在 [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

请以Root执行这个：
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```

## MySQL 8/MariaDB
MySQL >=8 默认会使用使用原版的AIO interface。WSL1并不兼容它，因此你必须手动配置它。
编辑 /etc/my.cnf.d/server.cnf ，增加 `innodb_use_native_aio=0` 到 `[mysqld]` 。


```
[mysqld]
innodb_use_native_aio=0
```

## D-Bus
Systemd D-Bus 守护进程在WSL1不能使用。
我建议转而使用 `dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/)。
下载 [dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz) 并运行 ```pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz``` 以安装。

要启动 D-Bus 守护进程，运行：
```
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl
WSL不支持Systemd。
我建议使用Systemd替代脚本或容器。

#### WSL1 / WSL2
你可以用 systemctl 替代脚本，
不过它只能部分兼容 systemctl.

下载 [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) 然后运行 ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` 以安装。

#### WSL2
你可以使用 Systemd 容器 "[subsystemctl](https://github.com/sorah/subsystemctl)" 或是 "[genie](https://github.com/arkane-systems/genie)".

使用它们，你就可以使用完整的Systemd了。

##### subsystemctl
你可以下载 [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) 然后构建它。

[读这里了解更多信息。](https://github.com/sorah/subsystemctl#usage)

##### genie
你可以下载 [这里的 PKGBUILDs](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[读这里了解更多信息。](https://github.com/arkane-systems/genie#usage)
