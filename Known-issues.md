## Launcher
'config *' command sometimes does not apply.(issue [#7](https://github.com/yuk7/ArchWSL/issues/7))

In that case please reboot the computer.

## glibc
Old version of `ArchWSL`(<17121600) uses patched `glibc` named `glibc-wsl`. Because old version of it has bug in `spawni.c`.

It has been fixed in the official glibc package (=> 2.26-7).

For that reason **no patched glibc is needed anymore**.


## fakeroot
fakeroot is using SYSV IPC by default.
but WSL is not supported it now.

You can use `fakeroot-tcp` package.

Download [fakeroot-tcp-1.22-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/17121600/fakeroot-tcp-1.22-1-x86_64.pkg.tar.xz) and run ```pacman -U fakeroot-tcp-1.22-1-x86_64.pkg.tar.xz``` to install.

## Qt5
qt5 library doesn't work in WSL. This is WSL issue.(Please see [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

Please excute this line on root:
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```