---
title: "如何安装"
parent: "简体中文"
grand_parent: "Translations"
has_children: true
---
# 如何安装

## 系统需求

* Windows 10 1709 秋季创意者更新或者更新
* “适用于Linux的Windows子系统”处于开启状态。

## 安装方法

有两种方法安装ArchWSL.

### 方法 1: zip 文件

1. [下载](https://github.com/yuk7/ArchWSL/releases/latest) 安装器 zip。
2. 解压缩Zip文件中的全部内容到相同的目录。
   请解压到一个你有写权限的目录。
   例如“`C:\Program Files`”就不该被使用。
3. 运行 `Arch.exe` 以释放rootfs和注册表配置。

另外，EXE文件名称是用作WSL实例名称的名称。
也就是说，如果重命名它，就可以多次安装。

### 方法 2: appx 包

1. [下载](https://github.com/yuk7/ArchWSL/releases/latest) `.appx` 以及 `.cer`。
2. 安装 `.cer` 到 “本地计算机”的"受信任的根证书颁发机构"。
   更多详情，请查看《[安装证书](Install-Certificate.md)》。
3. 双击安装 `.appx` 文件。

## 完成安装后的操作

### 设置Root密码

```shell
>Arch.exe
[root@PC-NAME user]# passwd
```

### 设置默认用户

参考 ArchWiki 的 
[Sudo](https://wiki.archlinux.org/index.php/Sudo#Example_entries)
和
[User and groups](https://wiki.archlinux.org/index.php/Users_and_groups) 页。

```shell
>Arch.exe
[root@PC-NAME]# EDITOR=nano visudo
    %wheel      ALL=(ALL) ALL
    (设置 sudoers 文件。)

[root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
(添加用户)

[root@PC-NAME user]# passwd {username}
(设置默认用户密码)

[root@PC-NAME user]# exit

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
(要使用pacman，必须执行此步骤！)

```shell
>Arch.exe
[user@PC-NAME]$ sudo pacman-key --init

[root@PC-NAME]$ sudo pacman-key --populate
```

### 安装 systemctl 替代品（可选）

WSL 并不支持 Systemd，但是也有一些解决方案。
可以查看 [已知问题](Known-issues.md#systemdsystemctl)。
