---
title: サポートされているファイル形式
description: ' [!DNL Assets view] の様々なユースケースでサポートされているファイル形式'
role: User, Leader, Admin, Developer
contentOwner: AG
exl-id: 5936ace2-318e-4888-9ad4-23e6f6bfb857
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# [!DNL Assets view] でサポートされているファイル形式 {#file-format-support}

[!DNL Assets view] では幅広いファイル形式をサポートしており、各機能は各種ファイルタイプに対応しています。

* ![画像ファイルタイプのアイコン](assets/image-icon.svg) 画像：JPG、PNG、GIF、TIFF およびその他
* ![Creative Cloud タイプのアイコン](assets/creative-cloud-files.svg) Creative Cloud ファイル：PSD、PSB、AI および INDD
* ![カメラタイプのアイコン](assets/camera-icon.svg) Camera Raw ファイル：CR2/CR3、NEF、SRW/SRF およびその他
* ![ドキュメントファイルタタイプのアイコン](assets/document-icon.svg) ドキュメント：DOCX、PDF、PPTX および XLSX
* ![ビデオファイルタイプのアイコン](assets/video-icon.svg) ビデオ：MP4

[!DNL Assets view] は、メタデータのストレージ、アップロード、コピー、移動、削除、追加など、基本サービスを備えた任意のバイナリファイル形式をサポートしています。

[!DNL Assets view] は Adobe Camera Raw を活用し、キヤノン（CR2/CR3）、ニコン（NEF）、ソニー（SRW/SRF）、富士フイルム（RAF）、オリンパス（ORF）など、幅広い大手カメラメーカーの Camera Raw ファイルもサポートしています。

以下に示すように、ユースケースや機能に対する各種ファイルタイプのサポートレベルは異なります。 凡例を使用すると、サポートレベルがわかります。

| サポートレベル | 説明 |
|-------------------|-------------------------|
| ✓ | サポート対象 |
| ✓ ‡ | 条件付きでサポート |
| − | 適用なし |

## アセットの追加、アップロード、表示 {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| アセットタイプ | [参照](/help/assets/navigate-assets-view.md) | コピー | [アップロード](/help/assets/add-delete-assets-view.md) | 作成 | [削除](/help/assets/add-delete-assets-view.md#delete-assets) | 詳細 | 画像のズーム | [最近表示された項目](/help/assets/navigate-assets-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| ラスター画像 | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| RAW ファイル | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| フォルダー | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| MP4 ビデオ | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD、PSB、AI および INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| その他のバイナリファイル | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## アセットの検索、使用、編集 {#support-to-search-use-edit}

<!--writer - please check RAW files row below. There was an extra column, so I deleted a duplicate section. I think I did it right. -->

| アセットタイプ | [ダウンロード](/help/assets/manage-organize-assets-view.md#download) | ドラッグ＆ドロップ | [画像エディター](/help/assets/edit-images-assets-view.md) | [検索](/help/assets/search-assets-view.md) | [スマートタグ](/help/assets/metadata-assets-view.md#tags) | [名前の変更](/help/assets/manage-organize-assets-view.md) | [バージョン](/help/assets/manage-organize-assets-view.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| ラスター画像 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW ファイル | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| フォルダー | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| ビデオ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| CC ライブラリ | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD と PSB | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| AI と INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| その他のバイナリファイル | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## アセットの確認と共同作業 {#support-to-review-collaborate}

| アセットタイプ | 注釈 | コメント | タスクの作成と確認 |
|---------------|----------|----------|-------------------------|
| ラスター画像 | ✓ | ✓ | ✓ |
| RAW ファイル | ✓ | ✓ | ✓ |
| フォルダー | − | − | − |
| ビデオ | − | ✓ | ✓ |
| CC ライブラリ | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD、PSB、AI および INDD | − | ✓ | ✓ |
| その他のバイナリファイル | − | ✓ | ✓ |
| DOC | − | ✓ | ✓ |
| DOCX | − | ✓ | ✓ |
| PPT | − | ✓ | ✓ |
| PPTX | − | ✓ | ✓ |
| XLS | − | ✓ | ✓ |
| XLSX | − | ✓ | ✓ |
| TXT | − | ✓ | ✓ |
| RTF | − | ✓ | ✓ |

## その他のアセット管理タスク {#support-to-manage-assets}

| アセットタイプ | [メタデータ](/help/assets/metadata-assets-view.md) | [レンディション](/help/assets/add-delete-assets-view.md#renditions) | [ごみ箱](/help/assets/add-delete-assets-view.md#delete-assets) | コピー | 移動 |
|---------------|-------------------|------------|----------|----------|----------|
| ラスター画像 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW ファイル | ✓ | ✓ | ✓ | ✓ | ✓ |
| フォルダー | ✓ | − | ✓ | ✓ | ✓ |
| ビデオ | ✓ | − | ✓ | ✓ | ✓ |
| CC ライブラリ | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| AI と INDD | ✓ | − | ✓ | ✓ | ✓ |
| PSD と PSB | ✓ | ✓ | ✓ | ✓ | ✓ |
| その他のバイナリファイル | ✓ | − | ✓ | ✓ | ✓ |

[!DNL Adobe Asset Link] のユーザーは、サポート対象の [!DNL Adobe Creative Cloud] デスクトップアプリケーションから [!DNL Assets view] リポジトリにファイルをアップロードしてチェックイン（新しいバージョンをアップロード）できます。

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD, PSB           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## 次の手順 {#next-steps}

* アセットビューユーザーインターフェイスの「[!UICONTROL フィードバック]」オプションを使用して、製品に関するフィードバックを提供する

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/ja?support-solution=General#support)に問い合わせる
