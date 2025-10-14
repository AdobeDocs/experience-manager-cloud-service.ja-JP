---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 リリースのリリースノート。'
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 84%

---

# [!DNL Adobe Experience Manager] as a Cloud Service の 2022.3.0 リリースノート {#release-notes}

以下の節では、[!DNL Experience Manager]as a Cloud Serviceの 2022.3.0 バージョンの機能リリースノートの概要を説明します。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の最新リリース（2022.3.0）のリリース日は 2022年03月31日（PT）です。次回のリリース（2022.4.0）は 2022年5月5日（PT）に予定されています。

## リリースビデオ {#release-video}

2022.3.0 リリースで追加された機能の概要については、[2022年3月リリースの概要](https://video.tv.adobe.com/v/341465)ビデオをご覧ください。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] プレリリースチャネルで利用できる新機能 {#prerelease-features-sites}

* コンテンツモデルのデータ型が、コンテンツモデルエディターで簡単なチェックボックスを使用して翻訳可能として定義できるようになりました。また、AEMの翻訳ルールと設定は自動的に更新されます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] は柔軟性が向上し、ユーザーインターフェイスで [1 つのエイリアスアカウントを設定](/help/assets/dynamic-media/dm-alias-account.md)できるようになったので、標準搭載の Dynamic Media URL とビューア埋め込みコードを確実に更新できます。これは、SEO に良い影響を及ぼし、リブランディングなどのビジネスコンテキストに応じて行われた更新を反映します。

* [!DNL Experience Manager Assets] のユーザーインターフェイスを使用して以下を行えるようになりました。

   * リポジトリー内の[重複アセットの検出](/help/assets/detect-duplicate-assets.md)の設定。

   * [画像へのデジタル透かしの追加](/help/assets/watermark-assets.md)の設定。

* 管理者は、大量のダウンロードに備えてメールサービスを設定できるようになりました。これにより、ユーザーは [!DNL Experience Manager Assets] インターフェイスから[大量ダウンロード時のメール通知を有効にする](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads)ことができます。ダウンロード処理の完了時に、アーカイブされた zip フォルダーのダウンロードリンクを記載したメール通知がユーザーに届きます。

* [公開を管理](/help/assets/manage-publication.md)機能が強化され、ユーザーインターフェイスが改善されました。ユーザーは、選択した宛先にコンテンツを公開または選択した宛先からコンテンツを非公開にしたり、DAM リポジトリー全体から公開リストに[コンテンツを追加](/help/assets/manage-publication.md#add-content)したり、[フォルダー設定を含めて](/help/assets/manage-publication.md#include-folder-settings)選択したフォルダーのコンテンツを公開しフィルターを適用したり、後の日時に[公開をスケジュール](/help/assets/manage-publication.md#publish-assets-later)したりできます。

### [!DNL Assets] プレリリースチャネルで利用できる新機能 {#prerelease-features-assets}

* タグピッカーウィンドウで、タグ名、作成日、変更日を基準に、[タグの並べ替え](/help/assets/organize-assets.md#use-tags-to-organize-assets)を昇順または降順に実行できるようになりました。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**：[ドキュメント生成 API](/help/forms/aem-forms-cloud-service-communications.md) は、PDF ドキュメントの結合、並べ替えおよび検証に役立ちます。このサービスを使用すると、同期モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * PDF ドキュメントのアセンブリ.
   * PDF ドキュメントのディスアセンブリ.
   * PDF/A 準拠ドキュメントへの変換と PDF/A 準拠ドキュメントの検証.

* **15 ページを超える PDF フォームのアダプティブフォームへの自動変換**：自動フォーム変換サービスを使用して、最大 40 ページの PDF フォームをアダプティブフォームに変換できるようになりました。変換サービスで、15 ページを超えるフォームの一部をアダプティブフォームフラグメントに変換するオプションが追加されました。これにより、変換後のフォームのレンダリング速度が向上し、アダプティブフォームエディターで大きなフォームを簡単に読み込むことができるようになります。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **レコードのドキュメントの生成にカスタム XCI を使用**：レコードのドキュメントの様々なプロパティを設定するために、カスタム XCI ファイルを使用できるようになりました。カスタムの変更でマスター XCI を上書きします。

* **アダプティブフォーム内で非表示の CAPTCHA を使用**：非表示の CAPTCHA を使用して、疑わしいアクティビティの場合にのみ CAPTCHA チャレンジを表示させることができます。疑わしいアクティビティが検出されない場合、CAPTCHA チャレンジは表示されません。

## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* マルチストアシナリオでの SEO の向上：PDP／PLP の URL 形式を、CIF Cloud Config プロパティを介してストアレベルで設定できるようになりました。
* 製品ピッカーは、UI の新しいフィルターオプションを介して、ステージングされた製品をサポートします。  これにより、コンテンツ担当者は、今後の製品の発売に備えて製品コンテンツ管理を準備できます
* 設定プロキシ URL の代わりに CIF Cloud Config 名を使用して、CIF 設定の管理とエラー処理を簡略化しました。
* 製品リストおよびカルーセルコンポーネントの手動カテゴリ選択。これにより、コンテンツ担当者は、カタログエクスペリエンス以外で、コンテンツページ上でこれらのコンポーネントを使用できます

### CIF プレリリースチャネルで使用できる新機能 {#prerelease-features-cif}

* AEM CIF Search コアコンポーネントは、Commerce LiveSearch をサポートします。

## [!DNL Experience Manager] as a [!DNL Cloud Service] の基盤 {#foundation}

### 新機能 {#what-is-new-foundation}

* クラウド環境のカスタム機能のトラブルシューティングをより効率的かつ効果的に行うために、新しい開発者ツール、[&#x200B; リポジトリーブラウザー &#x200B;](/help/implementing/developing/tools/repository-browser.md) がリリースされました。 軽量な読み取り専用のHTMLブラウザーで、Developer Consoleから起動できます。 パブリッシュ、オーサー、プレビューの各層および実稼動、ステージ、開発を含むすべての環境で、コンテンツリポジトリーを表示できます。コンテンツ構造を参照し、プロパティを表示し、バイナリをプレビューおよびダウンロードします。

  ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* サーバー間 API 呼び出しの認証に使用される資格情報（例えば、GraphQL API リクエストの場合）は、Developer Consoleからセルフサービス方式で有効期限が切れる前に更新できるようになりました。 詳しくは、[ドキュメント](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)を参照してください。

* 以前は有効になっていなかったバージョンパージと監査ログパージのメンテナンスタスクが、新しい環境で有効になりました。 関連する値を、[メンテナンスタスク](/help/operations/maintenance.md)記事で参照してください。

* AEM as a Cloud Service SDK Dispatcher ツールで、M1 チップを搭載した Mac コンピューターがサポートされるようになりました。

## Cloud Manager {#cloud-manager}

Cloud Manager の月次リリースの完全なリストは、[こちら](/help/implementing/cloud-manager/release-notes/current.md)で確認できます。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.9.0 のリリース日は 2022 年 2 月 28 日です。

### 新機能 {#what-is-new-ctt}

* サイズ確認ガードレール - コンテンツ転送ツールのサイズ確認機能は、コンテンツ転送の失敗を減らすうえで役に立ちます。サイズ確認機能を使用すると、1） `crx-quickstart` サブディレクトリに十分な空きディスク容量があるかどうかを抽出前に判断でき、2）移行セットのサイズを推定し、それが対応可能かどうかを確認できます。 これらのチェックのどちらか一方または両方に違反した場合、CTT UI に警告が表示されます。 このガードレールを使用すると、コンテンツ転送の失敗を回避し、アドビのカスタマーケアと一緒に移行オプションについて事前に検討することができます。詳しくは、[移行セットのサイズとディスク空き容量の決定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=ja#migration-set-size)を参照してください。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.26 のリリース日は 2022 年 3 月 16 日です。

### 新機能 {#what-is-new-bpa}

* 未処理のアセットを検出できるようになりました。未処理のアセットが検出された場合は、コンテンツの取り込み中に問題が発生するのを避けるために、これらのアセットを処理済みに設定するか、コンテンツ転送時に移行セットから削除する必要があります。
* コンテンツに 1,000 個を超えるバニティー URL があるかどうかを検出できるようになりました。多数のバニティー URL を使用すると、Dispatcher およびパブリッシュサーバーに負荷がかかるので、ベストプラクティスではありません。
* Oak インデックスの定義に関連する問題を特定し、AEM as a Cloud Service との非互換性を検出できるようになりました。
* Externalizer 設定の使用を検出してレポートできるようになりました。AEM as a Cloud Service では Externalizer 設定は Cloud Manager で設定されるので、互換性を保つには、既存の Externalizer 設定をリファクタリングする必要があります。

### バグの修正 {#bug-fixes-bpa}

* 一部のシナリオでは、FormsSelectiveFeaturesAnalysis がアサーションエラーをスローするので BPA を実行できませんでした。この問題が修正されました。
* BPA が、WRK パターンに関連する分析結果を「致命的」ではなく「重大」として報告していました。この問題が修正されました。
* BPA が、ui.apps の OAK インデックス定義に関連する分析結果を誤って「致命的」として報告していました。この問題が修正されました。
