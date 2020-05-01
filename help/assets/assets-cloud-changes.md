---
title: Adobe Experience Manager Assets as a Cloud Service の主な変更点
description: AEMクラウドサービスのAdobe Experience Manager Assetsに対するAdobe Experience Manager 6.5と比較した顕著な変更点。
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Adobe Experience Manager Assets as a Cloud Service の主な変更点 {#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。ただし、Experience Manager AssetsのオンプレミスとAdobe Managed Serviceの間には、Experience Managerのクラウドサービスと比べて多くの違いがあります。 このドキュメントでは、アセット機能の重要な違いについて説明します。 For other changes, see the generic [changes to Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Adobe Experience Manager 6.5 との主な違いは次の点です。

* [アセットの取り込みとアップロード](#asset-ingestion)。
* [クラウド処理用のAsset Microservices](#asset-microservices)。
* [クラシック UI の削除](#classic-ui).

## アセットの取り込みとアップロード {#asset-ingestion}

アセットの取り込みとアップロードの高速化をより効果的に拡大縮小できるようになり、アセットのアップロードが効率化されました。 製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されました。ただし、これは既存のカスタマイズの一部に影響を与える場合があります。

* Adobe Experience Manager では、アップロードとダウンロードに直接バイナリアクセスの原則を使用し、アセットの処理にアセットマイクロサービスを使用します。[アセットの取り込みの概要](/help/assets/asset-microservices-overview.md)を参照してください。。
   * Asset upload [with direct binary access](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * For technical details, see  of [direct binary upload protocol and APIs](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* 以前のバージョンの AEM に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。。
   * [アセットマイクロサービスの設定および使用方法](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。。
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

アセットマイクロサービスで生成された標準レンディションは、後方互換性のある方法でアセットリポジトリノードに保存されます（同じ命名規則が使用されます）。

## アセットマイクロサービスの開発とテスト {#asset-microservices}

アセットマイクロサービスは、クラウドサービスを使用して、アセットの拡張性と回復性に優れた処理を提供します。 様々なアセットタイプや処理オプションを最適に処理できるように、アドビはクラウドサービスを管理します。 Asset Microservicesを使用すると、サードパーティのレンダリングツールやメソッド（ImageMagickやFmpegトランスコードなど）が不要になり、設定が簡単になり、一般的なファイルタイプの機能をすぐに使用できます。 現在、ImageMagick統合とFFMpegトランスコードは、クラウドサービスでは使用できません。

Asset Microservicesは、Cloud Managerで管理されるお客様のプログラムや環境で、Experience Managerに自動的にプロビジョニングされ、Experience Managerに有線で接続されるクラウドネイティブのサービスです。 Experience Managerを拡張またはカスタマイズするには、開発者は、クラウド環境で生成されたレンディションを含む既存のコンテンツまたはアセットを使用し、アセットの使用、表示、ダウンロードを使用したコードのテストと検証を行います。

To do an end-to-end validation of the code and process including asset ingestion and processing, deploy the code changes to a cloud-dev environment using [the pipeline](/help/implementing/cloud-manager/configure-pipeline.md) and test with full execution of asset microservices processing.

## クラシック UI の削除 {#classic-ui}

Adobe Experience Manager as a Cloud Service ではクラシック UI が使用できなくなりました。標準のインターフェイスは、タッチ対応UIです。
