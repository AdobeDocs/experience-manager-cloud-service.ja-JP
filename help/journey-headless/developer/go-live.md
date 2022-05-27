---
title: ヘッドレスアプリケーションの運用開始方法
description: AEM ヘッドレスデベロッパージャーニーのこのパートでは、Git 内のローカルコードを CI／CD パイプライン用に Cloud Manager Git に移行することでヘッドレスアプリケーションをライブ環境にデプロイする方法を説明します。
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 81%

---

# ヘッドレスアプリケーションの運用開始方法 {#go-live}

[AEM ヘッドレスデベロッパージャーニー](overview.md)のこのパートでは、Git 内のローカルコードを CI／CD パイプライン用に Cloud Manager Git に移行することでヘッドレスアプリケーションをライブ環境にデプロイする方法を説明します。

## これまでの説明内容 {#story-so-far}

前のドキュメントのAEMヘッドレスジャーニーでは、 [すべてを組み合わせる方法 — アプリとコンテンツをAEMヘッドレスに組み込む](put-it-all-together.md) AEM開発ツールを使用して、プロジェクトのすべてのファセットを組み立てる方法を学びました。

この記事は、これらの基本事項に基づいているので、独自の AEM ヘッドレスプロジェクトの運用開始準備をする方法を理解できます。

## 目的 {#objective}

このドキュメントでは、AEMヘッドレス公開パイプラインと、アプリケーションの運用を開始する前に考慮する必要があるパフォーマンスに関する考慮事項について説明します。

* ローンチ前のアプリケーションのセキュリティ確保とスケーリング
* パフォーマンスとデバッグの問題の監視

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
AEMヘッドレスアプリケーションを起動に備えるには、以下に示すベストプラクティスに従います。

## ローンチ前のヘッドレスアプリケーションのセキュリティ確保とスケーリング {#secure-and-scale-before-launch}

1. GraphQL リクエストに[トークンベースの認証](/help/headless/security/authentication.md)を設定します。
1. [キャッシュ](/help/implementing/dispatcher/caching.md)を設定します。

## モデル構造と GraphQL 出力 {#structure-vs-output}

* 15 KB を超える JSON コード（gzip で圧縮）を出力するクエリを作成しないようにします。長い JSON ファイルの場合、クライアントアプリケーションで解析する際に大量のリソースを消費します。
* フラグメント階層のネストレベルは 5 以内にします。レベルを増やすと、コンテンツ作成者は変更の影響を考慮しにくくなります。
* モデル内の依存関係階層を使用したクエリをモデル化するのではなく、複数オブジェクトクエリを使用します。これにより、多数のコンテンツ変更を行わなくても、より長期にわたって柔軟に JSON 出力を再構成できます。

## CDN キャッシュヒット率の最大化 {#maximize-cdn}

* サーフェスからライブコンテンツをリクエストする場合を除き、直接の GraphQL クエリは使用しません。
   * 可能な限り、永続的クエリを使用します。
   * これらのクエリを CDN でキャッシュするために、CDN の TTL 値を 600 秒以上に設定します。
   * AEM は既存のクエリに対するモデル変更の影響を計算できます。
* CDN へのクライアントトラフィックを減らし、より高い TTL を割り当てるため、JSON ファイル／GraphQL クエリをコンテンツ変更率の低いものと高いものに分けます。これにより、CDN でのオリジンサーバーに対する JSON の再検証が最小限に抑えられます。
* CDN からコンテンツを能動的に無効にするには、ソフトパージを使用します。これにより、CDN は、キャッシュミスを引き起こすことなく、コンテンツを再ダウンロードできます。

## ヘッドレスコンテンツのダウンロード時間の短縮 {#improve-download-time}

* HTTP クライアントで必ず HTTP/2 を使用します。
* HTTP クライアントで gzip に対するリクエストには必ず Accept ヘッダーを付けます。
* JSON および参照先アーティファクトをホストするために使用するドメインの数を最小限に抑えます。
* `Last-modified-since` を利用してリソースを更新します。
* JSON ファイルで `_reference` 出力を使用すると、完全な JSON ファイルを解析しなくても、アセットのダウンロードを開始できます。

## 実稼動へのデプロイ {#deploy-to-production}

すべてがテスト済みで正常に動作していることを確認したら、コードの更新を [Cloud Manager での一元化された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=ja).

アップデートが Cloud Manager にアップロードされたら、[Cloud Managerの CI／CD パイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=ja#how-to-use)を使用して、アップデートを AEM as a Cloud Service にデプロイできます。

コードのデプロイを開始するには、Cloud Manager CI／CD パイプラインを利用します。このパイプラインについて詳しくは、[こちら](/help/implementing/deploying/overview.md)を参照してください。

## パフォーマンスの監視 {#performance-monitoring}

AEMヘッドレスアプリケーションを使用する際に、ユーザーが可能な限り最高のエクスペリエンスを得るためには、次に説明するように、主要なパフォーマンス指標を監視することが重要です。

* アプリのプレビューバージョンと実稼動バージョンの動作を検証する
* AEM ステータスページで現在のサービス稼働状況を確認する
* パフォーマンスレポートにアクセスする
   * 配信のパフォーマンス
      * CDN（Fastly）パフォーマンス - 呼び出し数、キャッシュ率、エラー率、ペイロードトラフィックを確認する
      * オリジンサーバー - 呼び出し数、エラー率、CPU 負荷、ペイロードトラフィックを確認する
   * オーサーのパフォーマンス
      * ユーザー数、リクエスト数、読み込み数を確認する
* アプリとスペース固有のパフォーマンスレポートへのアクセス
   * サーバーが起動したら、一般的な指標が緑／オレンジ／赤のどれになっているかを確認し、アプリの具体的な問題を特定する
   * 特定のアプリやスペース（例：Photoshop デスクトップ、ペイウォール）に限定した上記レポートを開く
   * Splunk ログ API を使用してサービスやアプリケーションのパフォーマンスにアクセスする
   * その他の問題が発生した場合は、カスタマーサポートに連絡する

## トラブルシューティング {#troubleshooting}

### デバッグ {#debugging}

デバッグに対する一般的なアプローチとして、次のベストプラクティスに従います。

* アプリケーションのプレビューバージョンで機能とパフォーマンスを検証する
* アプリケーションの実稼動バージョンで機能とパフォーマンスを検証する
* コンテンツフラグメントエディターの JSON プレビューを使用して検証する
* クライアントアプリケーションで JSON を調べて、クライアントアプリケーションや配信の問題の有無を確認する
* GraphQL を使用して JSON を調べ、キャッシュされたコンテンツまたは AEM に関係する問題の有無を確認する

### サポートへのバグの登録 {#logging-a-bug-with-support}

さらにサポートが必要な場合に備えてサポートにバグを効率的に登録するには、次の手順に従います。

* 必要に応じて、問題のスクリーンショットを撮る
* 問題の再現方法を説明する
* 問題が再現するコンテンツを説明する
* AEM サポートポータルを通じて問題を適切な優先度で登録する

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEM ヘッドレスデベロッパージャーニーが完了し、以下を理解できました。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い
* AEM のヘッドレス機能
* AEM ヘッドレスプロジェクトを編成する方法
* AEM でヘッドレスコンテンツを作成する方法
* AEM でヘッドレスコンテンツを取得および更新する方法
* AEM ヘッドレスプロジェクトの運用を開始する方法
* 運用開始後の作業

皆さんは初めての AEM ヘッドレスプロジェクトの運用を既に開始したかもしれませんし、そうでなくても、そのために必要な知識はすべて習得したことになります。お疲れ様でした。

### 単一ページアプリケーションの調査 {#explore-spa}

ただし、AEM のヘッドレスストアは、ここで終わる必要はありません。次の場所で [ジャーニーの開始の手引き](getting-started.md#integration-levels) AEMがヘッドレス配信と従来のフルスタックモデルをサポートするだけでなく、両方の利点を組み合わせたハイブリッドモデルをサポートする方法について簡単に説明しました。

このような柔軟性がプロジェクトに必要な場合は、さらにジャーニーのオプションパート [AEM で単一ページアプリケーション（SPA）を作成する方法](create-spa.md)に進んでください。

## その他のリソース {#additional-resources}

* [AEM as a Cloud Service へのデプロイの概要](/help/implementing/deploying/overview.md)
* [Cloud Manager を使用したコードのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Cloud Manager Git リポジトリーと外部 Git リポジトリーの統合および AEM as a Cloud Service へのプロジェクトのデプロイ](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=ja)
