---
title: サポートされているファイル形式
description: ' [!DNL Assets View] の様々なユースケースでサポートされているファイル形式'
role: User,Leader,Admin,Architect,Developer
contentOwner: AG
exl-id: bc44e98d-446e-41ff-b5b4-9dc324834630
source-git-commit: b4b397a09960f507df1daa0cf6f5dc49d6b286c6
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 96%

---

# [!DNL Assets View] でサポートされているファイル形式  {#file-format-support}

[!DNL Assets View] では幅広いファイル形式をサポートしており、各機能は各種ファイルタイプに対応しています。

* ![画像ファイルタイプのアイコン](assets/image-icon.svg) 画像：JPG、PNG、GIF、TIFF およびその他
* ![Creative Cloud タイプのアイコン](assets/creative-cloud-files.svg) Creative Cloud ファイル：PSD、AI および INDD
* ![カメラタイプのアイコン](assets/camera-icon.svg) Camera Raw ファイル：CR2/CR3、NEF、SRW/SRF およびその他
* ![ドキュメントファイルタタイプのアイコン](assets/document-icon.svg) ドキュメント：DOCX、PDF、PPTX および XLSX
* ![ビデオファイルタイプのアイコン](assets/video-icon.svg) ビデオ：MP4

[!DNL Assets View] は、メタデータのストレージ、アップロード、コピー、移動、削除、追加など、基本サービスを備えた任意のバイナリファイル形式をサポートしています。

[!DNL Assets View] は Adobe Camera Raw を活用し、キヤノン（CR2/CR3）、ニコン（NEF）、ソニー（SRW/SRF）、富士フイルム（RAF）、オリンパス（ORF）など、幅広い大手カメラメーカーの Camera Raw ファイルもサポートしています。

以下に示すように、ユースケースや機能に対する各種ファイルタイプのサポートレベルは異なります。凡例を使用すると、サポートレベルがわかります。

| サポートレベル | 説明 |
|-------------------|-------------------------|
| ✓ | サポート対象 |
| ✓ ‡ | 条件付きでサポート |
| − | 適用なし |

## アセットの追加、アップロード、表示 {#support-to-upload-view}

<!-- TBD: For AEM, AI files require the PDF option to be selected when saving the AI file.
-->

| アセットタイプ | [参照](/help/assets/navigate-view.md) | コピー | [アップロード](/help/assets/add-delete.md) | 作成 | [削除](/help/assets/add-delete.md#delete-assets) | 詳細 | 画像のズーム | [最近表示された項目](/help/assets/navigate-view.md) |
|-------------------|----------|----------|----------|----------|----------|-------------------|------------|-----------------|
| ラスター画像 | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| RAWファイル | ✓ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| フォルダー | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | − |
| MP4 ビデオ | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| PDF | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |
| PSD、AI、INDD | ✓ | ✓ | ✓ | − | ✓ | ✓ ‡ | − | ✓ |
| その他のバイナリファイル | ✓ | ✓ | ✓ | − | ✓ | ✓ | − | ✓ |

<!-- Hiding CC Libraries (considered beta) as per PM feedback.
| CC Libraries  | &#10003; | &minus;  | &#10003; | &#10003; | &#10003; | &#10003; | &minus;    | &minus;         |
-->

## アセットの検索、使用、編集 {#support-to-search-use-edit}

| アセットタイプ | [ダウンロード](/help/assets/manage-organize.md#download) | ドラッグ＆ドロップ | [画像エディター](/help/assets/edit-images.md) | [検索](/help/assets/search.md) | [スマートタグ](/help/assets/metadata.md#tags) | [名前の変更](/help/assets/manage-organize.md) | [バージョン](/help/assets/manage-organize.md#versions-of-assets) |
|---------------|----------|---------------|--------------|----------|------------|----------|----------|
| ラスター画像 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAWファイル | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | ✓ |
| フォルダー | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| ビデオ | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| CC ライブラリ | − | − | − | − | − | ✓ | ✓ |
| PDF | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| PSD | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ |
| AI と INDD | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |
| その他のバイナリファイル | ✓ | ✓ | − | ✓ | − | ✓ | ✓ |


## アセットの確認と共同作業 {#support-to-review-collaborate}

| アセットタイプ | 注釈 | コメント | タスクの作成と確認 |
|---------------|----------|----------|-------------------------|
| ラスター画像 | ✓ | ✓ | ✓ |
| RAWファイル | ✓ | ✓ | ✓ |
| フォルダー | − | − | − |
| ビデオ | − | ✓ | ✓ |
| CC ライブラリ | − | − | − |
| PDF | − | ✓ | ✓ |
| PSD、AI、INDD | − | ✓ | ✓ |
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

| アセットタイプ | [メタデータ](/help/assets/metadata.md) | [レンディション](/help/assets/add-delete.md#renditions) | [ごみ箱](/help/assets/add-delete.md#delete-assets) | コピー | 移動 |
|---------------|-------------------|------------|----------|----------|----------|
| ラスター画像 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAWファイル | ✓ | ✓ | ✓ | ✓ | ✓ |
| フォルダー | ✓ | − | ✓ | ✓ | ✓ |
| ビデオ | ✓ | − | ✓ | ✓ | ✓ |
| CC ライブラリ | ✓ | − | − | − | − |
| PDF | ✓ | − | ✓ | ✓ | ✓ |
| PSD、AI、INDD | ✓ | − | ✓ | ✓ | ✓ |
| その他のバイナリファイル | ✓ | − | ✓ | ✓ | ✓ |

[!DNL Adobe Asset Link] のユーザーは、サポート対象の [!DNL Adobe Creative Cloud] デスクトップアプリケーションから [!DNL Assets View] リポジトリにファイルをアップロードしてチェックイン（新しいバージョンをアップロード）できます。

<!-- TBD: Saving the template table separately for later use.
| Asset type    | Features |
|---------------|----------|
| Raster images |          |
| Folders       |          |
| Videos        |          |
| CC Libraries  |          |
| PDF files     |          |
| PSD           |          |
| AI            |          |
| INDD          |          |

>[!MORELIKETHIS]
>
>* []()
-->

## 次の手順 {#next-steps}

* 次を使用して製品に関するフィードバックを提供： [!UICONTROL フィードバック] 「アセット表示」ユーザーインターフェイスで使用できるオプション

* 右側のサイドバーにある「[!UICONTROL このページを編集]」（![ページを編集](assets/do-not-localize/edit-page.png)）または「[!UICONTROL 問題を記録] 」（![GitHub イシューを作成](assets/do-not-localize/github-issue.png)）を使用してドキュメントに関するフィードバックを提供する

* [カスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)に問い合わせる
