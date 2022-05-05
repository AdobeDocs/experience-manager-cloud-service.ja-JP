---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.3.0 リリースのリリースノート。'
source-git-commit: 5d0f6fb726527434c57dc058bcf3a7b9d512b551
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 19%

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

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2022.3.0) は 2022 年 3 月 31 日です。
次回のリリース (2022.4.0) は、2022 年 5 月 6 日に予定されています。

## リリースビデオ {#release-video}

以下をご覧ください： [2022 年 3 月リリースの概要](https://video.tv.adobe.com/v/341465) 2022.3.0 リリースで追加された機能の概要を示すビデオです。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースチャネルで利用できる新機能 {#prerelease-features-sites}

* コンテンツモデルのデータタイプを、コンテンツモデルエディターのシンプルなチェックボックスを使用して翻訳可能として定義できるようになりました。 さらに、AEMの翻訳ルールと設定は自動的に更新されます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] が次の柔軟性を提供 [1 つのエイリアスアカウントを設定](/help/assets/dynamic-media/dm-alias-account.md) を使用すると、標準のDynamic Media URL とビューア埋め込みコードを確実に更新できます。 これは、SEO に良い影響を与え、リブランディングなどのビジネスコンテキストの更新を反映します。

* これで、 [!DNL Experience Manager Assets] 次の操作を行うユーザーインターフェイス：

   * の設定 [重複アセットの検出](/help/assets/manage-digital-assets.md#detect-duplicate-assets) リポジトリ内にある。

   * 設定 [デジタル透かしの追加](/help/assets/watermark-assets.md) を画像に追加します。

* 管理者は、大量のダウンロード用に電子メールサービスを設定できるようになりました。 これにより、ユーザーは次の操作を実行できます。 [大量のダウンロード用に電子メール通知を有効にする](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) から [!DNL Experience Manager Assets] インターフェイス。 ダウンロード処理の完了時に、アーカイブされた zip フォルダーのダウンロードリンクを含む電子メール通知がユーザーに送信されます。

* この [公開を管理](/help/assets/manage-publication.md) の機能が強化され、ユーザーインターフェイスが改善されました。 ユーザーは、選択した宛先に対して、コンテンツを公開または非公開にできます。 [コンテンツを追加](/help/assets/manage-publication.md#add-content) を DAM リポジトリー全体の発行リストに追加する [フォルダ設定を含める](/help/assets/manage-publication.md#include-folder-settings) 選択したフォルダーのコンテンツを公開し、フィルターを適用するには、次の手順に従います。 [公開をスケジュール](/help/assets/manage-publication.md#publish-assets-later) を後の日時に変更する必要があります。

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#prerelease-features-assets}

* 次の操作を実行できます。 [タグを並べ替え](/help/assets/organize-assets.md#use-tags-to-organize-assets) タグ名、作成日または変更日に基づいて昇順または降順でタグピッカーウィンドウを表示します。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [ドキュメント生成 API](/help/forms/aem-forms-cloud-service-communications.md) ヘルプ：PDFドキュメントの組み合わせ、並べ替え、検証に役立ちます。 このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * PDF ドキュメントのアセンブリ.
   * PDF ドキュメントのディスアセンブリ.
   * PDF/A 準拠のドキュメントに変換して検証します。

* **15 ページを超えるPDF formsをアダプティブフォームに自動的に変換する**:automated forms conversionサービスを使用して、最大 40 ページのPDF formsをアダプティブフォームに変換できるようになりました。 変換サービスで、15 ページを超えるフォームの一部をアダプティブフォームフラグメントに変換するオプションが追加されました。 これにより、変換後のフォームのレンダリング速度が向上し、アダプティブフォームエディターで大きなフォームを簡単に読み込むことができるようになります。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **レコードのドキュメントの生成にカスタム XCI を使用**:カスタム XCI ファイルを使用して、レコードのドキュメントの様々なプロパティを設定できるようになりました。 カスタムの変更でマスター XCI を上書きします。

* **アダプティブフォーム内で非表示の CAPTCHA を使用する**:CAPTCHA チャレンジを表示するには、不審なアクティビティが発生した場合にのみ、非表示の CAPTCHA を使用できます。 疑わしいアクティビティが見つからない場合は、CAPTCHA チャレンジは表示されません。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* マルチストアシナリオでの SEO の改善：PDP/PLP の URL 形式を、CIF Cloud Config プロパティを介してストアレベルで設定できるようになりました。
* 製品ピッカーは、UI の新しいフィルターオプションを使用して、ステージングされた製品をサポートします。  これにより、コンテンツ担当者は、今後の製品の発売に備えて製品コンテンツ管理を準備できます
* 設定プロキシ URL の代わりに CIF Cloud Config 名を使用して、CIF 設定の管理とエラー処理を簡略化しました。
* 製品リストおよびカルーセルコンポーネントの手動カテゴリ選択。 これにより、コンテンツ担当者は、カタログエクスペリエンス以外で、コンテンツページ上でこれらのコンポーネントを使用できます

### CIF プレリリースチャネルで使用できる新機能 {#prerelease-features-cif}

* AEM CIF Search コアコンポーネントは、Commerce LiveSearch をサポートします。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* クラウド環境のカスタム機能のトラブルシューティングをより効率的かつ効果的におこなうために、新しい開発者ツールがリリースされました。 [リポジトリブラウザ](/help/implementing/developing/tools/repository-browser.md). 開発者コンソールから起動できる、軽量で読み取り専用のHTMLブラウザーです。 パブリッシャー、オーサー、プレビューの各層および実稼動、ステージ、開発を含むすべての環境で、コンテンツリポジトリを表示できます。 コンテンツ構造を参照し、プロパティを表示し、バイナリをプレビューおよびダウンロードします。

   ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* サーバー間 API 呼び出しの認証に使用される資格情報（例：GraphQL API 要求の場合）は、開発者コンソールからセルフサービス方式で有効期限が切れる前に更新できるようになりました。 詳しくは、 [ドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) 詳しくは、を参照してください。

* 以前に有効にしていなかったバージョンのパージと監査ログのパージのメンテナンスタスクは、新しい環境で有効になります。 関連する値を [メンテナンスタスク](/help/operations/maintenance.md) 記事。

* AEMas a Cloud ServiceSDK Dispatcher ツールで、M1 チップを搭載したMacコンピューターがサポートされるようになりました。

## Cloud Manager {#cloud-manager}

Cloud Manager の毎月のリリースの完全なリストを確認できます [ここ](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.9.0 のリリース日は 2022 年 2 月 28 日です。

### 新機能 {#what-is-new-ctt}

* サイズガードレールを確認 — コンテンツ転送ツールのサイズを確認機能を使用すると、失敗したコンテンツ転送を減らすことができます。  [ サイズの確認 ] 機能を使用すると、1) に十分なディスク容量があるかどうかを `crx-quickstart` 抽出前のサブディレクトリ、2) 移行セットのサイズを推定し、サポートされているかどうかを確認します。 これらのチェックの一方または両方に違反した場合、CTT UI に警告が表示されます。 このガードレールを使用すると、コンテンツ転送の失敗を回避し、Adobeカスタマーケアと移行オプションについて事前に話し合うことができます。 参照： [移行セットのサイズとディスク容量の決定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) を参照してください。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.26 のリリース日は 2022 年 3 月 16 日です。

### 新機能 {#what-is-new-bpa}

* 未処理のアセットを検出する機能。 未処理のアセットが検出された場合は、コンテンツの取り込み中に問題が発生するのを避けるために、これらのアセットを処理済みに設定するか、コンテンツの転送中に移行セットから削除する必要があります。
* コンテンツに 1,000 個を超えるバニティー URL があるかどうかを検出する機能。 バニティー URL の数を多く指定することは、Dispatcher およびパブリッシュサーバーに負荷がかかるので、ベストプラクティスではありません。
* Oak インデックスの定義に関連する問題を特定し、AEM as a Cloud Serviceとの非互換性を検出する機能。
* Externalizer 設定の使用方法を検出し、レポートする機能。 AEMas a Cloud Serviceの Externalizer 設定は Cloud Manager で設定されるので、互換性を維持するには、既存の Externalizer 設定をリファクタリングする必要があります。

### バグの修正 {#bug-fixes-bpa}

* 一部のシナリオでは、FormsSelectiveFeaturesAnalysis がアサーションエラーをスローしたため、BPA が実行に失敗しました。 この問題が修正されました。
* BPA は、WRK パターンに関連する結果を CRITICAL ではなく MAJOR として報告していました。 この問題が修正されました。
* BPA は、ui.apps の OAK インデックス定義に関連する結果を誤って「重大」としてレポートしていました。 この問題が修正されました。
