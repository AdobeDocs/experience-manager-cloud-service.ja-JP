---
title: AEM Dispatcher コンバーターツール
description: AEM Dispatcher コンバーターツール
translation-type: tm+mt
source-git-commit: 50d26dbec8281afec07ca56595b4b2a7b915eca9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 53%

---


# AEM Dispatcher コンバーター {#introduction}

Adobe Experience Managerディスパッチャーコンバーターは、既存のAEMディスパッチャー設定をCloud Serviceディスパッチャー設定としてAEMに変換します。

## Dispatcher の概要 {#introduction-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングを管理するツールです。AEM の Dispatcher は、AEM サーバーを攻撃から保護する目的にも役立ちます。したがって、Dispatcher をエンタープライズクラスの Web サーバーと組み合わせて使用すれば、AEM インスタンスのセキュリティを強化できます。

>[!NOTE]
>Dispatcher の最も一般的な使用法は、**AEM パブリッシュインスタンス**&#x200B;からの応答をキャッシュして、外部に公開されている Web サイトの応答性とセキュリティを高めることです。

Dispatcher によるキャッシュの実行、ドキュメントの返却、ロードバランシングの実行の方法については、[Dispatcher の概要](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/dispatcher.html)を参照してください。

### Apache および Dispatcher の設定とテスト {#dispatcher-configurations-cloud}

ここでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。

詳しくは、[クラウド内の Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) を参照してください。

## AEM Dispatcher コンバーター {#aem-dispatcher-converter}

AEM Dispatcher Converterは、既存のオンプレミスまたはAdobe Managed Services Dispatcher設定を、Cloud Service互換のディスパッチャー設定としてAEMにリファクタリングする機能を提供します。

## AEM Dispatcher コンバーターの使用 {#using-dispatcher-converter}

* AdobeI/O CLIを使用：AdobeI/O CLIのCloud Serviceコードリファクタリングプラグインとして、AEM Dispatcher Converterを `aio-cli-plugin-aem-cloud-service-migration` (AEMを使用して)使用することをお勧めします。

   詳しくは、 **[Gitリソースを参照してください。aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 」を参照してください。

* スタンドアロンユーティリティとして、AEM Dispatcher Converterツールは、スタンドアロンユーティリティとして実行することもできます。

   Refer to **[Git Resource: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** to learn about the usage and troubleshooting for this tool.

>[!IMPORTANT]
>AEM Dispatcher Converterは、NodeJSを使用して開発されました。 NodeJS 10.0以降をインストールすることをお勧めします。

