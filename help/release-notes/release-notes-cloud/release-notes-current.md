---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: e76ee82b44e48e88d5c750ebb22db11067cb11b5
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 51%

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

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2021.11.0) は 2021 年 12 月 16 日です。
次のリリース (2022.1.0) は 2022 年 1 月 27 日です。

## リリースビデオ {#release-video}

以下をご覧ください： [2021 年 12 月リリースの概要](https://video.tv.adobe.com/v/339278) 2021.11.0（2021 年 11 月）リリースで追加された機能の概要を示すビデオです。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* Dynamic Media画像のスマート切り抜きとスウォッチに、最新のSenseiサービスが適用され、改善された切り抜きとスウォッチが生成されるようになりました。 また、同じ縦横比で異なる解像度を持つ異なる切り抜きコンテンツを生成する機能が強化されました。 また、イメージプロファイルの幅と高さに変更がない場合、手動の編集は再処理時に保持されます。

### の新機能 [!DNL Assets] プレリリースチャネル {#assets-prerelease-features}

* [!DNL Dynamic Media] - Dynamic Media Classicデスクトップアプリケーションを使用しなくても、AEM Dynamic Mediaインターフェイスを使用して、一般設定と公開設定を設定できるようになりました。

* [!DNL Dynamic Media] MXF ビデオの取り込み、プレビュー、再生、公開をサポートするようになりました。 MXF ビデオの注釈とショッパブルビデオは、まだサポートされていません。

* リモート DAM と Sites デプロイメント間の接続を設定すると、リモート DAM 上のアセットが Sites デプロイメントで使用できるようになります。 これで、 [操作の更新、削除、名前変更、移動](../../assets/use-assets-across-connected-assets-instances.md) リモートの DAM アセットまたはフォルダー上で 更新は、Sites デプロイメントで自動的に利用できます（少し遅れて）。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **AEM ワークフローデータを外部化して処理を保護**：顧客が管理するリポジトリーに、機密の個人データ（SPD）要素を含むプロセス内の AEM ワークフローデータ（AEM ワークフロー変数データ）を保存して、安全に処理できます。データ要素とワークフロー変数は、AEM リポジトリに格納されず、ワークフローの処理中に顧客が管理するリポジトリからオンデマンドで取得されます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) では、テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および一括モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * テンプレートファイル（PDF および XDP）に XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。

* **コミュニケーション API で作成されたレコードのドキュメントおよびPDFドキュメント用のカスタムフォント**:コミュニケーション API を使用して生成されたPDFドキュメントで、ブランド承認済みフォントを使用して、組織の要件に合わせることができるようになりました。

* **Forms Portal**:以下を使用できます。 [Forms Portal](/help/forms/configure-forms-portal.md) 発行済みのアダプティブフォームをAEM Sitesページに一覧表示する。 これにより、サイト訪問者は利用可能なすべてのフォームを見つけることができます。 さらに、訪問者はフォームポータルを使用してアダプティブフォームのドラフトを保存してアクセスし、送信されたアダプティブフォームのPDFバージョンを確認することができます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* コマースの拡張可能な Peregrine コンポーネントに基づく myAccount コンポーネントの拡張

![拡張された myAccount コンポーネント](/help/assets/CIF/extended-myAccount-components.png)

* 作成者は、追加のレコメンデーションタイプを使用してアドホックコマース製品Recommendationsを作成できます

* AEM Storefront でのギフトカードのサポート

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.11.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 の Cloud Manager のリリース日は 2021 年 11 月 04 日です。次回のリリースは 2021 年 12 月 09 日（PT）に予定されています。

### 新機能 {#what-is-new-cm-nov}

* ユーザーは、新しいフロントエンドパイプラインを活用して、フロントエンドコードを迅速に排他的にデプロイできるようになりました。 詳しくは、 [Cloud Manager フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) を参照してください。

   >[!IMPORTANT]
   >AEM版である必要があります `2021.10.5933.20211012T154732Z` またはそれ以降で新しいフロントエンドパイプラインを利用できます。

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

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.22 のリリース日は 2021 年 12 月 1 日です。

### 新機能 {#what-is-new-bpa}

* 使用する ACS コモンのバージョンを検出し、レポートする機能。
* 1 つのグループ内のユーザーとサブグループの数を検出し、レポートする機能。
* 16MB を超える MongoDB のノードプロパティ値を検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* 偽陰性を減らすために、基盤コンポーネントの検出を改善しました。
* AEM Formsのお客様向けに、に関する BPA メッセージ `EMAIL_PDF_SUBMIT_ACTION` AEM as a Cloud Serviceで使用できない問題を修正しました。
