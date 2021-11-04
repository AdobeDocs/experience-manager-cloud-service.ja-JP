---
title: AEM as a Cloud Service Release 2021.11.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.11.0 Cloud Manager のリリースノート
feature: Release Information
exl-id: null
source-git-commit: 471924b2edd5e0bccd7c1eb9d6dd36ad2bd89f88
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 22%

---

# Adobe Experience Manager as a Cloud Service 2021.11.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.11.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.11.0 の Cloud Manager のリリース日は 2021 年 11 月 04 日です。次回のリリースは 2021 年 12 月 09 日に予定されています。

### 新機能 {#what-is-new}

* ユーザーは、新しいフロントエンドパイプラインを活用して、フロントエンドコードを迅速に排他的にデプロイできるようになりました。 詳しくは、 [Cloud Manager フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) を参照してください。

   >[!IMPORTANT]
   >AEM版である必要があります `2021.10.5933.20211012T154732Z` を使用して、新しいフロントエンドパイプラインを活用します。

* AEM画像全体を構築する必要なく、より効率的にコード分析を実行することで、コード品質パイプラインの期間を大幅に短縮できます。 この変更は、リリース後の数週間で徐々に適用される予定です。

* Git コミット ID がパイプライン実行の詳細に表示され、作成されたコードの追跡が容易になります。

* プログラムの作成は、公開されている API を通じて利用できるようになりました。

* 環境の作成は、公開されている API を介して使用できるようになりました。

* この `x-request-id` 応答ヘッダーが、API Playground の [www.adobe.io](https://www.adobe.io/). このヘッダーは、トラブルシューティングのためにカスタマーケアの問題を送信する際に役立ちます。

* ユーザーとして、パイプラインがゼロのパイプラインカードから適切なガイダンスが提供されるのを確認します。

* 詳細の概要を簡単に表示できる新しいパイプラインページと、オンホバー時のステータスポップオーバーが追加されました。 パイプラインの実行に関連する詳細と共に表示できます。

* パイプラインの編集 API で、デプロイフェーズで使用する環境の変更がサポートされるようになりました。

* OakPal スキャンプロセスの最適化が、大きなパッケージに導入されました。

* 品質の問題の CSV ファイルに、各品質の問題のタイムスタンプが含まれるようになりました。

### バグ修正 {#bug-fixes}

* 正常でないビルド設定があると、パイプラインの Maven アーティファクトキャッシュに不要なファイルが保存され、ビルドコンテナの開始と停止時に不要なネットワーク I/O が発生していました。

* デプロイフェーズが存在しない場合、パイプラインPATCHAPI は失敗します。

* この `ClientlibProxyResourceCheck` 共通のベースパスを持つクライアントライブラリがある場合、品質ルールで偽陽性の問題が発生していました。

* 最大数に達したリポジトリの場合のエラーメッセージで、エラーの理由が指定されていませんでした。

* まれに、特定の応答コードの不適切な再試行処理が原因でパイプラインが失敗することがありました。

