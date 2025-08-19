---
title: コマースマルチストアの設定
description: 複数のストアビューをAdobe CommerceからAdobe Experience Managerにマッピングする方法について説明します。 これにより、マルチテナントおよび多言語のユースケースをプロジェクトでサポートできます。
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 67%

---


# コマースマルチストアの設定 {#multi-store}

AEM CIF コアコンポーネントは複数の AEM サイト構造で使用でき、基盤となる GraphQL クライアントの実装は異なる Adobe Commerce ストア／ストア表示に接続できます。これにより、複雑なマルチストア／マルチサイトの設定をプロジェクトに実装できます。

複数の Adobe Commerce ストア表示を Adobe Experience Manager Sites と統合するためのオプションについて詳しく説明するビデオチュートリアルです。

>[!VIDEO](https://video.tv.adobe.com/v/34097/?quality=12&captions=jpn)

AEM マルチサイト管理のライブコピー機能および言語コピー機能を Commerce Integration Framework と組み合わせて使用すると、地域とロケールをまたいでサイトをグローバルに管理することができます。

推奨される設定は、AEM サイトとAdobe Commerce ストア表示の間に 1:1 の関係を使用することです。

AEM サイトと AEM CIF コアコンポーネントを専用のストア表示に接続するには、次の手順に従います。

## 設定 {#configuration}

1. [Adobe Commerceの Web サイト、ストア、表示に記載されているパターンに従って、複数のストアや表示を設定します。](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja)

1. AEM と Adobe Commerce 間の接続が動作していることを確認します。

1. 次の手順に従って、CIF Cloud Service 設定の子設定を作成します。

   * AEMで、ツール /一般/ [ 設定ブラウザー ](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) に移動します。
   * 作成したベース設定を選択します。
   * 上記のポイント 2 で説明した手順を使用して、設定を作成します。

   この新しい設定は、ベース設定の子設定として作成されます。ツール／一般／設定ブラウザーに移動して、設定を作成できます。

   >[!TIP]
   >
   > コマースカタログは、ID または UID を使用して対処できます。UID は Adobe Commerce 2.4.2 で導入されました。コマースバックエンドでバージョン 2.4.2 以降の GraphQL スキーマがサポートされている場合のみ、これを有効にしてください。

1. 子設定をAEM サイトに割り当てます。

   * AEM Sites コンソールに移動します。
   * サイトの地域または言語ルートに移動します。構造 例えば、Venia サンプルページの場合は `/content/venia/us _or_ /content/venia/us/en` です。
   * ページを選択して、ページのプロパティを開きます。
   * 「詳細」タブを選択します。
   * `Configuration` セクションで、手順 3 で作成した設定を選択します。

## その他のリソース {#additional-resources}

* [Adobe Commerce の web サイト、ストア、表示](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=ja)
* [AEM CIF コアコンポーネント - マルチストア／サイト設定](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [マルチサイトマネージャの使用](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html?lang=ja)
* [コンテンツの再利用：マルチサイトマネージャとライブコピー](/help/sites-cloud/administering/msm/overview.md)
