---
title: "알려진 이슈들"
parent: "한국어"
grand_parent: "Translations"
---
# 알려진 이슈들

## 실행기와 일반 사항
[wsldl 문서](https://git.io/wsldl-doc) 를 참조해주십시오.

## glibc
glibc의 새로운 버전은 WSL1과 호환성 오류가 있습니다.

WSL2를 사용하세요(그리고 WSL1은 너무 느립니다.)

## fakeroot
fakeroot은 SYSV IPC를 기본으로 사용중입니다.
WSL1은 그걸 더이상 지원하지 않습니다.

`fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp/) 를 사용해서 해결할 수 있습니다. (WSL2는 그런거 없으니까 제발 WSL2 쓰세요)

[fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz) 를 다운로드하고 ```pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz``` 를 실행하여 설치하십시오.

## Qt5
qt >=5.10 라이브러리는 WSL1에서 작동하지 않습니다. 이건 WSL 자체의 문제점입니다.(Please see [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

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

### WSL1 / WSL2
You can use a systemctl alternative script.
However, this is only partially compatible.

Download [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) and run ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` to install.

### WSL2
You can use systemd bottle "[subsystemctl](https://github.com/sorah/subsystemctl)" or "[genie](https://github.com/arkane-systems/genie)".

Using it, you can run systemd completely.

#### subsystemctl
You can download [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) and build it.

[See here for how to use it.](https://github.com/sorah/subsystemctl#usage)

#### genie
You can use [PKGBUILDs from here](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[See here for how to use it.](https://github.com/arkane-systems/genie#usage)
