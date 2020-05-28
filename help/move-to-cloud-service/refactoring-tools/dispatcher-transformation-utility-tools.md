---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 17%

---


# AEMディスパッチャーコンバーター {#introduction}

Adobe Experience Manager Dispatcher Converterは、既存のAMSディスパッチャー設定を、クラウドサービスディスパッチャー設定としてAEMに変換します。

## ディスパッチャーの概要 {#introduction-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングを管理するツールです。AEM の Dispatcher は、AEM サーバーを攻撃から保護する目的にも役立ちます。したがって、Dispatcher をエンタープライズクラスの Web サーバーと組み合わせて使用すれば、AEM インスタンスのセキュリティを強化できます。

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

ディスパッチャーがキャッシュを実行し、ドキュメントを返し、ロードバランシングを実行する方法については、 [ディスパッチャーの概要](https://docs.adobe.com/content/help/ja-JP/experience-manager-dispatcher/using/dispatcher.html) を参照してください。

### Apache and Dispatcher Configuration and Testing {#dispatcher-configurations-cloud}

AEMをクラウドサービスのApache設定およびディスパッチャー設定として構造化する方法、およびCloud環境にデプロイする前にローカルで検証および実行する方法を学習する必要があります。

詳しくは、「クラウドの [ディスパッチャー](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) 」を参照してください。

## AEMディスパッチャーコンバーター {#aem-dispatcher-converter}

AEM Dispatcher Converterは、既存のAMSディスパッチャーの設定を、クラウドサービスディスパッチャーの設定としてAEMに変換するためのユーティリティです。 このユーティリティはAMSインスタンス用です。

実装されているコンバーターは、変換のガイドラインに従った **AEMDispatcherConfigConverter** です。

AMSをクラウドサービスディスパッチャー設定としてAdobe Experience Managerに変換する方法については、「AMSをクラウドサービスディスパッチャー設定としてAdobe Experience Managerに [変換する](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) 」を参照してください。

## AEM Dispatcher Converterの使用 {#using-dispatcher-converter}

次の節では、AEM Dispatcher Converterツールの使用に必要なリソースと情報について説明します。

詳しくは、 **[Gitリソースを参照してください。 AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**（AEMクラウドサービスディスパッチャーコンバーター）を参照して、このツールの使用方法、制限事項、トラブルシューティングについて学んでください。

>[!IMPORTANT]
>AEM Dispatcher ConverterはPython 3.7.3を使用して開発されています。Python 3.5以降をインストールすることをお勧めします。

## 制限事項 {#limitations}

AEM Dispatcher Converterは、提供されたディスパッチャー設定フォルダーの構造がCloud Managerディスパッチャーの設定で説明されている構造と似ていることを前提として機能します。


