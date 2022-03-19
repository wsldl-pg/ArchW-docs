---
title: Instalar certificado para AppX
parent: "Como configurar"
#nav_order:
---

# Instalar certificado para AppX

ArchWSL não é aprovado pela Microsoft. Portanto, você precisará instalar um código
assinando o certificado manualmente se você deseja instalar usando o pacote `.appx`.
O certificado deve ser instalado no repositório de certificados "Pessoas Confiáveis"
da máquina local.

## Instruções

1. Abra o arquivo .cer e clique em "Instalar Certificado".

![captura de tela 1](img/cert/1.install.png)

2. Selecione "Máquina Local" e Avançar.

![captura de tela 2](img/cert/2.to-localmachine.png)

3. Selecione "Colocar todos os certificados no repositório a seguir" e clique em Procurar para selecionar o destino da instalação.

![captura de tela 3](img/cert/3.to-following.png)

4. Selecione "Pessoas Confiáveis" e OK.

![captura de tela 4](img/cert/4.to-trustedpeople.png)

5. feito