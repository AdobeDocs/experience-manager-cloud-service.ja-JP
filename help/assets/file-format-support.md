---
title: Experience Manager Assetsでクラウドサービスとしてサポートされるファイル形式とMIMEタイプ
description: Experience Manager Assetsでクラウドサービスとしてサポートされるファイル形式とMIMEタイプ。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# Assets supported file formats {#supported-file-formats}

クラウドサービスとしてのAdobe Experience Managerは、基本的なコンテンツ管理機能をサポート — ストレージ、メタデータのオンライン管理、バージョン管理、アップロードとダウンロードなど — 形式に関係なく、任意のバイナリファイルの場合。 Adobe Experience Manager Assetsは様々なファイル形式をサポートし、各製品機能は様々な形式をサポートしています。

さらに、Experience Manager Assetsは、プレビューとレンディションの生成、およびフルテキストインデックス用のメタデータとテキストの抽出をサポートする拡張機能を提供します。 この拡張サポートは、アセットマイクロサービスを [使用して提供されま](asset-microservices-configure-and-use.md)す。

次の凡例で、サポートのレベルを説明します。

| サポート レベル | 説明 |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | 対応 |
| * | 表の下の「備考」を参照 |
| - | 適用なし |

## アセットマイクロサービスを使用したアセットの変換 {#asset-microservices-supported-formats}

主なものを以下に示します。

* Adobe Photoshop [、InDesign、Illustrator、XD、Dimension、Acrobat/PDFなど、アドビのアプリケーションやサービスで生成される主要な](#adobe-formats) Adobeファイル形式です。
* 主要なイメ [ージングファイルの形式](#image-formats)。
* [Camera Rawファイル形式は](#camera-raw-formats) 、Canon、Nikon、Fujifilm、Olympus、その他のメーカー（Adobe Camera Rawで動作）など、様々なカメラを対象としています。
* 一般的 [な](#document-formats)ドキュメント形式 [(](#microsoft-office-formats) Microsoft Office [(Word、Excel、PowerPoint)やオープンドキュメント形](#opendocument-formats) 式など)。
* 幅広い[ビデオ](#video-formats)／[オーディオ](#audio-formats)形式.

次の表の列には、次の情報が表示されます。

| 列 | 説明 |
| ------------ | --------------------------------------------------------------- |
| 形式 | アセットの元のバイナリのファイル形式（ファイル拡張子） |
| GIF | レンディション生成用のGIF形式 |
| JPEG | レンディションを生成するためのJPEG形式 |
| PNG | レンディション生成用のPNG形式 |
| XMP | 元のバイナリのメタデータの抽出 |
| TXT | インデックス作成用のドキュメントのテキストの抽出 |
| 幅/高さ | レンディションの幅と高さの定義のサポート（ピクセル単位） |

### Adobe形式 {#adobe-formats}

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

\* INDD（InDesignファイル）の場合、レンディションのサイズはINDDファイルに埋め込まれたプレビューによって決まります。 InDesignで環境設定を行い(環境設定/フ&#x200B;**[!UICONTROL ァイル処理/常にプレビュー画像をドキュメントと共に保存(プレビューサイズ]**))、より大きなレンディションを埋め込むようにします。

### Image formats {#image-formats}

| ファイル形式 | GIF | JPEG | PNG | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

### Camera RAW形式 {#camera-raw-formats}

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

### ドキュメント形式 {#document-formats}

| ファイル形式 | TXT | XMP |
| ----------- | --- | --- |
| EPUB | ✓ | - |
| HTML | ✓ | - |
| PS | - | ✓ |
| RTF | ✓ | - |
| テキスト | ✓ | - |
| XML | ✓ | - |

### Microsoft Office形式 {#microsoft-office-formats}

| ファイル形式 | GIF | JPEG | PNG | テキスト | 幅/高さ |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

### OpenDocument形式 {#opendocument-formats}

| ファイル形式 | GIF | JPEG | PNG | テキスト | 高さ |
| ----------- | --- | ---- | --- | ---- | ------ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |

### ビデオ形式 {#video-formats}

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

### オーディオ形式 {#audio-formats}

クラウドサービスとしてのアセットは、次のオーディオ形式のXMPサポートを提供します。AIF、ASF、M4A、MP3、WAVおよびWMA。

## サポートされるドキュメント形式 {#doc-formats}

ドキュメント管理機能でサポートされるアセット形式は次のとおりです。

| ファイル形式 | ストレージ | メタデータの管理 | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|
| DOC | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ |
| ODT | ✓ | ✓ | ✓ |
| PDF | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |
| RTF | ✓ | ✓ | ✓ |
| TXT | ✓ | ✓ | ✓ |
| XLS | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ |
| PPT | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ |

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセットの処理](asset-microservices-overview.md)

