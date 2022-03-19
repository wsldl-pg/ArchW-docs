---
title: "Problemas conhecidos"
---
# Problemas conhecidos

## Iniciador e Comum
Consulte o [documento wsldl](https://git.io/wsldl-doc).

## glibc
O glibc padrão é otimizado para o novo kernel e usa syscall, que não é implementado no WSL1.

Se você não usar glibc com um patch que não seja a linha principal, sua instância não será iniciada.

Você pode usar o pacote `glibc-linux4`[ᴬᵁᴿ](https://aur.archlinux.org/packages/glibc-linux4) em vez disso.

Você pode instalar a partir do repositório da comunidade archlinuxcn (pode atualizar automaticamente, recomendado)
```
echo "[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch" >> /etc/pacman.conf
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring && sudo pacman -S glibc-linux4
```
ou você pode instalar a partir com um auxiliar do AUR ("AUR helper")
```
yay -S glibc-linux4
```

## fakeroot
fakeroot está usando SYSV IPC por padrão.
mas o WSL1 não o suporta agora.

Você pode usar o pacote `fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp/) em vez disso. (WSL2 não exige isso)

Baixe [fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg .tar.xz) e execute ```pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz``` para instalar.

## Qt5
A biblioteca qt >=5.10 não funciona no WSL1. Este é um problema com o WSL. (Consulte [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

Execute esta linha na raiz:
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```

## MySQL 8/MariaDB
MySQL >=8 usa a interface AIO nativa por padrão. O WSL1 não tem suporte a ela, então você precisa configurá-la.
Edite /etc/my.cnf.d/server.cnf para adicionar `innodb_use_native_aio=0` à seção `[mysqld]`.
```
[mysqld]
innodb_use_native_aio=0
```

## D-Bus
O daemon Systemd D-Bus não funciona no WSL1.
Recomendamos usar `dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/).
Baixe [dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1 -x86_64.pkg.tar.xz) e execute ```pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz``` para instalar.

Para iniciar o daemon D-Bus, execute:
```
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl
O WSL não oferece suporte ao systemd nativamente, portanto, recomendamos o uso de um script alternativo para systemctl ou bottle para aplicativos que o exigem.

### WSL1 / WSL2
Você pode usar um script alternativo para systemctl.
No entanto, isso é apenas parcialmente compatível.

Baixe [systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl -1.4.4181-1-any.pkg.tar.xz) e execute ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` para instalar.

### WSL2
Você pode usar bottle de systemd  "[subsystemctl](https://github.com/sorah/subsystemctl)", "[genie](https://github.com/arkane-systems/genie)", "[wsl-distrod](https://github.com/nullpo-head/wsl-distrod)" ou "[bottled-shell](https://github.com/lungothrin/bottled-shell)".

O uso de qualquer uma das soluções mencionadas permitirá que você execute o systemd completamente.

#### subsystemctl
Você pode baixar [PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD) e construí-lo.

[Veja aqui como usá-lo.](https://github.com/sorah/subsystemctl#usage)

#### genie
Você pode usar [PKGBUILDs daqui](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae).

[Veja aqui como usá-lo.](https://github.com/arkane-systems/genie#usage)