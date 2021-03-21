---
title: "使い方"
parent: "日本語"
grand_parent: "Translates"
---
# How to Use (after ArchWSL is installed)

## exe Usage

```
Usage :
    <no args>
      - Open a new shell with your default settings.

    run <command line>
      - Run the given command line in that distro. Inherit current directory.

    runp <command line (includes windows path)>
      - Run the path translated command line in that distro.

    config [setting [value]]
      - `--default-user <user>`: Set the default user for this distro to <user>
      - `--default-uid <uid>`: Set the default user uid for this distro to <uid>
      - `--append-path <on|off>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <on|off>`: Switch of Mount drives

    get [setting]
      - `--default-uid`: Get the default user uid in this distro
      - `--append-path`: Get on/off status of Append Windows PATH to $PATH
      - `--mount-drive`: Get on/off status of Mount drives
      - `--lxguid`: Get WSL GUID key for this distro

    backup [contents]
      - `--tar`: Output backup.tar to the current directory
      - `--reg`: Output settings registry file to the current directory

    clean
      - Uninstall the distro.

    help
      - Print this usage message.
```


## Open an interactive shell

```
>Arch.exe
[root@PC-NAME user]#
```

## Run a single command and exit

```
>Arch.exe run uname -r
4.4.0-43-Microsoft
```

## Run a command with path translation and exit

```
>Arch.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

## Change Default User (id command required)

```
>Arch.exe config --default-user user

>Arch.exe
[user@PC-NAME dir]$
```

If the default user has not been changed
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
please reboot the computer or alternatively, restart the LxssManager in an Admin
command prompt.

To restart the `LxssManager`, run this:

```batch
net stop lxssmanager && net start lxssmanager
```

## Backup Rootfs

Backup:

```
>Arch.exe backup
```

Restore/install backup tarball:

```
>Arch.exe install full/path/to/backup.tar
```

## Uninstall Instance

```
>Arch.exe clean
```
