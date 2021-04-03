---
title: "既知の問題"
parent: "日本語"
grand_parent: "Translations"
---
# Known issues

## Launcher and Common
Please see [wsldl document](https://git.io/wsldl-doc)

## glibc
最新のglibcはWSL1と互換性がありません。
古いバージョンでglibcを固定するか、WSL2をしようしてください。

## fakeroot
fakerootはSYSV IPCをデフォルトで使用しています。
WSL1では、SYSV IPCをサポートしていません。

`fakeroot-tcp`[ᴬᵁᴿ](https://aur.archlinux.org/packages/fakeroot-tcp/) 代わりに使用できます。(WSL2ではSYSV IPCをサポートしているため、必要ありません。)

[fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/18082100/fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz)をダウンロードし、```pacman -U fakeroot-tcp-1.23-1-x86_64.pkg.tar.xz``` をシェルで実行するとインストールすることが出来ます。

## Qt5
qt >=5.10ライブラリはWSL1では動作しません。 これはWSL1の問題に起因します。(Please see [Microsoft/WSL#3023](https://github.com/Microsoft/WSL/issues/3023))

このコマンドを実行してください。:
```strip --remove-section=.note.ABI-tag /usr/lib/libQt5Core.so.5```

## MySQL 8/MariaDB
MySQL >=8 はネイティブAIOインターフェイスをデフォルトで使用します。 WSL1はそれに対応していません。
そのため、ネイティブAIOインターフェイスを使用しないように設定を変更する必要があります。
`/etc/my.cnf.d/server.cnf`を編集し、`innodb_use_native_aio=0` を `[mysqld]`セクションに追加します。
```
[mysqld]
innodb_use_native_aio=0
```

## D-Bus
SystemdのD-BusデーモンはWSL1では動作しません。
`dbus-x11`[ᴬᵁᴿ](https://aur.archlinux.org/packages/dbus-x11/)の使用を推奨します。
[dbus-x11-1.12.16-1-x86_64.pkg.tar.xz](https://github.com/yuk7/arch-prebuilt/releases/download/20051200/dbus-x11-1.12.16-1-x86_64.pkg.tar.xz)をダウンロードし、 ```pacman -U dbus-x11-1.12.16-1-x86_64.pkg.tar.xz``` をシェルで実行することでインストール出来ます。

D-Busデーモンを起動するには、以下のコマンドを実行します:
```
sudo mkdir /run/dbus -p
sudo dbus-daemon --system
```

## systemd/systemctl
systemdはWSLに対応していません。
systemctlを使用する場合は、systemctlの代替スクリプトやボトルツールを推奨します。

#### WSL1 / WSL2
systemctlの互換スクリプトを使用できます。
しかし、これには完全な互換性はありません。

[systemd-altctl-1.4.4181-1-any.pkg.tar.xz](https://github.com/yuk7/arch-systemctl-alt/releases/download/1.4.4181-1/systemd-altctl-1.4.4181-1-any.pkg.tar.xz)をダウンロードし、シェルで ```pacman -U systemd-altctl-1.4.4181-1-any.pkg.tar.xz``` を実行するとインストール出来ます。

#### WSL2
"[subsystemctl](https://github.com/sorah/subsystemctl)"や"[genie](https://github.com/arkane-systems/genie)"のようなsystemdのbottleを使用できます。

これらを使用すると、systemdはコンテナ内で正しく動作します。

##### subsystemctl
[PKGBUILD](https://raw.githubusercontent.com/sorah/arch.sorah.jp/master/aur-sorah/PKGBUILDs/subsystemctl/PKGBUILD)をダウンロードして、ビルドします。

[詳細はプロジェクトページを参照してください](https://github.com/sorah/subsystemctl#usage)

##### genie
[リンク先にあるPKGBUILD](https://gist.github.com/arlllk/7001c521de601f01735af5ca440f03ae)を使用することも出来ます。

[詳細はプロジェクトページを参照してください](https://github.com/arkane-systems/genie#usage)
