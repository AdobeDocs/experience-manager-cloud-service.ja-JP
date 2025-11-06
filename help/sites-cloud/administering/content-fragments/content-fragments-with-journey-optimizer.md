---
title: Adobe Journey Optimizer のコンテンツフラグメントの使用
description: 'コンテンツフラグメントを Adobe Experience Manager で統合および使用する方法について説明します。 '
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 100%

---

# Adobe Journey Optimizer のコンテンツフラグメント {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/get-started) は、コンテキストに沿ったつながりのあるパーソナライズされたエクスペリエンスを顧客に提供するのに役立ちます。Adobe Experience Manager（AEM）as a Cloud Service と Adobe Journey Optimizer（AJO）を統合すると、web、SMS、メールなどの AJO インバウンドチャネルと AJO アウトバウンドチャネルで AEM コンテンツを再利用できます。

例えば、次のことができます。

* [AEM コンテンツフラグメント](/help/sites-cloud/administering/content-fragments/overview.md)を [Journey Optimizer のメール](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/email/email-landing-page)コンテンツにシームレスに組み込む
* AEM から AJO エクスペリエンスを直接プレビューする

コンテンツフラグメントと AJO 間の接続により、AEM コンテンツへのアクセスと活用のプロセスが簡素化され、パーソナライズされた動的なキャンペーンやジャーニーを作成できます。

詳しくは、次の AJO ドキュメントを参照してください。

* [AEM でのコンテンツフラグメントの使用](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html?lang=ja#integrations)
* [AJO オファーとコンテンツフラグメントの統合](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Dispatcher 設定 {#dispatcher-configuration}

AJO が [Content Fragment Management API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/) を通じて AEM コンテンツフラグメントにアクセスできるようにするには、Dispatcher を次のように設定する必要があります。

* `dispatcher/src/conf.dispatcher.d/filters/filters.any` に移動します。

* 次の行を追加します。

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## その他の情報 {#further-information}

詳しくは、次のセクションを参照してください。

* [AJO 外部参照拡張機能](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)
