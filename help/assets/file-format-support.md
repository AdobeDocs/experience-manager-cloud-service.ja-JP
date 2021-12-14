---
title: サポートされているファイル形式と MIME タイプ
description: ' [!DNL Experience Manager Assets] as a [!DNL Cloud Service] でサポートされているファイル形式と MIME タイプ。'
contentOwner: AG
feature: Asset Management,Renditions
role: User,Admin
exl-id: e848aa77-7829-4adc-8b88-0279791a4525
source-git-commit: ba752888601413dd4725a7a137f8b468b92ad5c7
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 90%

---

# [!DNL Assets] サポートされているファイル形式 {#supported-file-formats}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] では、任意のバイナリファイルについて、その形式によらず、基本的なコンテンツ管理機能（格納、メタデータのオンライン管理、バージョン管理、アップロード、ダウンロードなど）をサポートしています。[!DNL Adobe Experience Manager Assets] は様々なファイル形式をサポートし、各製品機能は様々な形式をサポートしています。

さらに、[!DNL Experience Manager Assets] は、プレビューとレンディションの生成、およびフルテキストインデックス用のメタデータとテキストの抽出をサポートする拡張機能を提供します。この拡張サポートは、[アセットマイクロサービス](asset-microservices-configure-and-use.md)を使用して提供されます。

アセットマイクロサービスを使用したアセット変換のハイライトは次のとおりです。

* アドビのアプリケーションおよびサービス（ または PDF など）で生成される主要な [Adobe ファイル形式](#adobe-formats)（[!DNL Adobe Photoshop]、[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe XD]、[!DNL Adobe Dimension]、および [!DNL Adobe Acrobat] または PDF。
* 主要な[イメージングファイル形式](#image-formats)。
* （Adobe Camera Raw を活用した）各種カメラ（キャノン、ニコン、富士フイルム、オリンパスなどのメーカー）に対応する [Camera Raw ファイル形式。](#camera-raw-formats)
* Microsoft Office 形式や OpenDocument 形式などの一般的な[ドキュメント形式](#document-formats)。
* 各種の[ビデオ](#video-formats)および[オーディオ](#audio-formats)形式。

次の凡例は、各形式に対するサポートのレベルを表しています。

| サポートレベル | 説明 |
| ------------- | --------------------------- |
| ✓ | サポート対象 |
| * | 表の下の備考を参照 |
| - | 適用なし |

## Adobe 形式 {#adobe-formats}

| ファイル形式 | サムネールの生成 | フルテキスト抽出 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------------- | ------------ |
| AI | ✓ | - | ✓ | ✓ |
| Collage | - | - | ✓ | - |
| DN | ✓ | - | ✓ | ✓ |
| Ideas | - | - | ✓ | - |
| INDD | ✓ | - | ✓ | ✓ * |
| INDT | - | - | ✓ | - |
| PDF | ✓ | ✓ | ✓ | ✓ |
| Proto | - | - | ✓ | - |
| PSB | ✓ | - | ✓ | ✓ |
| PSD | ✓ | - | ✓ | ✓ |
| XD | ✓ | - | ✓ | ✓ |

\* [!DNL Adobe InDesign] ファイル（INDD）の場合、レンディションのサイズは INDD ファイルに埋め込まれたプレビューで決まります。より大きなレンディションを埋め込むには、[!DNL InDesign] で環境の設定を行います（**[!UICONTROL 環境設定／ファイル管理／ドキュメントのプレビュー画像を常に保存／プレビューサイズ]**）。

## 画像形式 {#image-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ | 切り抜き |
| ----------- | -------------------- | ------------------- | ------------ | -------- |
| BMP | ✓ | - | ✓ | ✓ |
| EPS | - | ✓ | - | - |
| GIF | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ |
| PNG | ✓ | ✓ | ✓ | ✓ |
| RGB | ✓ | ✓ | ✓ | ✓ |
| RGBA | ✓ | ✓ | ✓ | ✓ |
| SGI | ✓ | ✓ | ✓ | ✓ |
| SVG | ✓ | - | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | - |

## [!DNL Dynamic Media] での画像形式  {#image-support-dynamic-media}

| 形式 | アップロード（入力形式） | 画像プリセットの作成（出力形式） | 動的レンディションのプレビュー | 動的レンディションの配信 | 動的レンディションのダウンロード |
| ------- | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| BMP | ✓ | - | - | - | - |
| EPS | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| PSD   ‡ | ✓ | - | - | - | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |

‡ 結合された画像は PSD ファイルから抽出されます。この画像は [!DNL Adobe Photoshop] によって生成され、PSD ファイルに含まれます。設定によって、結合された画像は実際の画像である場合とそうでない場合があります。

次のラスターイメージファイル形式のサブタイプは、[!DNL Dynamic Media] でサポートされていません。

* 100 MB を超える IDAT チャンクサイズを持つ PNG ファイル。
* PSB ファイル。
* CMYK、RGB、グレースケール、ビットマップ以外のカラースペースを持つ PSD ファイルはサポートされません。DuoTone、Lab、インデックス化カラースペースはサポートされません。
* 16 を超えるビット深度を持つ PSD ファイル。
* 浮動小数点データを持つ TIFF ファイル。
* Lab カラースペースを持つ TIFF ファイル。

## 3D 形式 {#support-3d-formats}

次の 3D 形式がサポートされています。

「[Dynamic Media での 3D アセット操作](/help/assets/dynamic-media/assets-3d.md)」も参照してください。

| 形式 | ストレージ | バージョン管理 | ワークフロー | 公開 | アクセス制御 | サムネールプレビュー | 3D プレビュー | Dynamic Media の配信 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | - | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | - | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

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

| ファイル形式 | サムネールの生成 | フルテキスト抽出 | 幅/高さ | メタデータの管理 | [Connected Assets](use-assets-across-connected-assets-instances.md) |
| ----------- | -------------------- | ------------------- | ------------ | ------------------- | ---------------- |
| DOC | - | - | - | ✓ | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | ✓ |
| EPUB | - | ✓ | - | - | - |
| HTML | - | ✓ | - | ✓ | ✓ |
| ODF | ✓ | ✓ | ✓ | - | - |
| ODM | ✓ | ✓ | ✓ | - | - |
| ODP | ✓ | ✓ | ✓ | - | - |
| ODS | ✓ | ✓ | ✓ | - | - |
| ODT | ✓ | ✓ | ✓ | ✓ | ✓ |
| OFG | ✓ | ✓ | ✓ | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |
| PPT | - | - | - | ✓ | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ |
| PS | - | - | ✓ | - | - |
| RTF | - | ✓ | - | ✓ | ✓ |
| TXT | ✓ | ✓ | - | ✓ | ✓ |
| XLS | - | - | - | ✓ | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | - | ✓ | - | - | - |

## [!DNL Dynamic Media] でのドキュメント形式  {#document-support-dynamic-media}

| 形式 | アップロード（入力形式） | 画像プリセットの作成（出力形式） | 動的レンディションのプレビュー | 動的レンディションの配信 | 動的レンディションのダウンロード |
| ------ | --------------------- | ----------------------------------- | ------------------------- | ------------------------- | -------------------------- |
| AI | ✓ | - | - | - | - |
| INDD | ✓ | - | - | - | - |
| PDF | ✓ | ✓ | ✓ | ✓ | ✓ |

## ビデオ形式 {#video-formats}

| ファイル形式 | サムネールの生成 | メタデータ抽出 | 幅/高さ |
| ----------- | -------------------- | ------------------- | ------------ |
| 3G2 | - | ✓ | - |
| 3GP | - | ✓ | - |
| AVI | ✓ | ✓ | ✓ |
| DIVX | ✓ | - | ✓ |
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
| MXF | ✓ | - | ✓ |
| OGV | ✓ | - | ✓ |
| QT | ✓ | - | ✓ |
| R3D | - | ✓ | ✓ |
| SWF | ✓ | - | ✓ |
| WebM | ✓ | - | ✓ |
| WMV | ✓ | ✓ | ✓ |

## をトランスコードするための [!DNL Dynamic Media] でのビデオ形式 {#video-dynamic-media-transcoding}

| ビデオファイル拡張子 | コンテナ | 推奨されるビデオコーデック | サポートされないビデオコーデック |
| --- | --- | --- | --- |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV（DV25）、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3（IV30）、MJPEG、Microsoft Video 1（MS-CRAM） |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（ベクターアニメーションファイル） |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV（DV25）、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| MP4 | MPEG-4 | H264/AVC（すべてのプロファイル） | - |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| MXF ‡ | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3（v9）、WMV2（v8）、WMV1（v7）、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen（MSS2）、Microsoft Photo Story（WVP2） |

‡このビデオ形式は、Dynamic Mediaのインタラクティブビデオでの使用や、Experience Manager Assetsの Annotation での使用には、まだサポートされていません。

## オーディオ形式 {#audio-formats}

[!DNL Assets] as a [!DNL Cloud Service] は、AIF、ASF、M4A、MP3、WAV、WMA オーディオ形式の XMP メタデータ抽出のサポートを提供します。

## オーディオおよびビデオの転写用にサポートされる入力形式 {#audio-video-transcription-formats}

* FLV（H.264 および AAC コーデックを使用）(.flv)
* MXF (.mxf)
* MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg)
* Windows Media ビデオ (WMV)/ASF (.wmv, .asf)
* AVI（非圧縮 8 ビット/10 ビット）(.avi)
* MP4 (.mp4、.m4a、.m4v)
* Microsoftデジタルビデオ録画 (DVR-MS) (.dvr-ms)
* Matroska/WebM (.mkv)
* WAVE/WAV (.wav)
* QuickTime (.mov)

## ヒントと制限事項 {#limitations-and-tips}

* 現在、メタデータ抽出のファイルサイズの上限は約 15 GB です。非常に大きなアセットをアップロードする場合は、メタデータの抽出操作に失敗することがあります。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスを使用したアセット処理](asset-microservices-overview.md)
>* [テキストベースのアセットのスマートタグ付けに対応しているファイル形式](/help/assets/smart-tags.md#smart-tags-supported-file-formats)

