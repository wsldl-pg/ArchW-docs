#### exe Usage
```dos
Useage :
    <no args>
      - Launches the distro's default behavior. By default, this launches your default shell.

    run <command line>
      - Run the given command line in that distro.

    config [setting [value]]
      - `--default-user <user>`: Set the default user for this distro to <user>
      - `--default-uid <uid>`: Set the default user uid for this distro to <uid>
      - `--append-path <on|off>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <on|off>`: Switch of Mount drives

    get [setting]
      - `--default-uid`: Get the default user uid in this distro
      - `--append-path`: Get on/off status of Append Windows PATH to $PATH
      - `--mount-drive`: Get on/off status of Mount drives
      - `--lxuid`: Get LxUID key for this distro

    backup
      - Execute the backup function using tar.

    clean
     - Uninstalls the distro.

    help
      - Print this usage message.
```


#### Just Run exe
```dos
>Arch.exe
[root@PC-NAME user]#
```

#### Run with command line
```dos
>Arch.exe run uname -r
4.4.0-43-Microsoft

```

#### Change Default User(id command required)
```dos
>Arch.exe config --default-user user

>Arch.exe
[user@PC-NAME dir]$
```
If the default user has not been changed, please reboot the computer.(issue [#7](https://github.com/yuk7/ArchWSL/issues/7))

#### How to backup instance image
backup
```
>Arch.exe backup
```
restore/install backup tarball
```
>Arch.exe install backup.tar.gz
```


#### How to uninstall instance
```dos
>Arch.exe clean

```