---
title: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ
description: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2e73a9bba91f15702bdeb1d57e87b688360661bd

---


# AEM Assets as a Cloud Service でサポートされているファイル形式 {#supported-file-formats}

Adobe Experience Manager as a Cloud Service では、任意のバイナリファイルについて、その形式によらず、基本的なコンテンツ管理機能（格納、メタデータのオンライン管理、バージョン管理、アップロード、ダウンロードなど）をサポートしています。Adobe Experience Manager Assets は様々なファイル形式をサポートし、各製品機能は様々な形式をサポートしています。

さらに、Experience Manager Assets は、プレビューとレンディションの生成、およびフルテキストインデックス用のメタデータとテキストの抽出をサポートする拡張機能を提供します。この拡張サポートは、[アセットマイクロサービス](asset-microservices-configure-and-use.md)を使用して提供されます。

次の凡例で、サポートのレベルを説明します。

| サポートレベル | 説明 |
| ------------- | --------------------------- |
| ✓ | サポート対象 |
| * | 表の下の備考を参照 |
| - | 適用なし |

## アセットマイクロサービスを使用したアセットコンバージョン {#asset-microservices-supported-formats}

主なものを以下に示します。

* Key [Adobe file formats](#adobe-formats) produced by Adobe applications and services, including Adobe Photoshop, Adobe InDesign, Adobe Illustrator, Adobe XD, Adobe Dimension, and Adobe Acrobat or PDF.
* 主要な[イメージングファイル形式](#image-formats).
* （Adobe Camera Raw を活用した）各種カメラ（キャノン、ニコン、富士フイルム、オリンパスなどのメーカー）に対応する [Camera Raw ファイル形式。](#camera-raw-formats)
* Common [document formats](#document-formats), including Microsoft Office and Open Document formats.
* 各種の[ビデオ](#video-formats)および[オーディオ](#audio-formats)形式.

### Adobe 形式 {#adobe-formats}

| ファイル形式 | サムネールの生成 | フルテキストの抽出 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| Collage | - | - | ✓ | - |
| DN | ✓ |  | ✓ | ✓ |
| Ideas | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| Proto | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* INDD（InDesign ファイル）の場合、レンディションのサイズは INDD ファイルに埋め込まれたプレビューで決まります。より大きなレンディションを埋め込むには、InDesign で環境の設定をおこないます（**[!UICONTROL 環境設定／ファイル管理／ドキュメントのプレビュー画像を常に保存／プレビューサイズ]**）。

### 画像形式 {#image-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ | 切り抜き  |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

### Camera Raw 形式 {#camera-raw-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | ✓ | ✓ | ✓ |
| ARW | ✓ | ✓ | ✓ |
| CR2 | ✓ | ✓ | ✓ |
| CR3 | ✓ | ✓ | ✓ |
| CRW | ✓ | ✓ | ✓ |
| DCR | ✓ | ✓ | ✓ |
| DNG | ✓ | ✓ | ✓ |
| ERF | ✓ | ✓ | ✓ |
| FFF | ✓ | ✓ | ✓ |
| GPR | ✓ | ✓ | ✓ |
| IIQ | ✓ | ✓ | ✓ |
| KDC | ✓ | ✓ | ✓ |
| MEF | ✓ | ✓ | ✓ |
| MFW | ✓ | ✓ | ✓ |
| MOS | ✓ | ✓ | ✓ |
| MRW | ✓ | ✓ | ✓ |
| NEF | ✓ | ✓ | ✓ |
| NRW | ✓ | ✓ | ✓ |
| ORF | ✓ | ✓ | ✓ |
| PEF | ✓ | ✓ | ✓ |
| RAF | ✓ | ✓ | ✓ |
| RAW | ✓ | ✓ | ✓ |
| RW2 | ✓ | ✓ | ✓ |
| RWL | ✓ | ✓ | ✓ |
| SRF | ✓ | ✓ | ✓ |
| SRW | ✓ | ✓ | ✓ |
| X3F | ✓ | ✓ | ✓ |

### ドキュメント形式 {#document-formats}

アセット管理機能でサポートされるドキュメント形式は次のとおりです。

| ファイル形式 | サムネールの生成 | フルテキストの抽出 | 幅/高さ | メタデータの管理 | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| DOC | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| OFG | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | - | ✓ | - | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

### ビデオ形式 {#video-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ |  | ✓ |
| F4V | ✓ | ✓ | ✓ |
| FLV | ✓ | ✓ | ✓ |
| M2T | ✓ | - | ✓ |
| M2TS | ✓ | - | ✓ |
| M2V | ✓ | - | ✓ |
| M4V | ✓ | ✓ | ✓ |
| MKV | ✓ | - | ✓ |
| MOV | ✓ | ✓ | ✓ |
| MP4 | ✓ | ✓ | ✓ |
| MPEG | ✓ | ✓ | ✓ |
| MPG | ✓ | ✓ | ✓ |
| MTS | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | ✓ | - | ✓ |
| SWF | ✓ | - | ✓ |
| WEBM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

### オーディオ形式 {#audio-formats}

クラウドサービスとしてのアセットは、AIF、ASF、M4A、MP3、WAVおよびWMAオーディオ形式用のXMPメタデータ抽出のサポートを提供します。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)

