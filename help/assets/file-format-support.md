---
title: サポートされているファイル形式と MIME タイプ
description: ' [!DNL Experience Manager Assets] でCloud Serviceとしてサポートされているファイル形式とMIME型です。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7e5ea5ccf0110d1fb55449c9c1933aff6aba0065
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 93%

---


# [!DNL Assets] サポートされるファイル形式  {#supported-file-formats}

[!DNL Adobe Experience Manager] as a Cloud Service では、任意のバイナリファイルについて、その形式によらず、基本的なコンテンツ管理機能（格納、メタデータのオンライン管理、バージョン管理、アップロード、ダウンロードなど）をサポートしています。[!DNL Adobe Experience Manager Assets] は様々なファイル形式をサポートし、各製品機能は様々な形式をサポートしています。

さらに、[!DNL Experience Manager Assets]は、プレビューとレンディションの生成、およびフルテキストインデックスのメタデータとテキストの抽出をサポートする拡張機能も提供します。 この拡張サポートは、[アセットマイクロサービス](asset-microservices-configure-and-use.md)を使用して提供されます。

アセットマイクロサービスを使用したアセットの変換の主な要素は次のとおりです。

* [!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]、[!DNL Adobe Acrobat]、PDFなど、Adobeのアプリケーションやサービスで生成されるキー[Adobeファイル形式](#adobe-formats)。
* 主要な[イメージングファイル形式](#image-formats).
* （Adobe Camera Raw を活用した）各種カメラ（キャノン、ニコン、富士フイルム、オリンパスなどのメーカー）に対応する [Camera Raw ファイル形式。](#camera-raw-formats)
* Microsoft Office 形式や OpenDocument 形式などの一般的な[ドキュメント形式](#document-formats)
* 各種の[ビデオ](#video-formats)および[オーディオ](#audio-formats)形式.

次の凡例で、サポートのレベルを説明します。

| サポートレベル | 説明 |
| ------------- | --------------------------- |
| ✓ | サポート対象 |
| * | 表の下の備考を参照 |
| - | 適用なし |

## Adobe 形式 {#adobe-formats}

| ファイル形式 | サムネールの生成 | フルテキスト抽出 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | kid | - | kid | kid |
| Collage | - | - | kid | - |
| DN | kid | - | kid | kid |
| Ideas | - | - | kid | - |
| INDD | kid | - | kid | ✓ * |
| INDT | - | - | kid | - |
| PDF | kid | kid | kid | kid |
| Proto | - | - | kid | - |
| PSB | kid | - | kid | kid |
| PSD | kid | - | kid | kid |
| XD | kid | - | kid | kid |

\* [!DNL Adobe InDesign] ファイル（INDD）の場合、レンディションのサイズは INDD ファイルに埋め込まれたプレビューで決まります。より大きなレンディションを埋め込むには、[!DNL InDesign] で環境の設定をおこないます（**[!UICONTROL 環境設定／ファイル管理／ドキュメントのプレビュー画像を常に保存／プレビューサイズ]**）。

## 画像形式 {#image-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ | 切り抜き |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | kid | - | kid | kid |
| EPS | - | kid | - | - |
| GIF | kid | kid | kid | kid |
| JPEG | kid | kid | kid | kid |
| PNG | kid | kid | kid | kid |
| TIFF | kid | kid | kid | - |
| SVG | kid | - | kid | kid |
| SGI | kid | kid | kid | kid |
| RGB | kid | kid | kid | kid |
| RGBA | kid | kid | kid | kid |

## [!DNL Dynamic Media] での画像形式 {#image-support-dynamic-media}

| 形式 | アップロード（入力形式） | 画像プリセットの作成（出力形式） | 動的レンディションのプレビュー | 動的レンディションの配信 | 動的レンディションのダウンロード |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | kid | kid | kid | kid | kid |
| GIF | kid | kid | kid | kid | kid |
| TIFF | kid | kid | kid | kid | kid |
| JPEG | kid | kid | kid | kid | kid |
| BMP | kid | - | - | - | - |
| PSD   ‡ | kid | - | - | - | - |
| EPS | kid | kid | kid | kid | kid |
| PICT | kid | - | - | - | - |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は [!DNL Adobe Photoshop] によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

次のラスターイメージファイル形式のサブタイプは、[!DNL Dynamic Media] でサポートされていません。

* 100 MB を超える IDAT チャンクサイズを持つ PNG ファイル。
* PSB ファイル。
* CMYK、RGB、グレースケール、ビットマップ以外のカラースペースを持つ PSD ファイルはサポートされません。DuoTone、Lab、インデックス化カラースペースはサポートされません。
* 16 を超えるビット深度を持つ PSD ファイル。
* 浮動小数点データを持つ TIFF ファイル。
* Lab カラースペースを持つ TIFF ファイル。

## 3D 形式 {#support-3d-formats}

次の 3D 形式のリストがサポートされています。

[Dynamic Media での 3D アセット操作](/help/assets/dynamic-media/assets-3d.md)も参照してください。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | サムネールプレビュー | 3D プレビュー | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | kid | kid | kid | - | kid | kid | - | - |
| gLB | kid | kid | kid | kid | kid | - | kid | kid |
| gLTF | kid | kid | kid | - | kid | - | kid | - |
| OBJ | kid | kid | kid | kid | kid | - | kid | kid |
| STL | kid | kid | kid | kid | kid | - | kid | kid |
| USDz | kid | kid | kid | kid | kid | - | - | kid |

## [!DNL Camera RAW] 形式 {#camera-raw-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------ |
| 3FR | kid | kid | kid |
| ARW | kid | kid | kid |
| CR2 | kid | kid | kid |
| CR3 | kid | kid | kid |
| CRW | kid | kid | kid |
| DCR | kid | kid | kid |
| DNG | kid | kid | kid |
| ERF | kid | kid | kid |
| FFF | kid | kid | kid |
| GPR | kid | kid | kid |
| IIQ | kid | kid | kid |
| KDC | kid | kid | kid |
| MEF | kid | kid | kid |
| MFW | kid | kid | kid |
| MOS | kid | kid | kid |
| MRW | kid | kid | kid |
| NEF | kid | kid | kid |
| NRW | kid | kid | kid |
| ORF | kid | kid | kid |
| PEF | kid | kid | kid |
| RAF | kid | kid | kid |
| RAW | kid | kid | kid |
| RW2 | kid | kid | kid |
| RWL | kid | kid | kid |
| SRF | kid | kid | kid |
| SRW | kid | kid | kid |
| X3F | kid | kid | kid |

## ドキュメント形式 {#document-formats}

アセット管理機能でサポートされるドキュメント形式は次のとおりです。

| ファイル形式 | サムネールの生成 | フルテキスト抽出 | 幅/高さ | メタデータの管理 | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| PDF | kid | kid | kid | kid | kid |
| DOCX | kid | kid | kid | kid | kid |
| DOC | - | - | - | kid | kid |
| PPTX | kid | kid | kid | kid | kid |
| PPT | - | - | - | kid | kid |
| XLSX | kid | kid | kid | kid | kid |
| XLS | - | - | - | kid | kid |
| ODF | kid | kid | kid | - | - |
| OFG | kid | kid | kid | - | - |
| ODM | kid | kid | kid | - | - |
| ODP | kid | kid | kid | - | - |
| ODS | kid | kid | kid | - | - |
| ODT | kid | kid | kid | kid | kid |
| EPUB | - | kid | - | - | - |
| HTML | - | kid | - | kid | kid |
| PS | - | - | kid | - | - |
| RTF | - | kid | - | kid | kid |
| TXT | - | kid | - | kid | kid |
| XML | - | kid | - | - | - |

## [!DNL Dynamic Media] でのドキュメント形式{#document-support-dynamic-media}

| 形式 | アップロード（入力形式） | 画像プリセットの作成（出力形式） | 動的レンディションのプレビュー | 動的レンディションの配信 | 動的レンディションのダウンロード |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| 愛 | kid | - | - | - | - |
| PDF | kid | kid | kid | kid | kid |
| INDD | kid | - | - | - | - |

## ビデオ形式 {#video-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | kid | - |
| 3GP | - | kid | - |
| AVI | kid | kid | kid |
| DIVX | kid | - | kid |
| F4V | kid | kid | kid |
| FLV | kid | kid | kid |
| M2T | kid | - | kid |
| M2TS | kid | - | kid |
| M2V | kid | - | kid |
| M4V | kid | kid | kid |
| MKV | kid | - | kid |
| MOV | kid | kid | kid |
| MP4 | kid | kid | kid |
| MPEG | kid | kid | kid |
| MPG | kid | kid | kid |
| MTS | kid | - | kid |
| OGV | kid | - | kid |
| QT | kid | - | kid |
| R3D | - | kid | kid |
| SWF | kid | - | kid |
| WebM | kid | - | kid |
| WMV | kid | kid | kid |

## をトランスコードするための [!DNL Dynamic Media] でのビデオ形式{#video-dynamic-media-transcoding} 

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|------------------------|--------------------|--------|-------|
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen（MSS2）、Microsoft Photo Story（WVP2） |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft Video 1（MS-CRAM） |
| WebM | WebM | Google VP8 | - |
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D、RM | Red Raw Video | MJPEG 2000 | - |
| RAM、RM | RealVideo | サポート対象外 | Real G2（RV20）、Real 8（RV30）、Real 10（RV40） |
| FLAC | Native Flac | Free lossless audio codec | - |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000 codec | - |

## オーディオ形式 {#audio-formats}

[!DNL Assets] as a Cloud Service は、AIF、ASF、M4A、MP3、WAV、WMA オーディオ形式の XMP メタデータ抽出のサポートを提供します。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)

