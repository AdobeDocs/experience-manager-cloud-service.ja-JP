---
title: OpenAPI 機能を備えたDynamic Media
description: Dynamic Mediaを OpenAPI 機能と共に使用する理由や有効にする方法など、主要な概念について説明します。
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# OpenAPI 機能を備えたDynamic Media {#new-dynaminc-media-apis-overview}

急速に変化する今日のデジタル世界において、ブランドのデジタルアセットの可能性を最大限に引き出すことは、競争に勝ち抜くために不可欠です。 総合的なデジタルアセット管理（DAM）ソリューションは、ブランドの整合性と優れた顧客体験を確保しながら、アセットガバナンスを促進し、ブランドの一貫性を高め、コンテンツ配信を高速化します。

OpenAPI 機能を備えたDynamic Mediaにより、DAM は、アセットガバナンスと配信を確実に行うための機敏で効率的なコンテンツサプライチェーンエコシステムのコアになります。

## Dynamic Mediaを OpenAPI 機能と共に使用する理由 {#new-dynamic-media-api-features}

OpenAPI 機能を備えたDynamic Mediaには、次のような主なメリットがあります。

* **シームレスな統合**:OpenAPI 機能を備えたDynamic Mediaは、包括的な検索および配信 API のセットを提供します。 これにより、開発者は次のことが容易になります [アセットの配信とそのアプリケーションの統合](/help/assets/integrate-new-dynamic-media-apis.md). アプリケーションには、Adobeアプリケーションだけでなく、サードパーティのアプリケーションも含まれます。 さらに、次の機能も提供します [マイクロフロントエンドアセットセレクターのユーザーインターフェイス](/help/assets/asset-selector.md) をクリックし、承認済みアセットを検索して選択します。 セレクターは、React JS、Application JS、Vanilla JS など、JavaScript フレームワークに基づくすべてのAngularと簡単に統合できます。

* **デジタルアセットの一元管理**:DAM は、すべてのデジタルアセットの唯一の情報源です。 デジタルアセットはAEM Assetsで一元管理され、アセットのバイナリをコピーせずに、配信 URL を使用して参照することで消費側のアプリケーションに配信されます。

* **リアルタイムの更新**：バージョンの更新やメタデータの変更など、DAM 内の承認済みアセットに加えられた変更は、自動的に配信 URL に反映されます。 CDN を介して OpenAPI 機能を備えたDynamic Mediaに 10 分の短期間有効（TTL）値が設定されていると、更新は 10 分以内にすべてのオーサリングインターフェイスと公開済みインターフェイスに表示されます。

* **ブランドの一貫性**：のみ [ブランド承認済みアセット](/help/assets/approved-assets.md) ダウンストリームのアプリケーションに公開される。 [ブランドマネージャーとマーケターは、ブランドアセットを厳格に管理しています](/help/assets/restrict-assets-delivery.md). アセットの承認済みの最新バージョンのみを使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性を確保できます。

* **Web に最適化された配信**：デジタルアセットは、デジタルエクスペリエンスのコア web バイタルを強化するために、web に最適化された形式で配信されます。 これには、画像用の WebP レンディション、ビデオ用の HLS または DASH プロトコルを介したアダプティブストリーミング、ドキュメント用の元のレンディションのサポートが含まれます。

* **動的なアセット変換**：アドビのシステムでは、画像修飾子と呼ばれる URL パラメーターを使用してその場で画像変換を行うことができます。 [例えば、幅、高さ、回転、反転、画質、切り抜き、形式などです](/help/assets/deliver-assets-apis.md). OpenAPI 機能を備えたDynamic Mediaは、画像スマート切り抜き機能もサポートしています。 変換後のレンディションは動的に生成され、CDN を介してシームレスに配信されます。

* **アセットの安全な配信**:OpenAPI 機能を備えたDynamic Mediaは、デジタルアセットへのアクセスを制御するためのメカニズムを提供します。 保護するアセットのメタデータとしてユーザーの役割またはグループを指定し、次の期間を事前定義した期間を設定できます [これらのアセットにアクセスできるのは、許可されたユーザーのみです](/help/assets/restrict-assets-delivery.md). セキュリティで保護されているアセットの配信 URL は、制限された期間中に、権限のないユーザーに対して解決されません。

* **十分な情報に基づいた意思決定を行うためのデータインサイト**：アセットの管理と配信に加えて、CDN でのアセット配信に関する配信データインサイトを取得するため、ブランドマネージャーはチャネルをまたいで配信指標を追跡できます。 これにより、アセットガバナンスと配信戦略を継続的に最適化するために、データに基づく意思決定を行うことができます。

![新しいDynamic Mediaのデータフロー図](assets/dm-openapi-dfd.png)

## OpenAPI 機能を使用してDynamic Mediaにアクセスするための前提条件 {#prerequisites-new-dynaminc-media-apis}

OpenAPI 機能を使用してDynamic Mediaにアクセスするには、次のライセンスが必要です。

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## OpenAPI 機能でDynamic Mediaを有効にする方法 {#enable-new-dynamic-media-apis}

AEM as a Cloud Service環境で OpenAPI 機能を使用してDynamic Mediaを有効にするリクエストを送信する前に、そのリクエストが既に有効になっていないことを確認します。

AEM as a Cloud Service環境で OpenAPI 機能を使用してDynamic Mediaを有効にするには、次の詳細を記載したAdobeサポートチケットを送信します。

* Cloud Serviceプログラムおよび環境 ID

* OpenAPI 機能統合を使用してDynamic Mediaで解決するユースケースの詳細です。

* OpenAPI 機能を使用してDynamic Mediaと統合するダウンストリームアプリケーションの詳細。

  >[!NOTE]
  >
  > Adobe以外のアプリケーションと統合する場合は、アプリケーションがホストされている場所を許可リストに加えるドメイン名を指定します。

* 統合プロジェクトに関わる主要顧客連絡先の詳細。

サポートチケットを送信すると、AdobeはCloud Service環境で OpenAPI 機能を備えたDynamic Mediaを有効にし、IMS クライアント ID などの詳細を共有して、統合を進めることができます。

## 主な機能の詳細 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approved-assets.md">
   <img alt="Experience Manager Assetsでのアセットの承認" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approved-assets.md">
      <strong>Experience Manager Assetsでのアセットの承認</strong>
      </a>
   </div>
   <p>
      <em>AEM Assetsでアセットを承認してアセット管理を効率化し、アセットの処理に関する制御された効率的なプロセスを確保します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-new-dynamic-media-apis.md">
   <img alt="AEM Assetsとダウンストリームアプリケーションの統合" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-new-dynamic-media-apis.md">
      <strong>AEM Assetsとダウンストリームアプリケーションの統合</strong>
      </a>
   </div>
   <p>
      <em>検索および配信 API を使用して独自のカスタムユーザーインターフェイスをExperience Manager Assets リポジトリと統合するか、Adobeのマイクロフロントエンドアセットセレクターを使用します。</em>
   </p>
</td>
<td>
   <a href="/help/assets/asset-selector.md">
   <img alt="Adobeのアセットセレクター" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/asset-selector.md">
      <strong>Adobeのマイクロフロントエンドアセットセレクター</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets リポジトリとやり取りしてアセットを検索し、アプリケーションオーサリングエクスペリエンスで使用するユーザーインターフェイス。</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="アセットのExperience Manager Assets リポジトリの検索" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Experience Manager Assets リポジトリ内のアセットの検索</strong>
      </a>
   </div>
   <p>
      <em>AEM Assets リポジトリ内のアセットを検索して、ダウンストリームアプリケーションに配信できるようにします。</em>
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
   <img alt="Experience Managerー内のアセットへのアクセスを制限する" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Experience Managerー内のアセットへのアクセスを制限する</strong>
      </a>
   </div>
   <p>
      <em> DAM 管理者またはブランドマネージャーは、AEMas a Cloud Serviceオーサーインスタンス上で承認済みアセットの役割を設定することで、アクセスを制限します。</em>
   </p>
</td>
</table>

