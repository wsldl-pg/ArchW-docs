## Launcher
Please see [wsldl wiki](https://github.com/yuk7/wsldl/wiki)

## glibc
Old version of `ArchWSL`(<17121600) uses patched `glibc` named `glibc-wsl`. Because old version of it has bug in `spawni.c`.

It has been fixed in the official glibc package (=> 2.26-7).

For that reason **no patched glibc is needed anymore**.


## fakeroot
fakeroot is using SYSV IPC by default.
but WSL does not support it now.

You can use `fakeroot-tcp` package instead.

Download [fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz) and run ```pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz``` to install.

## Qt5
qt >=5.10 library doesn't work in WSL. This is an issue with WSL.(Please see [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

Please execute this line on root:
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```