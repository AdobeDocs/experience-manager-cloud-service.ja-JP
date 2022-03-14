---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 リリースのリリースノート。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 90%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在のリリース（2021.9.0）のリリース日は 2021年10月06日（PT）です。
次回のリリース（2021.10.0）は 2021年11月4日（PT）です。

## リリースビデオ {#release-video}

追加された機能の概要については、](https://video.tv.adobe.com/v/337381)2021年9月リリースの概要[ビデオをご覧ください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースチャネルの新機能 {#sites-prerelease-features}

* コンテンツフラグメントモデルは、公開後、自動的に読み取り専用状態に設定されるようになりました。これにより、編集したモデルの再公開後にライブ API クエリが意図せず機能しなくなることを回避できます。公開済みのモデルを編集しようとすると、警告が表示されます。警告を了承すれば、編集は可能です。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* 検索結果に表示されるアセットを、ユーザーが列表示およびカード表示で並べ替えることができるようになりました。並べ替えは、「名前」、「作成日」、「変更日」、「なし」の各列に対して機能します。

   ![[!DNL Assets] での検索結果の並べ替え（列表示とカード表示）](/help/assets/assets/sort-searched-assets.png)
   *図：[!DNL Assets] での検索結果の並べ替え（列表示とカード表示）*

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

### [!DNL Forms] の新機能 {#what-is-new-forms-sep-2021}

* **アダプティブフォームでの Adobe Sign の役割の使用**：ビジネスおよびエンタープライズサービスレベルの Adobe Sign では、ワークフロー要件に適切に合致するように、契約書受信者の役割を署名者以外にも拡大できます。[契約書の受信者ごとに、アダプティブフォームでの自分の役割を設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?lang=ja#addsignerstoanadaptiveform)ようになりました。デフォルトの役割は署名者です。

* **アダプティブフォーム用の Analytics**：アダプティブフォーム用の Adobe Analytics でエンドユーザーの行動を捉えて追跡し、エンドユーザーに関するインサイトを収集できるようになりました。十分な情報に基づいて決定を行い、エンドユーザーのエクスペリエンスを向上させることができます。

* **AEM Forms と Microsoft Dynamics および Salesforce との簡単な接続**：Microsoft Dynamics と Salesforce のデータソース設定およびデータモデルが標準で提供されるので、[開発者が Microsoft Dynamics と Salesforce をアダプティブフォームのデータソースとしてより迅速かつ簡単に設定できる](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=ja)ようになりました。

* **DocuSign を使用したアダプティブフォームへの電子サイン**：DocuSign を使用してアダプティブフォームに電子サインすることができます。このサービスでは、アダプティブフォームで DocuSign を使用するためのカスタム送信アクションを提供します。ソフトウェア配布ポータルで入手可能なパッケージをインストールして、送信アクションをインポートすることができます。

### [!DNL Forms] のベータ版機能 {#sep-what-is-new-forms-prerelease}

* **統合ストレージコネクタ：**&#x200B;統合ストレージコネクタを使用すると、顧客側で管理されるリポジトリー内の処理中のデータを外部化することができます。例えば、次のことができます。
   * Forms ポータルの保存および再開機能を有効にし、顧客側で管理されるデータリポジトリにアダプティブフォームのドラフトを格納する
   * 個人の機密情報（SPD）を含んだ処理中の AEM ワークフローデータ（AEM ワークフロー変数データ）を、顧客側で管理されるリポジトリに格納する

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=ja) では、XDP テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。
   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式で出力フォームを生成します。
   * XFA フォーム PDF および Adobe Acrobat フォームから印刷用 PDF ファイルを生成します。

ベータ版プログラムに新規登録するには、[!DNL formscsbeta@adobe.com] 宛てに電子メールを送信します。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* サイトエディターの新しい「関連するコマースコンテンツ」タブでは、現在のコンテキストに関係のある AEM 製品コンテンツにすばやくアクセスできるので、作成者の効率が向上します。

   ![関連するコマースコンテンツ](/help/assets/CIF/associated-commerce-content.png)

* 製品ピッカー UI の改善により、ユーザーエクスペリエンス、効率および複雑な製品カタログのサポートが向上しました。

   ![新しい製品ピッカー](/help/assets/CIF/product-picker.png)

* ナビゲーションコンポーネントの「include_in_menu」プロパティに従います

### バグ修正 {#bug-fixes-cif}

* メニューキャッシュのフラッシュが正常に機能しませんでした

* AEM CS デプロイメントステップ中と、クライアント側コンポーネントを使用していないときに、JS エラーが発生していました

* sling:configs ノードを持つフォルダー内に CIF クラウド設定を作成できませんでした

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新機能 {#what-is-new-screens}

* Screens as a Cloud Service で、基本的な再生モニタリングがサポートされるようになりました。プレーヤーでは、各 ping（デフォルトは 30 秒）で様々な再生指標がレポートされるようになります。指標に基づいて、様々なエッジケース（動きのないエクスペリエンス、空白の画面、スケジュールの問題など）を検出できます。この機能を使用すると、プレーヤーがコンテンツを適切に再生しているかどうかをチームがリモートで監視できます。また、空白の画面やフィールド内のエクスペリエンスの不具合に対する反応性が向上し、不具合のあるエクスペリエンスがエンドユーザーに表示されるリスクが低くなります。
詳しくは、[基本的な再生モニタリング](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=ja#playback-monitoring)を参照してください。

* ビデオのサムネールが Screens as a Cloud Service でサポートされるようになりました。コンテンツ作成者は、ビデオのサムネールを定義して、その画像をプレースホルダーとして使用できるようにし、実際のビデオを該当チームが仕上げている間に、コンテンツの再生とターゲティングを適切にテストすることができます。その画像は、ビデオの再生に失敗した場合でも使用できます。
詳しくは、[ビデオのサムネールサポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html?lang=ja)を参照してください。

### バグ修正 {#bug-fixes-screens}

* プレーヤーで埋め込みページのコンテンツを表示できませんでしたが、この問題が修正されました。

* ログインに成功した後、デフォルトのページ（チャネル）に移動すると、最終的に内部サーバーエラーページが表示されていました。

* プレイリストを削除する際に、関連するタグエントリが削除されませんでした。

## [!DNL Experience Manager as a Cloud Service] 基盤 {#foundation}

### の新機能[!DNL Experience Manager as a Cloud Service] {#foundation-features}

**高度なネットワーク機能**

>[!INFO]
>
>高度なネットワーク機能は 2021.9.0 リリースに含まれており、10 月中旬に使用できるようになる予定です。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] では、数種類の高度なネットワーク機能を提供するようになりました。例えば、次のようなものがあります。

* 非標準ポートからトラフィックを出力するフレキシブルポートエグレス。アドビサポートに問い合わせなくても、利用可能になりました。
* AEM as a Cloud Service で一意の IP アドレスからトラフィックを出力するための専用エグレス IP アドレスが、すべてのポートをサポートするようになりました。
* お使いのインフラストラクチャと AEM as a Cloud Service の間でやり取りされるトラフィックのセキュリティを確保する VPN。

Cloud Manager API を使用して高度なネットワーク機能をセルフサービス方式でプロビジョニングする方法など、詳細については、[このドキュメント](/help/security/configuring-advanced-networking.md)を参照してください。

**インデックスの最適化**

検索クエリとインデックス作成のパフォーマンスを向上させるために、このリリース以降、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] では、フルテキストインデックス lucene-2 は標準では使用されなくなりました。AEM のお客様の要件に従って AEM 環境でこのフルテキストインデックスを削除するために、アドビのエンジニアリングチームは、問題が発生する前にお客様と個別に協力して、Lucene フルテキストインデックスの正常かつ持続可能な削除に対応しています。詳しくは、[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [ドキュメント](/help/operations/indexing.md#index-optimizations)を参照してください。また、ご質問がある場合は、アドビサポートにお問い合わせください。

## Cloud Manager {#cloud-manager}

この節では、AEM as a Cloud Service 2021.9.0 および 2021.8.0 に含まれている Cloud Manager のリリースノートの概要を説明しています。

## リリース日 {#release-date-cm-sept}

AEM as a Cloud Service 2021.9.0 の Cloud Manager のリリース日は 2021年9月09日（PT）です。次回のリリースは 2021 年 10 月 7 日（PT）に予定されています。

### 新機能 {#what-is-new-cm-sept}

* Cloud Manager で使用される AEM プロジェクトアーキタイプのバージョンが 30 に更新されました。

* Cloud Manager ランディングページのプログラムカードと関連するエクスペリエンスが新しくなりました。

* コード品質ステップログに、OakPal スキャンプロセスの詳細なログ情報が含まれるようになりました。

* アクティビティページのメニューオプションに、完了したコードジェネレーター実行に適用できる「**ログをダウンロード**」オプションが含まれるようになりました。これを選択すると、ビルド手順のログがダウンロードされます。

* 「プログラム」カードを直接クリックすると、Cloud Manager の概要ページに移動するようになりました。

### バグ修正 {#bug-fixes-sept}

* 設定可能な IP 許可リストの最大数に達したプログラムに新しい IP 許可リストを追加しようとしたときに表示されるメッセージがわかりやすくなりました。

* リポジトリー画面で　URL　コピーメニューオプションを選択すると、間違った　URL　がコピーされていました。

## Cloud Acceleration Manager {#cam}

### リリース日 {#release-date-october-cam}

Cloud Acceleration Manager のリリース日は 2021年10月4日です。

### 新機能 {#what-is-new-cam}

* Cloud Acceleration Manager では、BPA レポートを印刷可能なプレビューで表示できるようになり、印刷や PDF へのエクスポートが簡単になりました。これにより、共有が容易になりました。[ベストプラクティス分析カードの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=ja#best-practices-analysis)の手順 6 および 7 を参照してください。

## コンテンツ転送ツール {#content-transfer-tool}

### リリース日 {#release-date-ctt-latest}

コンテンツ転送ツール v1.6.0 のリリース日は 2021年10月4日です。

### 新機能 {#what-is-new-ctt}

* ユーザーマッピングが改善され、以下の機能を含むシンプルなユーザーエクスペリエンスが提供されました。 詳しくは、[ユーザーマッピングツールの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=ja#using-user-mapping-tool)を参照してください。
   * ユーザーマッピングを実行する前に、User Management API への接続をテストできます
   * エラーを適切にスキップし、「ユーザーマッピング」アクティビティを続行できます
   * アクセストークンの有効期限が 24 時間後に切れた場合、ユーザーマッピングが失敗しなくなりました。 最後に停止した位置からユーザーマッピングを再実行できます。

* CTT の堅牢性を高めるために、コンテンツは一度にオーサーインスタンスまたはパブリッシュインスタンスに取り込むことができます。

* バージョンが含まれる場合は、監査イベントを移行するために、パス `/var/audit` が自動的に含まれます。

## ベストプラクティスアナライザー {#best-practices-analyzer}

### リリース日 {#release-date-bpa-latest}

ベストプラクティスアナライザー v2.1.18 のリリース日は 2021 年 9 月 2 日です。

### 新機能 {#what-is-new}

* ノード数の合計を検出し、レポートする機能。

* ノードストアのタイプとサイズを検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPA は、コマース統合フレームワークの存在を誤って検出しました。
