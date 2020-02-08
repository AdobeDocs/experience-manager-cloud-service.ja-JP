---
title: Experience Manager Assetsでクラウドサービスとしてサポートされるファイル形式とMIMEタイプ
description: Experience Manager Assetsでクラウドサービスとしてサポートされるファイル形式とMIMEタイプ。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 776b089a322cc4f86fdcb9ddf1c3cc207fc85d39

---


# Assets supported file formats {#supported-file-formats}

クラウドサービスとしてのAdobe Experience Managerは、任意のバイナリファイルに対し、形式に依存せず、ストレージ、メタデータオンライン管理、バージョン管理、アップロード、ダウンロードなどの基本的なコンテンツ管理機能をサポートします。 また、画像、アドビ独自のファイル形式、ドキュメント、ビデオなど、一般的に使用されるファイル形式の場合は、プレビューやレンディションの生成、フルテキストインデックス用のメタデータやテキストの抽出のサポートが拡張されます。 この拡張サポートは、アセットマイクロサービスを [使用して提供され](asset-microservices-configure-and-use.md)ます。

拡張サポートを含むファイル形式の主な特徴は次のとおりです。

* Adobe Photoshop [、InDesign、Illustrator、XD、Dimension、Acrobat/PDFなど、アドビのアプリケーションおよびサービスによって生成される主要な](#adobe-formats) Adobeファイル形式です。
* 主要なイメ [ージングファイル形式](#image-formats)
* [Camera rawファイル形式](#camera-raw-formats) （Canon、Nikon、Fujifilm、Olympusなど、様々なカメラ用）（Adobe Camera rawで動作）
* [Microsoft Office](#document-formats)(Word、Excel、PowerPoint)や [Open Document](#microsoft-office-formats) （開いている文書）形式などの一般的な文書 [](#opendocument-formats) 形式
* 幅広いビデ [オ](#video-formats) /オー [ディオ](#audio-formats) 形式

## 詳細なサポート情報の凡例 {#legend-for-detailed-support-information}

次の凡例で、機能のサポートレベルを説明します。

| サポート レベル | 説明 |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | 対応 |
| * | 表の下の備考を参照 |
| - | 適用なし |

サポート表の列には、次の情報が表示されます。

| 列 | 説明 |
| ------------ | --------------------------------------------------------------- |
| 形式 | アセットの元のバイナリのファイル形式（ファイル拡張子） |
| GIF | レンディション生成用のGIF形式 |
| JPEG | レンディション生成用のJPEG形式 |
| PNG | レンディション生成用のPNG形式 |
| XMP | 元のバイナリからのメタデータの抽出 |
| TXT | インデックス作成用のドキュメントからのテキストの抽出 |
| 幅/高さ | レンディションの幅と高さの定義のサポート（ピクセル単位） |

<!-- Adding this checkmark icon ✓ does not look good in table. The icon's shade and size has to be toned down for good readability and less clutter.
@gklebus: I suggest using a checkmark character, either U+2713 ✓ CHECK MARK or U+2714 ✔ HEAVY CHECK MARK
-->

## Adobe形式 {#adobe-formats}

| ファイル形式 | GIF | JPEG | PNG | TXT | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| コラージュ | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| アイデア | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PROTO | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\* INDD（InDesignファイル）の場合、レンディションのサイズはINDDファイルに埋め込まれたプレビューによって決まります。 InDesignで環境設定を行い(環境設定/フ&#x200B;**[!UICONTROL ァイル処理/常にプレビュー画像をドキュメントと共に保存、プレビューサイズ]**)、より大きなレンディションを埋め込みます。

## Image formats {#image-formats}

| ファイル形式 | GIF | JPEG | PNG | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |


## Camera RAW形式 {#camera-raw-formats}

| ファイル形式 | GIF | JPEG | PNG | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3FR | ✓ | ✓ | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ | ✓ | ✓ |

## ドキュメント形式 {#document-formats}

| ファイル形式 | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| テキスト | ✓ | - |
| XML | ✓ | - |

## Microsoft office形式 {#microsoft-office-formats}

| ファイル形式 | GIF | JPEG | PNG | テキスト | 幅/高さ |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

## OpenDocument形式 {#opendocument-formats}

| ファイル形式 | GIF | JPEG | PNG | テキスト | 高さ |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

## ビデオ形式 {#video-formats}

| ファイル形式 | GIF | JPEG | PNG | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | ------------ |
| 3G2 | - | - | - | ✓ | - |
| 3GP | - | - | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ | ✓ | ✓ |
| DIVX | ✓ | ✓ | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ | ✓ | ✓ |
| M2T | ✓ | ✓ | ✓ | - | ✓ |
| M2TS | ✓ | ✓ | ✓ | - | ✓ |
| M2V | ✓ | ✓ | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ | ✓ | ✓ |
| MKV | ✓ | ✓ | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ | ✓ | ✓ |
| MTS | ✓ | ✓ | ✓ | - | ✓ |
| OGV | ✓ | ✓ | ✓ | - | ✓ |
| QT | ✓ | ✓ | ✓ | - | ✓ |
| R3D | ✓ | ✓ | ✓ | - | ✓ |
| SWF | ✓ | ✓ | ✓ | - | ✓ |
| WEBM | ✓ | ✓ | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ | ✓ | ✓ |

## オーディオ形式 {#audio-formats}

クラウドサービスとしてのアセットは、次のオーディオ形式のXMPサポートを提供します。AIF、ASF、M4A、MP3、WAVおよびWMA。

<!-- TBD: Some items from https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedinputvideoformatsforDynamicMediatranscoding may be applicable.

Bring more parity with https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#SupportedMIMEtypes.
https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-formats.html#Supportedmultimediaformats
-->

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)

