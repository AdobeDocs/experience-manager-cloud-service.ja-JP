---
title: AEM Dispatcher コンバーターツール
description: AEM Dispatcher コンバーターツール
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 100%

---

# AEM Dispatcher コンバーター {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher コンバーター"
>abstract="Adobe Experience Manager Dispatcher コンバーターは、既存の AEM Dispatcher 設定を AEM as a Cloud Service Dispatcher 設定に変換します。"

Adobe Experience Manager Dispatcher コンバーターは、既存の AEM Dispatcher 設定を AEM as a Cloud Service Dispatcher 設定に変換します。

## Dispatcher の概要 {#introduction-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングを管理するツールです。AEM の Dispatcher は、AEM サーバーを攻撃から保護する目的にも役立ちます。したがって、Dispatcher をエンタープライズクラスの Web サーバーと組み合わせて使用すれば、AEM インスタンスのセキュリティを強化できます。

>[!NOTE]
>Dispatcher の最も一般的な使用法は、**AEM パブリッシュインスタンス**&#x200B;からの応答をキャッシュして、外部に公開されている Web サイトの応答性とセキュリティを高めることです。

Dispatcher によるキャッシュの実行、ドキュメントの返却、ロードバランシングの実行の方法については、[Dispatcher の概要](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

### Apache および Dispatcher の設定とテスト {#dispatcher-configurations-cloud}

ここでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。

詳しくは、[クラウド内の Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=ja) を参照してください。

## AEM Dispatcher コンバーター {#aem-dispatcher-converter}

AEM Dispatcher コンバーターは、既存のオンプレミスまたは Adobe Managed Services Dispatcher 設定を、AEM as a Cloud Service と互換性のある Dispatcher 設定にリファクタリングする機能を提供します。

## AEM Dispatcher コンバーターの使用 {#using-dispatcher-converter}

* Adobe I/O CLI を使用：`aio-cli-plugin-aem-cloud-service-migration`（Adobe I/O CLI 用の AEM as a Cloud Service コードリファクタリングプラグイン）を使用して AEM Dispatcher Converter を使用することをお勧めします。

   プラグインをインストールして使用する方法について詳しくは、**[Git リソース：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** を参照してください。

* スタンドアロンユーティリティとして：AEM Dispatcher コンバーターツールは、スタンドアロンユーティリティとして実行することもできます。

   このツールの使用方法やトラブルシューティングについては、**[Git リソース：AEM Cloud Service Dispatcher コンバーター](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**&#x200B;を参照してください。

>[!IMPORTANT]
>AEM Dispatcher コンバーターは、NodeJS を使用して開発されました。NodeJS 10.0 以降をインストールすることをお勧めします。
