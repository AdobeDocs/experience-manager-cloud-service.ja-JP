---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 リリースのリリースノート。'
source-git-commit: dcc598b565dfeeb7c5f62671edc8b256b60d9ec4
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 25%

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

[!DNL Adobe Experience Manager]のCloud Service2021.6.0のリリース日は2021年6月28日です。
次のリリース(2021.7.0)は2021年7月30日に予定されています。

## リリースビデオ {#release-video}

追加された機能の概要については、 2021年6月リリースの概要](https://video.tv.adobe.com/v/334296)ビデオをご覧ください。[

## AEM as a cloud Service向けXMLドキュメント {#xml-documentation}

### 新機能 {#what-is-new-xml-documentation}

* AEM as aCloud ServiceのXMLドキュメントがGAになりました。
* これにより、既存のAEMCloud Serviceのお客様は、AEMサイトを含む複数のチャネルにわたる技術コンテンツの読み込み、作成、管理および配信に関するXMLドキュメントのアドオンを入手できます

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.6.0 および 2021.5.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-june-cm}

AEM as aCloud Service2021.6.0のCloud Managerのリリース日は2021年6月10日です。
次回のリリースは 2021 年 6 月 15 日（PT）に予定されています。

### 新機能 {#what-is-new-junecm}

* プレビューサービスは、すべてのプログラムに周期的にデプロイされます。 お客様は、プログラムがプレビューサービスに対して有効になると、製品内で通知を受けます。 詳しくは、[Preview Serviceへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)を参照してください。

* ビルド手順中にダウンロードされた Maven の依存関係は、パイプライン実行から次回の実行までの間にキャッシュされるようになりました。この機能は、今後数週間にわたり、お客様に対して有効になる予定です。

* プログラムの名前は、プログラムを編集ダイアログで編集できるようになりました。

* プロジェクトの作成時に使用されるデフォルトのブランチ名と、Git 管理ワークフロー経由のデフォルトのプッシュコマンドで使用されるデフォルトのブランチ名が `main` に変更されました。

* UI でのプログラムの編集エクスペリエンスが更新されました。

* 品質ルール `ImmutableMutableMixCheck` が更新され、`/oak:index` ノードが不変として分類されるようになりました。

* 品質ルール `CQBP-84` と `CQBP-84--dependencies` は、1 つのルールに統合されました。この統合の一環として、AEM ランタイムにデプロイされるサードパーティの依存関係の問題を、依存関係のスキャンでより正確に特定できます。

* 混乱を避けるために、環境の詳細ページのパブリッシュAEMとパブリッシュDispatcherのセグメント行が統合されました。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* `damAssetLucene`インデックスの構造を検証するための新しいコード品質ルールが追加されました。 詳しくは、[カスタムDAM Asset Lucene Oakインデックス](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)を参照してください。

* 環境の詳細ページに、公開サービスとプレビューサービスの複数のドメイン名が表示されるようになりました（該当する場合）。 詳しくは、[環境の詳細](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)を参照してください。

### バグ修正 {#bug-fixes-junecm}

* ルート要素名の後に改行を含む JCR ノード定義が正しく解析されなかった問題を修正しました。

* リストリポジトリー API は、削除されたリポジトリをフィルタリングしません。

* スケジュール手順に無効な値が指定された場合、誤ったエラーメッセージが表示されていました。

* 場合によっては、IP許可リストがデプロイされていない場合でも、その設定の横に緑色の&#x200B;*アクティブ*&#x200B;ステータスが表示されることがあります。

* 一部のプログラム編集シーケンスでは、実稼動パイプラインを作成または編集できなくなる可能性があります。

* 一部のプログラム編集シーケンスでは、**概要**&#x200B;ページに、プログラム設定を再実行する際に誤解を招くようなメッセージが表示される場合があります。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]の新機能 {#ga-features-assets}

* コンテンツ自動化機能を使用すると、 [!DNL Experience Manager Assets]は[!DNL Adobe Creative Cloud] APIを活用して、アセットの大規模な生産を自動化できます。 同じアセットのバリエーションを作成するのに必要な時間と繰り返しを大幅に減らし、コンテンツの速度を向上させます。 機能にはコードは不要で、DAM内から機能します。
* [!DNL Adobe Asset Link] 、 、のv3.0お [!DNL Adobe Photoshop]よびの [!DNL Adobe Illustrator]v2.0がリリー [!DNL Adobe InDesign]  [!DNL Adobe Asset Link]  [!DNL Adobe XD] スされました。以下を提供します。

   * [!DNL Assets Essentials]のサポート。
   * [!DNL Experience Manager]に[!DNL Cloud Service]または[!DNL Assets Essentials]として自動的に接続する機能。

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### [!DNL Assets]プレリリースチャネルで利用できる新機能 {#beta-features-assets}

* ビュー設定が強化され、ユーザーがデフォルトのビューとデフォルトの並べ替えパラメーターを選択できるようになりました。
* Linkshareのダウンロード機能は、非同期ダウンロードを使用してダウンロード速度を向上させます。
* プロパティの述語に基づいて、フォルダーを検索およびフィルタリングできます。
* [!DNL Experience Manager Assets] を使用してPDFビューアを埋め込み、サポートされ [!DNL Adobe Document Cloud] ているドキュメントをプレビューします。この機能を使用すると、複雑な処理をおこなわずに、PDFファイルやその他の複数ページファイルをプレビューできます。 これにより、[!DNL Experience Manager] 6.5と同等の機能が向上します。

### [!DNL Assets] で修正されたバグ  {#bugs-fixed-assets}

* サブフォルダーに所有者を追加すると、[!DNL Assets]は親フォルダーの所有者と同じユーザーも追加します。 （CQ-4323737）
* コレクションにアセットを追加する際に、ユーザーがコレクション検索でフィルターを適用すると、ユーザーはリスト表示でコレクションを表示できません。 （CQ-4323181）
* ファイルとフォルダーを検索する場合、ユーザーがフィルターを適用し、「[!UICONTROL ファイルとフォルダー]」を選択すると、ファイルのみが表示され、フォルダーは表示されません。 （CQ-4319543）

## [!DNL Experience Manager Sites] として  [!DNL Cloud Service] {#sites}

### [!DNL Sites]の新機能 {#ga-features-sites}

* Sites管理UIで、プレビュー層への公開がページステータスとして表示されるようになりました。
* 「プレビュー層に公開」で、アクションの最後にプレビューURLが表示され、後で参照できるようにページプロパティにURLが保持されるようになりました。

## [!DNL Experience Manager Forms] として  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms}

* AEM Inboxのカスタム列をフィルタリングする機能を追加しました。
* アダプティブフォームエディターのテーマエディターとスタイルレイヤーを使用して、Captchaコンポーネントのスタイルを設定する機能を追加しました。
* ソースフォーム内の論理セクションを自動的に検出し、対応するアダプティブフォームPDF formsに変換する際の速度と精度が向上しました。
* PDFまたはXDPファイルをあるフォルダーから別のフォルダーに移動する移動アクションが追加されました。

### [!DNL Forms]のベータ機能 {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:通信APIを使用すると、XDPテンプレートとXMLデータを組み合わせて様々な形式の印刷ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。 APIを使用すると、次の操作を可能にするアプリケーションを作成できます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する
   * 非インタラクティブPDF印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFAフォームPDFおよびAdobe Acrobatフォーム(AcroForms)から印刷用PDFを生成します。

* **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

[!DNL formscsbeta@adobe.com]に書き込んで、ベータ版プログラムにサインアップできます。

### [!DNL Forms] で修正されたバグ  {#forms-bugs-fixed}

* フォームデータモデル(FDM)を使用してデータをバックエンドサービスに送信する前にフィールドの検証が完了すると、検証は成功しますが、フォームデータモデルサービスは検証後にデータを呼び出せません。
* Apple iOSデバイスから標準のHTMLアップロードフィールドを含むフォームを送信すると、ファイルのコンテンツが送信されず、0バイトのファイルがもう一方の端に届く場合があります。 Apple iOS では、これは既知の問題です。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] として  [!DNL Cloud Service] {#screens}

この節では、 AEM Screens as aCloud Serviceのリリースノートの概要を説明します。

### リリース日 {#release-date-june-screens}

AEM Screens as aCloud Serviceのリリース日は2021年6月24日です。

### 新機能 {#what-is-new-screens-june}

>[!NOTE]
>ScreensをCloud Serviceとして正常にインストール、設定、実行するために必要な基本的な知識と、詳細な概念に関する技術ドキュメントへのリンクについては、『[Cloud ServiceとしてのAEM Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=ja)ガイド』を参照してください。

* デバイスの一括登録管理は、大量のプレーヤーデバイスのプロビジョニングを高速化し、より効率的に行うことを意味します。

* デバイス、ディスプレイ、チャネルの各在庫ビューの検索およびフィルターオプションを改善しました。

* デバイスのヒーススナップショットは、重要なステータスを一目で確認することで、時間を節約します。

* オブジェクトの詳細ページには、プロジェクト内の各オブジェクトに関する最も関連性の高い情報の概要が表示されます。

## CIFアドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* コンテンツフラグメント( 製品/カテゴリピッカーのUIのサポート)
* 新しいコマースコンテンツフラグメントコアコンポーネント
* AEMバックエンドでサポートされるフルテキストコマース検索
* コマースコアコンポーネントは、AdobeCommerce Sensei Recsのデータ収集をサポートします。
* カテゴリページのSEOに対応するURLの改善
* サイト/設定ごとのカスタムHTTPヘッダーのサポート

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツールv1.5.4のリリース日は2021年6月28日です。

### 新機能 {#what-is-new-ctt-latest}

* CTTで使用するためのオプションの[プリコピー](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)手順のサポートが追加されました。 コピー前の手順を使用すると、ソースAEMインスタンスがAmazon S3またはAzure Blob Storageデータストアを使用するように設定されている場合に、コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に高速化できます。

* ガードレールがCTTに追加され、取得が停止するのを防ぎ、取得段階で重要なポイントに到達したデータが破損する可能性があることを防ぎます。

* 抽出ログは、トラブルシューティングに役立つより説明的になりました。

* UIに、より説明的な取り込みステータスメッセージを追加しました。

### バグ修正 {#bug-fixes-ctt-latest}

* オーサーインスタンスでインジェストを停止する際、UIは、以前に完了したパブリッシュインスタンスのインジェストを`FINISHED`から`STOPPED`に上書きしました。 この問題が修正されました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

Best Practices Analyzer v2.1.16のリリース日は2021年6月30日です。

### 新機能 {#what-is-new-bpa-latest}

* `/content/dam`の下のフォルダーに見つからない子ノードを検出し、報告する機能。

* 使用するベストプラクティスアナライザーのバージョンを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa-latest}

* サポートされていないリポジトリ構造(URS)に関するログエラーを修正しました。

