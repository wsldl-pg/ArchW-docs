---
title: "AppX用の証明書のインストール方法"
parent: "インストール方法"
#nav_order:
---

# AppX用の証明書をインストールする

ArchWSLはMicrosoftの承認を受けていません。そのため、`.appx`パッケージを使用してインストールする場合は、署名証明書を手動で取得する必要があります。
証明書は、ローカルコンピューターの「信頼されたルート証明書ストア」にインストールされている必要があります。

## 手順

1. `.cer`ファイルを開き、「証明書のインストール」をクリックします。

![screenshot1](img/cert/1.install.png)

2. 「ローカルコンピューター」を選択し、「次へ」をクリックします。

![screenshot2](img/cert/2.to-localmachine.png)

3. 「証明書をすべて次のストアに配置する」を選択し、「参照」をクリックしてインストール先を選択します。

![screenshot3](img/cert/3.to-following.png)

4. 「信頼されたルート証明機関」を選択し、OKを押す。

![screenshot4](img/cert/4.to-rootstore.png)

5. インストール完了！