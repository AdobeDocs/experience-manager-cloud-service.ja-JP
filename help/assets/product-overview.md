---
title: Content Hubの概要
description: Content Hubの詳細、主なメリット、アクセス方法、Content Hubで使用できるオプションに関するフィードバックの提供方法について説明します。
source-git-commit: 1aea6c6095aebd38f4c7c078701b29eebd3329b4
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Content Hubの概要 {#overview-content-hub}

![Content Hubの概要](assets/content-hub-overview.png)

Content Hubは、組織やビジネスパートナーがオンブランドのコンテンツにアクセスしやすくするために、Experience Manager Assetsas a Cloud Serviceの一部として利用できます。 大規模なアクティベーション用のアセットの配布と、マーケティングの俊敏性を向上させるためのオンブランドコンテンツバリアントの作成に重点を置いています。

## Content Hubを選ぶ理由

Content Hubには次のような主な利点があります。

**直感的なポータルで利用可能な、すべてのブランド承認済みアセットを検索して共有する**

AEM Assetsは唯一の情報源として機能し、承認されたすべてのアセットは、Content Hubでフラットな階層で自動的に利用できるようになり、検索エクスペリエンスが向上します。

**設定可能なユーザーインターフェイス**

Content Hub内の最も一般的なプロパティ（検索用のフィルター、アセットの追加または読み込み時に使用できるフィールド、アセットプロパティ、ブランディング用のバナーコンテンツなど）は設定でき、管理者は要件に基づいてContent Hub ユーザーインターフェイスを簡単に設定できます。

**クリエイティブ以外のユーザーが、ブランドを維持しながらコンテンツを編集およびリミックスできるようにする**

Content Hubでは、（Adobe Expressの使用権限がある場合は）Adobe Expressを持つ新しいコンテンツを作成できます。 使いやすいツールで既存のコンテンツを編集したり、テンプレートやブランド要素を使用してオンブランドのバリエーションを作成したり、Adobe Fireflyの最新の GenAI 機能で新しいコンテンツを作成したりできます。

**チーム全体でのコンテンツの使用方法に関するインサイトを取得**

[!DNL Content Hub] は、マーケティングキャンペーン、チャネル、様々な地域で使用されるアセットの使用状況の統計など、マーケティング関係者が頻繁に遭遇する一般的な課題に対処して、アセットに関する貴重なインサイトを提供します。 アセットのパフォーマンスと人気を明確に理解することで、ユーザーエクスペリエンスの向上に不可欠な実用的なインサイトを提供します。

## 前提条件 {#prerequisites-content-hub}

Experience Manager 6 月リリースas a Cloud Service

## Content Hubへのアクセス方法 {#access-content-hub}

ユーザーをに追加した後 [Content Hub製品プロファイル](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)の場合、Content Hubには次の方法でアクセスできます。

* 次のリンクを使用してContent Hubにアクセスします。

  `https://experience.adobe.com/#/assets/contenthub`

* experience.adobe com にログオンし、 **[!UICONTROL Experience Manager AssetsContent Hub]** で利用可能 **[!UICONTROL クイックアクセス]** セクション：
  ![Content Hubへのアクセス](assets/access-content-hub.png)

* experience.adobe com にログオンし、 **[!UICONTROL Experience Manager AssetsContent Hub]** 製品スイッチャーで使用できます。
  ![Content Hub アクセス方法 3](assets/access-content-hub-alternate.png)



## Content Hubに関するフィードバックの提供 {#provide-content-hub-feedback}

製品に関する改善点をレコメンデーションするには、 **[!UICONTROL Feedback]** 組織名の横にあるContent Hub ユーザーインターフェイスの上部。

必要に応じて、件名、レコメンデーションの説明、ファイルの添付を指定します。 クリック **[!UICONTROL Submit]** :Adobeにフィードバックを送信します。

![Content Hubのフィードバック](assets/content-hub-feedback.png)

## チーム用のContent Hubの設定 {#setup-content-hub}

チーム用にContent Hubをセットアップするには、次の手順に従います。

1. [Cloud Managerを使用してExperience Manager AssetsのContent Hubを有効にする](deploy-content-hub.md#enable-content-hub).

1. [Onboard Content Hub管理者](deploy-content-hub.md#onboard-content-hub-administrator).

1. [主なContent Hub ユーザーを追加](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [DAM 作成者または管理者がExperience Managerアセットを使用してアセットを承認](approve-assets.md).

1. [管理者は、他のユーザー向けにContent Hub ユーザーインターフェイスを設定できます](configure-content-hub-ui-options.md).

1. [チームの他のユーザーにContent Hub アクセス権を付与する](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Content Hub ポータルへのアクセス](#access-content-hub).

1. [Content Hubに関するフィードバックの提供](#provide-content-hub-feedback).


## 主な機能の詳細情報 {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Content Hubのデプロイ" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>Content Hub ユーザーインターフェイスの設定</strong>
      </a>
   </div>
   <p>
      <em>管理者によるContent Hub ユーザーインターフェイスの設定方法を説明します。 </em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="Content Hubで使用可能なアセットの検索" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>Content Hubで使用可能なアセットの検索</strong>
      </a>
   </div>
   <p>
      <em>様々な機能を利用して検索結果を絞り込む方法を説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Adobe Express を使用した画像の編集" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Adobe Expressを使用した画像の編集</strong>
      </a>
   </div>
   <p>
      <em>Adobe Expressを使用してContent Hubで画像のバリアントを作成する方法を説明します</em>
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
      <strong>Content Hubで使用可能なアセットの共有</strong>
      </a>
   </div>
   <p>
      <em>1 つまたは複数のアセットをリンクとして共有し、それらにアクセスする方法を説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="Content Hubでのコレクションの管理" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>Content Hubでのコレクションの管理</strong>
      </a>
   </div>
   <p>
      <em>アセットを使用してコレクションを作成し、管理する方法を説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Content Hubで使用可能なアセットの共有" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Content Hubでのアセットインサイトの表示</strong>
      </a>
   </div>
   <p>
      <em> コンテンツモジュールは、アセットに関する貴重なインサイトを提供し、マーケティング関係者が頻繁に遭遇する一般的な課題に対処します</em>
   </p>
</td>
</table>
