---
title: "Como configurar"
has_children: true
---
# Como configurar o ArchWSL

## Requisitos

* Windows 10 1709 Fall Creators Update 64 bits ou posterior.
* O recurso Windows Subsystem for Linux estar ativado.

## Instruções de instalação

Existem duas maneiras de instalar o ArchWSL.

### Método 1: arquivo zip

1. [Baixe](https://github.com/yuk7/ArchWSL/releases/latest) o zip do instalador.
2. Extraia todos os arquivos do arquivo zip para o mesmo diretório.
   Extraia para uma pasta que você tenha permissão de gravação.
   Por exemplo, `C:\Program Files` não pode ser usada porque o rootfs não pode ser modificado lá.
3. Execute `Arch.exe` para extrair o rootfs e registre no WSL

Note que o nome do executável é o que é usado como o nome da instância WSL.
Se você renomeá-lo, poderá ter várias instalações.

### Método 2: pacote appx

1. [Baixe o `.appx` e o `.cer`](https://github.com/yuk7/ArchWSL/releases/latest)
2. Instale o `.cer` no "Armazenamento de Autoridades de Certificação Confiáveis" da máquina local.
   Para obter detalhes, consulte a [página Instalar certificado](Install-Certificate.md).
   Você precisará de privilégios de administrador para instalar o certificado.
3. Instale o `.appx`

## Configuração após a instalação
### [Se você é um usuário do WSL1, você **deve** alterar o pacote glibc. Consulte Problemas conhecidos.](Known-issues.md#wsl1--wsl2)

### Configurando a senha de root

```shell
>Arch.exe
[root@NOME-PC]# passwd
```

### Configurar o usuário padrão

Veja
[Sudo](https://wiki.archlinux.org/index.php/Sudo#Example_entries)
e
[User and groups](https://wiki.archlinux.org/index.php/Users_and_groups).
no ArchWiki

```shell
>Arch.exe
[root@NOME-PC]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
(configurar o arquivo sudoers.)

[root@NOME-PC]# useradd -m -G wheel -s /bin/bash {usuário}
(adicionar usuário)

[root@NOME-PC]# passwd {usuário}
(definir senha de usuário padrão)

[root@NOME-PC]# exit

>Arch.exe config --default-user {usuário}
    (configuração para usuário padrão)
```

Se o usuário padrão não foi alterado
([issue #7](https://github.com/yuk7/ArchWSL/issues/7)),
reinicie o computador ou, alternativamente, reinicie o LxssManager em um prompt de
comando de Administrador.

Para reiniciar o `LxssManager`, execute isto:

```batch
net stop lxssmanager && net start lxssmanager
```

### Inicializar chaveiro

Execute estes comandos para inicializar o chaveiro.
(Esta etapa é necessária para usar o pacman.)

```shell
>Arch.exe
[usuario@NOME-PC]$ sudo pacman-key --init

[usuario@NOME-PC]$ sudo pacman-key --populate

[usuario@NOME-PC]$ sudo pacman -Syy archlinux-keyring
```

### Instalar o glibc corrigido (necessário no WSL1)
O glibc do Arch é construído para o kernel Linux 4.4 e superior e não funciona com o WSL1.

Os usuários do WSL1 **devem** sempre seguir as etapas em [Problemas conhecidos](Known-issues.md#wsl1--wsl2).

### Instalar a alternativa systemctl (opcional)
O WSL não tem suporte a systemd. No entanto, existem várias soluções.
Consulte [Problemas conhecidos](Known-issues.md#systemdsystemctl).