---
title: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ
description: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# AEM Assets as a Cloud Service でサポートされているファイル形式 {#supported-file-formats}

クラウドサービスとしてのAdobe Experience Managerは、任意のバイナリファイルに対して、形式に関係なく、ストレージ、オンラインでのメタデータの管理、バージョン管理、アップロードとダウンロードなどの基本的なコンテンツ管理機能をサポートします。 Adobe Experience Manager Assetsは様々なファイル形式をサポートしており、製品の各機能は様々な形式をサポートしています。

また、Experience Manager Assetsは、プレビューとレンディションの生成、フルテキストインデックス用のメタデータとテキストの抽出のサポートを拡張します。 この拡張サポートは、[アセットマイクロサービス](asset-microservices-configure-and-use.md)を使用して提供されます。

次の凡例で、サポートのレベルを説明します。

| サポートレベル | 説明 |
| ------------- | --------------------------- |
| ✓ | 対応 |
| * | 表の下の備考を参照 |
| - | 適用なし |

## Asset conversion using asset microservices {#asset-microservices-supported-formats}

主なものを以下に示します。

* Key [Adobe file formats](#adobe-formats) produced by Adobe applications and services, including Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension, and Adobe Acrobat or PDF.
* 主要な[イメージングファイル形式](#image-formats).
* [Camera Rawファイル形式](#camera-raw-formats) 。Canon、Nikon、Fujifilm、Olympus、その他のメーカー（Adobe Camera Raw搭載）など、様々なカメラを対象としています。
* Common [document formats](#document-formats), including Microsoft Office and Open Document formats.
* 各種の[ビデオ](#video-formats)および[オーディオ](#audio-formats)形式.

次の表の列には、次の情報が表示されます。

| 列 | 説明 |
| ------------ | --------------------------------------------------------------- |
| ファイル形式 | アセットの元のバイナリのファイル形式（ファイル拡張子）。 |
| GIF | レンディション生成用の GIF 形式. |
| JPEG | レンディション生成用の JPEG 形式。 |
| PNG | レンディション生成用の PNG 形式。 |
| 幅/高さ | レンディションの幅と高さをピクセル単位で定義できるようになりました。 |

### Adobe 形式 {#adobe-formats}

| ファイル形式 | GIF | JPEG | PNG | フルテキストの抽出 | メタデータ抽出 | 幅/高さ |
| ----------- | -------- | -------- | -------- | ------------------- | ------------------- | ------------ |
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

| ファイル形式 | GIF | JPEG | PNG | メタデータ抽出 | 幅/高さ |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
| BMP | ✓ | ✓ | ✓ | - | ✓ |
| EPS | - | - | - | ✓ | - |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| SVG | - | - | - | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

### Camera Raw 形式 {#camera-raw-formats}

| ファイル形式 | GIF | JPEG | PNG | メタデータ抽出 | 幅/高さ |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
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

アセット管理機能でサポートされるドキュメント形式は次のとおりです。

|  | GIF | JPEG | PNG | フルテキストの抽出 | 幅/高さ | メタデータの管理 | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ---- | -------- | -------- | -------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | - | - | ✓ | - | - | - |
| HTML | - | - | - | ✓ | - | ✓ | ✓ |
| PS | - | - | - | - | ✓ | - | - |
| RTF | - | - | - | ✓ | - | ✓ | ✓ |
| TXT | - | - | - | ✓ | - | ✓ | ✓ |
| XML | - | - | - | ✓ | - | - | - |

### ビデオ形式 {#video-formats}

| ファイル形式 | GIF | JPEG | PNG | メタデータ抽出 | 幅/高さ |
| ----------- | -------- | -------- | -------- | ------------------- | ------------ |
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

クラウドサービスとしてのアセットは、AIF、ASF、M4A、MP3、WAVおよびWMAオーディオ形式用のXMPメタデータ抽出のサポートを提供します。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)

