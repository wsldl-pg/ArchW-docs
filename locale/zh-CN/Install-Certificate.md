---
title: 安装 AppX 所用的证书
parent: "如何安装"
#nav_order:
---

# 安装 AppX 的证书

ArchWSL 并不是 Microsoft 开发的。因此，你必须手动安装
一个代码签名证书才能正常使用 `.appx` 包。
这个证书需要被安装到本地计算机的“受信任人”存储区。

## 第一步

1. 打开 .cer 文件，然后点击“安装证书”。

![screenshot1](img/cert/1.install.png)

2. 选择“本地计算机”，然后下一步。

![screenshot2](img/cert/2.to-localmachine.png)

3. 选择 “将所有的证书都放入下列存储”，然后点击“浏览”选择安装目标。

![screenshot3](img/cert/3.to-following.png)

4. 现在选择“受信任人”。完成后点击确定。

![screenshot4](img/cert/4.to-trustedpeople.png)

5. 安装完成！
