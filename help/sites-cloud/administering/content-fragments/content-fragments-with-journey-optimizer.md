---
title: Adobe Journey Optimizerでのコンテンツフラグメントの使用
description: コンテンツフラグメントをAdobe Journey Optimizerと統合し、使用する方法を説明します。
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: 0fd7b2633488ceb14d34b1978a91a3a830d8762a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 10%

---

# Adobe Journey Optimizer のコンテンツフラグメント {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/get-started) は、顧客とのつながり、コンテキスト、パーソナライズされたエクスペリエンスを提供するのに役立ちます。 Adobe Experience Manager（AEM）as a Cloud ServiceをAdobe Journey Optimizer（AJO）と統合すると、AJOのインバウンドチャネルと、AJOのアウトバウンドチャネル（web、SMS、メールなど）でAEM コンテンツを再利用できます。

例えば、次のことができます。

* [AEM コンテンツフラグメント ](/help/sites-cloud/administering/content-fragments/overview.md) を [Journey Optimizer メール ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/email-landing-page) コンテンツにシームレスに組み込みます
* AEMからのAJO エクスペリエンスの直接プレビュー

コンテンツフラグメントとAJOを結び付けることで、AEM コンテンツへのアクセスおよび活用のプロセスが簡略化され、パーソナライズされた動的なキャンペーンやジャーニーを作成できます。

詳しくは、AJOのドキュメントを参照してください。

* [AJOでのコンテンツフラグメントの使用 ](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html?lang=ja#integrations)
* [AJO オファーとコンテンツフラグメントの統合 ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Dispatcher 設定 {#dispatcher-configuration}

AJOが [Content Fragment Management API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/) を介してAEM コンテンツフラグメントにアクセスできるようにするには、Dispatcherを設定する必要があります。

* `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

* 追加：

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## その他の情報 {#further-information}

詳しくは、次のセクションを参照してください。

* [AJO外部参照拡張機能 ](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)
