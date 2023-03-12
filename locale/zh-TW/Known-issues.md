---
title: "已知問題"
parent: "繁體中文"
grand_parent: "Translations"
---
# 已知問題

## 快捷方式

請 [檢視 wsldl 的文件](https://git.io/wsldl-doc)。

## glibc
Arch 預設的 glibc 包是為新版本 Linux 內核的 syscall 設計的，而 WSL1 並不支援它們。

因此，如果你不使用打過 patch 的 glibc 包，你的實例會完全開不起來。

你可以使用 AUR 中的 `glibc-linux4`[ᴬᵁᴿ](https://aur.archlinux.org/packages/glibc-linux4) 包。

你可以從 archlinuxcn 社區倉庫安裝此包，以方便自動更新。
```
echo '[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch' >> /etc/pacman.conf
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring && sudo pacman -S glibc-linux4
```
當然，你也可以直接使用 AUR helper 安裝。
```
yay -S glibc-linux4
```

## fakeroot

fakeroot 預設使用 SYSV IPC，
但是 WSL1 目前還不支援它。

你可以轉而使用 `fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp) 包。 (WSL2 無此問題)

下載 [fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz) 然後執行 `pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz` 以安裝。

## Qt5

qt >=5.10 庫在 WSL1 不能使用，這是 WSL 的問題。(在 [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

請以 root 執行這個：
`strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5`

## MySQL 8/MariaDB

MySQL >=8 預設會使用使用原版的 AIO interface。WSL1 並不相容它，因此你必須手動配置它。
編輯 `/etc/my.cnf.d/server.cnf` ，增加 `innodb_use_native_aio=0` 到 `[mysqld]` 。

```text
[mysqld]
innodb_use_native_aio=0
```

## D-Bus

systemd D-Bus 守護程序在 WSL1 不能使用。
我建議使用 `dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/)。
下載 [dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz) 並執行 `pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz` 以安裝。

要啟動 D-Bus 守護程序，執行：

```bash
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl

WSL 並沒有 systemd 的原生支援。
如果你需要使用依賴 systemd 支援的程式，我們建議使用替代指令碼或容器。

### WSL1 / WSL2

你可以用 systemctl 替代指令碼，
不過它只能部分相容 systemctl。

下載 [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) 然後執行 `pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz` 以安裝。

### WSL2

你可以使用 systemd 容器 [subsystemctl](https://github.com/sorah/subsystemctl) 或是 [genie](https://github.com/arkane-systems/genie)。

使用它們，你就可以使用完整的 systemd 了。

#### subsystemctl

你可以下載 [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) 然後構建它。

[讀這裡瞭解更多資訊](https://github.com/sorah/subsystemctl#usage)。

#### genie

你可以下載 [這裡的 PKGBUILDs](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[讀這裡瞭解更多資訊](https://github.com/arkane-systems/genie#usage)。

#### Intel 顯示卡

ArchWSL 預設可能無法正常載入 Intel WSL 驅動，這會導致無法在 Intel 顯示卡上使用 D3D12 驅動程式。

導致這個問題的原因是 Intel WSL 驅動檔案連結了 ArchLinux 並不存在的庫檔案，你可以手動修復它們使其正常工作。

你需要先使用 `ldd` 檢視它們連結了哪些庫，例如: `ldd /usr/lib/wsl/drivers/iigd_dch_d.inf_amd64_49b17bc90a910771/*.so`，然後查詢標記為 `not found` 的庫。接著檢視 ArchLinux 軟體包倉庫是否有對應的包，如果有，安裝它們，問題或許就解決了。如果在軟體包倉庫找不到對應的庫檔案，那可能是庫檔案的版本後綴不一樣，比如 `libedit.so.0.0.68` 和 `libedit.so.2`，這時你可以試著為其建立一個指向現有版本的軟連結。

Issue: [#308](https://github.com/yuk7/ArchWSL/issues/308)
