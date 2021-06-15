---
title: "알려진 이슈들"
parent: "한국어"
grand_parent: "Translations"
---
# 알려진 문제점

## 실행파일과 일반 사항
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
qt >=5.10 라이브러리는 WSL1에서 작동하지 않습니다. 이건 WSL 자체의 문제점입니다.([Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023) 을 참고하십시오.)

루트 권한으로 이 명령을 실행하십시오:
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```

## MySQL 8/MariaDB
MySQL >=8은 네이티브 AIO 인터페이스를 기본으로 사용합니다. WSL1은 기본으로 지원하지 않음으로, 수동으로 설정하십시오.
/etc/my.cnf.d/server.cnf 에서 `innodb_use_native_aio=0` 를 `[mysqld]` 섹션으로 추가 편집하십시오.
```
[mysqld]
innodb_use_native_aio=0
```

## D-Bus
Systemd D-Bus 데몬은 WSL1에서 작동하지 않습니다.
`dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/) 사용을 권장합니다.
[dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz) 를 다운로드하고 ```pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz``` 를 실행하여 설치하십시오.

D-Bus daemon을 시작하려면, 이걸 실행하십시오:
```
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl
WSL은 systemd를 지원하지 않습니다.
systemctl 대체 스크립트나 bottle응 사용하십시오.

### WSL1 / WSL2
systemctl 대체 스크립트를 사용가능합니다.
그러나, 부분적으로만 호환됩니다.

[systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) 를 다운로드하고 ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` 를 실행하여 설치하십시오.

### WSL2
systemd bottle "[subsystemctl](https://github.com/sorah/subsystemctl)" 또는 "[genie](https://github.com/arkane-systems/genie)"를 사용가능합니다.

그걸 사용하면, systemd 를 사용할 수 있습니다.

#### subsystemctl
[PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) 를 다운로드하고 빌드할 수 있습니다.

[사용법으로 이걸 보십시오.](https://github.com/sorah/subsystemctl#usage)

#### genie
[여기 있는 PKGBUILD들](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae)

[그것들을 어떻게 사용하는지 보십시오.](https://github.com/arkane-systems/genie#usage)
