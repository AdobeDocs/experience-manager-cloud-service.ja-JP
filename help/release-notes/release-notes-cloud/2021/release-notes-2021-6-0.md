---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 リリースのリリースノート。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 97%

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

[!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 のリリース日は 2021 年 6 月 28 日です。次回のリリース（2021.7.0）は、2021 年 7 月 29 日に予定されています。

## リリースビデオ {#release-video}

追加された機能の概要については、[2021 年 6 月リリースの概要](https://video.tv.adobe.com/v/334296)ビデオをご覧ください。

## AEM as a cloud Service 向け XML ドキュメント {#xml-documentation}

### 新機能 {#what-is-new-xml-documentation}

* AEM as a Cloud Service の XML ドキュメントが GA になりました。
* これにより、既存の AEM Cloud Service の顧客は、AEM サイトを含む複数のチャネルで、XML ドキュメントのアドオンを入手して、技術コンテンツをインポート、作成、管理、配信することができます。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.6.0 および 2021.5.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

### リリース日 {#release-date-june-cm}

AEM as a Cloud Service 2021.6.0 の Cloud Manager のリリース日は 2021 年 6 月 10 日です。次回のリリースは 2021 年 6 月 15 日（PT）に予定されています。

### 新機能 {#what-is-new-junecm}

* プレビューサービスは、すべてのプログラムに周期的にデプロイされます。顧客は、プログラムがプレビューサービスに対して有効になると、製品内で通知を受け取ります。詳しくは、[プレビューサービスへのアクセス](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)を参照してください。

* ビルド手順中にダウンロードされた Maven の依存関係は、パイプライン実行から次回の実行までの間にキャッシュされるようになりました。この機能は、今後数週間にわたり、お客様に対して有効になる予定です。

* プログラムを編集ダイアログでプログラムの名前を編集できるようになりました。

* プロジェクトの作成時に使用されるデフォルトのブランチ名と、Git 管理ワークフロー経由のデフォルトのプッシュコマンドで使用されるデフォルトのブランチ名が `main` に変更されました。

* UI でのプログラムの編集エクスペリエンスが更新されました。

* 品質ルール `ImmutableMutableMixCheck` が更新され、`/oak:index` ノードが不変として分類されるようになりました。

* 品質ルール `CQBP-84` と `CQBP-84--dependencies` は、1 つのルールに統合されました。この統合の一環として、AEM ランタイムにデプロイされるサードパーティの依存関係の問題を、依存関係のスキャンでより正確に特定できます。

* 混乱を避けるために、環境の詳細ページのパブリッシュ AEM とパブリッシュ Dispatcher のセグメント行が統合されました。

  ![Dispatcher環境 &#x200B;](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* `damAssetLucene` インデックスの構造を検証するための新しいコード品質ルールが追加されました。詳しくは、[カスタム DAM Asset Lucene Oak インデックス](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)を参照してください。

* 環境の詳細ページに、公開サービスとプレビューサービスの複数のドメイン名が表示されるようになりました（該当する場合）。詳しくは、[環境の詳細](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)を参照してください。

### バグの修正 {#bug-fixes-junecm}

* ルート要素名の後に改行を含む JCR ノード定義が正しく解析されなかった問題を修正しました。

* リストリポジトリー API は、削除されたリポジトリーをフィルタリングしません。

* スケジュール手順に無効な値が指定された場合、誤ったエラーメッセージが表示されていました。

* 該当する設定がデプロイされていない場合でも、IP 許可リストの横に緑色の「*アクティブ*」ステータスが表示される場合がありました。

* 一部のプログラム編集シーケンスで実稼動パイプラインを作成または編集できなくなることがありました。

* 一部のプログラム編集シーケンスでは、**概要**&#x200B;ページに、プログラム設定を再実行する際に誤解を招くようなメッセージが表示される場合があります。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#ga-features-assets}

* コンテンツ自動化機能を使用 [!DNL Experience Manager Assets] ると、[!DNL Adobe Creative Cloud] API を使用して、アセットの大規模な生成を自動化できます。 同じアセットのバリエーションを作成するのに必要な時間と繰り返しを大幅に減らし、コンテンツの速度を向上させます。機能はコードは必要とせず、DAM 内から機能します。
* [!DNL Adobe Asset Link] v3.0（[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]、[!DNL Adobe InDesign]、[!DNL Adobe Asset Link] v2.0（[!DNL Adobe XD]）がリリースされました。これには次の機能があります。

   * [!DNL Assets Essentials] のサポート。
   * [!DNL Experience Manager] as a [!DNL Cloud Service] または [!DNL Assets Essentials] に自動的に接続する機能。

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#beta-features-assets}

* ビュー設定が強化され、デフォルトのビューとデフォルトの並べ替えパラメーターを選択できるようになりました。
* Linkshare のダウンロード機能は、非同期ダウンロードを使用してダウンロード速度を向上させます。
* プロパティの述語に基づいて、フォルダーを検索およびフィルタリングできます。
* [!DNL Experience Manager Assets] に [!DNL Adobe Document Cloud] を使用したPDF ビューアが埋め込まれ、サポートされているドキュメントをプレビューできます。 この機能を使用すると、複雑な処理を行わずに、PDF ファイルやその他の複数ページファイルをプレビューできます。これにより、[!DNL Experience Manager] 6.5 との機能の等価性が向上します。

### [!DNL Assets] で修正されたバグ  {#bugs-fixed-assets}

* サブフォルダーに所有者を追加すると、[!DNL Assets] は親フォルダーの所有者と同じユーザーも追加します。（CQ-4323737）
* コレクションにアセットを追加する際にコレクション検索でフィルターを適用すると、リスト表示でコレクションを表示できません。（CQ-4323181）
* ファイルとフォルダーを検索する場合、フィルターを適用して「[!UICONTROL ファイルとフォルダー]」を選択すると、ファイルのみが表示され、フォルダーは表示されません。（CQ-4319543）

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能[!DNL Sites] {#ga-features-sites}

* Sites 管理 UI で、プレビュー層への公開がページステータスとして表示されるようになりました。
* 「プレビュー層に公開」で、アクションの最後にプレビュー URL が表示され、後で参照できるようにページプロパティに URL が保持されるようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms}

* AEM インボックスのカスタム列をフィルタリングする機能を追加しました。
* アダプティブフォームエディターのテーマエディターとスタイルレイヤーを使用して Captcha コンポーネントのスタイルを設定する機能を追加しました。
* ソース PDF フォーム内の論理セクションを自動的に検出し、対応するアダプティブフォームパネルに変換する際の速度と精度が向上しました。
* PDF または XDP ファイルをフォルダー間で移動する移動アクションが追加されました。

### [!DNL Forms] のベータ版機能  {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：通信 API を使用すると、XDP テンプレートと XML データを組み合わせて様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFA フォーム PDF および Adobe Acrobat フォーム（AcroForms）から印刷用 PDF を生成する。

* **Variable Data Externalizer**：AEM ワークフロー変数のデータを、組織で管理される外部ストレージシステムに保存できます。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てにメールを送信します。

### [!DNL Forms] で修正されたバグ  {#forms-bugs-fixed}

* フォームデータモデル（FDM）を使用してデータをバックエンドサービスに送信する前にフィールドの検証が完了すると、検証は成功しますが、フォームデータモデルサービスで事後検証が呼び出されません。
* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS では、これは既知の問題です。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

この節では、 AEM Screens as a Cloud Service のリリースノートの概要を説明します。

### リリース日 {#release-date-june-screens}

AEM Screens as a Cloud Service のリリース日は 2021 年 6 月 24 日です。

### 新機能 {#what-is-new-screens-june}

>[!NOTE]
>AEM Screens as a Cloud Service を正常にインストール、設定、実行するために必要な基本的な知識と、詳細な概念に関する技術ドキュメントへのリンクについては、『[AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=ja) ガイド』を参照してください。

* デバイスの一括登録管理によって、大量のプレーヤーデバイスのプロビジョニングをより速く、より効率的に行うことができます。

* デバイス、ディスプレイ、チャネルの各在庫ビューの検索およびフィルターオプションを改善しました。

* デバイスの正常性スナップショットでは、重要なステータスを一目で確認できるので時間を節約できます。

* オブジェクトの詳細ページには、プロジェクト内の各オブジェクトに関する最も関連性の高い情報の概要が表示されます。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* コンテンツフラグメントの新しい CIF 製品およびカテゴリ参照データタイプ（製品／カテゴリ選択ツール UI のサポートを含む）製品／カテゴリ選択ツール UI のサポート)
* 新しいコマースコンテンツフラグメントコアコンポーネント
* AEM バックエンドでフルテキストコマース検索をサポート
* Commerce コアコンポーネントは、Adobe Commerce AI Recs のデータ収集をサポートします
* カテゴリページの SEO に対応する URL の改善
* サイト／設定ごとのカスタム HTTP ヘッダーのサポート

## コンテンツトランスファーツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツトランスファーツール v1.5.4 のリリース日は 2021 年 6 月 28 日です。

### 新機能 {#what-is-new-ctt-latest}

* CTT で使用するためのオプションの[コピー前](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=ja)手順のサポートが追加されました。コピー前手順を使用すると、ソース AEM インスタンスが Amazon S3 または Azure Blob Storage データストアを使用するように設定されている場合に、コンテンツ転送アクティビティの抽出段階と取り込み段階を大幅に高速化できます。

* CTT に追加されたガードレールは、取り込みの停止を防ぎ、取り込み段階で重要なポイントに到達したデータが破損する可能性を防ぎます。

* トラブルシューティングに役立つように抽出ログの記述を増やしました。

* UI に、より説明的な取り込みステータスメッセージを追加しました。

### バグ修正 {#bug-fixes-ctt-latest}

* オーサーインスタンスで取り込みを停止する際、UI は、以前に完了したパブリッシュインスタンスの取り込みを `FINISHED` から `STOPPED` に上書きしていました。この問題が修正されました。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.16 のリリース日は 2021 年 6 月 30 日です。

### 新機能 {#what-is-new-bpa-latest}

* `/content/dam` の下のフォルダーに見つからない子ノードを検出し、報告する機能。

* 使用するベストプラクティスアナライザーのバージョンを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa-latest}

* サポートされていないリポジトリー構造（URS）に関するログエラーを修正しました。
