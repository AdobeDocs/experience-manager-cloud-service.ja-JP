---
title: OpenAPI 機能を備えたDynamic Media
description: Dynamic Mediaを OpenAPI 機能と共に使用する理由や有効にする方法など、主要な概念について説明します。
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---

# OpenAPI 機能を備えたDynamic Media {#new-dynaminc-media-apis-overview}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

急速に変化する今日のデジタル世界において、ブランドのデジタルアセットの可能性を最大限に引き出すことは、競争に勝ち抜くために不可欠です。 総合的なデジタルAssets管理（DAM）ソリューションは、ブランドの整合性と卓越したカスタマーエクスペリエンスを確保しながら、アセットガバナンスを促進し、ブランドの一貫性を高め、コンテンツ配信を促進します。

OpenAPI 機能を備えたDynamic Mediaにより、DAM は、アセットガバナンスと配信を確実に行うための機敏で効率的なコンテンツサプライチェーンエコシステムのコアになります。

## Dynamic Mediaを OpenAPI 機能と共に使用する理由 {#dynamic-media-open-api-features}

OpenAPI 機能を備えたDynamic Mediaには、次のような主なメリットがあります。

* **シームレスな統合**: OpenAPI 機能を備えたDynamic Mediaは、包括的な検索および配信 API のセットを提供します。 これにより、開発者は簡単に [ アセットの配信をアプリケーションと統合 ](/help/assets/integrate-dynamic-media-open-apis.md) できます。 アプリケーションには、Adobeアプリケーションだけでなく、サードパーティのアプリケーションも含まれます。 承認済みアセットを検索して選択する [ マイクロフロントエンドアセットセレクターのユーザーインターフェイス ](/help/assets/overview-asset-selector.md) を提供します。 このセレクターは、React JS、Angular JS、Vanilla JS など、JavaScript フレームワークに基づくすべてのアプリケーションと簡単に統合できます。

* **デジタルアセットの一元管理**:DAM は、すべてのデジタルアセットの唯一の情報源です。 デジタルアセットはAEM Assetsで一元管理され、アセットのバイナリをコピーせずに、配信 URL を使用して参照することで消費側のアプリケーションに配信されます。

* **リアルタイムの更新**：バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに加えられた変更は、配信 URL に自動的に反映されます。 CDN を介して OpenAPI 機能を備えたDynamic Mediaに 10 分の短期間有効（TTL）値が設定されていると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。

* **ブランドの一貫性**:[ ブランドが承認したアセット ](/help/assets/approve-assets.md) のみがダウンストリームアプリケーションに公開されます。 [ ブランドマネージャーとマーケターは、ブランドアセットを厳格に管理しています ](/help/assets/restrict-assets-delivery.md)。 アセットの承認済みの最新バージョンのみを使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性を確保できます。

* **Web に最適化された配信**：デジタルアセットは、web に最適化された形式で配信され、デジタルエクスペリエンスのコア Web Vitals を強化します。 これには、画像用の WebP レンディション、ビデオ用の HLS または DASH プロトコルを介したアダプティブストリーミング、ドキュメント用の元のレンディションのサポートが含まれます。

* **動的アセット変換**：当社のシステムでは、画像修飾子と呼ばれる URL パラメーターを使用してその場で画像変換を行うことができます。 [ 例：幅、高さ、回転、反転、画質、切り抜き、形式、スマート切り抜き ](/help/assets/deliver-assets-apis.md)。 変換後のレンディションは動的に生成され、CDN を介してシームレスに配信されます。

* **アセットの安全な配信**:OpenAPI 機能を備えたDynamic Mediaは、デジタルアセットへのアクセスを制御するメカニズムを提供します。 ユーザーの役割またはグループを保護するアセットのメタデータとして指定し、事前に定義した期間 [ 許可されたユーザーのみがアセットにアクセスできる ](/help/assets/restrict-assets-delivery.md) を設定できます。 セキュリティで保護されているアセットの配信 URL は、制限された期間中に、権限のないユーザーに対して解決されません。

* **十分な情報に基づいた意思決定を行うためのデータインサイト（今後）:** アセットの管理や配信に加えて、CDN でのアセット配信に関する配信データインサイトを取得するため、ブランドマネージャーはチャネルをまたいで配信指標を追跡できます。 これにより、アセットガバナンスと配信戦略を継続的に最適化するために、データに基づく意思決定を行うことができます。

![Dynamic Media Open API のデータフロー図 ](assets/dm-openapi-dfd.png)

## OpenAPI 機能を使用してDynamic Mediaにアクセスするための前提条件 {#prerequisites-dynaminc-media-open-apis}

OpenAPI 機能を使用してDynamic Mediaにアクセスするには、次のライセンスが必要です。

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## OpenAPI 機能でDynamic Mediaを有効にする方法 {#enable-dynamic-media-open-apis}

AEM as a Cloud Serviceで OpenAPI 機能を使用してDynamic Mediaを有効にするリクエストを送信する前に、そのリクエストがまだ有効になっていないことを確認します。

[ 前提条件 ](#prerequisites-dynaminc-media-open-apis) が満たされ、OpenAPI 機能を持つDynamic MediaがAEM as a Cloud Service インスタンスで有効になっている場合、リポジトリ内の承認済みアセットごとに 1 つの配信 URL を使用できます。 配信 URL のコピー方法について詳しくは、[ 承認済みアセットの配信 URL のコピー ](approve-assets.md#copy-delivery-url-approved-assets) を参照してください。 Adobeは、サポートチケットを送信して有効にする前に、この方法を使用して、OpenAPI 機能を持つDynamic MediaがAEM as a Cloud Serviceで有効になっていることを確認することをお勧めします。

AEM as a Cloud Serviceで OpenAPI 機能を備えたDynamic Mediaを有効にするには、次の詳細を記載したAdobeサポートチケットを送信します。

* Cloud Serviceプログラムおよび環境 ID

* OpenAPI 機能統合を使用してDynamic Mediaで解決するユースケースの詳細です。

* OpenAPI 機能を使用してDynamic Mediaと統合するダウンストリームアプリケーションの詳細。

  >[!NOTE]
  >
  Adobe以外のアプリケーションと統合するには、アプリケーションがホストされている許可リストにドメイン名を指定します。

* 統合プロジェクトに関わる主要顧客連絡先の詳細。

* 主要なAdobeアカウントチームメンバーのリスト （電子メール）。

サポートチケットを送信すると、AdobeはCloud Service環境で OpenAPI 機能を備えたDynamic Mediaを有効にし、IMS クライアント ID などの詳細を共有して、統合を進めることができます。

>[!NOTE]
>
OpenAPI 機能を持つDynamic Mediaが無効になるのを防ぐため、任意のコンテンツパッケージから `/conf/global/settings/dam/assets-configurations/assetdelivery` を除外します。

## 主な機能の詳細 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="Experience Manager Assetsでのアセットの承認" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>Experience Manager Assetsでのアセットの承認 </strong>
      </a>
   </div>
   <p>
      <em>AEM Assetsでアセットを承認してアセット管理を効率化し、アセットの処理に関する制御された効率的なプロセスを確保します </em>。
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="AEM Assetsとダウンストリームアプリケーションの統合" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>AEM Assetsとダウンストリームアプリケーションの統合 </strong>
      </a>
   </div>
   <p>
      <em> 検索および配信 API を使用して独自のカスタムユーザーインターフェイスをExperience Manager Assets リポジトリと統合するか、Adobeのマイクロフロントエンドアセットセレクターを使用します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Adobeのアセットセレクター" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Adobeのマイクロフロントエンドアセットセレクター </strong>
      </a>
   </div>
   <p>
      <em>AEM Assets リポジトリとやり取りしてアセットを検索し、アプリケーションのオーサリングエクスペリエンスで使用するユーザーインターフェイス。</em>
   </p>
</td>
</table>
<table>



<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="アセットのExperience Manager Assets リポジトリの検索" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Experience Manager Assets リポジトリ内のアセットの検索 </strong>
      </a>
   </div>
   <p>
      <em> ダウンストリームアプリケーションに配信できるように、AEM Assets リポジトリ内のアセットを検索します </em>。
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="ダウンストリームアプリケーションへのアセットの配信" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong> ダウンストリームアプリケーションへのアセットの配信 </strong>
      </a>
   </div>
   <p>
      <em> 配信 URL を使用して、統合されたダウンストリームアプリケーションにアセットを配信します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Experience Managerー内のアセットへのアクセスを制限する" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Experience Managerー内のアセットへのアクセスの制限 </strong>
      </a>
   </div>
   <p>
      DAM 管理者または Brand Manager<em>、AEM as a Cloud Service オーサーインスタンス上で承認済みアセットのロールを設定することで、アクセスを制限します。</em>
   </p>
</td>

</table>
<table>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="リモート AEM Assets と AEM Sites の統合" src="./assets/connected-assets-rdam.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong> リモート AEM AssetsとAEM Sitesの統合 </strong>
      </a>
   </div>
   <p>
      <em> リモート AEM AssetsをAEM Sites環境と統合する方法を説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="OpenAPI 機能を備えたDynamic Mediaに関するよくある質問" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>OpenAPI 機能を備えたDynamic Mediaに関するよくある質問 </strong>
      </a>
   </div>
   <p>
      <em>OpenAPI 機能に関するよくある質問と、最もよくあるDynamic Mediaの回答を示します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="カスタムドメインの設定" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong> カスタムドメインの設定 </strong>
      </a>
   </div>
   <p>
      <em>AEM as a Cloud Serviceにはデフォルトドメインが付属していますが、必要に応じてカスタマイズできます。</em>
   </p>
</td>

</table>
