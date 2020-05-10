## Launcher
Please see [wsldl wiki](https://github.com/yuk7/wsldl/wiki)

## glibc
Old version of `ArchWSL`(<17121600) uses patched `glibc` named `glibc-wsl`. Because old version of it has bug in `spawni.c`.

It has been fixed in the official glibc package (=> 2.26-7).

For that reason **no patched glibc is needed anymore**.


## fakeroot
fakeroot is using SYSV IPC by default.
but WSL1 does not support it now.

You can use `fakeroot-tcp` package instead. (WSL2 doesn't require that)

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


## systemd/systemctl
WSL does not supports systemd.
I recommend use systemctl alternative script or bottle.

#### WSL1 / WSL2
You can use a systemctl alternative script.
However, this is only partially compatible.

Download [systemd-altctl-1.4.3424-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.3424-1/systemd-altctl-1.4.3424-1-x86_64.pkg.tar.xz) and run ```pacman -U systemd-altctl-1.4.3424-1-x86_64.pkg.tar.xz``` to install.

#### WSL2
You can use systemd bottle "[genie](https://github.com/arkane-systems/genie)".

Using it, you can run systemd completely.

Please install AUR package [genie-systemd](https://aur.archlinux.org/packages/genie-systemd)

Run `genie -s` command to start the systemd daemon.