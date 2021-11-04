---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 リリースのリリースノート。'
source-git-commit: bef02a7e72d54b7c9eb5726bb046460c5902fb84
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 46%

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

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2021.9.0) は 2021 年 10 月 7 日です。
次のリリース (2021.10.0) は 2021 年 11 月 4 日です。

## リリースビデオ {#release-video}

以下をご覧ください： [2021 年 9 月リリース概要](https://video.tv.adobe.com/v/337381) 追加された機能の概要を示すビデオ。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### の新機能 [!DNL Sites] プレリリースチャネル {#sites-prerelease-features}

* コンテンツフラグメントモデルは、公開後、自動的に読み取り専用状態に設定されるようになりました。これにより、編集後のモデルの再公開後に、意図せずライブ API クエリが壊れるのを防ぎます。 公開済みのモデルを編集しようとすると、警告が表示されます。 編集は、警告を受け入れる際に可能です。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* 検索結果に表示されるアセットを列表示およびカード表示で並べ替えることができるようになりました。 並べ替えは、「名前」、「作成日」、「変更日」、「なし」の各列でおこなわれます。

   ![検索結果の並べ替え [!DNL Assets] 列表示とカード表示](/help/assets/assets/sort-searched-assets.png)
   *図：検索結果の並べ替え [!DNL Assets] （列表示およびカード表示）*

* アセットマイクロサービスを使用してプログラムによって処理を呼び出すために、新しい API が導入されました。 開発者は、フォルダー内の 1 つ以上の特定のアセットに、既存のフォルダーレベルの処理プロファイルを適用できるようになりました。 処理プロファイルは、カスタムメタデータプロパティの更新に基づいて適用されます。 詳しくは、 `AssetProcessor` 内 [[!DNL Experience Manager] API リファレンス](https://www.adobe.io/experience-manager/reference-materials/). 以前と同様に、 [ユーザーインターフェイスからのアセットマイクロサービスの使用](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能  {#what-is-new-forms-sep-2021}

* **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。[契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)ようになりました。デフォルトの役割は署名者です。

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーのインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

* **AEM Forms と Microsoft Dynamics および Salesforce との簡単な接続**：Microsoft Dynamics と Salesforce のデータソース設定およびデータモデルが標準で提供されるので、[開発者が Microsoft Dynamics と Salesforce をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en)ようになりました。

* **DocuSign を使用したアダプティブフォームへの電子サイン**：DocuSign を使用してアダプティブフォームに電子サインすることができます。このサービスでは、アダプティブフォームで DocuSign を使用するためのカスタム送信アクションを提供します。ソフトウェア配布ポータルで入手可能なパッケージをインストールして、送信アクションをインポートすることができます。

### [!DNL Forms] のベータ版機能 {#sep-what-is-new-forms-prerelease}

* **統合ストレージコネクタ：**&#x200B;統合ストレージコネクタを使用すると、顧客側で管理されるリポジトリ内の処理中のデータを外部化することができます。例えば、次のことができます。
   * Forms ポータルの保存および再開機能を有効にし、顧客側で管理されるデータリポジトリにアダプティブフォームのドラフトを格納する
   * 個人の機密情報（SPD）を含んだ処理中の AEM ワークフローデータ（AEM ワークフロー変数データ）を、顧客側で管理されるリポジトリに格納する

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* サイトエディターの新しい「関連するコマースコンテンツ」タブで、現在のコンテキストに関連するAEM製品コンテンツにすばやくアクセスできるので、作成者の効率が向上しました。

   ![関連するコマースコンテンツ](/help/assets/CIF/associated-commerce-content.png)

* 製品ピッカー UI が改善され、ユーザーエクスペリエンスが向上し、効率が向上し、複雑な製品カタログのサポートが向上しました。

   ![新しい製品ピッカー](/help/assets/CIF/product-picker.png)

* ナビゲーションコンポーネントの「include_in_menu」プロパティに従う

### バグ修正 {#bug-fixes-cif}

* メニューキャッシュのフラッシュが期待どおりに動作しません

* AEM CS のデプロイメント手順中および clientside コンポーネントを使用していない場合の JS エラー

* sling:configs ノードを持つフォルダー内に CIF クラウド設定を作成できません

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新機能 {#what-is-new-screens}

* Screens as a Cloud Serviceで、基本的な再生監視がサポートされるようになりました。 プレーヤーでは、各 ping（デフォルトは 30 秒）で様々な再生指標がレポートされるようになります。指標に基づいて、様々なエッジケース（動きのないエクスペリエンス、空白の画面、スケジュールの問題など）を検出できます。この機能を使用すると、プレーヤーがコンテンツを適切に再生しているかどうかをチームがリモートで監視できます。また、空白の画面やフィールド内のエクスペリエンスの不具合に対する反応性が向上し、不具合のあるエクスペリエンスがエンドユーザーに表示されるリスクが低くなります。
詳しくは、[基本的な再生モニタリング](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring)を参照してください。

* でのビデオのサムネールのサポートが、Screens as a Cloud Serviceでサポートされるようになりました。 コンテンツ作成者は、ビデオのサムネールを定義して、その画像をプレースホルダーとして使用できるようにし、実際のビデオを該当チームが仕上げている間に、コンテンツの再生とターゲティングを適切にテストすることができます。その画像は、ビデオの再生に失敗した場合でも使用できます。
詳しくは、[ビデオのサムネールサポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html)を参照してください。

### バグ修正 {#bug-fixes-screens}

* 埋め込みページからコンテンツを表示できず、この問題が修正されました。

* ログインに成功した後、デフォルトのページ（チャネル）に移動すると、最終的に内部サーバーエラーページが表示されます。

* プレイリストを削除する際に、関連するタグエントリが削除されませんでした。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### の新機能[!DNL Experience Manager as a Cloud Service] {#foundation-features}

**高度なネットワーク**

>[!INFO]
>
>高度なネットワーク機能は 2021.9.0 リリースの一部で、10 月中旬にお客様が有効になる予定です。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] では、次のような高度なネットワーク機能をいくつか提供しています。

* 非標準ポートからトラフィックを出力する柔軟なポート出力。 Adobe・サポートに連絡しなくても可能になりました。
* 固有の IP からas a Cloud ServiceのAEMからトラフィックを出力するための、専用の出力 IP アドレスで、すべてのポートをサポートするようになりました。
* インフラストラクチャとAEM as a Cloud Service間のトラフィックを保護する VPN

詳しくは、 [ドキュメント](/help/security/configuring-advanced-networking.md) Cloud Manager API を使用してプロビジョニングされたアドバンスネットワークをセルフサービスで提供する方法など、詳細について説明します。

**インデックスの最適化**

検索クエリとインデックス作成のパフォーマンスを向上させるために、フルテキストインデックス lucene-2 は、 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] このリリースから。 AEMのお客様に合わせてAEM環境でこのフルテキストインデックスを削除するために、Adobeエンジニアリングは、Lucene のフルテキストインデックスを柔軟かつ持続可能に削除するために、お客様と個別かつ積極的に連携します。 次を参照してください： [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [ドキュメント](/help/operations/indexing.md#index-optimizations) 詳細については、お問い合わせください。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.9.0 および 2021.8.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-sept}

AEM as a Cloud Service 2021.9.0 の Cloud Manager のリリース日は 2021 年 9 月 09 日です。
次回のリリースは 2021 年 10 月 7 日（PT）に予定されています。

### 新機能 {#what-is-new-cm-sept}

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 30 に更新されました。

* Cloud Manager ランディングページのプログラムカードと関連するエクスペリエンスが新しくなりました。

* コード品質ステップログに、OakPal スキャンプロセスの詳細なログ情報が含まれるようになりました。

* アクティビティページのメニューオプションに、 **ログをダウンロード** 完了したコードジェネレーターの実行。 これを選択すると、ビルド手順のログがダウンロードされます。

* 「プログラム」カードを直接クリックすると、Cloud Manager の概要ページに移動するようになりました。

### バグ修正 {#bug-fixes-sept}

* 設定可能な IP許可リストの最大数に達したプログラムに新しい IP許可リストを追加しようとすると、よりわかりやすくなるメッセージが表示されるようになりました。

* リポジトリ画面で　URL　コピーメニューオプションを選択すると、間違った　URL　がコピーされていました。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-october-cam}

Cloud Acceleration Manager のリリース日は 2021 年 10 月 4 日です。

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager では、BPA レポートを印刷可能なプレビューで表示できるようになり、印刷や印刷を簡単にPDFでき、共有が容易になりました。 手順 6 および 7( [ベストプラクティス分析カードの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.6.0 のリリース日は 2021 年 10 月 4 日です。

### 新機能 {#what-is-new-ctt}

* ユーザーマッピングが改善され、以下の機能を含むシンプルなユーザーエクスペリエンスが提供されました。 詳しくは、 [ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool).
   * ユーザーマッピングを実行する前に、User Management API への接続をテストする
   * エラーを適切にスキップし、「ユーザーマッピング」アクティビティに進みます
   * アクセストークンの有効期限が 24 時間後に切れた場合、ユーザーマッピングが失敗しなくなりました。 ユーザーマッピングは、最後に停止した場所から再実行できます。

* CTT の堅牢性を高めるために、コンテンツは一度にオーサーインスタンスまたはパブリッシュインスタンスに取り込むことができます。

* バージョンが含まれる場合、パス `/var/audit` 監査イベントを移行するために、が自動的に含まれます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

ベストプラクティスアナライザー v2.1.18 のリリース日は 2021 年 9 月 2 日です。

### 新機能 {#what-is-new}

* ノード数の合計を検出し、レポートする機能。

* ノードストアのタイプとサイズを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPA は、コマース統合フレームワークの存在を誤って検出しました。
