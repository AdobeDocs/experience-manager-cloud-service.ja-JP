---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.11.0 リリースのリリースノート。'
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 94%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在リリース（2021.11.0）のリリース日は、2021年12月16日（PT）です。
次回のリリース（2022.1.0）は 2022年2月3日（PT）です。

## リリースビデオ {#release-video}

2021.11.0（2021年11月）リリースで追加された機能の概要については、[2021年12月リリースの概要](https://video.tv.adobe.com/v/339278)ビデオをご覧ください。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* Dynamic Media の画像スマート切り抜きおよびスウォッチが最新のAdobe AI サービスを活用するようになり、改善された切り抜きとスウォッチを生成します。 また、同じ縦横比で解像度が異なる様々な切り抜きコンテンツを生成する機能が強化されました。さらに、画像プロファイルの幅と高さに変更がない場合、手動編集は再処理時に保持されます。

### [!DNL Assets] プレリリースチャネルの新機能 {#assets-prerelease-features}

* [!DNL Dynamic Media] - Dynamic Media Classic デスクトップアプリケーションを使用しなくても、AEM Dynamic Media インターフェイスを使用して、一般設定と公開設定を設定できるようになりました。

* [!DNL Dynamic Media] は、MXF ビデオの取り込み、プレビュー、再生、公開をサポートするようになりました。MXF ビデオの注釈とショッパブルビデオは、まだサポートされていません。

* リモート DAM と Sites デプロイメント間の接続を設定すると、リモート DAM 上のアセットが Sites デプロイメントで使用できるようになります。これで、リモート DAM アセットまたはフォルダーに対して、[更新、削除、名前変更、移動の操作](/help/assets/use-assets-across-connected-assets-instances.md)を実行できます。更新は、Sites デプロイメントで自動的に（少し遅れて）利用できます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **AEM ワークフローデータを外部化して処理を保護**：顧客が管理するリポジトリに、機密の個人データ（SPD）要素を含むプロセス内の AEM ワークフローデータ（AEM ワークフロー変数データ）を保存して、安全に処理できます。データ要素とワークフロー変数は、AEM リポジトリに格納されず、ワークフローの処理中に顧客が管理するリポジトリからオンデマンドで取得されます。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=ja) では、テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および一括モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * テンプレートファイル（PDF および XDP）に XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。

* **Communications API で作成されたレコードのドキュメントおよび PDF ドキュメント用のカスタムフォント**：Communications API を使用して生成された PDF ドキュメントで、ブランド承認済みフォントを使用して、組織の要件に合わせることができるようになりました。

* **フォームポータル**：[フォームポータル](/help/forms/configure-forms-portal.md)を使用して、AEM Sites ページに公開されたアダプティブフォームを一覧表示できます。これにより、サイト訪問者は利用可能なすべてのフォームを見つけることができます。さらに、訪問者はフォームポータルを使用してアダプティブフォームのドラフトを保存してアクセスし、送信されたアダプティブフォームの PDF バージョンを確認することができます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* コマースの拡張可能な Peregrine コンポーネントに基づくマイアカウントコンポーネントを拡張しました

![拡張されたマイアカウントコンポーネント](/help/assets/CIF/extended-myAccount-components.png)

* 作成者は、追加のレコメンデーションタイプを使用してアドホックなコマース製品レコメンデーションを作成できます

* AEM ストアフロントでのギフトカードのサポート

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.11.0 の Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-cm-nov}

AEM as a Cloud Service 2021.11.0 の Cloud Manager のリリース日は 2021年11月4日（PT）です。
次回のリリースは 2021年12月9日（PT）に予定されています。

### 新機能 {#what-is-new-cm-nov}

* ユーザーは、新しいフロントエンドパイプラインを活用して、フロントエンドコードを迅速かつ排他的にデプロイできるようになりました。詳しくは、[Cloud Manager フロントエンドパイプライン](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)を参照してください。

  >[!IMPORTANT]
  >新しいフロントエンドパイプラインを使用するには、AEM バージョン `2021.10.5933.20211012T154732Z` 以降を使用している必要があります。

* AEM 画像全体を作成する必要がなく、より効率的にコード分析を実行することで、コード品質パイプラインの期間を大幅に短縮できます。この変更は、リリース後の数週間で徐々に適用される予定です。

* パイプライン実行の詳細に Git コミット ID が表示されるようになり、ビルドされたコードの追跡が容易になりました。

* プログラムの作成は、公開されている API を通じて利用できるようになりました。

* 環境の作成は、公開されている API を介して利用できるようになりました。

* この `x-request-id` 応答ヘッダーが、[www.adobe.io](https://www.adobe.io/) の API Playground に表示されるようになりました。このヘッダーは、トラブルシューティングのためにカスタマーケアに関する問題を送信する際に役立ちます。

* ユーザーには、パイプラインがゼロのパイプラインカードから適切なガイダンスが提供されます。

* 新しいアクティビティページが使用できるようになりました。このページでは、パイプラインやコード実行などのアクティビティに関連する詳細を表示できます。時間が経つと、このページに表示されるアクティビティの範囲は拡大し、詳細も表示されるようになります。

* カーソルを合わせたときにステータスのポップオーバーが表示され、詳細の概要を簡単に確認できる新しいパイプラインページが追加されました。パイプライン実行状況が、関連する詳細と共に表示されます。

* パイプラインの編集 API で、デプロイフェーズで使用する環境の変更がサポートされるようになりました。

* OakPal スキャンプロセスの最適化が、大規模パッケージに導入されました。

* 品質問題の CSV ファイルに、品質問題ごとのタイムスタンプが含まれるようになりました。

### バグの修正 {#bug-fixes-nov}

* 正常でないビルド設定があると、パイプラインの Maven アーティファクトキャッシュに不要なファイルが保存され、ビルドコンテナの開始と停止時に不要なネットワーク I/O が発生していました。

* デプロイフェーズが存在しない場合、パイプライン PATCH API は失敗します。

* 共通の基本パスを持つクライアントライブラリがある場合、`ClientlibProxyResourceCheck` 品質ルールで偽陽性の問題が発生していました。

* リポジトリーの最大数に達したエラーメッセージで、エラーの理由が明記されていませんでした。

* まれに、特定の応答コードの不適切な再試行処理が原因でパイプラインが失敗することがありました。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.22 のリリース日は 2021年12月1日（PT）です。

### 新機能 {#what-is-new-bpa}

* 使用する ACS Commons のバージョンを検出し、レポートする機能。
* 1 つのグループ内のユーザーとサブグループの数を検出し、レポートする機能。
* 16MB を超える MongoDB のノードプロパティ値を検出し、レポートする機能。

### バグの修正 {#bug-fixes-bpa}

* 偽陰性を減らすために、基盤コンポーネントの検出を改善しました。
* AEM Forms のお客様向けに、AEM as a Cloud Service で利用できない `EMAIL_PDF_SUBMIT_ACTION` に関する BPA メッセージングを修正しました。
