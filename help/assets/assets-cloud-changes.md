---
title: クラウドサービスとしてのAdobe Experience Manager Assetsの顕著な変更
description: AEMクラウドサービスのAdobe Experience Manager Assetsに対するAdobe Experience Manager 6.5との比較における顕著な変更。
translation-type: tm+mt
source-git-commit: ab79c3dabb658e242df08ed065ce99499c9b7357

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

クラウドサービスとしてのAdobe Experience Managerは、AEMプロジェクトを管理するための多くの新機能と可能性を提供します。 ただし、Experience Manager AssetsのオンプレミスとAdobe Managed Serviceの間には、Experience Managerをクラウドサービスとして使用する場合と比べて多くの違いがあります。 このドキュメントでは、重要な違いに焦点を当てます。

>[!NOTE]
>
>このドキュメントでは、Experience Manager Assetsに固有のクラウドサービスとしての注目すべき変更点について説明します。 Experience Managerに対する一 [般的な変更をクラウドサービスとして確認します](/help/release-notes/aem-cloud-changes.md)。

Experience Manager 6.5との主な違いは、次の点です。

* [アセットの取り込み](#asset-ingestion)
* [クラシックUIの削除](#classic-ui)

## アセットの取り込み {#asset-ingestion}

アセットの取り込みとアップロードの高速化をより適切に行うことで、アセットのアップロードが効率化されました。 製品機能（Webユーザーインターフェイス、デスクトップクライアント）が更新されました。 ただし、これは既存のカスタマイズに影響を与える場合があります。

* Experience Managerは、直接バイナリアクセスの原則を使用して、アセットのアップロードとダウンロードを行い、アセットの処理にアセットのマイクロサービスを使用します。 アセット [の取り込みの概要を参照](/help/assets/asset-microservices-overview.md)。
   * 直接バイナリアク [セスでのアセットのアップロード](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 技術的な詳細については、直接バイナリ [アップロードプロトコルとAPIを参照してください](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。
* 以前のバージョンのAEMのデフォ **[!UICONTROL ルトのワークフロー]** 「DAM Asset Update」は使用できなくなりました。 代わりに、アセットマイクロサービスは、デフォルトのアセット処理(レンディション、メタデータ抽出、インデックス作成用のテキスト抽出)のほとんどを網羅する、スケーラブルで、容易に使用できるサービスを提供します。
   * アセットマイ [クロサービスの設定と使用を参照してください。](/help/assets/asset-microservices-configure-and-use.md)
   * 処理のワークフロー手順をカスタマイズするために、後 [処理ワークフロー](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) を使用できます。
* Package Managerから取り込まれるアセットは、アセットインターフェイスの「アセットの再処理」アク **[!UICONTROL ションを使用し]** 、手動で再処理する必要があります。

アセットマイクロサービスで生成された標準レンディションは、アセットリポジトリノード（同じ命名規則）で下位互換の方法で保存されます。

## 資産マイクロサービスの開発とテスト {#developing-testing-asset-microservices}

Asset Microservicesは、Cloud Managerで管理される顧客プログラムや環境で、Experience Managerに自動的にプロビジョニングされ、配線されるネイティブのクラウドサービスです。 Experience Managerの拡張やカスタマイズを行う開発者は、既存のコンテンツ(またはクラウド環境で生成されたレンディションを含むアセット)を使用して、アセットの使用、表示、ダウンロードを使用してコードのテストと検証を行うことができます。

アセットの取り込みと処理を含むコードとプロセスのエンドツーエンドの検証を行うには、コードの変更をパイプラインを使用してクラウド開発環境にデプロイし、アセットのマイクロサービス処理を完全に実行してテストします。

## クラシックUIの削除 {#classic-ui}

Classic UIは、Experience Managerでクラウドサービスとして使用できなくなりました。
