---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.1.0 リリースのリリースノート。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.1.0 リリースのリリースノート。'
exl-id: 1c40ab67-8fd7-4f29-b8c9-dd98b6d5b490
source-git-commit: a66215277ca83c011f2f4df621d055049c4c93a7
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 97%

---

# 2022.1.0 リリースノート： [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下の節では、の 2022.1.0 バージョンの機能リリースノートの概要を説明します [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>ここから、以前のバージョン（例えば、2020 年、2021 年のバージョンなど）のリリースノートに移動できます。

>[!NOTE]
>
>リリースに直接関連しないドキュメント更新の詳細については、[最近のドキュメントの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=ja)を参照してください。

## リリース日 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] の現在リリース（2022.1.0）のリリース日は、2022年02月3日（PT）です。次回のリリース（2022.3.0）は 2022年03月31日（PT）です。

## リリースビデオ {#release-video}

2022.1.0 リリースで追加された機能の概要については、[2022年1月リリースの概要](https://video.tv.adobe.com/v/340120)ビデオをご覧ください。

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* ページコアコンポーネント v2 を使用するサイトの Sites コンソールの&#x200B;**サイト**&#x200B;パネルで「**[フロントエンドパイプラインを有効化](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)**」ボタンを使用できます。このボタンを使用すると、フロントエンドパイプラインでデプロイされるテーマを既存のクライアントライブラリの上に読み込むようにサイトを設定できます。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - Dynamic Media Classic デスクトップアプリケーションを使用しなくても、AEM Dynamic Media インターフェイスを使用して、一般設定と公開設定を設定できるようになりました。

* [!DNL Dynamic Media] は、MXF ビデオの取り込み、プレビュー、再生、公開をサポートするようになりました。MXF ビデオの注釈とショッパブルビデオは、まだサポートされていません。

* リモート DAM と Sites デプロイメント間の接続を設定すると、リモート DAM 上のアセットが Sites デプロイメントで使用できるようになります。これで、リモート DAM アセットまたはフォルダーに対して、[更新、削除、名前変更、移動の操作](/help/assets/use-assets-across-connected-assets-instances.md)を実行できます。更新は、Sites デプロイメントで自動的に（少し遅れて）利用できます。

### [!DNL Assets] プレリリースチャネルの新機能 {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] は柔軟性が向上し、ユーザーインターフェイスで [1 つのエイリアスアカウントを設定](/help/assets/dynamic-media/dm-alias-account.md)できるようになったので、標準搭載の Dynamic Media URL とビューア埋め込みコードを確実に更新できます。これは、SEO に良い影響を及ぼし、リブランディングなどのビジネスコンテキストに応じて行われた更新を反映します。

* [!DNL Experience Manager Assets] のユーザーインターフェイスを使用して以下を行えるようになりました。

   * リポジトリー内の重複アセットの検出を設定する。

   * 画像へのデジタル透かしの追加を設定する。

* 管理者は、大量のダウンロードに備えてメールサービスを設定できるようになりました。これにより、ユーザーは [!DNL Experience Manager Assets] インターフェイスから[大量ダウンロード時のメール通知を有効にする](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads)ことができます。ダウンロード処理の完了時に、アーカイブされた zip フォルダーのダウンロードリンクを記載したメール通知がユーザーに届きます。


* [公開を管理](/help/assets/manage-publication.md)機能が強化され、ユーザーインターフェイスが改善されました。ユーザーは、選択した宛先にコンテンツを公開または選択した宛先からコンテンツを非公開にしたり、DAM リポジトリー全体から公開リストに[コンテンツを追加](/help/assets/manage-publication.md#add-content)したり、[フォルダー設定を含めて](/help/assets/manage-publication.md#include-folder-settings)選択したフォルダーのコンテンツを公開しフィルターを適用したり、後の日時に[公開をスケジュール](/help/assets/manage-publication.md#publish-assets-later)したりできます。

### バグの修正 {#bug-fixes}

* 元のレンディションがない未処理のアセットは、オンプレミスの AEM から Cloud Services へのアセットの移行中に、Asset Compute に送信されて処理されます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=ja) では、テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および一括モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式のフォームを生成する
   * XFA フォームの PDF ファイルから印刷用 PDF を生成する。
   * ソーステンプレートを用いて複数のデータセットを結合することにより、PDF、PostScript、PCL および ZPL の各種形式のドキュメントを一括生成する

* **Communications API で作成されたレコードのドキュメントおよび PDF ドキュメント用のカスタムフォント**：Communications API を使用して生成された PDF ドキュメントで、ブランド承認済みフォントを使用して、組織の要件に合わせることができるようになりました。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **[Assembler API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**：Assembler API で PDF ドキュメントの結合、並べ替え、拡張および情報取得を行えます。


## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* myAccount コンポーネントの強化機能
* 「製品のレコメンデーション」コンポーネントで追加のページタイプ（ホームページ、買い物かご、注文確認）がサポートされるようになりました
* **ウィッシュリスト**
   * ログインした訪問者は、ウィッシュリストに製品を追加できます
   * ウィッシュリストとその製品の管理は、myAccount を使用して行えます
   * 「ウィッシュリストに追加」ボタンは、ポリシー（製品ティーザー、製品詳細など）を介して、コンポーネントレベルで有効／無効にできます
   * コアコンポーネントおよび AEM Venia ストアフロントで使用できます。

![ウィッシュリスト](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2022.01.0 における Cloud Manager のリリース日は 2022年1月20日（PT）です。次回のリリースは 2022年2月10日（PT）の予定です。

### 新機能 {#what-is-new-cm}

* Cloud Manager は、複数のフルスタックパイプライン実行で [同じ git コミットが使用されていることを検出した場合、コードベースの再ビルドを避けます](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。
* AEM 環境ログにアクセスするには、**Deployment Manager** 製品プロファイルが必要になりました。このプロファイルを持たないユーザーには、ユーザーインターフェイスに無効なボタンが表示されます。
* UI は、Sites がソリューションとして有効化されていないプログラムのフロントエンドパイプライン設定を許可しません。
* Git パスワードの生成時に、有効期限が表示されます。

### バグの修正 {#bug-fixes-cm}

* 一部のフロントエンドパイプラインデプロイメントで発生した null ポインター例外が修正されました。
* 古いバージョンの AEM が実行されている環境で、環境変数を追加、更新、削除できるようになりました。
* まれに、スケジュールされたステップを使用したパイプラインでは、イメージのビルドステップが「エラー」としてマークされなくなりました。
* リポジトリーが 1 つだけのプログラムの場合、パイプライン実行画面にリポジトリー名が表示されるようになりました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.8.6 のリリース日は 2022 年 2 月 03 日です。

### 新機能 {#what-is-new-ctt}

* コンテンツの検証 - コンテンツ転送ツールで抽出されたすべてのコンテンツがターゲットインスタンスに正常に取り込まれたかどうかをユーザーが確実に判断できます。この機能を使用するには、ソース AEM 環境の `System Console` で機能を有効にする必要があります。詳しくは、[コンテンツ転送の検証 - はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=ja#getting-started)を参照してください。

### バグの修正 {#bug-fixes-ctt}

* ユーザーマッピングでは大文字と小文字が区別されるので、一部のユーザーがマッピングされませんでした。この問題が修正されました。ユーザーマッピングでは、大文字と小文字が区別されなくなりました。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.24 のリリース日は 2022 年 2 月 01 日です。

### 新機能 {#what-is-new-bpa}

* スマートタグを使用するアセットと使用しないアセットの数を検出してレポートできるようになりました。
* 使用されているコアコンポーネントのバージョンを検出しレポートできるようになりました。
* BPA が実行されたソース層（オーサーまたはパブリッシュ）の種類を検出してレポートできるようになりました。

### バグの修正 {#bug-fixes-bpa}

* BPA のサイズ決定ロジックがより高速かつ効率的になりました。
* 一部のシナリオで、BPA が実行時に分析済みのカウントを増分しないことがありました。この問題が修正されました。
