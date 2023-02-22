---
title: "已知问题"
parent: "简体中文"
grand_parent: "Translations"
---
# 已知问题

## 快捷方式

请查看 [wsldl 的文档](https://git.io/wsldl-doc)。

## glibc
Arch 默认的 Glibc 包是为新版本 Linux 内核的 syscall 设计的，而 WSL1 并不支持它们。

因此，如果你不使用打过 Patch 的 Glibc 包，你的实例会完全开不起来。

建议使用 AUR 中的 `glibc-linux4`[ᴬᵁᴿ](https://aur.archlinux.org/packages/glibc-linux4) 包。

建议从 archlinuxcn 社区仓库安装此包，以方便自动更新。
```
echo '[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch' >> /etc/pacman.conf
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring && sudo pacman -S glibc-linux4
```
当然，你也可以直接使用 AUR 助手安装。
```
yay -S glibc-linux4
```

## fakeroot

fakeroot 默认使用 SYSV IPC，
但是 WSL1 目前还不支持它。

你可以转而使用 `fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp/) 包。 (WSL2 无此问题)

下载 [fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz) 然后运行 `pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz` 以安装。

## Qt5

qt >=5.10 库在 WSL1 不能使用，这是 WSL 的问题。(在 [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

请以 Root 执行这个：
`strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5`

## MySQL 8/MariaDB

MySQL >=8 默认会使用使用原版的 AIO interface。WSL1 并不兼容它，因此你必须手动配置它。
编辑 `/etc/my.cnf.d/server.cnf` ，增加 `innodb_use_native_aio=0` 到 `[mysqld]` 。

```text
[mysqld]
innodb_use_native_aio=0
```

## D-Bus

systemd D-Bus 守护进程在 WSL1 不能使用。
我建议使用 `dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/)。
下载 [dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz) 并运行 `pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz` 以安装。

要启动 D-Bus 守护进程，运行：

```bash
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl

WSL 并没有 systemd 的原生支持。
如果你需要使用依赖 systemd 支持的程序，我们建议使用替代脚本或容器。

### WSL1 / WSL2

你可以用 systemctl 替代脚本，
不过它只能部分兼容 systemctl。

下载 [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz) 然后运行 `pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz` 以安装。

### WSL2

你可以使用 systemd 容器 [subsystemctl](https://github.com/sorah/subsystemctl) 或是 [genie](https://github.com/arkane-systems/genie)。

使用它们，你就可以使用完整的 systemd 了。

#### subsystemctl

你可以下载 [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) 然后构建它。

[读这里了解更多信息。](https://github.com/sorah/subsystemctl#usage)

#### genie

你可以下载 [这里的 PKGBUILDs](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[读这里了解更多信息。](https://github.com/arkane-systems/genie#usage)

#### Intel 显卡

ArchWSL 默认可能无法正常加载 Intel WSL 驱动，这会导致无法在 Intel 显卡上使用 D3D12 驱动程序。

导致这个问题的原因是 Intel WSL 驱动文件链接了 ArchLinux 并不存在的库文件，你可以手动修复它们使其正常工作。

你需要先使用 `ldd` 查看它们链接了那些库，例如: `ldd /usr/lib/wsl/drivers/iigd_dch_d.inf_amd64_49b17bc90a910771/*.so`，然后查找标记为 `not found` 的库。接着查看 ArchLinux 软件包仓库是否有对应的包，如果有，安装它们，问题或许就解决了。如果在软件包仓库找不到对应的库文件，那可能是库文件的版本后缀不一样，比如 `libedit.so.0.0.68` 和 `libedit.so.2`，这时你可以试着为其创建一个指向现有版本的软链接。

Issue: [#308](https://github.com/yuk7/ArchWSL/issues/308)
