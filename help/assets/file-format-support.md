---
title: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ
description: Adobe Experience Manager Assets as a Cloud Service でサポートされているファイル形式と MIME タイプ。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c65a5ebf204e25e56d518db3b354b95aef631621
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 96%

---


# AEM Assets as a Cloud Service でサポートされているファイル形式 {#supported-file-formats}

Adobe Experience Manager as a Cloud Service では、任意のバイナリファイルについて、その形式によらず、基本的なコンテンツ管理機能（格納、メタデータのオンライン管理、バージョン管理、アップロード、ダウンロードなど）をサポートしています。Adobe Experience Manager Assets は様々なファイル形式をサポートし、各製品機能は様々な形式をサポートしています。

さらに、Experience Manager Assets は、プレビューとレンディションの生成、およびフルテキストインデックス用のメタデータとテキストの抽出をサポートする拡張機能を提供します。この拡張サポートは、[アセットマイクロサービス](asset-microservices-configure-and-use.md)を使用して提供されます。

アセットマイクロサービスを使用したアセットの変換の主な要素は次のとおりです。

* アドビのアプリケーションおよびサービス（Adobe Photoshop、Adobe InDesign、Adobe Illustrator、Adobe XD、Adobe Dimension、Adobe Acrobat または PDF など）で生成される主要な [Adobe ファイル形式](#adobe-formats)
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

\* [!DNL Adobe InDesign] ファイル（INDD）の場合、レンディションのサイズは INDD ファイルに埋め込まれたプレビューで決まります。より大きなレンディションを埋め込むには、[!DNL InDesign] で環境の設定をおこないます（**[!UICONTROL 環境設定／ファイル管理／ドキュメントのプレビュー画像を常に保存／プレビューサイズ]**）。

## 画像形式 {#image-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ | 切り抜き |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| SVG | - | ✓ | - | - |
| TIFF | ✓ | ✓ | ✓ | - |

## [!DNL Dynamic Media] での画像形式 {#image-support-dynamic-media}

| 形式 | アップロード（入力形式） | 画像プリセットの作成（出力形式） | 動的レンディションのプレビュー | 動的レンディションの配信 | 動的レンディションのダウンロード |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD   ‡ | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は [!DNL Adobe Photoshop] によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

次のラスターイメージファイル形式のサブタイプは、[!DNL Dynamic Media] でサポートされていません。

* 100 MB を超える IDAT チャンクサイズを持つ PNG ファイル。
* PSB ファイル。
* CMYK、RGB、グレースケール、ビットマップ以外のカラースペースを持つ PSD ファイルはサポートされません。DuoTone、Lab、インデックス化カラースペースはサポートされません。
* 16 を超えるビット深度を持つ PSD ファイル。
* 浮動小数点データを持つ TIFF ファイル。
* Lab カラースペースを持つ TIFF ファイル。

## 3D形式 {#support-3d-formats}

次の3D形式のリストがサポートされています。

Dynamic Mediaでの3Dアセットの [操作も参照してください。](/help/assets/dynamic-media/assets-3d.md)

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | サムネールプレビュー | 3次元プレビュー | Dynamic Media配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ |  |  |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ |  | ✓ |  |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |

## [!DNL Camera RAW] 形式 {#camera-raw-formats}

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

## ドキュメント形式 {#document-formats}

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

## [!DNL Dynamic Media] でのドキュメント形式{#document-support-dynamic-media}

| 形式 | アップロード（入力形式） | 画像プリセットの作成（出力形式） | 動的レンディションのプレビュー | 動的レンディションの配信 | 動的レンディションのダウンロード |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| INDD | ✓ | - | - | - | - |

## ビデオ形式 {#video-formats}

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

## をトランスコードするための [!DNL Dynamic Media] でのビデオ形式{#video-dynamic-media-transcoding}

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen（MSS2）、Microsoft Photo Story（WVP2） |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft Video 1（MS-CRAM） |
| WebM | WebM | Google VP8 |  |
| OGV、OGG | Ogg | Theora、VP3、Dirac |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D、RM | Red Raw Video | MJPEG 2000 |  |
| RAM、RM | RealVideo | サポート対象外 | Real G2（RV20）、Real 8（RV30）、Real 10（RV40） |
| FLAC | Native Flac | Free lossless audio codec |  |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000 codec |  |

## オーディオ形式 {#audio-formats}

Assets as a Cloud Service は、AIF、ASF、M4A、MP3、WAV、WMA オーディオ形式の XMP メタデータ抽出のサポートを提供します。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)

