---
title: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ
description: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9a7d2cff969a7920eb4fa3597846c11aa16392d9

---


# AEM Assets as a Cloud Service でサポートされているファイル形式 {#supported-file-formats}

クラウドサービスとしてのAdobe Experience Managerは、基本的なコンテンツ管理機能をサポート — ストレージ，メタデータのオンライン管理，バージョン管理，アップロードとダウンロードなど — 形式に関係なく、任意のバイナリファイルの場合。 Adobe Experience Manager Assetsは様々なファイル形式をサポートし、各製品機能は様々な形式をサポートしています。

さらに、Experience Manager Assetsは、プレビューとレンディションの生成、およびフルテキストインデックス用のメタデータとテキストの抽出をサポートする拡張機能を提供します。 この拡張サポートは、[アセットマイクロサービス](asset-microservices-configure-and-use.md)を使用して提供されます。

次の凡例で、サポートのレベルを説明します。

| サポートレベル | 説明 |
| ------------------------------------------------------------ | --------------------------- |
| ✓ | 対応 |
| * | 表の下の備考を参照 |
| - | 適用なし |

## Asset conversion using asset microservices {#asset-microservices-supported-formats}

主なものを以下に示します。

* アドビのアプリケーションおよびサービス（Adobe Photoshop、InDesign、Illustrator、XD、Dimension、Acrobat/PDF など）で生成される主要な [Adobe ファイル形式](#adobe-formats)
* 主要な[イメージングファイル形式](#image-formats)。
* [Camera Rawファイル形式は](#camera-raw-formats) 、Canon、Nikon、Fujifilm、Olympus、その他のメーカー（Adobe Camera Rawで動作）など、様々なカメラを対象としています。
* [Microsoft Office](#microsoft-office-formats)（Word、Excel、PowerPoint）形式や [OpenDocument](#opendocument-formats) 形式などの一般的な[ドキュメント形式.](#document-formats)
* 各種の[ビデオ](#video-formats)および[オーディオ](#audio-formats)形式.

次の表の列には、次の情報が表示されます。

| 列 | 説明 |
| ------------ | --------------------------------------------------------------- |
| ファイル形式 | アセットの元のバイナリのファイル形式（ファイル拡張子） |
| GIF | レンディション生成用の GIF 形式 |
| JPEG | レンディション生成用の JPEG 形式 |
| PNG | レンディション生成用の PNG 形式 |
| XMP | 元のバイナリからのメタデータの抽出 |
| TXT | インデックス作成を目的とした、ドキュメントからのテキストの抽出 |
| 幅/高さ | レンディションの幅と高さの定義のサポート（ピクセル単位） |

### Adobe 形式 {#adobe-formats}

| ファイル形式 | GIF | JPEG | PNG | TXT | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | --- | ------------ |
| AI | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| Collage | - | - | - | - | ✓ | - |
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| Ideas | - | - | - | - | ✓ | - |
| INDD | ✓ | ✓ | ✓ | - | ✓ | ✓* |
| INDT | - | - | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Proto | - | - | - | - | ✓ | - |
| PSB | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| PSD | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| XD | ✓ | ✓ | ✓ | - | ✓ | ✓ |

\* INDD（InDesign ファイル）の場合、レンディションのサイズは INDD ファイルに埋め込まれたプレビューで決まります。より大きなレンディションを埋め込むには、InDesign で環境の設定をおこないます（**[!UICONTROL 環境設定／ファイル管理／ドキュメントのプレビュー画像を常に保存／プレビューサイズ]**）。

### 画像形式 {#image-formats}

| ファイル形式 | GIF | JPEG | PNG | XMP | 幅/高さ |
| ----------- | --- | ---- | --- | --- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

### Camera Raw 形式 {#camera-raw-formats}

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

### Microsoft Office 形式 {#microsoft-office-formats}

| ファイル形式 | GIF | JPEG | PNG | テキスト | 幅/高さ |
| ----------- | --- | ---- | --- | ---- | ------------ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |

### OpenDocument 形式 {#opendocument-formats}

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

AEM Assets as a Cloud Service では、AIF、ASF、M4A、MP3、WAV、WMA の各オーディオ形式について、XMP をサポートしています。

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
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)

