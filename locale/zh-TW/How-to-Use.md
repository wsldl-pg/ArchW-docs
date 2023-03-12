---
title: "如何使用"
parent: "繁體中文"
grand_parent: "Translations"
---
# 如何使用 (ArchWSL 安裝以後)

## exe 用法

```shell
用法 :
    <無參數>
      - 以你的預設設定打開一個新的 Shell。

    run <命令列>
      - 在此實例中執行你所給出的命令，繼承當前Shell的所在目錄。

    runp <命令列 (包含 windows 路徑)>
      - 在此實例里執行轉譯過的命令列。

    config [setting [值]]
      - `--default-user <使用者>`: 設定此實例的預設使用者到 <使用者>。
      - `--default-uid <uid>`: 設定此實例的預設使用者 UID 到 <uid>。
      - `--append-path <on|off>`: 加入 Windows PATH 到 $PATH 的開關。
      - `--mount-drive <on|off>`: 掛載驅動器的開關。
      - `--default-term <default|wt|flute>`: 設定預設的終端視窗樣式。

    get [setting]
      - `--default-uid`: 輸出此實例的預設使用者UID。
      - `--append-path`: 輸出「加入 Windows PATH 到 $PATH」的開關狀態。
      - `--mount-drive`: 輸出「掛載驅動器」的開關狀態。
      - `--wsl-version`: 輸出此實例的WSL版本（1/2）。
      - `--default-term`: 輸出此實例啟動器的預設終端樣式。
      - `--lxguid`: 輸出此實例的 WSL GUID key。

    backup [contents]
      - `--tar`: 輸出 backup.tar 到目前目錄。
      - `--reg`: 輸出設定註冊表檔案到目前目錄。

    clean
      - 解除安裝此實例。

    help
      - 顯示此幫助資訊。
```

## 打開預設 Shell

```shell
>Arch.exe
[root@PC-NAME user]#
```

## 立刻執行一個命令後退出

```shell
>Arch.exe run uname -r
4.4.0-43-Microsoft
```

## 執行一個命令（轉譯路徑）後退出

```shell
>Arch.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

## 更改預設使用者（需要 ID 命令）

```shell
>Arch.exe config --default-user 使用者

>Arch.exe
[user@PC-NAME dir]$
```

若是預設使用者未被更改
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
請重啟電腦或者重啟 LxssManager 服務。

若要重啟 `LxssManager`, 在管理員命令提示符中執行：

```batch
net stop lxssmanager && net start lxssmanager
```

## 備份 Rootfs

備份:

```shell
>Arch.exe backup
```

還原備份檔案：

```shell
>Arch.exe install full/path/to/backup.tar
```

## 解除安裝實例

```shell
>Arch.exe clean
```
