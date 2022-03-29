---
title: コマースマルチストアの設定
description: 複数のストアビューをAdobe CommerceからAEMにマッピングする方法を説明します。 これにより、マルチテナントおよび多言語のユースケースをプロジェクトでサポートできます。
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94,7f6e04a2-89e9-4613-8ea8-9dac1acea30b
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 67%

---

# コマースマルチストアの設定 {#multi-store}

AEM CIF コアコンポーネントは複数のAEMサイト構造で使用でき、基盤となる GraphQL クライアントの実装は異なるAdobe Commerceストア/ストア表示に接続できます。 これにより、複雑なマルチストア／マルチサイトの設定をプロジェクトに実装できます。

複数のAdobe Commerceストア表示をAdobe Experience Manager Sitesと統合するためのオプションについて詳しく説明するビデオチュートリアルです。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

地域とロケールをまたいでサイトをグローバルに管理するために、AEM マルチサイト管理のライブコピー機能および言語コピー機能を Commerce Integration Framework と組み合わせて使用できます。

推奨される設定は、AEMサイトとAdobe Commerceストア表示の間に 1 対 1 の関係を使用することです。

AEM サイトと AEM CIF コアコンポーネントを専用のストア表示に接続するには、次の手順に従います。

## 設定 {#configuration}

1. 次に示すパターンに従って、複数のストアや表示を設定します。 [Adobe Commerce Web サイト、ストア、表示](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. AEMとAdobe Commerceの間の接続が動作していることを確認します。

3. 次の手順に従って、CIF Cloud Service 設定の子設定を作成します。

   * AEM で、ツール／一般／[設定ブラウザー](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)に移動します。
   * 作成したベース設定を選択します。
   * 上記のポイント 2 で説明した手順を使用して、新しい設定を作成します。

   この新しい設定は、基本設定の子設定として作成されます。ツール／一般／設定ブラウザーに移動して、設定を作成できるようになっています。

   >[!TIP]
   >
   > コマースカタログは、ID または UID を使用して対処できます。Adobe Commerce 2.4.2 で UID が導入されました。コマースバックエンドがバージョン 2.4.2 以降の GraphQL スキーマをサポートしている場合にのみ、これを有効にしてください。

4. AEM Sites に子設定を割り当てます。

   * AEM Sites コンソールに移動します。
   * サイト構造の地域または言語ルート（Venia サンプルページの場合は /content/venia/us _または_ /content/venia/us/en）に移動します。
   * ページを選択し、ページのプロパティを開きます。
   * 「詳細」タブを選択します。
   * `Configuration` セクションで、手順で作成した設定を選択します。3

## その他のリソース

* [Adobe Commerce Web サイト、ストア、表示](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF コアコンポーネント - マルチストア／サイト設定](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [マルチサイトマネージャの使用](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html?lang=ja)
* [コンテンツの再利用：マルチサイトマネージャとライブコピー](/help/sites-cloud/administering/msm/overview.md)
