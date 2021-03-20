---
title: "AppX用の証明書のインストール方法"
parent: "インストール方法"
#nav_order:
---

# Install Certificate for AppX

ArchWSL is not approved by Microsoft. Therefore, you will need to install a code
signing certificate manually if you want to install using the `.appx` package.
The certificate must be installed in the "Trusted Root Certificate Store" of the
local machine.

## Instructions

1. Open the .cer file and click "Install Certificate".

![screenshot1](img/cert/1.install.png)

2. Select "Local Machine" and Next.

![screenshot2](img/cert/2.to-localmachine.png)

3. Select "Place ~ in the following store" and Click Browse to select installation destination.

![screenshot3](img/cert/3.to-following.png)

4. Select "Trusted Root Certification Authorities" and OK.

![screenshot4](img/cert/4.to-rootstore.png)

5. done
