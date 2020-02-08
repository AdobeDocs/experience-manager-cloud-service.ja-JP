---
title: クラウドサービスとしてのAdobe Experience Manager Assetsの顕著な変更
description: AEMクラウドサービスのAdobe Experience Manager Assetsに対するExperience Manager 6.5との主な変更点
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# クラウドサービスとしてのExperience Manager Assetsに対する注目すべき変更 {#notable-changes}

クラウドサービスとしてのAdobe Experience Managerは、AEMプロジェクトを管理するための多くの新機能と可能性を提供します。 ただし、Experience Manager AssetsのオンプレミスとAdobe Managed Serviceの違いは、Experience Managerのクラウドサービスとの違いに多数あります。 本書では、重要な違いについて説明します。

>[!NOTE]
>
>このドキュメントでは、Experience Manager Assetsにクラウドサービスとして適用される主な変更点について説明します。 Experience Managerに対する一 [般的な変更をクラウドサービスとして確認します](/help/release-notes/aem-cloud-changes.md)。

Experience Manager 6.5との主な違いは次の点です。

* [アセットの取り込み](#asset-ingestion)
* [クラシックUIの削除](#classic-ui)

## アセットの取り込み {#asset-ingestion}

アセットのアップロードが最適化され、アセットの取り込みと高速なアップロードをより効率的に拡大縮小できるようになりました。 製品機能（Webユーザーインターフェイス、デスクトップクライアント）が更新されました。 ただし、これは既存のカスタムコードの一部に影響を与える可能性があります。

* Experience Managerでは、直接バイナリアクセスの原則を使用してアップロードとダウンロードを行い、アセットの処理にアセットマイクロサービスを使用します。 アセット [の取り込みの概要を参照](/help/assets/asset-microservices-overview.md)
   * 直接バイナリアクセス [を使用したアセットのアップロード](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)
   * 技術的な詳細については、直接バイナリアップロード [プロトコルおよびAPIに関するページを参照してください](/help/assets/developer-reference-material-apis.md#overview-binary-upload)
* 以前のバージョンのAEM **[!UICONTROL では、デフォルトのワークフロー]** 「DAM Asset Update」は使用できなくなりました。 代わりに、アセットマイクロサービスは、デフォルトのアセット処理（レンディション、メタデータ抽出、インデックス作成用のテキスト抽出）のほとんどを対象とする、スケーラブルで、容易に利用可能なサービスを提供します。
   * アセットマイ [クロサービスの設定と使用を参照してください](/help/assets/asset-microservices-configure-and-use.md)
   * 処理のワークフロー手順をカスタマイズするには、後 [処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) を使用できます
* Package Managerから取り込まれるアセットは、アセットインターフェイスの「アセットを再処理」アクシ **[!UICONTROL ョンを使用して]** 、手動で再処理する必要があります。

アセットマイクロサービスで生成された標準レンディションは、アセットリポジトリノードに下位互換性のある方法で保存されます（同じ命名規則）。

## 資産マイクロサービスの開発とテスト {#developing-testing-asset-microservices}

アセットマイクロサービスは、Cloud Managerで管理されるお客様のプログラムや環境で、Experience Managerに自動的にプロビジョニングされ、Experience Managerに結線されるネイティブのクラウドサービスです。 Experience Managerの拡張やカスタマイズを行う開発者は、既存のコンテンツ（またはクラウド環境で生成されたレンディションを含むアセット）を使用して、アセットの使用、表示、ダウンロードを使用してコードをテストし、検証できます。

アセットの取り込みと処理を含むコードとプロセスのエンドツーエンドの検証を行うには、コードの変更をパイプラインを使用してクラウド開発環境にデプロイし、アセットマイクロサービス処理を完全に実行してテストします。

## クラシックUIの削除 {#classic-ui}

Classic UIは、Experience Managerでクラウドサービスとして使用できなくなりました。
