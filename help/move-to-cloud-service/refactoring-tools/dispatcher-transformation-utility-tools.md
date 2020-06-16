---
title: AEM Dispatcher コンバーターツール
description: AEM Dispatcher コンバーターツール
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 94%

---


# AEM Dispatcher コンバーター {#introduction}

Adobe Experience Manager Dispatcher コンバーターは、既存の AMS Dispatcher 設定を AEM as a Cloud Service Dispatcher 設定に変換します。

## Dispatcher の概要 {#introduction-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングを管理するツールです。AEM の Dispatcher は、AEM サーバーを攻撃から保護する目的にも役立ちます。したがって、Dispatcher をエンタープライズクラスの Web サーバーと組み合わせて使用すれば、AEM インスタンスのセキュリティを強化できます。

>[!NOTE]
>Dispatcher の最も一般的な使用法は、**AEM パブリッシュインスタンス**&#x200B;からの応答をキャッシュして、外部に公開されている Web サイトの応答性とセキュリティを高めることです。

Dispatcher によるキャッシュの実行、ドキュメントの返却、ロードバランシングの実行の方法については、[Dispatcher の概要](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/dispatcher.html)を参照してください。

### Apache および Dispatcher の設定とテスト {#dispatcher-configurations-cloud}

ここでは、AEM as a Cloud Service の Apache および Dispatcher の設定を構築する方法と、クラウド環境にデプロイする前にローカルで検証および実行する方法について説明します。

詳しくは、[クラウド内の Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)を参照してください。

## AEM Dispatcher コンバーター {#aem-dispatcher-converter}

AEM Dispatcher コンバーターは、既存の AMS Dispatcher 設定を AEM as a Cloud Service Dispatcher 設定に変換するユーティリティです。このユーティリティは AMS インスタンス用です。

実装されているコンバーターは、変換ガイドラインに従った **AEMDispatcherConfigConverter** です。

AMS を Adobe Experience Manager as a Cloud Service Dispatcher 設定に変換する方法については、[AMS を Adobe Experience Manager as a Cloud Service Dispatcher 設定に変換する方法](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration)を参照してください。

## AEM Dispatcher コンバーターの使用 {#using-dispatcher-converter}

次の節では、AEM Dispatcher コンバーターツールの使用に必要なリソースと情報について説明します。

このツールの使用方法、制限事項、トラブルシューティングについては、**[Git リソース：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**を参照してください。

>[!IMPORTANT]
>AEM Dispatcher コンバーターは Python 3.7.3 を使用して開発されています。Python 3.5 以降をインストールしておくことをお勧めします。

## 制限事項 {#limitations}

AEM Dispatcher コンバーターは、提供された Dispatcher 設定フォルダーの構造が Cloud Manager の Dispatcher 設定で記述されている構造と同様であることを前提として機能します。


