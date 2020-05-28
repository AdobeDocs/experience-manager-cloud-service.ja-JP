---
title: 移行後の段階
description: 移行後の段階
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 9%

---


# 移行後 {#post-migration}

移行後のフェーズでは、一時ファイルのクリーンアップ、継続的な開発とログの管理に関するベストプラクティスの確認を行う必要があります。

AEMをクラウドサービス環境としてトラブルシューティングするには、次のツールを使用できます。

* **開発者コンソール**
* **CRXDE Lite**
* **ログの管理**


## 開発者コンソール {#developer-console}

AEMをクラウドサービス開発者環境としてデバッグする方法については、開発環境、ステージ環境、実稼働環境について、Developer Consoleを参照してください。

開発ツールについて詳しくは、 [「クラウドサービスとしてのAEM用の](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) 実装」を参照してください。

## CRXDE Lite {#crxde-lite}

ユーザーは、ステージまたは実稼働環境ではなく、開発環境上の **CRXDE** Liteにアクセスできます。

>[重要]
>実行時に `/libs` およびなどの不変リポジトリに書き込むと、エラー `/apps` が発生します。 また、お客様は、ステージングおよび実稼動環境用の開発者ツールを利用できません。

CRXDE Liteを使用したAEMアプリケーションの開発方法については、 [『CRXDE Liteを使用した](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) 開発』を参照してください。

## ログの管理 {#managing-logs}

ユーザーは、選択した環境の使用可能なログファイルのリストにアクセスできます。

UI経由、またはCloud Manager経由のAPI経由でログにアクセスして管理する方法については、 [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) ログへのアクセスと管理を参照してください。

### その他のサポート {#additional-support}

クラウドサービスへのアクセスに関するご質問は、アドビの担当者またはAdobe AEM CQサポートポータルにお問い合わせください。
