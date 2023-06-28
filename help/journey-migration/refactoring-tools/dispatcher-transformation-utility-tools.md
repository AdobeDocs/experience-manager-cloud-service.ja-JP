---
title: AEM Dispatcher コンバーターツール
description: AEM Dispatcher コンバーターツール
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 34%

---

# AEM Dispatcher コンバーター {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher コンバーター"
>abstract="Adobe Experience Manager Dispatcher コンバーターは、AEM Dispatcher 上の既存の設定を、AEM as a Cloud Service Dispatcher 上の設定に変換します。"

Adobe Experience Manager Dispatcher コンバーターは、AEM Dispatcher 上の既存の設定を、AEM as a Cloud Service Dispatcher 上の設定に変換します。

## Dispatcher の概要 {#introduction-dispatcher}

Dispatcher は、Adobe Experience Managerのキャッシュ、ロードバランシング、またはその両方を使用するツールです。 AEM Dispatcher を使用すると、AEMサーバーを攻撃から保護するのにも役立ちます。 したがって、エンタープライズクラスの Web サーバーと共に Dispatcher を使用することで、AEMインスタンスのセキュリティを高めることができます。

>[!NOTE]
>Dispatcher の最も一般的な使用法は、**AEM パブリッシュインスタンス**&#x200B;からの応答をキャッシュして、外部に公開されている Web サイトの応答性とセキュリティを高めることです。

詳しくは、 [Dispatcher の概要](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) Dispatcher によるキャッシュの実行方法を学ぶには、ドキュメントを返してロードバランシングを実行します。

### Apache および Dispatcher の設定とテスト {#dispatcher-configurations-cloud}

AEMas a Cloud Serviceの Apache および Dispatcher 設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。

詳しくは、 [クラウド内の Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=ja) を参照してください。

## AEM Dispatcher コンバーター {#aem-dispatcher-converter}

AEM Dispatcher コンバーターは、既存のオンプレミスまたは Adobe Managed Services Dispatcher 設定を、AEM as a Cloud Service と互換性のある Dispatcher 設定にリファクタリングする機能を提供します。

## AEM Dispatcher コンバーターの使用 {#using-dispatcher-converter}

* Adobe Developer CLI を使用する場合：Adobeでは、 `aio-cli-plugin-aem-cloud-service-migration` (Adobe Developer CLI 用のAEMas a Cloud Service的なコードリファクタリングプラグイン )。

  詳しくは、 **[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** そのため、プラグインをインストールして使用する方法を学ぶことができます。

* スタンドアロンユーティリティとして：AEM Dispatcher Converter ツールは、スタンドアロンユーティリティとして実行することもできます。

  詳しくは、 **[Git リソース：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** このツールの使用方法やトラブルシューティングについて学ぶことができます。

>[!IMPORTANT]
>AEM Dispatcher コンバーターは、NodeJS を使用して開発されました。Adobeでは、NodeJS 10.0 以降がインストールされていることをお勧めします。
