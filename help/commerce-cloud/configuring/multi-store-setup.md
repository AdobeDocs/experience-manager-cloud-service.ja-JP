---
title: マルチストアの設定
description: マルチストアの設定
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---


# マルチストアの設定 {#multi-store}

AEM CIFコアコンポーネントは複数のAEMサイト構造で使用でき、基盤となるGraphQLクライアントは異なるMagentoストア/ストア表示に接続できます。 これにより、複雑なマルチストア/マルチサイトの設定をプロジェクトに実装できます。

複数のMagentoストア表示をAdobe Experience Manager Sitesと統合するためのオプションについて詳しく説明するビデオチュートリアルです。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM Live Copyのマルチサイト管理機能と言語コピー機能は、Commerce Integration Frameworkと組み合わせて使用し、地域とロケールをまたいでサイトをグローバルに管理します。

推奨される設定は、AEMサイトとMagentoストア表示の間に1対1の関係を使用することです。

AEMサイトとAEM CIFコアコンポーネントを専用のストア表示に接続するには、次の手順に従います。

## 設定 {#configuration}

1. 「 [MagentoのWebサイト、店舗、表示」に記載されているパターンに従って、複数の店舗や表示を設定する](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. AEMとMagento間の接続が動作していることを確認します。

3. 次の手順に従って、CIFCloud Service設定の子設定を作成します。

   * AEMで、ツール/一般/ [設定ブラウザに移動します。](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 作成したベース設定を選択します
   * 上記のポイント2で説明した手順を使用して、新しい設定を作成します

   この新しい設定は、基本の設定の子設定として作成されます。 ツール/一般/設定ブラウザーに移動して、設定を作成できるようになりました。

4. AEMサイトへの子設定の割り当て

   * AEM Sitesコンソールに移動
   * サイト構造の地域または言語ルート(Veniaサンプルページ _の場合は_ /content/venia/usまたは/content/venia/us/en
   * ページを選択し、ページのプロパティを開きます
   * 「詳細設定」タブを選択します。
   * セクションで、手順で作成した設定を `Configuration` 選択します

## その他のリソース

* [MagentoWebサイト、ストア、表示](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIFコアコンポーネント — マルチストア/サイト設定](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [マルチサイトマネージャの使用](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [コンテンツの再利用：マルチサイトマネージャーとライブコピー](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
