---
title: Configure the Translation Connector
description: Learn how to connect AEM to a translation service.
exl-id: c91b2701-7ede-4d0b-93dd-3636c6638be2
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 12%

---

# Configure the Translation Connector {#configure-connector}

Learn how to connect AEM to a translation service.

## これまでの説明内容 {#story-so-far}

[](learn-about.md)

* Understand the importance of content structure to translation.
* Understand how AEM stores headless content.
* Be familiar with AEM&#39;s translation tools.

This article builds on those fundamentals so you can take the first configuration step and set up a translation service, which you will use later in the journey to translate your content.

## 目的 {#objective}

This document helps you understand how to set up an AEM connector to your chosen translation service. ドキュメントを読めば、以下が可能です。

* Understand the important parameters of the Translation Integration Framework in AEM.
* Be able to set up your own connection to your translation service.

## The Translation Integration Framework {#tif}

AEM&#39;s Translation Integration Framework (TIF) integrates with third-party translation services to orchestrate the translation of AEM content. これには 3 つの基本的な手順が必要です。

1. 翻訳サービスプロバイダーに接続します。
1. 翻訳統合フレームワーク設定を作成します。
1. Associate the configuration with your content.

The following sections describe these steps in more detail.

## 翻訳サービスプロバイダーへの接続 {#connect-translation-provider}

The first step is to choose which translation service you wish to use. There are many choices for human and machine translation services available to AEM. Most providers offer a translator package to be installed. [](#additional-resources)

>[!NOTE]
>
>The translation specialist is generally responsible for choosing which translation service to use, but the administrator typically is responsible for installing the required translation connector package.

For the purposes of this journey, we use the Microsoft Translator which AEM provides with a trial license out-of-the-box. [](#additional-resources)

If you choose another provider your administrator must install the connector package as per the instructions provided by the translation service.

>[!NOTE]
>
>Using the out-of-the-box Microsoft Translator in AEM does not require additional setup and works as-is without additional connector configuration.
>
>[](#create-config)[](#associate)
>
>[](#additional-resources)

## 翻訳統合フレームワーク設定の作成 {#create-config}

After the connector package for your preferred translation service is installed, you must create a Translation Integration Framework configuration for that service. この設定には以下の情報が含まれます。

* 使用する翻訳サービスプロバイダー
* 人間による翻訳と機械翻訳のどちらを実行するか
* Whether to translate other content that is associated with the Content Fragment such as tags

新しい翻訳設定を作成するには：

1. ************
1. コンテンツ構造内で設定を作成する場所に移動します。This is often based on a particular project or can be global.
   * For example, in this case, a configuration could be made globally to apply to all content, or just for the WKND project.

   ![](assets/translation-configuration-location.png)

1. ****
   1. ドロップダウンで「**設定タイプ**」を選択します。****
   1. 設定の&#x200B;**タイトル**&#x200B;を入力します。この&#x200B;**タイトル**&#x200B;によって、**Cloud Services** コンソールおよびページプロパティのドロップダウンリストで設定が識別されます。
   1. オプションとして、設定を格納するリポジトリノードに使用する&#x200B;**名前**&#x200B;を入力します。

   ![翻訳設定の作成](assets/create-translation-configuration.png)

1. ********

1. Remember that Content Fragments are stored as assets in AEM. ****

![](assets/translation-configuration.png)

1. 以下の情報を入力します。

   1. ************ For the purposes of this journey we assume machine translation.
   1. ****
   1. ****
   1. ****
   1. ****
   1. ****
   1. ****
   1. ****

1. 「**保存して閉じる**」をタップまたはクリックします。

You have now configured the connector to your translation service.

## Associate the Configuration with Your Content {#associate}

AEM is a flexible and powerful tool and supports multiple, simultaneous translation services via multiple connectors and multiple configurations. Setting up such a configuration is beyond the scope of this journey. However this flexibility means that you must specify which connectors and configuration should be used to translate your content by associating ths configuration with your content.

To do this, navigate to the language root of your content. For our example purposes this is

```text
/content/dam/<your-project>/en
```

1. ************
1. ****
1. ****
1. ********[](#connect-translation-provider)
1. ********
1. 「**保存して閉じる**」をタップまたはクリックします。

![](assets/select-cloud-service-configurations.png)

## 次の手順 {#what-is-next}

Now that you have completed this part of the headless translation journey you should:

* Understand the important parameters of the Translation Integration Framework in AEM.
* Be able to set up your own connection to your translation service.

[](translation-rules.md)

## その他のリソース {#additional-resources}

[](translation-rules.md)

* [](/help/sites-cloud/administering/translation/integration-framework.md)
* [](/help/sites-cloud/administering/translation/connect-ms-translator.md)
