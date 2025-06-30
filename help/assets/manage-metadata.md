---
title: デジタルアセットのメタデータの管理
description: メタデータのタイプについて、および  [!DNL Adobe Experience Manager Assets]  を使用してアセットのメタデータを管理してアセットの分類と整理を容易にする方法について説明します。 [!DNL Experience Manager]  を使用すると、メタデータに基づいてアセットを自動的に整理および処理できます。
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management, Metadata
role: User, Architect, Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 100%

---

# デジタルアセットのメタデータの管理 {#managing-metadata-for-digital-assets}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

[!DNL Adobe Experience Manager Assets] では、あらゆるアセットのメタデータを保持します。したがって、アセットの分類と編成が容易にでき、特定のアセットを検索しやすくなります。メタデータ管理は、[!DNL Experience Manager Assets] にアップロードされるファイルからメタデータを抽出する機能と共に、クリエイティブワークフローに統合されます。アセットの任意のメタデータを保持して管理する機能によって、メタデータに基づいてアセットを自動的に編成および処理できます。

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## メタデータが必要な理由 {#why-metadata}

メタデータとは、データに関する情報のことです。この点に関して、データは、例えば画像などのデジタルアセットを指します。メタデータは、効率的なアセット管理を行うために重要です。

メタデータは、対象のアセットで使用できるすべてのデータのコレクションですが、次のようなデータはそのアセットに含まれているとは限りません。メタデータの例を以下に示します。

* アセットの名前。
* 最終変更の日時。
* リポジトリーに格納されたときのアセットのサイズ。
* アセットが含まれるフォルダーの名前。
* 関連するアセットまたは適用したタグ。

上記は、アセットに対して [!DNL Experience Manager] が管理できる基本的なメタデータプロパティです。これにより、ユーザーはすべてのアセットを表示できます。例えば、最終変更日にアセットを並べ替えると、最近追加された、または変更されたアセットを検出する場合に便利です。

デジタルアセットに、次のようなデータをさらに追加できます。

* アセットのタイプ（画像、ビデオ、オーディオクリップ、ドキュメントなど）。
* アセットの所有者。
* アセットのタイトル。
* アセットの説明。
* アセットに割り当てられたタグ。

メタデータが多いほど、アセットをより細かく分類でき、デジタル情報量が大きくなるにつれ便利です。数百個のファイルをファイル名だけに基づいて管理することは可能です。ただし、このアプローチは拡張性に欠けます。関係者の数や管理対象のアセット数が増えると不十分になります。

メタデータを追加すると、以下の理由からデジタルアセットの価値が大きくなります。

* アクセスが容易になる - システムやユーザーが簡単に見つけることができます。
* 管理しやすくなる - 一連の同じプロパティを持つアセットを容易に検索し、これらのアセットに変更を適用できます。
* 完全 - アセットは、より多くの情報とコンテキスト、より多くのメタデータを保持します。

したがって、[!DNL Assets] ではデジタルアセットのメタデータの作成、管理およびやり取りを行う適切な方法を提供します。

## メタデータのタイプ {#types-of-metadata}

メタデータは、テクニカルメタデータ、情報メタデータおよび管理メタデータに分類されます。

### テクニカルメタデータ

テクニカルメタデータは、デジタルアセットの技術的側面に焦点を当て、以下に関する重要な情報を提供します。

* ファイルサイズ
* 形式
* 解像度
* 寸法
* カラーモード

このタイプのメタデータは、デジタルアセットを理解し、効率的に使用するのに役立ちます。

### 情報メタデータ

情報メタデータは、コンテンツの理解を深め、コンテンツの検出と検索を簡単にするための説明情報を提供します。キーワード、キャプション、説明が含まれます。<br>例えば、Experience Manager Assets でビデオを管理する際、次の情報メタデータを含めることができます。

* **キーワード**：マーケティング、製品ローンチ、プロモ
* **キャプション**：魅力的な機能を備えた最新製品の紹介
* **説明**：ビデオコンテンツの詳細な概要。

### 管理メタデータ

管理メタデータは、デジタルアセットの管理の側面に関連しています。これにより、デジタルアセット管理システム内のアセットのアクセス制御、コンプライアンスおよびライフサイクル全体の管理を実行できます。以下に関する情報が含まれます。

* アセットの所有権
* 使用権限
* 権限
* その他の管理に関する詳細

このメタデータタイプでは、効果的なアセット管理、アクセス制御、コンプライアンスを保証できます。

<!-- Learn more about [metadata best practices](metadata-best-practices.md) to manage your digital assets effectively. -->

<!-- The two basic types of metadata are technical metadata and descriptive metadata.

Technical metadata is useful for software applications that are dealing with digital assets and should not be maintained manually. [!DNL Experience Manager Assets] and other software automatically determine technical metadata and the metadata may change when the asset is modified. The available technical metadata of an asset depends largely on the file type of the asset. Some examples of technical metadata are:

* Size of a file.
* Dimensions (height and width) of an image.
* Bit rate of an audio or video file.
* Resolution (level of detail) of an image.

Descriptive metadata is metadata concerned with the application domain, for example, the business that an asset is coming from. Descriptive metadata cannot be determined automatically. It is created manually or semi-automatically. For example, a GPS-enabled camera can automatically track the latitude and longitude and add geotag the image.

The cost of manually creating descriptive metadata information is high. So, standards are established to ease the exchange of metadata across software systems and organizations. [!DNL Experience Manager Assets] supports all relevant standards for metadata management. -->

## メタデータと最終変更 {#last-modification}

アセットの最終変更日は、アセットの元のファイルが最後に変更された日時を反映しています。その結果、変更日とユーザーは、次の場合にのみ変更されます。

* アセットの新しいバージョンがアップロードされたとき
* アセットが再処理されたとき

最終変更日とユーザーは、次の場合には変更されません。

* アセットを移動または名前変更したとき
* アセットがチェックアウト、チェックインまたはバージョン化されたとき
* アセットが公開または非公開にされたとき
* メタデータの更新時
* 参照またはコレクションの更新

## エンコーディング規格 {#encoding-standards}

メタデータをファイルに埋め込む方法は様々です。エンコーディング規格は、次の中から選択できます。

* XMP：[!DNL Assets] で抽出したメタデータをリポジトリーに格納するために使用されます。
* ID3：オーディオファイルおよびビデオファイル用の規格です。
* Exif：画像ファイル用の規格です。
* その他、従来の規格：[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel] など。

### XMP {#xmp}

[!DNL Extensible Metadata Platform]（XMP）は、すべてのメタデータ管理に対して [!DNL Experience Manager Assets] で使用されるオープンな標準です。XMP は、すべてのファイル形式に埋め込むことができる、ユニバーサルメタデータエンコーディングを提供します。アドビやその他の企業は、リッチコンテンツモデルを提供する XMP 標準をサポートしています。XMP 標準および [!DNL Experience Manager Assets] のユーザーは、基盤となる強力なプラットフォームを持っています。詳しくは、[XMP](https://www.adobe.com/products/xmp.html) を参照してください。

### ID3 {#id}

これらの ID3 タグに格納されたデータは、コンピューターまたはポータブル MP3 プレーヤーでデジタルオーディオファイルを再生すると表示されます。

ID3 タグは、MP3 ファイル形式用に設計されています。形式に関する追加情報：

* ID3 タグは、MP3 ファイルおよび mp3PRO ファイルで使用できます。
* WAV ではタグが使用されません。
* WMA には、オープンソースの実装を許可しない独自のタグがあります。
* Ogg Vorbis では、Ogg コンテナに埋め込まれた Xiph コメントを使用します。
* AAC では独自のタグ形式を使用します。

### Exif {#exif}

Exchangeable image file format（Exif）は、デジタル写真で最も一般的に使用されるメタデータフォーマットです。JPEG、TIFF、RIFF、WAV など、多くのファイル形式でメタデータプロパティの固定語彙を埋め込む方法を提供します。Exif は、メタデータをメタデータ名とメタデータ値のペアとして保存します。これらのメタデータの名前と値のペアは、タグとも呼ばれます。[!DNL Experience Manager] のタグと混同しないようにしてください。最新のデジタルカメラは Exif メタデータを作成し、最新のグラフィックソフトウェアでサポートされています。Exif 形式は、特に画像に関するメタデータ管理で最も一般的な共通項です。

Exif の主な制限は、BMP、GIF、PNG などの一般的な画像ファイル形式ではサポートされないことです。

Exif で定義されるメタデータフィールドは、通常、テクニカルなもので、記述メタデータ管理では使用が制限されています。このため、[!DNL Experience Manager Assets] は Exif プロパティのマッピングを、[共通のメタデータスキーマ](metadata-schemas.md)と XMP に提供します。

#### その他のメタデータ {#other-metadata}

ファイルから埋め込み可能なその他のメタデータには、[!DNL Microsoft Word]、[!DNL PowerPoint]、[!DNL Excel] などがあります。

## デジタルアセットのメタデータの管理 {#manage-assets-metadata}

Adobe Experience Manager Assets を使用すると、複数のアセットのメタデータを同時に編集できるので、アセットに対して共通のメタデータの変更を一括ですばやくプロパゲートできます。[!UICONTROL プロパティ]ページを使用すると、メタデータのプロパティを共通の値に変更したり、タグを追加または変更したりできます。メタデータのプロパティページをカスタマイズ（メタデータのプロパティの追加、編集、削除など）するには、スキーマエディターを使用します。

>[!NOTE]
>
>一括編集メソッドは、フォルダーまたはコレクションで使用可能なアセットに対して機能します。フォルダー全体で使用可能なアセットまたは共通の基準に一致するアセットについては、[検索後にメタデータを一括更新する](/help/assets/search-assets.md#metadata-updates)ことが可能です。

1. 編集するアセットの場所に移動します。
1. 共通のプロパティを編集するアセットを選択します。
1. ツールバーで「**[!UICONTROL プロパティ]**」を選択して、選択したアセットの「[!UICONTROL プロパティ]」ページを開きます。

   >[!NOTE]
   >
   >複数のアセットを選択すると、それらのアセットに対して最も下位の共通親フォームが選択されます。つまり、複数のアセットを選択すると、[!UICONTROL プロパティ]ページには、個々のアセットすべての[!UICONTROL プロパティ]ページで共通するメタデータフィールドのみ表示されます。

1. 様々なタブで選択したアセットのメタデータプロパティを変更します。
1. 特定のアセットのメタデータエディターを表示するには、リストの残りのアセットの選択をキャンセルします。メタデータエディターのフィールドには、その特定のアセットのメタデータが入力されています。

   >[!NOTE]
   >
   >* [!UICONTROL プロパティ]ページで、選択をキャンセルすることでアセットリストからアセットを削除できます。アセットリストは、デフォルトではすべてのアセットが選択されています。リストから削除するアセットのメタデータは更新されていません。
   >* アセットリストの上部で、「**[!UICONTROL タイトル]**」の横にあるチェックボックスをオンにして、アセットの選択とリストの消去を切り替えます。

1. アセットに別のメタデータスキーマを選択するには、ツールバーの「**[!UICONTROL 設定]**」で目的のスキーマを選択します。変更内容を保存します。
1. 複数の値が含まれるフィールドで、既存のメタデータに新しいメタデータを追加するには、「**[!UICONTROL 追加モード]**」を選択します。このオプションを選択しないと、フィールド内の既存のメタデータが新しいメタデータに置き換えられます。「**[!UICONTROL 送信]**」を選択します。

   >[!CAUTION]
   >
   >1 つの値のみを指定できるフィールドの場合、「**[!UICONTROL 追加モード]**」を選択しても、フィールド内の既存の値に新しいメタデータが追加されません。

## 処理プロファイルを使用したカスタムメタデータ {#metadata-compute-service}

Assets as a [!DNL Cloud Service] では、クラウドネイティブのサービスを使用して、アセットのカスタムメタデータを生成できます。カスタムメタデータを生成する処理プロファイルを設定します。「[処理プロファイルの使用方法](/help/assets/asset-microservices-configure-and-use.md#use-profiles)」を参照してください。

![処理プロファイルでのメタデータのレンダリング](assets/processing-profile-metadata.png)

>[!TIP]
>
>1 つのフォルダーに適用できる処理プロファイルは 1 つだけです。フォルダー内のアセットに複数の処理を適用するには、1 つの処理プロファイルに複数のオプションを追加します。例えば、1 つのプロファイルでレンディションの生成、アセットのトランスコード、カスタムメタデータの生成などを行うことができます。各タスクに MIME タイプのフィルターを適用して、必要なファイル形式に対して適切なタスクがトリガされるようにできます。

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## メタデータスキーマ {#metadata-schemata}

メタデータスキーマは、メタデータプロパティの事前定義のセットで、様々なアプリケーションで使用できます。プロパティは常にアセットと関連付けられています。つまり、プロパティはリソースの「説明」です。

必要なメタデータスキーマが存在しない場合は、独自のメタデータスキーマを設計することもできます。既存の情報を重複しないようにします。組織内でスキーマを分割すると、メタデータを共有しやすくなります。[!DNL Experience Manager] は、最も頻繁に使用されるメタデータスキーマのデフォルトリストを提供します。このリストを使用すると、メタデータ戦略がすぐに開始でき、必要なメタデータプロパティをすばやく選択できます。

サポートされるメタデータスキーマを以下に示します。

### 標準的なメタデータ {#standard-metadata}

* DC - [!DNL Dublin Core] は、重要で広く使用されている一連のメタデータです。
* DICOM - Digital Imaging and Communications in Medicine。
* `Iptc4xmpCore` および `iptc4xmpExt` - International Press Communications Standard には、多くのサブジェクト固有のメタデータが含まれています。
* RDF - Resource Description Framework - 汎用のセマンティック Web メタデータ用。
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpBJ` - Basic Job Ticketing。

### アプリケーション固有のメタデータ {#application-specific-metadata}

アプリケーション固有のメタデータには、テクニカルメタデータも記述メタデータも存在します。そのようなメタデータを使用する場合、他のアプリケーションでそのメタデータを使用することはできません。例えば、別の画像レンダリングアプリケーションが [!DNL Adobe Photoshop] メタデータにアクセスできない場合があります。アプリケーション固有のプロパティを標準プロパティに変更するワークフロー手順を作成できます。

* ACDSee - [!DNL ACDSee] プログラムで管理されるメタデータ。[www.acdsee.com/](https://www.acdsee.com/) を参照してください。
* Album - [!DNL Adobe Photoshop Album]。
* CQ - [!DNL Experience Manager Assets] で使用。
* DAM - [!DNL Experience Manager Assets] で使用。
* DEX - [Optima SC Description explorer](https://www.optimasc.com/products/dex/index.html) は、Windows オペレーティングシステム向けのメタデータおよびファイル管理向けのツールのコレクションです。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/jp/camera-raw/using/introduction-camera-raw.html)。
* LR - [!DNL Adobe Lightroom]。
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro)。
* MicrosoftPhoto および MP - Microsoft Photo。
* PDF および PDF/X。
* Photoshop および psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management メタデータ {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons]。
* [!DNL XMPRights]。
* PLUS - [Picture Licensing Universal System](https://www.useplus.com)。
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* PRL - PRISM Rights Language。
* PUR - PRISM Usage Rights。
* `xmpPlus` - PLUS と XMP の統合。

### 写真固有のメタデータ {#photography-specific-metadata}

* Exif - GPS 位置など、カメラからのテクニカル情報。
* CRS - [!DNL Camera Raw] スキーマ。
* `iptc4xmpCore` および `iptc4xmpExt`。
* TIFF - 画像メタデータ（TIFF 画像に限らない）。

### 印刷固有のメタデータ {#print-specific-metadata}

* PDF および PDF/X：Adobe PDF およびサードパーティのアプリケーション
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* XMP - [!DNL Extensible Metadata Platform]。
* `xmpPG` - ページテキストの XMP メタデータ。

### マルチメディア固有のメタデータ {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media]。
* `xmpMM` - メディア管理。

## メタデータ駆動型のワークフロー {#metadata-driven-workflows}

メタデータ駆動型のワークフローを作成することで、一部のプロセスを自動化し、効率性を高めることができます。メタデータ駆動型のワークフローでは、ワークフロー管理システムでワークフローが読み取られ、その結果、事前定義された動作が実行されます。例として、メタデータ駆動型のワークフローの使用方法をいくつか示します。

* ワークフローで画像にタイトルがあるかチェックできます。タイトルがない場合、システムはタイトルを追加するよう通知します。
* ワークフローでアセットの著作権情報によって配布が許可されているかをチェックできます。そのため、システムはアセットを 1 台のサーバーまたは他のサーバーに送信します。
* ワークフローでは、定義済みの必須のメタデータがないアセット、または&#x200B;*無効な*&#x200B;メタデータを持つアセットがないことを確認できます。

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [XMP メタデータ](xmp-metadata.md)
>* [メタデータの編集と追加](meta-edit.md)
