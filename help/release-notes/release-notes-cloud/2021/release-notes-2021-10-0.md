---
title: リリースノート（2021.10.0） ～の放出 [!DNL Adobe Experience Manager] as a Cloud Service。
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.10.0 リリースのリリースノート。'
source-git-commit: 7d5850cf3b16885c11d1f450a171493a74008a6c
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 52%

---



# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2021.10.0) は 2021 年 11 月 4 日です。
次のリリース (2021.11.0) は 2021 年 12 月 2 日です。

## リリースビデオ {#release-video}

以下をご覧ください： [2021 年 10 月リリースの概要](https://video.tv.adobe.com/v/338253) 追加された機能の概要を示すビデオ。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能 [!DNL Sites] {#sites-features}

* コンテンツフラグメントモデルは、公開後、自動的に読み取り専用状態に設定されるようになりました。これにより、編集後のモデルの再公開後に、ライブ API クエリが意図せず壊れるのを防ぎます。 公開済みのモデルを編集しようとすると、警告が表示されます。 編集は、警告を受け入れる際に可能です。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [!DNL Experience Manager] が、サポート対象のオーディオおよびビデオアセットからのテキストトランスクリプトの自動生成をサポートするようになりました。 [!DNL Azure Media Services]. この [サポートされているファイルタイプ](/help/assets/file-format-support.md#audio-video-transcription-formats) は自動的に書き込まれ、テキストは WebVTT 形式で保存されます。 WebVTT キャプションは、より効果的な検索、キャプション、翻訳に使用されます。 また、この機能により、アセットのアクセシビリティ、検出性およびローカライゼーションが向上します。

### の新機能 [!DNL Assets] プレリリースチャネル {#assets-prerelease-features}

* [!DNL Dynamic Media] 画像のスマート切り抜きとスウォッチが、最新のSenseiサービスによって強化され、改善された切り抜きとスウォッチが生成されます。 また、同じ縦横比で異なる解像度を持つ異なる切り抜きコンテンツを生成する機能が強化されました。 また、イメージプロファイルの幅と高さに変更がない場合、手動の編集は再処理時に保持されます。

* スマートタグは、スマートコンテンツサービスの代わりに、アセットマイクロサービスを使用して、アセットに自動的に適用されます。 タグ付けの結果を改善し、バイアスを減らすために、基になるモデルが更新されます。 <!-- As it uses asset microservices, it is now possible to develop custom workers using Stock10-based Smart Tags. -->

<!-- Leave this commented.
### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Oct release. Details in CQDOC-18404.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms-oct-2021}

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics を使用して、ログイン済みとログインしていない（匿名）状態の両方の動作を取得および追跡して、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms-oct-2021}

* **AEM ワークフローデータを外部化して処理を保護**：顧客が管理するリポジトリーに、機密の個人データ（SPD）要素を含むプロセス内の AEM ワークフローデータ（AEM ワークフロー変数データ）を保存して、安全に処理できます。データ要素とワークフロー変数は、AEM リポジトリに格納されず、ワークフローの処理中に顧客が管理するリポジトリからオンデマンドで取得されます。

### [!DNL Forms] のベータ版機能 {#what-is-new-forms-oct2021-beta}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) では、テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および一括モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * テンプレートファイル（PDF および XDP）に XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* CIF アドオンは、新しい GraphQL API とスキーマを備えた最新の Commerce v2.4.3 をサポートしています

* 作成者は、リッチテキストエディター (RTE) を使用して、テキストフィールドに製品ページやカタログページへのリンクを追加できます。 RTE ツールバーに CIF アイコンが追加され、選択者が開いて、コンテキストを離れることなく製品やカテゴリをすばやく検索および選択できるようになりました。

* 既存のポップアップ買い物かごとチェックアウトは、AEM専用の買い物かごとチェックアウトページに置き換えられました。 これらのページ上のコンポーネントは、Magentoの拡張可能な Peregrine コンポーネントを使用して構築されます

* マーチャントは、コマースバックエンドを使用して、ナビゲーション内の特定の製品カタログカテゴリを非表示にできます。 CIF ナビゲーションコアコンポーネントは、コマースバックエンド設定に従って、ナビゲーションでカテゴリを表示/非表示にする「メニューに含める」を設定します

* カテゴリまたは製品ページが見つからない場合、AEM Storefront Venia は HTTP 404 エラーを返します

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.10.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 の Cloud Manager のリリース日は 2021 年 11 月 04 日です。次回のリリースは 2021 年 12 月 09 日（PT）に予定されています。

### 新機能 {#what-is-new-cm-nov}

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

### バグ修正 {#bug-fixes-nov}

* 正常でないビルド設定があると、パイプラインの Maven アーティファクトキャッシュに不要なファイルが保存され、ビルドコンテナの開始と停止時に不要なネットワーク I/O が発生していました。

* デプロイフェーズが存在しない場合、パイプライン PATCH API は失敗します。

* 共通の基本パスを持つクライアントライブラリがある場合、`ClientlibProxyResourceCheck` 品質ルールで偽陽性の問題が発生していました。

* リポジトリーの最大数に達したエラーメッセージで、エラーの理由が明記されていませんでした。

* まれに、特定の応答コードの不適切な再試行処理が原因でパイプラインが失敗することがありました。


## リリース日 {#release-date-cm-oct}

AEM as a Cloud Service 2021.10.0の Cloud Manager のリリース日は 2021 年 10 月 14 日です。

### 新機能 {#what-is-new-cm-oct}

* 今後の変更に備えて、既存のデプロイメントパイプラインが参照され、ユーザーインターフェイスで次のようにラベル付けされるようになりました。 **フルスタック** パイプライン。

* パイプラインカードが更新され、実稼動パイプラインと実稼動以外のパイプラインの両方が 1 つのカードでまとめて表示されるようになりました。ユーザーは、各パイプラインに関連付けられたアクションメニューから「実行」／「一時停止」／「再開」を直接選択することができます。

* デプロイメントマネージャーの役割を持つユーザーが、UI を使用して、セルフサービス方式で実稼働パイプラインを削除できるようになりました。

* パイプラインの追加操作と編集操作が更新され、使い慣れた最新のモーダルを使用するようになりました。

* Cloud Manager のユーザーは、 **フィードバック** ボタンをクリックします。

* 年別の SLA グラフを Cloud Manager のユーザーインターフェイスからダウンロードできるようになりました。

* コード品質パイプラインと実稼動以外のパイプラインの実行で、より効率的なシャロー（shallow）クローン作成プロセスをビルドステップ中に使用するようになりました。これにより、特に大きな Git リポジトリーを使用しているお客様の場合、ビルド時間が短縮されます。

* IP許可リストの追加ウィザードで、許可されている最大数に達した場合に、ユーザーに許可リストを送信するようになりました。

* ログインしたユーザーがブラウザーで API を試すことができるインタラクティブなプレイグラウンドに関する説明が、Cloud Manager API ドキュメントに含まれるようになりました。詳しくは、[Cloud Manager API Playground](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) を参照してください。

* 「移動先」の選択オプションが無効になっている場合のプログラムカードのツールヒントがわかりやすくなりました。「実稼動環境が存在しません」と表示されるようになりました。

### バグ修正 {#bug-fixes-cm-oct}

* まれに、Adobe・スタッフがお客様の環境をリストアする場合、環境が完全に稼働する前にリストアが完了したと見なされました。

* 環境の作成中におこなわれた一部の内部リクエストが再試行されませんでした。

* ドメイン名の検証後にデプロイメントの失敗エラーが発生した場合、エラーメッセージが修正され、お客様にAdobe担当者への連絡をリクエストするようになりました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

ベストプラクティスアナライザー v2.1.20 のリリース日は 2021 年 10 月 5 日です。

### 新機能 {#what-is-new}

* ノード名の長さを検出し、レポートする機能。

* 合計インデックスサイズを検出し、レポートする機能。

* 元のレンディションが欠落しているアセットを検出し、レポートする機能。
