---
title: Adobe Experience Manager Assets as a Cloud Service の主な変更点
description: AEMクラウドサービスのAdobe Experience Manager Assetsに対するAdobe Experience Manager 6.5との比較における顕著な変更。
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Adobe Experience Manager Assets as a Cloud Service の主な変更点 {#notable-changes}

Adobe Experience Manager as a Cloud Service は、AEM プロジェクトを管理するための様々な新機能と可能性を提供します。ただし、Experience Manager AssetsのオンプレミスとAdobe Managed Serviceの間には、Experience Managerをクラウドサービスとして使用する場合と比べて多くの違いがあります。 ここでは、重要な相違点について重点的に説明します。

>[!NOTE]
>
>ここでは、Adobe Experience Manager Assets as a Cloud Service に限定した主な変更点について重点的に説明します。Adobe Experience Manager as a Cloud Service 全般の変更点については、[Adobe Experience Manager (AEM) as a Cloud Service の主な変更点](/help/release-notes/aem-cloud-changes.md)を参照してください。

Adobe Experience Manager 6.5 との主な違いは次の点です。

* [アセットの取り込み](#asset-ingestion)
* [クラシック UI の削除](#classic-ui)

## アセットの取り込み {#asset-ingestion}

アセットの取り込みとアップロードの高速化をより適切に行うことで、アセットのアップロードが効率化されました。 製品機能（Web ユーザーインターフェイス、デスクトップクライアント）が更新されました。ただし、これは既存のカスタマイズに影響を与える場合があります。

* Adobe Experience Manager では、アップロードとダウンロードに直接バイナリアクセスの原則を使用し、アセットの処理にアセットマイクロサービスを使用します。[アセットの取り込みの概要](/help/assets/asset-microservices-overview.md)を参照してください。。
   * Asset upload [with direct binary access](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * For technical details, see  of [direct binary upload protocol and APIs](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* 以前のバージョンの AEM に用意されていたデフォルトの **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローは使用できなくなりました。代わりに、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどに対応できる、拡張性と可用性の高いサービスをアセットマイクロサービスが提供します。。
   * [アセットマイクロサービスの設定および使用方法](/help/assets/asset-microservices-configure-and-use.md)を参照してください。
   * 処理におけるワークフローステップをカスタマイズするには、[後処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)を使用できます。。
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

アセットマイクロサービスで生成された標準レンディションは、後方互換性のある方法でアセットリポジトリノードに保存されます（同じ命名規則が使用されます）。

## アセットマイクロサービスの開発とテスト {#developing-testing-asset-microservices}

アセットマイクロサービスは、Cloud Manager で管理されるユーザープログラムおよび環境の Adobe Experience Manager に自動的にプロビジョニングおよび接続されるネイティブクラウドサービスです。開発者が Adobe Experience Manager の拡張やカスタマイズをおこなう場合は、既存のコンテンツ（またはクラウド環境で生成されたレンディションを含んだアセット）を使用して、アセットの使用、表示、ダウンロードをおこなうコードをテストし検証できます。

コードとプロセス（アセットの取り込みや処理を含む）のエンドツーエンドの検証をおこなうには、コードの変更をパイプラインを使用してクラウド開発環境にデプロイし、アセットマイクロサービスの処理をすべて実行してテストします。

## クラシック UI の削除 {#classic-ui}

Adobe Experience Manager as a Cloud Service ではクラシック UI が使用できなくなりました。
