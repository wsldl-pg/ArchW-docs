---
title: "Como usar"
---
# Como usar (após a instalação do ArchWSL)

## Uso do exe

```
Uso:
    <sem argumentos>
      - Abre um novo shell com suas configurações padrão.

    run <linha de comando>
      - Executa a linha de comando fornecida nessa instância. Herda o diretório atual.

    runp <linha de comando (inclui o caminho do Windows)>
      - Executa a linha de comando fornecida nessa instância após converter seu caminho.

    config [configuração [valor]]
      - `--default-user <usuário>`: Define o usuário padrão desta instância para <usuário>.
      - `--default-uid <uid>`: Define o uid de usuário padrão desta instância para <uid>.
      - `--append-path <true|false>`: Troca de Append Windows PATH para $PATH
      - `--mount-drive <true|false>`: Ativa ou desativa a unidades de montagem
      - `--wsl-version <1|2>`: Define a versão do WSL desta instância para <1 ou 2>
      - `--default-term <default|wt|flute>`: Define o tipo padrão da janela do terminal.

    get [configuração]
      - `--default-uid`: Obtém o uid de usuário padrão nesta instância.
      - `--append-path`: Obtém o status true/false de Append Windows PATH para $PATH.
      - `--mount-drive`: Obtém o status true/false das unidades de montagem.
      - `--wsl-version`: Obtém a versão do WSL (1/2) desta instância.
      - `--default-term`: Obtém o tipo de terminal padrão deste lançador de instâncias.
      - `--lxguid`: Obtém a chave WSL GUID para esta instância.

    backup [conteúdo]
      - `--tar`: Gera backup.tar no diretório atual.
      - `--tgz`: Gera backup.tar.tar no diretório atual.
      - `--vhdx`: Gera backup.ext4.vhdx no diretório atual. (somente WSL2)
      - `--vhdxgz`: Gera backup.ext4.vhdx.gz no diretório atual. (somente WSL2)
      - `--reg`: Gera um arquivo de registro de configurações no diretório atual.

    clean
      - Desinstala essa instância.

    help
      - Imprime esta mensagem de uso.
```


## Abrir um shell interativo

```
>Arch.exe
[root@NOME-PC usuario]#
```

## Executar um único comando e sair

```
>Arch.exe run uname -r
4.4.0-43-Microsoft
```

## Executar um comando com tradução de caminho e sair

```
>Arch.exe runp echo C:\Windows\System32\cmd.exe
/mnt/c/Windows/System32/cmd.exe
```

## Alterar o usuário padrão (comando id necessário)

```
>Arch.exe config --default-user usuario

>Arch.exe
[usuario@NOME-PC dir]$
```

Se o usuário padrão não foi alterado
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
reinicie o computador ou, alternativamente, reinicie o LxssManager em um prompt de
comando de Administrador.

Para reiniciar o `LxssManager`, execute isto:

```batch
net stop lxssmanager && net start lxssmanager
```

## Fazer backup de rootfs

Fazer o backup:

```
>Arch.exe backup
```

Restaurar/instalar o tarball de backup:

```
>Arch.exe install caminho/completo/para/o/backup.tar.gz
```

Restaurar/instalar backup vhdx:
```
>Arch.exe install caminho/completo/para/o/backup.ext4.vhdx.gz
```

## Desinstalar a instância

```
>Arch.exe clean
```