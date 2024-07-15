---
title: AEM SDK を再起動するにはどうすればよいですか？
description: AEM SDK を再起動するためのベストプラクティス
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 27%

---

# AEM SDK の再起動

Java™ プロセスを停止してAEM SDK を再起動すると、AEM開発環境で不整合が発生する場合があります。次のようなエラーが発生します。

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## 解決策

AEM SDK を再起動するには、アクティブなコマンドウィンドウに移動し、コマンド `Ctrl + C` 押して SDK を再起動します。

「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 Java™ プロセスの停止などの別の方法を使用してAEM SDK を再起動すると、AEM開発環境で不一致が発生する場合があります。

## 関連トピック

* [AEM Forms 用のローカル開発環境を設定](/help/forms/setup-local-development-environment.md)
* [アダプティブフォームのコアコンポーネントの有効化](/help/forms/enable-adaptive-forms-core-components.md)
