---
title: "インストール方法"
parent: "日本語"
grand_parent: "Translations"
has_children: true
---
# ArchWSLのセットアップ

## システム要件

* Windows 10 1709 Fall Creators Update x64以上
* Windows Subsystem for Linux機能が有効になっていること

## インストール手順
現在は2種類のパッケージを提供しています。

### 1: zipファイル

1. zipファイルを[ダウンロード](https://github.com/yuk7/ArchWSL/releases/latest)
2. zip内のすべてのファイルを同じディレクトリに展開します
   展開先のディレクトリには書き込み権限が必要です。
   例えば、`C:\Program Files` は使用できません。
3. `Arch.exe` を実行するとそのディレクトリ内でインストールが実行されます。

exeファイルのファイル名がWSLのインスタンス名に使用されます。
リネームすると、

### 2: appxパッケージ

1. [`.appx`と`.cer`ファイルをダウンロード](https://github.com/yuk7/ArchWSL/releases/latest)します。
2. `.cer`ファイルを"ローカルマシン"の"信頼されたルート証明機関"にインストールします。
   詳細は[証明書のインストール](Install-Certificate.md)ページを参照してください。
   証明書のインストールには管理者権限が必要です。
3. `.appx`をダブルクリックし、インストールします。

## インストール後の設定

### rootパスワードの設定

```shell
>Arch.exe
[root@PC-NAME]# passwd
```

### デフォルトユーザーの設定
ArchWikiを参照してください。
[Sudo](https://wiki.archlinux.jp/index.php/Sudo#.E3.82.A8.E3.83.B3.E3.83.88.E3.83.AA.E3.81.AE.E4.BE.8B)

[ユーザーとグループ](https://wiki.archlinux.jp/index.php/%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%81%A8%E3%82%B0%E3%83%AB%E3%83%BC%E3%83%97)

```shell
>Arch.exe
[root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
(sudoersファイルを設定します)

[root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
({username}というユーザーを追加します)

[root@PC-NAME]# passwd {username}
({username}というユーザーにパスワードを設定します)

[root@PC-NAME]# exit

>Arch.exe config --default-user {username}
    (デフォルトのユーザーを{username}に設定します)
```

デフォルトユーザーの変更がうまく行かない場合は,
コンピュータを再起動するか、LxssManagerサービスを再起動してください。
詳細は([issue #7](https://github.com/yuk7/ArchWSL/issues/7))を参照してください。

`LxssManager`を再起動するには、管理者権限のコマンドプロンプトで以下のコマンドを実行します:

```batch
net stop lxssmanager && net start lxssmanager
```

### キーリングの初期化
以下のコマンドを実行してｍキーリングを初期化してください。
(この作業はpacmanを使用する前に必ず必要です。)

```shell
>Arch.exe
[user@PC-NAME]$ sudo pacman-key --init

[user@PC-NAME]$ sudo pacman-key --populate

[user@PC-NAME]$ sudo pacman -Syy archlinux-keyring
```

### systemctl代替ツールをインストール (任意)

WSLはsystemdをサポートしていません。 しかし、systemdを代替するツールや別の名前空間を作成しsystemdを実行するツールを使用できます。
[既知の問題](Known-issues.md#systemdsystemctl)を参照してください。
