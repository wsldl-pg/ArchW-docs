---
title: "如何安装"
parent: "简体中文"
grand_parent: "Translations"
has_children: true
---
# 如何安装

## 系统需求

* Windows 10 1709 秋季创意者更新或者更高版本
* 开启 `适用于 Linux 的 Windows 子系统` 功能

## 安装方法

有两种方法安装 ArchWSL.



### 方法 1：zip 文件
1. 下载 [[GH](https://github.com/yuk7/ArchWSL/releases/latest)/[镜像](https://gitee.com/yuk7/archwsl-mirror)] zip 安装包。
2. 解压缩 zip 文件中的全部内容到相同的目录。
   请解压到一个你拥有写权限的目录。
   例如， `C:\Program Files` 就不该被使用。
3. 运行 `Arch.exe` 来安装 rootfs 和注册表配置。

另外，EXE 文件的名称会同时用作你的 WSL 实例名称。

也就是说，如果复制多个 EXE 文件，并重命名成不同的名称，你就同时拥有了多个不同的 ArchWSL 并且互不冲突。

### 方法 2：appx 包
1. 从 [[GH](https://github.com/yuk7/ArchWSL/releases/latest)/[镜像](https://gitee.com/yuk7/archwsl-mirror)] 下载发布的 .appx 和 .cer 文件。

2. 安装 .cer 文件到 “本地计算机” 的 “受信任的根证书颁发机构”。
   更多详情，请查看对应[文档页面](https://wsldl-pg.github.io/ArchW-docs/locale/zh-CN/Install-Certificate/)。
3. 双击安装 appx 文件。

## 完成安装后的操作
### [若你使用 WSL1 ，你将**必须**修改一下 glibc 包。更多详情，请查看已知问题章节。](Known-issues.md#wsl1--wsl2)

### 设置Root密码

```shell
>Arch.exe
[root@PC-NAME]# passwd
```

### 设置默认用户

参考 ArchWiki 的
 [Sudo](https://wiki.archlinux.org/index.php/Sudo#Example_entries)
和
 [User and groups](https://wiki.archlinux.org/index.php/Users_and_groups) 页。

```shell
>Arch.exe
[root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
    (设置 sudoers 文件。)

[root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
(添加用户)

[root@PC-NAME]# passwd {username}
(设置默认用户密码)

[root@PC-NAME]# exit

>Arch.exe config --default-user {username}
    (设置默认用户)
```

如果默认用户密码被更改
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
请重启电脑或者用管理员CMD重启LxssManager。

要重启 `LxssManager`, 请运行：

```batch
net stop lxssmanager && net start lxssmanager
```

### 初始化密钥环（keyring）

请执行这些命令以初始化密钥环（keyring）。
(必须执行此步骤才可以使用 Pacman)

```shell
>Arch.exe
[user@PC-NAME]$ sudo pacman-key --init

[user@PC-NAME]$ sudo pacman-key --populate

[user@PC-NAME]$ sudo pacman -Syy archlinux-keyring
```

### 安装修改版 GLibc (WSL1 环境下必需)
Arch Linux 的官方 glibc 包是为新版内核（4.4以上版本）设计的，并且使用了未在 WSL1 被实现的系统调用。

因此，如果你不使用打过 Patch 的 Glibc 包，你的实例会完全开不起来。

WSL1 用户 **必须** 跟着[这些](Known-issues.md#wsl1--wsl2)步骤修改 GLibc 后才可使用。

### 安装 systemctl 替代品（可选）

WSL 并不支持 systemd，但是也有一些解决方案。
可以查看 [已知问题](Known-issues.md#systemdsystemctl)。
