---
title: AEM as a Cloud Service Release 2021.11.0 Cloud Manager のリリースノート
description: AEM as a Cloud Service Release 2021.11.0 Cloud Manager のリリースノート
feature: Release Information
source-git-commit: d6aa3097e558d4e78f20493f214167db57f1a013
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 79%

---

# Adobe Experience Manager as a Cloud Service 2021.11.0 の Cloud Manager のリリースノート {#release-notes}

このページでは、AEM as a Cloud Service Release 2021.11.0 Cloud Manager のリリースノートの概要を説明しています。

>[!NOTE]
>Adobe Experience Manager as a Cloud Service の最新のリリースノートを参照するには、[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=ja)をクリックしてください。

## リリース日 {#release-date}

AEM as a Cloud Service 2021.11.0 の Cloud Manager のリリース日は 2021 年 11 月 04 日です。次回のリリースは 2021 年 12 月 16 日（PT）に予定されています。

### 新機能 {#what-is-new}

* ユーザーは、新しいフロントエンドパイプラインを活用して、フロントエンドコードを迅速に排他的にデプロイできるようになりました。 詳しくは、 [Cloud Manager フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) を参照してください。

   >[!IMPORTANT]
   >AEM版である必要があります `2021.10.5933.20211012T154732Z` を使用して、新しいフロントエンドパイプラインを活用します。

* AEM画像全体を構築する必要なく、より効率的にコード分析を実行することで、コード品質パイプラインの期間を大幅に短縮できます。 この変更は、リリース後の数週間で徐々に適用される予定です。

* パイプライン実行の詳細に Git Commit ID が表示されるようになり、ビルドされたコードの追跡が容易になりました。

* プログラムの作成は、公開されている API を通じて利用できるようになりました。

* 環境の作成は、公開されている API を介して使用できるようになりました。

* この `x-request-id` 応答ヘッダーが、[www.adobe.io](https://www.adobe.io/) の API Playground に表示されるようになりました。このヘッダーは、トラブルシューティングのためにカスタマーケアに関する問題を送信する際に役立ちます。

* ユーザーには、パイプラインがゼロのパイプラインカードから適切なガイダンスが提供されます。

* 新しいアクティビティページが使用できるようになりました。このページでは、パイプラインやコード実行などのアクティビティに関連する詳細を表示できます。時間が経つと、このページに表示されるアクティビティの範囲は拡大し、詳細も表示されるようになります。

* カーソルを合わせたときにステータスのポップオーバーが表示され、詳細の概要を簡単に確認できる新しいパイプラインページが追加されました。パイプラインの実行状況が、関連する詳細と共に表示されます。

* パイプラインの編集 API で、デプロイフェーズで使用する環境の変更がサポートされるようになりました。

* OakPal スキャンプロセスの最適化が、大規模パッケージに導入されました。

* 品質問題の CSV ファイルに、品質問題ごとのタイムスタンプが含まれるようになりました。

### バグ修正 {#bug-fixes}

* 正常でないビルド設定があると、パイプラインの Maven アーティファクトキャッシュに不要なファイルが保存され、ビルドコンテナの開始と停止時に不要なネットワーク I/O が発生していました。

* デプロイフェーズが存在しない場合、パイプライン PATCH API は失敗します。

* 共通の基本パスを持つクライアントライブラリがある場合、`ClientlibProxyResourceCheck` 品質ルールで偽陽性の問題が発生していました。

* リポジトリーの最大数に達したエラーメッセージで、エラーの理由が明記されていませんでした。

* まれに、特定の応答コードの不適切な再試行処理が原因でパイプラインが失敗することがありました。

