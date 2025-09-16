---
title: AEM SDK を再起動する方法
description: AEM SDK を再起動するためのベストプラクティス
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: ht
source-wordcount: '102'
ht-degree: 100%

---

# AEM SDK の再起動

Java™ プロセスを停止して AEM SDK を再起動すると、AEM 開発環境で不整合が発生し、次のようなエラーが表示される場合があります。

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![AEM SDK の再起動エラー](/help/forms/assets/restart-sdk-error.png)

## 解決策

AEM SDK を再起動するには、アクティブなコマンドウィンドウに移動し、`Ctrl + C` キーコマンドを押して SDK を再起動します。

「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。Java™ プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が発生する場合があります。

## 関連トピック

* [AEM Forms 用のローカル開発環境を設定](/help/forms/setup-local-development-environment.md)

