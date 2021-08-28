---
title: "How to Use"
---
# How to Use (after ArchWSL is installed)

## exe Usage

```
Usage :
    <no args>
      - Open a new shell with your default settings.

    run <command line>
      - Run the given command line in that instance. Inherit current directory.

    runp <command line (includes windows path)>
      - Run the given command line in that instance after converting its path.

    config [setting [value]]
      - `--default-user <user>`: Set the default user of this instance to <user>.
      - `--default-uid <uid>`: Set the default user uid of this instance to <uid>.
      - `--append-path <true|false>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <true|false>`: Switch of Mount drives
      - `--wsl-version <1|2>`: Set the WSL version of this instance to <1 or 2>
      - `--default-term <default|wt|flute>`: Set default type of terminal window.

    get [setting]
      - `--default-uid`: Get the default user uid in this instance.
      - `--append-path`: Get true/false status of Append Windows PATH to $PATH.
      - `--mount-drive`: Get true/false status of Mount drives.
      - `--wsl-version`: Get the version os the WSL (1/2) of this instance.
      - `--default-term`: Get Default Terminal type of this instance launcher.
      - `--lxguid`: Get WSL GUID key for this instance.

    backup [contents]
      - `--tar`: Output backup.tar to the current directory.
      - `--tgz`: Output backup.tar.tar to the current directory.
      - `--vhdx`: Output backup.ext4.vhdx to the current directory. (WSL2 only)
      - `--vhdxgz`: Output backup.ext4.vhdx.gz to the current directory. (WSL2 only)
      - `--reg`: Output settings registry file to the current directory.

    clean
      - Uninstall that instance.

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
>Arch.exe install full/path/to/backup.tar.gz
```

Restore/install backup vhdx:
```
>Arch.exe install full/path/to/backup.ext4.vhdx.gz
```

## Uninstall Instance

```
>Arch.exe clean
```
