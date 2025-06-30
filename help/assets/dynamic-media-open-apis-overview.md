---
title: OpenAPI 機能を備えた Dynamic Media
description: OpenAPI 機能を備えた Dynamic Media を使用する理由や有効にする方法などの主な概念について説明します。
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 100%

---

# OpenAPI 機能を備えた Dynamic Media {#new-dynaminc-media-apis-overview}

今日の急速に変化するデジタルの世界では、ブランドのデジタルアセットの潜在能力を最大限に引き出すことが、競争で優位に立つために不可欠です。総合的なデジタルアセット管理（DAM）ソリューションは、アセットガバナンスを容易にし、ブランドの一貫性を促進し、コンテンツ配信を高速化すると共に、ブランドの整合性と優れたカスタマーエクスペリエンスを確保します。

OpenAPI 機能を備えた Dynamic Media では、DAM をアジャイルで効率的なコンテンツサプライチェーンエコシステムのコアに置き、アセットのガバナンスと配信を確実に行います。

## OpenAPI 機能を備えた Dynamic Media を使用する理由 {#dynamic-media-open-api-features}

OpenAPI 機能を備えたDynamic Media には、次のような主なメリットがあります。

* **シームレスな統合**：OpenAPI 機能を備えた Dynamic Media は、包括的な検索および配信 API セットを提供します。これにより、開発者は簡単に[アセットの配信をアプリケーションと統合](/help/assets/integrate-dynamic-media-open-apis.md)できます。アプリケーションには、アドビおよびサードパーティのアプリケーションが含まれます。承認済みアセットを検索および選択する[マイクロフロントエンドのアセットセレクターのユーザーインターフェイス](/help/assets/overview-asset-selector.md)を提供します。セレクターは、React JS、Angular JS、Vanilla JS などの JavaScript フレームワークに基づくすべてのアプリケーションと簡単に統合できます。

* **デジタルアセットの一元管理**：DAM は、すべてのデジタルアセットに対して信頼できる唯一の情報源です。デジタルアセットは AEM Assets で一元管理され、アセットバイナリをコピーすることなく、配信 URL を使用した参照によって消費アプリケーションに配信されます。

* **リアルタイムの更新**：バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに行われた変更は、配信 URL に自動的に反映されます。CDN 経由の OpenAPI 機能を備えた Dynamic Media に 10 分という短い有効期限（TTL）値を設定すると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。

* **ブランドの一貫性**：[ブランド承認済みアセット](/help/assets/approve-assets.md)のみがダウンストリームアプリケーションに公開されます。[ブランドマネージャーとマーケターは、ブランドアセットを厳密に管理します](/help/assets/restrict-assets-delivery.md)。承認済みの最新バージョンのアセットのみが使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性が確保されます。

* **Web に最適化された配信**：デジタルアセットは、web に最適化された形式で配信され、デジタルエクスペリエンスのコア web バイタルを強化します。これには、画像の WebP レンディション、ビデオの HLS または DASH プロトコルによるアダプティブストリーミング、ドキュメントの元のレンディションのサポートが含まれます。

* **動的アセット変換**：当社のシステムでは、画像修飾子と呼ばれる URL パラメーターを使用して、その場で画像を変換できます。[例えば、幅、高さ、回転、反転、画質、切り抜き、形式、スマート切り抜きなどです](/help/assets/deliver-assets-apis.md)。変換したレンディションは動的に生成され、CDN 経由でシームレスに配信されます。

* **アセットの安全な配信**：OpenAPI 機能を備えた Dynamic Media は、デジタルアセットへのアクセスを制御するメカニズムを提供します。セキュリティ保護対象のアセットのメタデータとしてユーザーの役割またはグループを指定し、[承認済みユーザーのみがこれらのアセットにアクセスできる](/help/assets/restrict-assets-delivery.md)定義済みの期間を設定できます。制限期間中、セキュリティ保護対象のアセットの配信 URL は、承認されていないユーザーに対しては解決されません。

* **十分な情報に基づく意思決定を行うデータインサイト（今後）**：アセットの管理と配信に加えて、CDN でのアセット配信に関する配信データインサイトを取得し、ブランドマネージャーがチャネル全体で配信指標を追跡できます。これにより、データに基づく意思決定を行うことができ、アセットガバナンスと配信戦略を継続的に最適化できます。

![Dynamic Media Open API のデータフロー図](assets/dm-openapi-dfd.png)

## OpenAPI 機能を備えた Dynamic Media にアクセスする前提条件 {#prerequisites-dynaminc-media-open-apis}

OpenAPI 機能を備えた Dynamic Media にアクセスするには、次のライセンスが必要です。

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## OpenAPI 機能を備えた Dynamic Media を有効にする方法 {#enable-dynamic-media-open-apis}

AEM as a Cloud Service で OpenAPI 機能を備えた Dynamic Media を有効にするリクエストを送信する前に、この機能がまだ有効になっていないことを確認します。

[前提条件](#prerequisites-dynaminc-media-open-apis)が満たされ、OpenAPI 機能を備えた Dynamic Media が AEM as a Cloud Service インスタンスで有効になっている場合は、リポジトリ内の承認済みアセットごとに配信 URL が使用可能になります。配信 URL をコピーする方法について詳しくは、[承認済みアセットの配信 URL のコピー](approve-assets.md#copy-delivery-url-approved-assets)を参照してください。アドビでは、サポートチケットを送信して有効にする前に、この方法を使用して、OpenAPI 機能を備えた Dynamic Media が AEM as a Cloud Service で有効になっていることを確認することをお勧めします。

AEM as a Cloud Service で OpenAPI 機能を備えた Dynamic Media を有効にするには、次の詳細が記載されたアドビサポートチケットを送信します。

* Cloud Service プログラムおよび環境 ID

* OpenAPI 機能を備えた Dynamic Media の統合で解決するユースケースの詳細。

* OpenAPI 機能を備えた Dynamic Media と統合するダウンストリームアプリケーションの詳細。

  >[!NOTE]
  >
  > アドビ以外のアプリケーションと統合するには、アプリケーションがホストされている場所の許可リストにドメイン名を指定します。

* 統合プロジェクトに関与する主要な顧客連絡先の詳細。

* 主要なアドビアカウントチームメンバーのリスト（メール）。

サポートチケットを送信すると、アドビでは Cloud Service 環境で OpenAPI 機能を備えた Dynamic Media を有効にし、統合を続行できるように IMS クライアント ID などの詳細を共有します。

>[!NOTE]
>
>OpenAPI 機能を備えた Dynamic Media の非アクティブ化を回避するには、任意のコンテンツパッケージから `/conf/global/settings/dam/assets-configurations/assetdelivery` を除外します。

## 主な機能の詳細 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="Experience Manager Assets でのアセットの承認" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>Experience Manager Assets でのアセットの承認</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets でアセットを承認し、アセット管理を効率化して、アセットを処理することを目的とした制御された効率的なプロセスを確保します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="AEM Assets とダウンストリームアプリケーションの統合" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>AEM Assets とダウンストリームアプリケーションの統合</strong>
      </a>
   </div>
   <p>
      <em>検索および配信 API を使用して独自のカスタムユーザーインターフェイスを Experience Manager Assets リポジトリと統合するか、アドビのマイクロフロントエンドのアセットセレクターを使用します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="アドビのアセットセレクター" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>アドビのマイクロフロントエンドのアセットセレクター</strong>
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
   <img alt="Experience Manager Assets リポジトリのアセットの検索" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Experience Manager Assets リポジトリのアセットの検索</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets リポジトリのアセットを検索して、ダウンストリームアプリケーションに配信できます。</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="ダウンストリームアプリケーションへのアセットの配信" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>ダウンストリームアプリケーションへのアセットの配信</strong>
      </a>
   </div>
   <p>
      <em>配信 URL を使用して、統合されたダウンストリームアプリケーションにアセットを配信します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Experience Manager でのアセットへのアクセスの制限" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Experience Manager でのアセットへのアクセスの制限</strong>
      </a>
   </div>
   <p>
      <em>DAM 管理者またはブランドマネージャーは、AEM as a Cloud Service オーサーインスタンスで承認済みアセットの役割を設定して、アクセスを制限します。</em>
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
      <strong>リモート AEM Assets と AEM Sites の統合</strong>
      </a>
   </div>
   <p>
      <em>リモート AEM Assets を AEM Sites 環境と統合する方法について説明します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="OpenAPI 機能を備えた Dynamic Media に関するよくある質問" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>OpenAPI 機能を備えた Dynamic Media に関するよくある質問</strong>
      </a>
   </div>
   <p>
      <em>OpenAPI 機能を備えた Dynamic Media に関するよくある質問への回答を入手します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="カスタムドメインの設定" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>カスタムドメインの設定</strong>
      </a>
   </div>
   <p>
      <em>AEM as a Cloud Service にはデフォルトのドメインが付属していますが、必要に応じてカスタマイズできます。</em>
   </p>
</td>

</table>
