---
title: Adobe Experience Manager Assets as a Cloud Service の主な変更点
description: Adobe Experience Manager 6.5 と比較した、AEM Assets as a Cloud Service の主な変更点
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Adobe Experience Manager Assets as a Cloud Service の主な変更点 {#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。ただし、Adobe Experience Manager as a Cloud Service と、オンプレミスまたは Adobe Managed Services の Adobe Experience Manager Assets を比較すると、両者には数々の違いがあります。ここでは、重要な相違点について重点的に説明します。

>[!NOTE]
>
>ここでは、Adobe Experience Manager Assets as a Cloud Service に限定した主な変更点について重点的に説明します。Adobe Experience Manager as a Cloud Service 全般の変更点については、[Adobe Experience Manager (AEM) as a Cloud Service の主な変更点](/help/release-notes/aem-cloud-changes.md)を参照してください。

Adobe Experience Manager 6.5 との主な違いは次の点です。

* [アセットの取り込み](#asset-ingestion)
* [クラシック UI の削除](#classic-ui)

## アセットの取り込み {#asset-ingestion}

アセットのアップロードが最適化されて効率が向上し、アセット取り込みの規模をより適切に拡大／縮小できるようになったほか、アップロードが高速化されました。製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されました。ただし、これによって、一部の既存カスタムコードが影響を受ける可能性があります。

* Adobe Experience Manager では、アップロードとダウンロードに直接バイナリアクセスの原則を使用し、アセットの処理にアセットマイクロサービスを使用します。[アセットの取り込みの概要](/help/assets/asset-microservices-overview.md)を参照してください。
   * [直接バイナリアクセス](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)を使用したアセットのアップロード
   * 技術的な詳細については、[直接バイナリアップロードのプロトコルと API](/help/assets/developer-reference-material-apis.md#overview-binary-upload) を参照してください
* 以前のバージョンの AEM に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。
   * [アセットマイクロサービスの設定および使用方法](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。
* パッケージマネージャーで取り込まれたアセットについては、Assets インターフェイスの「**[!UICONTROL アセットを再処理]**」アクションを使用して、手動で再処理する必要があります。

アセットマイクロサービスで生成された標準レンディションは、後方互換性のある方法でアセットリポジトリノードに保存されます（同じ命名規則が使用されます）。

## アセットマイクロサービスの開発とテスト {#developing-testing-asset-microservices}

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムおよび環境の Adobe Experience Manager に自動的にプロビジョニングおよび接続されるネイティブクラウドサービスです。開発者が Adobe Experience Manager の拡張やカスタマイズをおこなう場合は、既存のコンテンツ（またはクラウド環境で生成されたレンディションを含んだアセット）を使用して、アセットの使用、表示、ダウンロードをおこなうコードをテストし検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証をおこなうには、コードの変更をパイプラインを使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## クラシック UI の削除 {#classic-ui}

Adobe Experience Manager as a Cloud Service ではクラシック UI が使用できなくなりました。
