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
qt5.10 library doesn't work in WSL. This is WSL issue.

Downgrade qt5-base and qt5-script to 5.9.
1. Download [qt5-base-5.9.3-1-x86_64.pkg.tar.xz](https://archive.archlinux.org/packages/q/qt5-base/qt5-base-5.9.3-1-x86_64.pkg.tar.xz) and [qt5-script-5.9.3-1-x86_64.pkg.tar.xz](https://archive.archlinux.org/packages/q/qt5-script/qt5-script-5.9.3-1-x86_64.pkg.tar.xz).
2. run ```pacman -U qt5-base-5.9.3-1-x86_64.pkg.tar.xz qt5-script-5.9.3-1-x86_64.pkg.tar.xz``` to install base and script
3. Add qt5-base and qt5-script to IgnorePkg in pacman.conf