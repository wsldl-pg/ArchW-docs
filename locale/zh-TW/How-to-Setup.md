---
title: "如何安裝"
parent: "繁體中文"
grand_parent: "Translations"
has_children: true
---
# 如何安裝

## 系統需求

* Windows 10 1709 秋季創作者更新或者更高版本
* 開啟 `適用於 Linux 的 Windows 子系統` 功能

## 安裝方法

有兩種方法安裝 ArchWSL.



### 方法 1：zip 檔案
1. 下載 [[GH](https://github.com/yuk7/ArchWSL/releases/latest) / [鏡像](https://gitee.com/yuk7/archwsl-mirror)] zip 安裝包。
2. 解壓縮 zip 檔案中的全部內容到相同的目錄。
   請解壓到一個你擁有寫許可權的目錄。
   例如， `C:\Program Files` 就不該被使用。
3. 執行 `Arch.exe` 來安裝 rootfs 和註冊表配置。

另外，EXE 檔案的名稱會同時用作你的 WSL 實例名稱。

也就是說，如果複製多個 EXE 檔案，並重命名成不同的名稱，你就同時擁有了多個不同的 ArchWSL 並且互不衝突。

### 方法 2：appx 包
1. 從 [[GH](https://github.com/yuk7/ArchWSL/releases/latest) / [鏡像](https://gitee.com/yuk7/archwsl-mirror)] 下載發佈的 .appx 和 .cer 檔案。

2. 安裝 .cer 檔案到 「本機電腦」 的 「受信任的根憑證授權單位」。
   更多詳情，請 [檢視對應的文件頁面](Install-Certificate.md)。
3. 雙擊安裝 appx 檔案。

## 完成安裝後的操作
### 若你使用 WSL1 ，你將**必須**修改一下 glibc 包。更多詳情，請 [檢視已知問題章節](Known-issues.md#wsl1--wsl2)。

### 設定Root密碼

```shell
>Arch.exe
[root@PC-NAME]# passwd
```

### 設定預設使用者

參考 ArchWiki 的
 [Sudo](https://wiki.archlinux.org/index.php/Sudo#Example_entries)
和
 [User and groups](https://wiki.archlinux.org/index.php/Users_and_groups) 頁。

```shell
>Arch.exe
[root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
    (設定 sudoers 檔案。)

[root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
(新增使用者)

[root@PC-NAME]# passwd {username}
(設定預設使用者密碼)

[root@PC-NAME]# exit

>Arch.exe config --default-user {username}
    (設定預設使用者)
```

如果預設使用者密碼被更改
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
請重啟電腦或者用管理員CMD重啟LxssManager。

要重啟 `LxssManager`, 請執行：

```batch
net stop lxssmanager && net start lxssmanager
```

### 初始化金鑰環（keyring）

請執行這些命令以初始化金鑰環（keyring）。
(必須執行此步驟才可以使用 Pacman)

```shell
>Arch.exe
[user@PC-NAME]$ sudo pacman-key --init

[user@PC-NAME]$ sudo pacman-key --populate

[user@PC-NAME]$ sudo pacman -Syy archlinux-keyring
```

### 安裝修改版 glibc (WSL1 環境下必需)
Arch 官方的 glibc 包是為新版內核（4.4以上版本）設計的，並且使用了未在 WSL1 被實現的系統呼叫。

因此，如果你不使用打過 patch 的 glibc 包，你的實例會完全開不起來。

WSL1 使用者 **必須** 跟著 [這些步驟](Known-issues.md#wsl1--wsl2) 修改 glibc 後才可使用。

### 安裝 systemctl 替代品（可選）

WSL 並不支援 systemd，但是也有一些解決方案。
可以 [檢視已知問題](Known-issues.md#systemdsystemctl)。
