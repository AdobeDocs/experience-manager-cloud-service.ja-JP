---
title: デジタルアセットのメタデータの管理
description: メタデータのタイプについて、および AEM Assets を使用してアセットのメタデータを管理してアセットの分類と整理を容易にする方法について説明します。アセットの任意のメタデータを保持および管理する機能を持つ AEM Assets によって、メタデータに基づいたアセットの自動編成および自動処理ができます。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

Adobe Experience Manager（AEM）Assets では、あらゆるアセットのメタデータを保持します。したがって、アセットの分類および編成が容易にでき、特定のアセットを検索しやすくなります。メタデータ管理は、AEM Assets にアップロードされるファイルからメタデータを抽出する機能と共に、クリエイティブワークフローに統合されます。アセットの任意のメタデータを保持および管理する機能を持つ AEM Assets によって、メタデータに基づいたアセットの自動編成および自動処理ができます。

>[!MORELIKETHIS]
>
>* [XMP メタデータ](xmp-metadata.md)
>* [メタデータの編集と追加](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## メタデータを使用する理由 {#why-metadata}

メタデータとは、データに関する情報のことです。この場合、データとは操作するアセット（画像など）を指します。メタデータによってアセットをより効率的に管理できるので、メタデータは重要なものです。

メタデータは、対象の画像で使用できるすべてのデータのコレクションですが、次のようなデータは、その画像に含まれているとは限りません。

* アセットの名前
* 最終変更日時
* リポジトリに格納されたときの画像のサイズ
* アセットが含まれるフォルダーの名前

これらは AEM でアセットごとに管理できる基本的なメタデータプロパティです。これらのプロパティを使用して、例えばすべてのアセットを最終変更日順に並べることができ、最近リポジトリに追加されたアセットを探したい場合に便利です。

デジタルアセットに、次のようなさらに詳細なデータを追加できます。

* アセットのタイプ（画像、ビデオ、オーディオクリップ、ドキュメントなど）
* アセットの所有者
* アセットのタイトル
* アセットの説明
* アセットに割り当てられたタグ

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。1 人のユーザーが数百ファイルのリストをファイル名だけで管理することはできても、多数のユーザーが関係し、管理するアセットの数が多くなると、ファイル名だけの管理では不十分です。

メタデータをアセットに追加すると、アセットは次のような特徴を持つので、アセットの価値が高まります。

* アクセスのしやすさ - 検索が容易になります
* 管理のしやすさ - 一連の同じプロパティを持つアセットを容易に検索し、これらのアセットに変更を適用できます
* より高い複雑性 - アセットに追加するメタデータが多くなるほど、メタデータの管理がより重要になります

したがって、AEM Assets ではデジタルアセットのメタデータの作成、管理およびやり取りを行う適切な方法を提供します。

## Metadata basics {#metadata-basics}

メタデータは、アセットの読み込み（取り込み）時に抽出されます。メタデータを追加すると、アセットをより細かく分類できます。

この節では、メタデータおよびエンコーディング規格のタイプについて説明します。

### テクニカルメタデータ {#technical-metadata}

テクニカルメタデータは、デジタルアセットを操作しているソフトウェアアプリケーションで役に立つもので、手動で管理できません。テクニカルメタデータは AEM Assets などのソフトウェアで自動で定義でき、アセットを変更するとテクニカルメタデータも変更されます。アセットで使用可能なテクニカルメタデータは、主にアセットのファイルタイプによって決まります。テクニカルメタデータの例を次に示します。

* ファイルのサイズ
* 画像のサイズ（高さと幅）
* オーディオファイルやビデオファイルのビットレート
* 画像の解像度（詳細レベル）

### 記述メタデータ {#descriptive-metadata}

記述メタデータは、アセットが属するビジネスなど、アプリケーションドメインに関するメタデータです。記述メタデータは自動で定義できません。手動または半自動で作成する必要があります。例えば、画像が撮影された場所の緯度と経度を GPS が有効なカメラで自動的に追跡し、その情報を画像のメタデータに追加します。

記述メタデータ情報の作成にかかる手動作業はコストが高いので、ソフトウェアシステムと組織との間でメタデータのやり取りを容易にするための規格が確立されています。

AEM Assets は、メタデータの管理に関連するすべての規格をサポートします。

メタデータは重要なもので、メタデータの作成には膨大な手動作業を必要とするので、やり取りを容易にするための規格が確立されています。

### Encoding standards {#encoding-standards}

メタデータは、様々な方法でファイルに埋め込むことができます。エンコーディング規格は、次の中から選択できます。

* XMP：AEM Assets で、抽出したメタデータをリポジトリに格納するために使用されます。
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* EXIF：画像ファイル用の規格です。
* その他/レガシー：Microsoft Word、PowerPoint、Excelなどから

#### XMP {#xmp}

XMPはExtensible Metadata Platformを意味し、AEM Assetsですべてのメタデータ管理に使用されるメタデータ標準です。XMPは、すべてのファイル形式に埋め込むことのできるユニバーサルメタデータエンコーディングを提供するだけでなく、リッチコンテンツモデルを提供し、アドビや他の会社でもサポートされているので、AEM Assetsと組み合わせたXMPのユーザーは強力なプラットフォームを構築できます。

#### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤー上でデジタルオーディオファイルの再生時に表示されます。

ID3 タグは、MP3 ファイルフォーマット用に設計されています。各フォーマットのその他の情報：

* ID3 タグは、MP3 ファイルおよび MP3pro ファイルで使用できます。
* WAV ではタグが使用されません。
* WMA では独自のタグが使用され、オープンソースの実装は許可されていません。
* Ogg Vorbisは、OGGコンテナに埋め込まれたXiphコメントを使用します。
* AAC では独自のタグフォーマットが使用されます。

#### EXIF {#exif}

EXIF は Exchangeable image file format のことで、デジタル写真で最も一般的に使用されるメタデータフォーマットです。固定されたメタデータプロパティを、次のような多くのファイルフォーマットに埋め込むことができます。

* JPEG
* TIFF
* RIFF
* WAV

EXIF の大きな制限は、その他の一般的な画像ファイル（BMP、GIF、PNG など）でサポートされないことです。

EXIF によって、メタデータの名前と値のペアとして、メタデータが格納されます。これらのメタデータの名前と値のペアは、タグとも呼ばれます。AEM のタグと混同しないようにしてください。

EXIF は最新のデジタルカメラで自動的に作成され、最新のグラフィックソフトウェアでサポートされているので、メタデータの管理では最も下位の共通項目として表示されます。

EXIF で定義されるメタデータフィールドのほとんどは、高度な技術で作成されたもので、記述メタデータの管理では使用が制限されています。For this reason, AEM Assets offers mapping of EXIF properties into [common metadata schemata](metadata-schemas.md) and into [XMP](xmp-metadata.md), the powerful metadata format AEM Assets uses for metadata management.

#### その他のメタデータ {#other-metadata}

ファイルから埋め込むことのできるその他のメタデータには、Microsoft Word、PowerPoint、Excelなどがあります。

## デジタルアセットのメタデータの管理 {#manage-assets-metadata}

Enterprise Manager Assetsでは、複数のアセットのメタデータを同時に編集できるので、一般的なメタデータの変更をアセットに一括してすばやく反映できます。 プロパティペ [!UICONTROL ージを使用して] 、メタデータのプロパティを共通の値に変更したり、タグを追加または変更したりします。 メタデータのプロパティの追加、変更、削除など、メタデータのプロパティページをカスタマイズするには、スキーマエディターを使用します。

>[!NOTE]
>
>一括編集メソッドは、フォルダーまたはコレクションで使用可能なアセットに対して機能します。フォルダー全体で使用可能なアセットまたは共通の基準に一致するアセットについては、[検索後にメタデータを一括更新する](/help/assets/search-assets.md#metadataupdates)ことが可能です。

1. 編集するアセットの場所に移動します。
1. 共通のプロパティを編集するアセットを選択します。
1. From the toolbar, tap/click **[!UICONTROL Properties]** to open the [!UICONTROL Properties] page for the selected assets.

   >[!NOTE]
   >
   >複数のアセットを選択すると、それらのアセットに対して最も下位の共通親フォームが選択されます。In other words, the [!UICONTROL Properties] page only displays metadata fields that are common across the [!UICONTROL Properties] pages of all the individual assets.

1. 様々なタブで選択したアセットのメタデータプロパティを変更します。
1. 特定のアセットのメタデータエディターを表示するには、リストの残りのアセットの選択を解除します。メタデータエディターのフィールドには、その特定のアセットのメタデータが入力されています。

   >[!NOTE]
   >
   >* In the [!UICONTROL Properties] page, you can remove assets from the asset list by deselecting them. アセットリストは、デフォルトではすべてのアセットが選択されています。リストから削除するアセットのメタデータは更新されていません。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. To select a different metadata schema for the assets, tap/click **[!UICONTROL Settings]** from the toolbar, and select the desired schema. 変更内容を保存します。
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. このオプションを選択しないと、フィールド内の既存のメタデータが新しいメタデータに置換されます。Tap/click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >1 つの値のみを指定できるフィールドの場合、「**[!UICONTROL 追加モード]**」を選択しても、フィールド内の既存の値に新しいメタデータが追加されません。

## 一括メタデータ更新の上限を設定する {#configlimit}

DOSに似た状況を防ぐため、AEMはSling要求でサポートされるパラメーターの数を制限します。 一度に多くのアセットのメタデータを更新すると、上限に到達する可能性があり、それ以上のアセットでメタデータが更新されなくなります。AEM はログに次の警告を生成します。

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

制限を変更するには、Web コンソール（**[!UICONTROL ツール]**／**[!UICONTROL オペレーション]**／**[!UICONTROL Web コンソール]**）にアクセスし、**[!UICONTROL Apache Sling 要求のパラメーター処理]** OSGi 構成で&#x200B;**[!UICONTROL 最大 POST パラメーター]** の値を変更します。

## メタデータスキーマ {#metadata-schemata}

メタデータスキーマは、メタデータプロパティの事前定義のセットで、多様なアプリケーションで使用できます。プロパティは常にアセットと関連付けられています。つまり、プロパティはリソースの「説明」です。

ニーズに合うメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計できます（ただし、既存のスキーマを複製しないようにしてください）。組織内でスキーマを分割すると、メタデータを共有しやすくなります。

AEMは、最も人気のあるメタデータスキーマのあらかじめ用意されたリストを提供します。これにより、メタデータ戦略を迅速に開始し、既に定義されたスキーマから必要なメタデータプロパティを選択できます。

サポートされるメタデータスキーマを、以下に示します。

### 標準的なメタデータ {#standard-metadata}

* dc - Dublin Core - 最も重要で広く使用されるメタデータのセット
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore、Iptc4xmpExt - International Press Communications Standard - 多数のテーマ専用のメタデータ
* rdf - Resource Description Framework - 汎用のセマンティック Web メタデータ用
* xmp - Extensible Metadata Platform
* xmpBJ - Basic Job Ticketing

### アプリケーション固有のメタデータ {#application-specific-metadata}

>[!NOTE]
>
>アプリケーション固有のメタデータには、テクニカルメタデータも記述メタデータも存在します。これらのメタデータを使用すると、他のアプリケーションでそのメタデータを使用することはできません。例えば、アセットが Adobe Photoshop メタデータを持つ場合、他の画像レンダリングアプリケーションでこのアセットにアクセスしようとしても失敗します。
>
>アセット内にアプリケーション固有のメタデータが数多く存在する場合、アプリケーション固有のプロパティを標準プロパティに変更するワークフロー手順を作成できます。

* acdsee - metadata managed by the ACDSee program [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop アルバム
* cq - AEM Assetsで使用
* dam - AEM Assets で使用
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - iView MediaPro
* MicrosoftPhoto、MP - Microsoft Photo
* pdf、pdfx
* photoshop、psAux - Adobe Photoshop

### デジタル著作権管理メタデータ {#digital-rights-management-metadata}

* cc - クリエイティブコモンズ
* xmpRights
* プラス — Picture Licensing Universal System - https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata Publishing Requirements for Industry Standard Metadata
* prl - Prism Rights Language
* pur - Prism Usage Rights
* xmpPlus - PLUS と XMP との統合

### 写真固有のメタデータ {#photography-specific-metadata}

* exif - カメラからの数多くのテクニカル情報（GPS 位置など）
* crs - Photoshop Camera Raw
* Iptc4xmpCoreとiptc4xmpExt
* TIFF - 画像メタデータ（TIFF 画像に限りません）

### 印刷固有のメタデータ {#print-specific-metadata}

* pdfおよびpdfx - Adobe PDFおよびサードパーティアプリケーション
* prism - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata
* xmp
* xmpPG - ページ化されたテキスト用の xmp

### Multimedia-specific metadata {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - Media Management

## Metadata-driven workflows {#metadata-driven-workflows}

メタデータ駆動型のワークフローを作成することで、一部のプロセスを自動化し、効率性を高めることができます。メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。

例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローで、画像にタイトルがあるかどうかをチェックできます。タイトルがない場合、タイトルを追加するよう特定のユーザーに通知されます。
* ワークフローで、アセットの著作権情報によって配布が許可されているかどうかをチェックできます。許可されている場合、アセットが 1 つのサーバーに送信されます。許可されていない場合、アセットが別のサーバーに送信されます。
