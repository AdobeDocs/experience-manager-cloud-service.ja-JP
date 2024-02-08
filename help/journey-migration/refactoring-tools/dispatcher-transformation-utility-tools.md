---
title: AEM Dispatcher コンバーターツール
description: AEM Dispatcher 上の既存の設定を、AEMas a Cloud Serviceの Dispatcher 上の設定に変換する方法について説明します。
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 94%

---

# AEM Dispatcher コンバーター {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher コンバーター"
>abstract="Adobe Experience Manager Dispatcher コンバーターは、AEM Dispatcher の既存の設定を AEM as a Cloud Service Dispatcher の設定に変換します。"

Adobe Experience Manager Dispatcher コンバーターは、AEM Dispatcher の既存の設定を AEM as a Cloud Service Dispatcher の設定に変換します。

## Dispatcher の概要 {#introduction-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュ、ロードバランシングまたはその両方を使用するツールです。AEM Dispatcher を使用すると、AEM サーバーを攻撃から保護するのにも役立ちます。したがって、エンタープライズクラスの web サーバーと共に Dispatcher を使用することで、AEM インスタンスのセキュリティを高められます。

>[!NOTE]
>Dispatcher の最も一般的な使用法は、**AEM パブリッシュインスタンス**&#x200B;からの応答をキャッシュして、外部に公開されている Web サイトの応答性とセキュリティを高めることです。

Dispatcher によるキャッシュの実行、ドキュメントの返却、ロードバランシングの実行の方法について詳しくは、[Dispatcher の概要](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

### Apache および Dispatcher の設定とテスト {#dispatcher-configurations-cloud}

ここでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。

詳しくは、[クラウド内の Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=ja) を参照してください。

## AEM Dispatcher コンバーター {#aem-dispatcher-converter}

AEM Dispatcher コンバーターは、既存のオンプレミスまたは Adobe Managed Services Dispatcher 設定を、AEM as a Cloud Service と互換性のある Dispatcher 設定にリファクタリングする機能を提供します。

## AEM Dispatcher コンバーターの使用 {#using-dispatcher-converter}

* Adobe Developer CLI を使用する場合：アドビでは、`aio-cli-plugin-aem-cloud-service-migration`（Adobe Developer CLI 用のAEM as a Cloud Service 的なコードリファクタリングプラグイン）を介して AEM Dispatcher コンバーターを使用することをお勧めします。

  プラグインをインストールして使用する方法について詳しくは、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;を参照してください。

* スタンドアロンユーティリティとして：AEM Dispatcher コンバーターツールは、スタンドアロンユーティリティとしても実行できます。

  このツールの使用方法やトラブルシューティングについて詳しくは、**[Git リソース：AEM Cloud Service Dispatcher コンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**&#x200B;を参照してください。

>[!IMPORTANT]
>AEM Dispatcher コンバーターは、NodeJS を使用して開発されました。アドビでは、NodeJS 10.0 以降をインストールすることをお勧めします。
