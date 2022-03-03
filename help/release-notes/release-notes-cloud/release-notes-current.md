---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service の最新のリリースノート'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 08ed7f06b60ab65a0060c4fa00f902006f3afbdd
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 26%

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

のリリース日 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 現在のリリース (2022.1.0) は 2022 年 2 月 4 日です。
次のリリース (2022.2.0) は 2022 年 3 月 10 日です。

## リリースビデオ {#release-video}

以下をご覧ください： [2022 年 1 月リリースの概要](https://video.tv.adobe.com/v/340120) 2022.1.0 リリースで追加された機能の概要を示すビデオです。

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* この **[フロントエンドパイプラインの有効化](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** ボタンが **サイト** ページコアコンポーネント v2 を使用するサイトの場合は、サイトコンソールのパネル。 このボタンを使用して、フロントエンドパイプラインで既存のクライアントライブラリの上にデプロイされるテーマを読み込むようにサイトを設定します。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### の新機能[!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - Dynamic Media Classicデスクトップアプリケーションを使用しなくても、AEM Dynamic Mediaインターフェイスを使用して、一般設定と公開設定を設定できるようになりました。

* [!DNL Dynamic Media] MXF ビデオの取り込み、プレビュー、再生、公開をサポートするようになりました。 MXF ビデオの注釈とショッパブルビデオは、まだサポートされていません。

* リモート DAM と Sites デプロイメント間の接続を設定すると、リモート DAM 上のアセットが Sites デプロイメントで使用できるようになります。 これで、 [操作の更新、削除、名前変更、移動](/help/assets/use-assets-across-connected-assets-instances.md) リモートの DAM アセットまたはフォルダー上で 更新は、Sites デプロイメントで自動的に利用できます（少し遅れて）。

### の新機能 [!DNL Assets] プレリリースチャネル {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] が次の柔軟性を提供 [1 つのエイリアスアカウントを設定](../../assets/dynamic-media/dm-alias-account.md) を使用すると、標準のDynamic Media URL とビューア埋め込みコードを確実に更新できます。 これは、SEO に良い影響を与え、リブランディングなどのビジネスコンテキストの更新を反映します。

* これで、 [!DNL Experience Manager Assets] 次の操作を行うユーザーインターフェイス：

   * リポジトリ内の重複アセットの検出を設定します。

   * 画像へのデジタル透かしの追加を設定します。

* 管理者は、大量のダウンロード用に電子メールサービスを設定できるようになりました。 これにより、ユーザーは次の操作を実行できます。 [大量のダウンロード用に電子メール通知を有効にする](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) から [!DNL Experience Manager Assets] インターフェイス。 ダウンロード処理の完了時に、アーカイブされた zip フォルダーのダウンロードリンクを含む電子メール通知がユーザーに送信されます。


* この [公開を管理](/help/assets/manage-publication.md) の機能が強化され、ユーザーインターフェイスが改善されました。 ユーザーは、選択した宛先に対して、コンテンツを公開または非公開にできます。 [コンテンツを追加](/help/assets/manage-publication.md#add-content) を DAM リポジトリー全体の発行リストに追加する [フォルダ設定を含める](/help/assets/manage-publication.md#include-folder-settings) 選択したフォルダーのコンテンツを公開し、フィルターを適用するには、次の手順に従います。 [公開をスケジュール](/help/assets/manage-publication.md#publish-assets-later) を後の日時に変更する必要があります。

### バグ修正 {#bug-fixes}

* 元のレンディションがない未処理のアセットは、AEM On-premise から Cloud Services へのアセットの移行中に、Asset computeに送信されて処理されます。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] の新機能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html) では、テンプレートと XML データを組み合わせて、様々な形式の印刷用ドキュメントを生成できます。このサービスを使用すると、同期および一括モードでドキュメントを生成できます。API により、以下のような機能を備えたアプリケーションを作成することができます。

   * テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成します。
   * 非インタラクティブ PDF 印刷ストリームを含む様々な形式のフォームを生成する
   * XFA フォームの PDF ファイルから印刷用 PDF を生成する。
   * ソーステンプレートを用いて複数のデータセットを結合することにより、PDF、PostScript、PCL および ZPL の各種形式のドキュメントを一括生成する

* **コミュニケーション API で作成されたレコードのドキュメントおよびPDFドキュメント用のカスタムフォント**:コミュニケーション API を使用して生成されたPDFドキュメントで、ブランド承認済みフォントを使用して、組織の要件に合わせることができるようになりました。

### [!DNL Forms] プレリリースチャネルで利用できる新機能 {#prerelease-features-forms}

* **[Assembler API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**:Assembler API を使用して、組み合わせ、並べ替え、増やし、情報を取得するPDFドキュメント。


## CIF アドオン {#cloud-services-cif}

### 新機能 {#what-is-new-cif}

* myAccount コンポーネントの強化
* 製品レコメンデーションコンポーネントは、追加のページタイプ（ホームページ、買い物かご、注文の確認）をサポートします。
* **ウィッシュリスト**
   * ログインした訪問者は、ウィッシュリストに製品を追加できます
   * ウィッシュリストとその製品の管理は、myAccount を通じて可能です
   * 「ウィッシュリストに追加」ボタンは、ポリシー（製品ティーザー、製品の詳細など）を介して、コンポーネントレベルで有効/無効にできます
   * コアコンポーネントおよびAEM Venia ストアフロントで使用できます。

![ウィッシュリスト](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### リリース日 {#release-date-cm}

AEM as a Cloud Service 2022.01.0の Cloud Manager のリリース日は 2022 年 1 月 20 日です。 次回のリリースは 2022年2月10日（PT）の予定です。

### 新機能 {#what-is-new-cm}

* Cloud Manager では次の処理がおこなわれます。 [同じ git コミットが使用されたことを検出した場合は、コードベースを再構築しないでください](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 複数のフルスタックパイプライン実行で実行する場合。
* AEM環境ログにアクセスするには、 **デプロイメントマネージャー** 製品プロファイル。 このプロファイルを持たないユーザーには、ユーザーインターフェイスに無効なボタンが表示されます。
* Sites がソリューションとして有効になっていないプログラムに対しては、UI ではフロントエンドパイプライン設定を許可しません。
* Git パスワードの生成時に、有効期限が表示されます。

### バグ修正 {#bug-fixes-cm}

* 一部のフロントエンドパイプラインデプロイメントで発生した Null ポインターの例外が修正されました。
* 環境で古いバージョンのAEMが実行されている場合に、環境変数を追加、更新および削除できるようになりました。
* まれに、スケジュール済みステップを使用したパイプラインでは、イメージのビルドステップがエラーとしてマークされなくなりました。
* リポジトリーが 1 つだけのプログラムの場合、パイプライン実行画面にリポジトリー名が表示されるようになりました。

## コンテンツ転送ツール {#ctt-release}

### リリース日 {#release-date-ctt}

コンテンツ転送ツール v1.8.6 のリリース日は 2022 年 2 月 03 日です。

### 新機能 {#what-is-new-ctt}

* コンテンツの検証 — コンテンツ転送ツールで抽出されたすべてのコンテンツがターゲットインスタンスに正常に取り込まれたかどうかを確実に判断できます。 この機能を使用するには、 `System Console` ソースAEM環境の 参照： [コンテンツ転送の検証 — はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) を参照してください。

### バグ修正 {#bug-fixes-ctt}

* ユーザーマッピングでは大文字と小文字が区別されるので、一部のユーザーがマッピングされませんでした。 この問題が修正されました。ユーザーマッピングでは、大文字と小文字が区別されなくなりました。

## ベストプラクティスアナライザー {#bpa-release}

### リリース日 {#release-date-bpa}

ベストプラクティスアナライザー v2.1.24 のリリース日は 2022 年 2 月 01 日です。

### 新機能 {#what-is-new-bpa}

* スマートタグを使用するアセットの数、およびスマートタグを使用しないアセットの数を検出してレポートする機能。
* 使用されているコアコンポーネントのバージョンを検出してレポートする機能。
* BPA が実行されたソース層（オーサー層またはパブリッシュ層）の種類を検出し、レポートする機能。

### バグ修正 {#bug-fixes-bpa}

* BPA サイズ設定ロジックがより高速で効率的になりました。
* BPA は、実行時に分析済みのカウントを増分しないことがありました。 この問題が修正されました。
