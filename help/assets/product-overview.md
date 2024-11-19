---
title: Content Hubの概要
description: コンテンツハブの詳細、その主なメリット、アクセス方法、コンテンツハブで使用可能なオプションに関するフィードバックの提供方法について説明します。
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 11%

---

# Content Hubの概要 {#overview-content-hub}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |----|-----|

![Content Hubの概要 ](assets/content-hub-overview.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

コンテンツハブは、Experience Manager Assets as a Cloud Service の一部として使用でき、組織とそのビジネスパートナーがオンブランドのコンテンツに簡単にアクセスできます。大規模なアクティベーション用のアセットの配布と、マーケティングの俊敏性を向上させるためのオンブランドコンテンツバリアントの作成に重点を置いています。

## Content Hubを選ぶ理由

Content Hubには次のような主な利点があります。

**ブランドが承認したすべてのアセットを直感的なポータルで検索して共有する**

AEM Assetsは唯一の情報源として機能し、承認されたすべてのアセットは、Content Hubでフラットな階層で自動的に利用できるようになり、検索エクスペリエンスが向上します。

**設定可能なユーザーインターフェイス**

Content Hub内の最も一般的なプロパティ（検索用のフィルター、アセットの追加または読み込み時に使用できるフィールド、アセットプロパティ、ブランディング用のバナーコンテンツなど）は設定でき、管理者は要件に基づいてContent Hub ユーザーインターフェイスを簡単に設定できます。

**クリエイティブ以外のユーザーが、ブランドを維持しながらコンテンツを編集およびリミックスできるよう支援**

Content Hubでは、（Adobe Expressの使用権限がある場合は）Adobe Expressを持つ新しいコンテンツを作成できます。 使いやすいツールで既存のコンテンツを編集したり、テンプレートやブランド要素を使用してオンブランドのバリエーションを作成したり、Adobe Fireflyの最新の GenAI 機能で新しいコンテンツを作成したりできます。

**チーム間でのコンテンツの使用方法に関するインサイトを得る**

[!DNL Content Hub] は、マーケティングキャンペーン、チャネル、様々な地域で使用されるアセットの使用状況統計など、マーケティング関係者が頻繁に発生する一般的な課題に対処し、アセットに関する貴重なインサイトを提供します。 アセットのパフォーマンスと人気を明確に理解することで、ユーザーエクスペリエンスの向上に不可欠な実用的なインサイトを提供します。

## 前提条件 {#prerequisites-content-hub}

Content Hubには、Experience Manageras a Cloud Serviceの 2024.6 リリース以降（最小バージョンは 2024.6.16799）の実稼動オーサー環境が必要です。

## Content Hubへのアクセス方法 {#access-content-hub}

[Content Hubを設定 ](/help/assets/deploy-content-hub.md) し、[Content Hub製品プロファイルにユーザーを追加 ](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) した後、次の方法を使用してContent Hubにアクセスできます。

* 次のリンクを使用してContent Hubにアクセスします。

  `https://experience.adobe.com/#/assets/contenthub`

* experience.adobe com にログオンし、「**[!UICONTROL クイックアクセス]** セクションの **[!UICONTROL Experience Manager Assets Content Hub]** をクリックします。
  ![Content Hub アクセス ](assets/access-content-hub.png)

* experience.adobe com にログオンし、製品スイッチャーにある **[!UICONTROL Experience Manager Assets Content Hub]** をクリックします。
  ![Content Hub アクセス メソッド 3](assets/access-content-hub-alternate.png)



## Content Hubに関するフィードバックの提供 {#provide-content-hub-feedback}

製品に関する改善点をお勧めするには、Content Hub ユーザーインターフェイス上部の組織名の横にある **[!UICONTROL フィードバック]** をクリックします。

必要に応じて、件名、レコメンデーションの説明、ファイルの添付を指定します。 「**[!UICONTROL 送信]**」をクリックして、フィードバックをAdobeに送信します。

![Content Hub フィードバック ](assets/content-hub-feedback.png)

## チーム用のContent Hubの設定 {#setup-content-hub}

チーム用にContent Hubをセットアップするには、次の手順に従います。

1. [Cloud Managerを使用してExperience Manager AssetsのContent Hubを有効にする ](deploy-content-hub.md#enable-content-hub)。

1. [Content Hub管理者をオンボーディングします ](deploy-content-hub.md#onboard-content-hub-administrator)。

1. [ 主なContent Hub ユーザーを追加 ](deploy-content-hub.md#onboard-content-hub-consumer-users) します。

1. [DAM 作成者または管理者がExperience Managerアセットを使用してアセットを承認 ](approve-assets.md)。

1. [ 管理者は、他のユーザー用にContent Hub ユーザーインターフェイスを設定できます ](configure-content-hub-ui-options.md)。

1. [ チームの追加ユーザーにContent Hub アクセス権を付与します ](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [Content Hub ポータルへのアクセス ](#access-content-hub)。

1. [Content Hubに関するフィードバックを提供 ](#provide-content-hub-feedback) ます。


## 主な機能の詳細情報 {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="コンテンツハブのデプロイ" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>Content Hub ユーザーインターフェイスの設定 </strong>
      </a>
   </div>
   <p>
      <em> 管理者によるContent Hub ユーザーインターフェイスの設定方法を説明します。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="Content Hubで使用可能なアセットの検索" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>Content Hubで使用可能なアセットを検索 </strong>
      </a>
   </div>
   <p>
      <em> 様々な機能を利用して検索結果を絞り込む方法を説明します </em>。
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Adobe Express を使用した画像の編集" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Adobe Expressを使用した画像の編集 </strong>
      </a>
   </div>
   <p>
      <em>Adobe Expressを使用してContent Hubで画像のバリアントを作成する方法を説明します </em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="Content Hubで使用可能なアセットの共有" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>Content Hubで使用可能なアセットの共有 </strong>
      </a>
   </div>
   <p>
      <em>1 つ以上のアセットをリンクとして共有し、それらにアクセスする方法を説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="コンテンツハブでのコレクションの管理" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>Content Hubでのコレクションの管理 </strong>
      </a>
   </div>
   <p>
      <em> アセットを使用してコレクションを作成し、管理する方法を説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Content Hubで使用可能なアセットの共有" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Content Hubでのアセットインサイトの表示 </strong>
      </a>
   </div>
   <p>
      コンテンツモジュール <em>、アセットに関する貴重なインサイトを提供し、マーケティング関係者が頻繁に発生する一般的な課題に対処 </em> ます。
   </p>
</td>
</table>
