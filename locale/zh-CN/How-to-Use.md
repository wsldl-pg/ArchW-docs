---
title: "如何使用"
parent: "简体中文"
grand_parent: "Translations"
---
# 如何使用 (ArchWSL 安装以后)

## exe 用法

```shell
用法 :
    <无参数>
      - 以你的默认设置打开一个新的Shell。

    run <命令行>
      - 在此实例中运行你所给出的命令，继承当前Shell的所在目录。

    runp <命令行 (包含 windows 路径)>
      - 在此实例里运行转译过的命令行。

    config [setting [值]]
      - `--default-user <用户>`: 设定此实例的默认用户到 <用户>。
      - `--default-uid <uid>`: 设定此实例的默认用户 UID 到 <uid>。
      - `--append-path <on|off>`: 加入 Windows PATH 到 $PATH 的开关。
      - `--mount-drive <on|off>`: 挂载驱动器的开关。
      - `--default-term <default|wt|flute>`: 设置默认的终端窗口样式。

    get [setting]
      - `--default-uid`: 输出此实例的默认用户UID。
      - `--append-path`: 输出”加入 Windows PATH 到 $PATH“的开关状态。
      - `--mount-drive`: 输出”挂载驱动器”的开关状态。
      - `--wsl-version`: 输出此实例的WSL版本（1/2）。
      - `--default-term`: 输出此实例启动器的默认终端样式。
      - `--lxguid`: 输出此实例的 WSL GUID key。

    backup [contents]
      - `--tar`: 输出 backup.tar 到当前目录。
      - `--reg`: 输出设置注册表文件到当前目录。

    clean
      - 卸载此实例。

    help
      - 显示此帮助信息。
```

## 打开默认 Shell

```shell
>Arch.exe
[root@PC-NAME user]#
```

## 立刻运行一个命令后退出

```shell
>Arch.exe run uname -r
4.4.0-43-Microsoft
```

## 运行一个命令（转译路径）后退出

```shell
>Arch.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

## 更改默认用户（需要 ID 命令）

```shell
>Arch.exe config --default-user 用户

>Arch.exe
[user@PC-NAME dir]$
```

若是默认用户未被更改
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
请重启电脑或者重启 LxssManager 服务。

若要重启 `LxssManager`, 在管理员命令提示符中运行：

```batch
net stop lxssmanager && net start lxssmanager
```

## 备份 Rootfs

备份:

```shell
>Arch.exe backup
```

还原备份文件：

```shell
>Arch.exe install full/path/to/backup.tar
```

## 卸载实例

```shell
>Arch.exe clean
```
