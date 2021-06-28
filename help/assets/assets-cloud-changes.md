---
title: ' [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] の主な変更点'
description: '[!DNL Adobe Experience Manager 6.5] と比較した [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] の主な変更点。'
feature: リリース情報
role: Business Practitioner,Leader,Architect,Administrator
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: e3efbaf5cb590b079ccc228a0f130ecec198d2ff
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 66%

---

# 主な変更点：[!DNL Experience Manager Assets]as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] は、Adobe Experience Manager プロジェクトを管理するための様々な新機能と可能性を提供します。オンプレミスまたは Adobe Managed Service としてホストされている [!DNL Experience Manager Assets] と [!DNL Experience Manager] as a [!DNL Cloud Service] には様々な違いがあります。この記事では、[!DNL Assets] 機能の重要な違いについて説明します。

[Adobe Experience Manager] 6.5 との主な違いは次の点です。

* [アセットの取り込み、アップロード、処理](#asset-ingestion)。
* [クラウドネイティブ処理用のアセットマイクロサービス](#asset-microservices)。
* [クラシック UI の削除](#classic-ui)。

## アセットの取り込み、処理、配布 {#asset-ingestion-distribution}

アセットのアップロードは、取り込み規模の調整向上、アップロードの高速化、マイクロサービスを使用した処理の高速化、一括取り込みを可能にすることで、効率が最適化されています。製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されています。また、これによって、一部の既存カスタマイズが影響を受ける可能性があります。

* [!DNL Experience Manager] では、直接バイナリアクセスの原則に基づいてアセットをアップロードおよびダウンロードし、アセットマイクロサービスを使用してアセットを処理します。詳しくは、[マイクロサービスの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセスを使用した](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)アセットのアップロード。
   * 技術的な詳細については、[直接バイナリアップロードのプロトコルと API](/help/assets/developer-reference-material-apis.md#upload-binary) を参照してください
   * 基本的な CRUD 操作に使用できる API メソッドの比較については、[API とアセット操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)を参照してください。
* 以前のバージョンの [!DNL Experience Manager] に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。
   * 詳しくは、[アセットマイクロサービスの設定と使用](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。

* 変換をおこなわずにバイナリファイルを配信するWebサイトコンポーネントでは、直接ダウンロードを使用できます。 SlingGETサーブレットが更新され、開発者がデフォルトでこれをおこなえるようになりました。 バイナリを何らかの変換（例えば、サーブレットを介してサイズ変更）で配信するWebサイトコンポーネントは、引き続きそのまま動作します。

アセットマイクロサービスで生成された標準レンディションは、同じ命名規則を使用して、後方互換性のある方法でアセットリポジトリノードに保存されます。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、拡張性と回復性に優れたアセット処理を提供します。アドビは、様々なアセットタイプや処理オプションを最適に処理するための Cloud Services を管理します。アセットマイクロサービスを利用すると、サードパーティ製のレンダリングツールやメソッド（ImageMagick など）が不要になり、システムの設定が簡単になると同時に、一般的なファイルタイプにそのまま使用できる機能が提供されます。以前のバージョンの Experience Manager で可能だったよりも幅広く、[様々なファイルタイプ](/help/assets/file-format-support.md)の形式を追加設定なしで処理できるようになりました。例えば、以前は ImageMagick などのサードパーティソリューションが必要だった PSD 形式と PSB 形式を、サムネール抽出できるようになりました。ImageMagick の複雑な設定は、[!UICONTROL 処理プロファイル]の設定に使用できません。ビデオの高度な FFmpeg トランスコードに [!DNL Dynamic Media] を使用し、[MP4 ビデオの基本的なトランスコード](/help/assets/manage-video-assets.md#transcode-video)に処理プロファイルを使用します。

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムと環境にある Adobe [!DNL Experience Manager] に自動的にプロビジョニングされて接続される、クラウドネイティブなサービスです。Adobe [!DNL Experience Manager] の拡張やカスタマイズを行う場合、開発者は、既存のコンテンツまたはクラウド環境で生成されたレンディションを含んだアセットを使用して、アセットの使用、表示、ダウンロードを行うコードをテストし検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証を行うには、コードの変更を[パイプライン](/help/implementing/cloud-manager/configure-pipeline.md)を使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## [!DNL Experience Manager] 6.5と同等の機能 {#cloud-service-feature-status}

[!DNL Experience Manager] as  [!DNL Cloud Service] では、既存の機能の多くの新機能とより高いパフォーマンスの方法を紹介しています。ただし、[!DNL Experience Manager] 6.5から[!DNL Experience Manager]に[!DNL Cloud Service]として移行すると、一部の機能は、動作が異なる、使用できない、または部分的に使用できない、という点に気が付く場合があります。 次に、そのような機能のリストを示します。 また、[非推奨（廃止予定）の機能と削除された機能](/help/release-notes/deprecated-removed-features.md)も参照してください。

| 機能または使用例 | [!DNL Experience Manager]の状態([!DNL Cloud Service]) | コメント |
|-----|-----|-----|
| [重複アセットの検出](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 動作は異なります。 | [ [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=ja)での動作を参照してください。 |
| [配置専用(FPO)レンディション](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | 動作が異なる |  |
| メタデータの書き戻し | 動作が異なる | デフォルトで無効. 必要に応じて、対応するワークフローランチャーを有効にします。 書き戻しは、アセットマイクロサービスによって処理されます。 |
| パッケージマネージャーを使用してアップロードされたアセットの処理 | 手動の介入が必要です。 | 「**[!UICONTROL アセットを再処理]**」アクションを使用して、手動で再処理します。 |
| MIMEタイプの検出 | サポートされていない。 | 拡張子がない、または誤った拡張子を持つデジタルアセットをアップロードした場合、必要に応じて処理されないことがあります。 それでも、ユーザーは、拡張子のないバイナリファイルを DAM に保存できます。[Adobe  [!DNL Experience Manager] 6.5 の MIME タイプ検出](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html?lang=ja)を参照してください。 |
| 複合アセットのサブアセットの生成または注釈の作成 | サポートされていない。 | 従属使用例は満たされません。 例えば、複数ページのPDF、INDD、PPT、PPTX、AIファイルを表示または注釈付けすることはできません。 [Adobe  [!DNL Experience Manager] 6.5 でのサブアセットの作成](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html?lang=ja#generate-subassets)を参照してください。 |
| ホームページ | サポートされていない。 | [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html?lang=ja)を参照 |
| ZIPアーカイブからのアセットの抽出 | サポートされていない。 | [Adobe  [!DNL Experience Manager] 6.5 の ZIP 抽出](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)を参照してください。 |
| Assetsの評価 | サポートされていない。 | メタデータスキーマエディターの評価ウィジェットはサポートされていません。 |
| クラシック UI | サポートされていない。 | タッチ操作対応のユーザーインターフェイスのみ使用できます。 |

>[!MORELIKETHIS]
>
>Adobe [!DNL Experience Manager] as a [!DNL Cloud Service] には次のリソースがあります。
>
>* [非推奨（廃止予定）および削除された機能のリスト](/help/release-notes/deprecated-removed-features.md)
* [概要紹介](/help/overview/introduction.md)
* [新機能と相違点](/help/overview/what-is-new-and-different.md)
* [アーキテクチャ](/help/core-concepts/architecture.md)
* [主要な変更点](/help/release-notes/aem-cloud-changes.md)
* [主要な変更点 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
* [ビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=ja)

