---
title: "使い方"
parent: "日本語"
grand_parent: "Translates"
---
# 使い方(インストール後)
## exe Usage

```
Usage :
    <引数なし>
      - デフォルト設定で新しいシェルを起動します

    run <command line>
      - 与えられたコマンドラインをインスタンス内で実行します。 カレントディレクトリが引き継がれます。

    runp <command line (windowsのパスを含む)>
      - 与えられたコマンドラインのパスを変換した上でインスタンス内で実行します。

    config [setting [value]]
      - `--default-user <user>`: インスタンスのデフォルトユーザーを<user>に設定します。
      - `--default-uid <uid>`: インスタンスのデフォルトユーザーのuidを<uid>に設定します。
      - `--append-path <on|off>`: Windows側のPATH設定をLinux側に引き継ぐ機能のon/offを設定します。
      - `--mount-drive <on|off>`: Windowsのドライブをマウントする機能のon/offを設定します。
      - `--default-term <default|wt|flute>`: デフォルトのターミナルを設定します。

    get [setting]
      - `--default-uid`: インスタンスのデフォルトユーザーのuidを取得します。
      - `--append-path`: Windows側のPATH設定をLinux側に引き継ぐ機能のon/offを確認します。
      - `--mount-drive`: Windowsのドライブをマウントする機能のon/offを確認します。
      - `--wsl-version`: WSLのバージョン(1/2)を確認します。
      - `--default-term`: このランチャーに設定されたデフォルトのターミナルを確認します。
      - `--lxuid`: システム内部で使用されているLxUIDを取得します。

    backup [contents]
      - `--tar`: カレントディレクトリにbackup.tarを出力します。
      - `--reg`: 設定のレジストリファイルをbackup.regとしてカレントディレクトリに出力します。
      
    clean
      - インスタンスをアンインストールします。

    help
      - helpを表示します。
```


## 対話シェルを起動

```
>Arch.exe
[root@PC-NAME user]#
```

## コマンドを実行し終了

```
>Arch.exe run uname -r
4.4.0-43-Microsoft
```

## 与えられたコマンドラインのパスを変換し実行

```
>Arch.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

## デフォルトユーザーを変更

```
>Arch.exe config --default-user user

>Arch.exe
[user@PC-NAME dir]$
```

デフォルトユーザーの変更がうまく行かない場合は,
コンピュータを再起動するか、LxssManagerサービスを再起動してください。
詳細は([issue #7](https://github.com/yuk7/ArchWSL/issues/7))を参照してください。

`LxssManager`を再起動するには、管理者権限のコマンドプロンプトで以下のコマンドを実行します:

```batch
net stop lxssmanager && net start lxssmanager
```

## rootfsをバックアップ

バックアップ:

```
>Arch.exe backup
```

バックアップしたtarをインストール/リストア:

```
>Arch.exe install full/path/to/backup.tar
```

## インスタンスをアンインストール

```
>Arch.exe clean
```
