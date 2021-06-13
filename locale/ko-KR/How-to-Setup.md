---
title: "셋업하는법"
parent: "한국어"
grand_parent: "Translations"
has_children: true
---
# ArchWSL 셋업하기

## 요구사항

* 윈도우 10 1709 또는 그 이상
* WSL(Windows용 Linux 하위 시스템) 활성화됨

## 설치 과정

ArchWSL을 설치하는 2가지 방법이 있습니다.

### 1: zip파일 설치

1. 설치 zip 파일을 [다운로드합니다](https://github.com/yuk7/ArchWSL/releases/latest) .
2. zip 파일에 있는 모든 파일들을 같은 디렉토리에 압축해제하십시오.
   쓰기 권한이 있는 경로에 압축 해제 하십시오.
   예를 들어, `C:\Program Files` 는 사용될 수 없습니다.
3. `Arch.exe` 를 실행해 루트 파일시스템을 압축해제하고 WSL에 등록하십시오. 프로세스는 자동입니다.

참고로, 실행파일의 이름은 WSL에서 등록되는 이름과 동일합니다.
이름을 변경하시면, 다중설치가 가능합니다.

### 2: appx 패키지

1. [`.appx` 와 `.cer` 를 다운로드하십시오](https://github.com/yuk7/ArchWSL/releases/latest)
2. `.cer` 파일을 기기의 "신뢰받는 루트 인증 기관" 에 설치하십시오.
   추가적인 설명이 필요하시다면, [증명서 설치 가이드](Install-Certificate.md) 를 따라주십시오.
   인증서 설치를 위해서는 관리자 권한이 필요합니다.
3. `.appx` 를 클릭해 설치하십시오.

## 설치 후에 셋업하기

### 루트 계정 비밀번호 설정하기

```shell
>Arch.exe
[root@PC-NAME user]# passwd
```

### 기본 유저 설정하기

ArchWiki를 참고하십시오.
[Sudo](https://wiki.archlinux.org/index.php/Sudo#Example_entries)
와
[User and groups](https://wiki.archlinux.org/index.php/Users_and_groups) 페이지도 참고하십시오.

```shell
>Arch.exe
[root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
(sudoers 설정)

[root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
(유저 추가)

[root@PC-NAME user]# passwd {username}
({username}의 비밀번호 설정)

[root@PC-NAME user]# exit

>Arch.exe config --default-user {username}
    ({username}을 기본 유저로 설정)
```

기본 유저가 변경되지 않았다면
([이슈 #7](https://github.com/yuk7/ArchWSL/issues/7)),
디바이스를 재시작하거나 LxssManager를 재시작하십시오.

`LxssManager` 를 재시작하려면, 이 명령을 실행하십시오:

```batch
net stop lxssmanager && net start lxssmanager
```

### 키링 초기화

이 명령을 실행하여 키링 초기화를 하십시오.
(pacman 사용을 위해서 필수적인 단계입니다.)

```shell
>Arch.exe
[user@PC-NAME]$ sudo pacman-key --init

[root@PC-NAME]$ sudo pacman-key --populate
```

### systemctl 설치하기(선택)

WSL 은 systemd를 기본적으로 사용하지 않지만, 여러가지의 솔루션이 있습니다.
[알려진 이슈](Known-issues.md#systemdsystemctl) 를 참고해주십시오.
