---
title: ' [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] の主な変更点'
description: ' [!DNL Adobe Experience Manager]  6.5 と比較した、  [!DNL Experience Manager] as a [!DNL Cloud Service] の [!DNL Adobe Experience Manager Assets]  の主な変更点。'
feature: Release Information
role: User, Leader, Architect, Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 97%

---

# 主な変更点：[!DNL Experience Manager Assets]as a [!DNL Cloud Service] {#notable-changes}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] は、Adobe Experience Manager プロジェクトを管理するための様々な新機能と可能性を提供します。オンプレミスまたは Adobe Managed Service としてホストされている [!DNL Experience Manager Assets] と [!DNL Experience Manager] as a [!DNL Cloud Service] には様々な違いがあります。この記事では、[!DNL Assets] 機能の重要な違いについて説明します。

[!DNL Experience Manager] 6.5 との主な違いは次の点です。

* [アセットの取り込み、アップロード、処理](#asset-ingestion)。
* [クラウドネイティブ処理用のアセットマイクロサービス](#asset-microservices)。
* [クラシック UI の削除](#classic-ui)。

## アセットの取り込み、処理、配布 {#asset-ingestion-distribution}

アセットのアップロードは、取り込み規模の調整向上、アップロードの高速化、マイクロサービスを使用した処理の高速化、一括取り込みを可能にすることで、効率が最適化されています。製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されています。また、これらは既存のカスタマイズの一部に影響を与える場合があります。

* [!DNL Experience Manager] では、直接バイナリアクセスの原則に基づいてアセットをアップロードおよびダウンロードし、アセットマイクロサービスを使用してアセットを処理します。[マイクロサービスの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセスを使用した](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)アセットのアップロード。
   * 技術的な詳細については、[直接バイナリアップロードのプロトコルと API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください
   * 基本的な CRUD 操作に使用できる API メソッドの比較については、[API とアセット操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)を参照してください。
* 以前のバージョンの [!DNL Experience Manager] に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。
   * 詳しくは、[アセットマイクロサービスの設定と使用](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。

* 変換を行わずにバイナリファイルを配信する Web サイトコンポーネントでは、直接ダウンロードを使用できます。Sling GET サーブレットが更新され、この機能がデフォルトで有効になります。何らかの変換（サーブレットを使用したサイズ変更など）を行ってバイナリを配信する Web サイトコンポーネントは、引き続きそのまま動作します。

アセットマイクロサービスで生成された標準レンディションは、同じ命名規則を使用して、下位互換性のある方法でアセットリポジトリーノードに保存されます。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するための Cloud Services を管理します。アセットマイクロサービスを利用すると、サードパーティ製のレンダリングツールやメソッド（[!DNL ImageMagick] など）が不要になり、システムの設定が簡単になると同時に、一般的なファイルタイプにそのまま使用できる機能が提供されます。以前のバージョンの Experience Manager で可能だったよりも幅広く、[様々なファイルタイプ](/help/assets/file-format-support.md)の形式を追加設定なしで処理できるようになりました。例えば、以前は [!DNL ImageMagick] などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。[!DNL ImageMagick] の複雑な設定は、[!UICONTROL 処理プロファイル]の設定には使用できません。ビデオの高度な FFmpeg トランスコードに [!DNL Dynamic Media] を使用し、[MP4 ビデオの基本的なトランスコード](/help/assets/manage-video-assets.md#transcode-video)に処理プロファイルを使用します。

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムと環境にある Adobe [!DNL Experience Manager] に自動的にプロビジョニングされて接続される、クラウドネイティブなサービスです。[!DNL Experience Manager] を拡張またはカスタマイズするために、開発者はクラウド環境で生成されたレンディションを使用して既存のコンテンツまたはアセットを使用できます。この機能により、アセットを使用、表示またはダウンロードして、コードをテストおよび検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証を行うには、コードの変更を[パイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)を使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## [!DNL Experience Manager] 6.5 と同等の機能  {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] では、多くの新機能と、既存の機能をより高いパフォーマンスで動作させる方法を導入しています。ただし、[!DNL Experience Manager] 6.5 から [!DNL Experience Manager] as a [!DNL Cloud Service] に移行すると、一部の機能が、動作が異なる、使用できない、部分的にのみ使用できる、のいずれかになる場合があります。そのような機能の一覧を以下に示します。また、 [非推奨（廃止予定）の機能と削除された機能](/help/release-notes/deprecated-removed-features.md) も参照してください。

| 機能またはユースケース | [!DNL Experience Manager] as a [!DNL Cloud Service] のステータス | コメント |
|-----|-----|-----|
| [重複アセットの検出](/help/assets/detect-duplicate-assets.md) | 動作が異なる | [ [!DNL Experience Manager] 6.5 での動作](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/managing/duplicate-detection)を参照してください。 |
| [プレースメント専用（FPO）レンディション](/help/assets/configure-fpo-renditions.md) | 動作が異なる | 処理プロファイルは、アセットマイクロサービスを使用して FPO レンディションを生成します。Experience Manager 6.5 では、[!DNL ImageMagick] などのサードパーティソリューションをレンディションの生成に使用できました。 |
| メタデータの書き戻し | 動作が異なる | デフォルトで無効必要に応じて、対応するワークフローランチャーを有効にします。アセットマイクロサービスが書き戻しを処理します。 |
| パッケージマネージャーを使用してアップロードされたアセットの処理 | 手動の介入が必要 | 「**[!UICONTROL アセットを再処理]**」アクションを使用して手動で再処理します。 |
| MIME タイプの検出 | 非対応 | 拡張子のないデジタルアセットや誤った拡張子のデジタルアセットをアップロードした場合は、希望どおりには処理されない可能性があります。それでも、ユーザーは、拡張子のないバイナリファイルを DAM に保存できます。[Adobe  [!DNL Experience Manager] 6.5 の MIME タイプ検出](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/administer/detect-asset-mime-type-with-tika)を参照してください。 |
| 複合アセットのサブアセットの生成 | 非対応 | 注釈などの従属ユースケースが実行されない可能性があります。[Adobe  [!DNL Experience Manager] 6.5 でのサブアセットの作成](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/managing/managing-linked-subassets#generate-subassets)を参照してください。[2021.7.0 リリース](/help/release-notes/release-notes-cloud/release-notes-current.md)以降、一部のファイルタイプの PDF プレビューが使用可能になりました。 |
| 画像の編集 | サポート対象外 | アセットの編集は、Experience Manager as a Cloud Service ではサポートされていません。詳しくは、 [Experience Manager 6.5 での仕組み](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/managing/manage-assets#editing-images) を参照してください。 |
| ホームページ | サポート対象外 |  [!DNL Experience Manager]  6.5 ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/using/assets-home-page) の [[!DNL Assets]  ホームページエクスペリエンスを参照 |
| ZIP アーカイブからのアセットの抽出 | サポート対象外 | [ [!DNL Experience Manager]  6.5 の ZIP 抽出](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/assets/managing/manage-assets#extractzip) を参照してください。 |
| アセット評価 | サポート対象外 | メタデータスキーマエディターの評価ウィジェットはサポートされていません。 |
| Content Disposition フィルター | サポート対象外 | `ContentDispositionFilter` の一般的なユースケースは、管理者が HTML ファイルを提供し、PDF ファイルをダウンロードする代わりにインラインで開くように [!DNL Experience Manager] を設定できるようにすることです。パブリッシュインスタンスでは、Dispatcher 設定を使用して配置を管理できます。オーサーインスタンスでは、アドビは Content Disposition ヘッダーの変更をお勧めしません。[Content Disposition フィルター： [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/security/content-disposition-filter) を参照してください。 |
| 製品撮影テンプレート | サポート対象外 | [製品撮影テンプレート： [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/sites/authoring/projects/managing-product-information) を参照してください。 |
| スマート翻訳 | サポート対象外 | スマート翻訳は [!DNL Experience Manager] as a [!DNL Cloud Service] ではサポートされていません。 |
| WebDAV | サポート対象外 | 代替手段については、[[!DNL Creative Cloud] 統合](/help/assets/aem-cc-integration-best-practices.md)または[開発者向けリファレンス資料](/help/assets/developer-reference-material-apis.md)を参照してください。 |
| クラシック UI | サポート対象外 | タッチ操作対応ユーザーインターフェイスのみが使用できます。 |

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>Adobe [!DNL Experience Manager] as a [!DNL Cloud Service] には次のリソースがあります。
>
>* [非推奨（廃止予定）の機能と削除された機能のリスト](/help/release-notes/deprecated-removed-features.md)
>* [概要紹介](/help/overview/introduction.md)
>* [新機能と相違点](/help/overview/what-is-new-and-different.md)
>* [アーキテクチャ](/help/overview/architecture.md)
>* [主要な変更点](/help/release-notes/aem-cloud-changes.md)
>* [主要な変更点 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [ビデオチュートリアル](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/overview)
