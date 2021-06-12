---
title: "사용법"
parent: "한국어"
grand_parent: "Translations""
---
# 사용법 (설치된 후)
## exe 사용법

```
Usage :
    <인수 없음>
      - 기본 설정으로 새로운 쉘을 엽니다.


    run <command line>
      - 현재 디렉토리에서 주어진 명령을 실행합니다.

    runp <command line (실행할 디렉토리 경로)>
      - 주어진 경로에서 명령을 실행합니다.

    config [setting [value]]
      - `--default-user <user>`: 배포판의 기본 유저를 <user> 로 설정
      - `--default-uid <uid>`: 배포판의 기본 유저 uid를 <uid> 로 설정
      - `--append-path <on|off>`: 환경 변수 PATH 를 $PATH 에 추가하기
      - `--mount-drive <on|off>`: 드라이브 마운트 켜기/끄기

    get [setting]
      - `--default-uid`: 배포판의 기본 uid 출력
      - `--append-path`: PATH를 $PATH에 추가했는지 확인하기
      - `--mount-drive`: 드라이브 마운트 설정 확인하기
      - `--lxguid`: 본 배포판의 WSL GUID 키 가져오기

    backup [contents]
      - `--tar`: backup.tar을 현재 디렉토리에 생성하기
      - `--reg`: 설정 레지스트리 파일을 현재 디렉토리에 생성하기

    clean
      - 설치를 제거합니다.

    help
      - 본 사용법 메시지를 출력합니다.
```


## 명령 쉘 열기

```
>Arch.exe
[root@PC-NAME user]#
```

## 명령 하나 실행하고 끝내기

```
>Arch.exe run uname -r
4.4.0-43-Microsoft
```

## 주어진 디렉토리에서 명령 실행하고 끝내기

```
>Arch.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

## 기본 사용자 바꾸기 (id 필수)

```
>Arch.exe config --default-user user

>Arch.exe
[user@PC-NAME dir]$
```

기본 유저가 바뀌지 않았으면, 디바이스를 재부팅하거나 LxssManager을 관리자 명령 프롬프트에서 재시작하십시오.
([issue #7](https://github.com/yuk7/ArchWSL/issues/7))

`LxssManager`를 재시작하려면, 이걸 실행하세요 :

```batch
net stop lxssmanager && net start lxssmanager
```

## 루트 파일시스템 백업하기 

백업:

```
>Arch.exe backup
```

백업된 tar 파일을 복구하거나 설치:

```
>Arch.exe install full/path/to/backup.tar
```

## 설치 제거하기

```
>Arch.exe clean
```
