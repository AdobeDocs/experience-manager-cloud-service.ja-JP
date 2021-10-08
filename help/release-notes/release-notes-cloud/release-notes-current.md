---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 5f80ad85ddf9ffdda7cd975d00699eb5085d2365
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 40%

---


# [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート  {#release-notes}

以下では、[!DNL Experience Manager] as a Cloud Service の現在（最新）のバージョンのリリースノート全般の概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョンのリリースノートに移動できます。例えば、2020、2021 の場合は、

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] のリリース日 (2021.9.0) は 2021 年 10 月 6 日です。
[!DNL Cloud Service]次のリリース (2021.10.0) は 2021 年 10 月 28 日です。

## リリースビデオ {#release-video}

追加された機能の概要については、[2021 年 9 月リリースの概要 ](https://video.tv.adobe.com/v/337381) ビデオをご覧ください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースチャネルの新機能 {#sites-prerelease-features}

* コンテンツフラグメントモデルは、公開後、自動的に読み取り専用の状態に設定され、編集後のモデルの再公開後に意図せずライブ API クエリが壊れるのを防ぎます。 公開済みのモデルを編集しようとすると、警告が表示されます。 警告を受け付けると、編集が可能になります。

## [!DNL Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### [!DNL Assets] の新機能 {#assets-features}

* 列表示およびカード表示で、検索結果に表示されたアセットを並べ替えることができるようになりました。 並べ替えは、「名前」、「作成済み」、「変更済み」、「なし」の各列で行います。

   ![列表示およびカード表示での [!DNL Assets] 検索結果の並べ替え](/help/assets/assets/sort-searched-assets.png)
   *図：列表示およびカード表示で [!DNL Assets] 検索結果を並べ替えます。*

<!-- TBD: 'Unpublishing' this feature as suggested by engineering.

* To programmatically invoke processing using asset microservices, a new API is introduced. Developers can now apply an existing folder-level processing profile on one or more specific assets in a folder. The processing profile gets applied based on custom metadata properties updates. See `AssetProcessor` in the [[!DNL Experience Manager] API reference](https://www.adobe.io/experience-manager/reference-materials/). As before, it is possible to [use asset microservices from the user interface](/help/assets/asset-microservices-configure-and-use.md).

-->
<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms-sep-2021}

* **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。[契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)ようになりました。デフォルトの役割は署名者です。

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定をおこない、エンドユーザーエクスペリエンスを向上させることができます。

* **AEM Forms と Microsoft Dynamics および Salesforce との簡単な接続**：Microsoft Dynamics と Salesforce のデータソース設定およびデータモデルが標準で提供されるので、[開発者が Microsoft Dynamics と Salesforce をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en)ようになりました。

* **DocuSign を使用したアダプティブフォームの電子署名：** DocuSign を使用してアダプティブフォームの電子署名を行うことができます。このサービスは、アダプティブフォームで DocuSign を使用するためのカスタム送信アクションを提供します。

### [!DNL Forms] のベータ機能 {#sep-what-is-new-forms-prerelease}

* **統合ストレージコネクタ：**&#x200B;統合ストレージコネクタを使用すると、顧客側で管理されるリポジトリー内の処理中のデータを外部化することができます。例えば、次のことができます。 顧客が管理するリポジトリに機密の個人データ (SPD) を含むプロセス内のAEM Workflows データ (AEM Workflow Variables データ ) を格納します。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、ドキュメントを同期モードで生成できます。この API により、以下の機能を備えたアプリケーションを作成できます。
   * テンプレートファイルに XML データを入力することでドキュメントを生成する
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式の出力フォームを生成する
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成する

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* サイトエディターの新しい「関連するコマースコンテンツ」タブでは、現在のコンテキストの関連するAEM製品コンテンツにすばやくアクセスできるので、作成者の効率が向上します。

   ![関連するコマースコンテンツ](/help/assets/CIF/associated-commerce-content.png)

* 製品ピッカーの UI が改善され、ユーザーエクスペリエンスが向上し、効率が向上し、複雑な製品カタログのサポートが向上

   ![新しい製品ピッカー](/help/assets/CIF/product-picker.png)

* ナビゲーションコンポーネントで「include_in_menu」プロパティを適用する

### バグ修正 {#bug-fixes-cif}

* メニューキャッシュのフラッシュが期待どおりに機能しない

* AEM CS のデプロイメント手順中およびクライアント側コンポーネントを使用していない場合の JS エラー

* sling:configs ノードを持つフォルダー内に CIF クラウド設定を作成できない

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 新機能 {#what-is-new-screens}

* Screensas a Cloud Serviceで、基本的な再生監視がサポートされるようになりました。 プレーヤーでは、各 ping（デフォルトは 30 秒）で様々な再生指標がレポートされるようになります。指標に基づいて、様々なエッジケース（動きのないエクスペリエンス、空白の画面、スケジュールの問題など）を検出できます。この機能を使用すると、プレーヤーがコンテンツを適切に再生しているかどうかをチームがリモートで監視できます。また、空白の画面やフィールド内のエクスペリエンスの不具合に対する反応性が向上し、不具合のあるエクスペリエンスがエンドユーザーに表示されるリスクが低くなります。
詳しくは、[ 基本的な再生監視 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) を参照してください。

* でのビデオのサムネールのサポートが、Screens as a Cloud Serviceでサポートされるようになりました。 コンテンツ作成者は、ビデオのサムネールを定義して、その画像をプレースホルダーとして使用できるようにし、実際のビデオを該当チームが仕上げている間に、コンテンツの再生とターゲティングを適切にテストすることができます。その画像は、ビデオの再生に失敗した場合でも使用できます。
詳しくは、[ ビデオのサムネールのサポート ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) を参照してください。

### バグ修正 {#bug-fixes-screens}

* 埋め込みページのコンテンツをプレーヤーに表示できず、この問題が修正されました。

* ログインに成功した後、デフォルトのページ（チャネル）に移動すると、内部サーバーエラーページが表示されます。

* プレイリストを削除する際に、関連するタグエントリが削除されませんでした。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### [!DNL Experience Manager as a Cloud Service] の新機能 {#foundation-features}

**高度なネットワーク**

>[!INFO]
>
>高度なネットワーク機能は 2021.9.0 リリースの一部で、10 月中旬にお客様向けに有効になります。

[!DNL Adobe Experience Manager] as  [!DNL Cloud Service] as now では、次のようないくつかのタイプの高度なネットワーク機能を提供しています。

* 非標準ポートからトラフィックを出力する柔軟なポート出力。 現在は、Adobe・サポートに連絡する必要はありません。
* 固有の IP からAEMからトラフィックを出力するための、専用の出力 IP アドレスで、すべてのポートをサポートするようになりました。
* VPN ：インフラストラクチャとAEM as a Cloud Service間のトラフィックを保護します。

Cloud Manager API を使用してプロビジョニングされた高度なネットワークのセルフサービス方法など、詳細については、[ ドキュメント ](/help/security/configuring-advanced-networking.md) をお読みください。

**インデックスの最適化**

検索クエリとインデックス作成のパフォーマンスを向上させるために、フルテキストインデックス lucene-2 はこのリリースから [!DNL Cloud Service] として [!DNL Adobe Experience Manager] に追加設定なしで含まれなくなりました。 AEMのお客様に合わせてAEM環境でこのフルテキストインデックスを削除するため、Adobeエンジニアリングは、お客様との間で個別かつ積極的に連携し、Lucene のフルテキストインデックスを柔軟かつ持続的に削除します。 詳細については、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [ ドキュメント ](/help/operations/indexing.md#index-optimizations) をご覧ください。ご質問がある場合は、直接サポートにお問い合わせください。

## Cloud Manager  {#cloud-manager}

この節では、AEM as a Cloud Service 2021.9.0 および 2021.8.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-sept}

AEM as a Cloud Service 2021.9.0 の Cloud Manager のリリース日は 2021 年 9 月 09 日です。
次回のリリースは 2021 年 10 月 7 日（PT）に予定されています。

### 新機能 {#what-is-new-cm-sept}

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 30 に更新されました。

* Cloud Manager ランディングページのプログラムカードと関連するエクスペリエンスが新しくなりました。

* コード品質ステップログに、OakPal スキャンプロセスの詳細なログ情報が含まれるようになりました。

* アクティビティページのメニューオプションに、完了したコードジェネレーターの実行に対して **ログをダウンロード** するオプションが追加されました。 これを選択すると、ビルド手順のログがダウンロードされます。

* 「プログラム」カードを直接クリックすると、Cloud Manager の概要ページに移動するようになりました。

### バグ修正 {#bug-fixes-sept}

* 設定可能な IP許可リストの最大数に達したプログラムに新しい IP許可リストを追加しようとすると、わかりやすいメッセージが表示されるようになりました。

* リポジトリ画面で　URL　コピーメニューオプションを選択すると、間違った　URL　がコピーされていました。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-october-cam}

Cloud Acceleration Manager のリリース日は 2021 年 10 月 4 日です。

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager では、BPA レポートを印刷可能なプレビューで表示できるようになり、印刷や印刷をPDFに簡単に行え、共有が容易になりました。 [ ベストプラクティス分析カードの使用 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis) の手順 6 と 7 を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.6.0 のリリース日は 2021 年 10 月 4 日です。

### 新機能 {#what-is-new-ctt}

* ユーザーマッピングが改善され、以下の機能を含むシンプルなユーザーエクスペリエンスが提供されました。 詳しくは、[ ユーザーマッピングツールの使用 ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool) を参照してください。
   * ユーザーマッピングを実行する前に、User Management API への接続をテストする
   * エラーを適切にスキップし、ユーザーマッピングアクティビティを続行します
   * アクセストークンの有効期限が（24 時間後に）切れても、ユーザーマッピングが失敗しなくなりました。 ユーザーマッピングは、最後に停止した場所から再実行できます。

* CTT の堅牢性を高めるために、コンテンツを一度にオーサーインスタンスまたはパブリッシュインスタンスに取り込むことができます。

* バージョンを含めると、パス `/var/audit` が自動的に含まれ、監査イベントを移行します。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18 のリリース日は 2021 年 9 月 2 日です。

### 新機能 {#what-is-new}

* ノード数の合計を検出し、レポートする機能。

* ノードストアのタイプとサイズを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPA が誤ってコマース統合フレームワークの存在を検出しました。
