---
title: XMP メタデータ
description: メタデータ管理用のXMP(Extensible Metadata Platform)メタデータ標準について説明します。 AEMでは、メタデータの作成、処理および交換のための標準化された形式として使用されます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# XMP メタデータ {#xmp-metadata}

XMP（Extensible Metadata Platform）は、AEM Assets であらゆるメタデータ管理に使用されるメタデータ規格です。XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。

Aside from offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich [content model](#xmp-core-concepts) and is [supported by Adobe](#advantages-of-xmp) and other companies, so that users of XMP in combination with AEM Assets have a powerful platform to build upon.

## XMPの概要とエコシステム {#xmp-ecosystem}

AEM Assetsは、XMPメタデータ標準をネイティブにサポートします。 XMP は、デジタルアセット内の標準化されたメタデータと独自メタデータを処理および格納するための規格です。XMP は、複数のアプリケーションでメタデータを効率的に使用するための共通規格となるよう設計されています。

例えば制作のプロフェッショナルは、アドビのアプリケーションに組み込まれた XMP サポートを使用して、複数のファイル形式に情報を渡します。AEM Assets リポジトリでは、XMP メタデータを抽出し、そのデータをコンテンツのライフサイクルの管理に使用します。自動化ワークフローを作成することもできます。

XMP が提供するデータモデル、ストレージモデルおよびスキーマを使用して、メタデータの定義、作成および処理方法を規格化できます。これらの概念は、すべてこの節で説明します。

EXIF、ID3、Microsoft Office などの従来のメタデータは、すべて自動的に XMP に解釈され、製品カタログなどの顧客固有のメタデータスキーマをサポートするよう拡張することができます。

XMP のメタデータは、一連のプロパティで構成されます。これらのプロパティは、常に 資源という特定の事業者つまり、プロパティはリソースに関する「概要」です。 XMP の場合、リソースとなるのは常にアセットです。

XMP によって定義される[メタデータ](https://en.wikipedia.org/wiki/Metadata)モデルは、任意の定義済みメタデータ項目のセットと併用できます。また、XMP によって、リソースで複数の処理手順がおこなわれる際にその履歴を記録する上で便利な基本的なプロパティに対して、特定の[スキーマ](https://en.wikipedia.org/wiki/XML_schema)も定義されます。処理手順は、撮影、[スキャン](https://en.wikipedia.org/wiki/Image_scanner)またはテキスト作成から、画像編集手順（[切り抜き](https://en.wikipedia.org/wiki/Cropping_%28image%29)やカラー調整など）を経て、最終的な画像へのアセンブリまでです。XMP の処理中に、各ソフトウェアプログラムまたはデバイスでデジタルリソースに独自の情報を付加できます。この情報は、最終的なデジタルファイルで保持されます。

XMP のシリアライズおよび格納は、通常 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework)（RDF）のサブセットを使用して実行され、[XML](https://en.wikipedia.org/wiki/XML) で表記されます。

### XMP の利点 {#advantages-of-xmp}

XMP には、他のエンコーディング規格およびエンコーディングスキーマに比べて次の利点があります。

* XMP ベースのメタデータは利便性が高く、細かく分類されています。   
* XMP では 1 つのプロパティに複数の値を指定できます。
* XMP の規格化されたエンコーディングによって、メタデータを簡単にやり取りできます。
* XMP は拡張可能です。アセットに追加情報を追加できます。

XMP 規格は拡張できるように設計されていて、カスタムタイプのメタデータを XMP データに追加できます。一方、EXIF は拡張できません。EXIF のプロパティのリストは固定されていて、拡張することはできません。

>[!NOTE]
>
>XMP では通常、バイナリデータタイプを埋め込むことはできません。To carry binary data in XMP, for example, thumbnail images, they must be encoded in an XML-friendly format such as `Base64`.

### XMP core concepts {#xmp-core-concepts}

**名前空間とスキーマ**

XMP スキーマは、一連のプロパティ名を共通の XML 名前空間で定義したものです。
名前空間には、データタイプや識別情報が含まれます。XMP スキーマは、そのスキーマの XML 名前空間 URI によって識別されます。名前空間を使用すると、異なるスキーマに存在する、名前が同じで意味が異なるプロパティとの競合を防ぐことができます。

例えば、別個に設計された 2 つのスキーマにある **Creator** プロパティは、アセットを作成した個人を意味する場合と、アセットの作成元アプリケーション（Adobe Photoshop など）を意味する場合があります。

**XMPのプロパティと値**

XMP には、1 つ以上のスキーマからプロパティを選択し含めることができます。多くのアドビアプリケーションで使用される一般的なサブセットに含まれるプロパティの例を示します。

* ダブリンコアスキーマ： `dc:title`, `dc:creator`, `dc:subject`, `dc:format`,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,, `dc:rights`
* XMP基本スキーマ： `xmp:CreateDate`、 `xmp:CreatorTool`、 `xmp:ModifyDate`、 `xmp:metadataDate`
* XMP rights management schema: `xmpRights:WebStatement``xmpRights:Marked`
* XMP media management schema: `xmpMM:DocumentID`

**言語の代替**

XMP には、`xml:lang` プロパティをテキストプロパティに追加して、テキストの言語を指定する機能があります。

## レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

Adobe Experience Manager(AEM)AssetsのこのXMP書き戻し機能は、アセットのメタデータの変更をアセットのレンディションに複製します。

AEM Assets内から、またはアセットのアップロード中に、アセットのメタデータを変更すると、変更は最初にCRXDEのアセットノード内に保存されます。

XMPのライトバック機能は、アセットのすべてのレンディションまたは特定のレンディションにメタデータの変更を反映します。

Consider a scenario where you modify the [!UICONTROL Title] property of the asset titled `Classic Leather` to `Nylon`.

![メタデータ](assets/metadata.png)

この場合、AEM Assets ではこの「**[!UICONTROL タイトル]**」プロパティへの変更が、アセット階層に格納されたアセットメタデータ用の `dc:title` パラメーターに保存されます。

![metadata_stored](assets/metadata_stored.png)

ただし、AEM Assets では、メタデータの変更はアセットのレンディションに自動的に反映されません。

XMPのライトバック機能を使用すると、メタデータの変更をアセットのすべてのレンディションまたは特定のレンディションに反映できます。 ただし、変更はアセット階層の metadata ノード以下には保存されません。代わりに、この機能によって、レンディションのバイナリファイル内に変更内容が埋め込まれます。

### XMP書き戻しの有効化 {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. Configuration Managerを開くには、にアクセスしま `https://[aem_server]:[port]/system/console/configMgr`す。
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### 特定のレンディションに対するXMP書き戻しの有効化 {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. デフォルトでは、このステップには元のレンディションが設定されています。

XMPの書き戻し機能で、レンディションのサムネール140.100.pngおよび319.319.pngにメタデータを反映するには、次の手順を実行します。

1. Tap/click the AEM logo, and then navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. 「 **[!UICONTROL Arguments]** 」ボックスにを追加 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`し、「 **[!UICONTROL OK]**」をタップまたはクリックします。

   ![step_properties](assets/step_properties.png)

1. 変更内容を保存します。
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF レンディションは、Dynamic Media ハイブリッド実装でのみ、ローカルで作成および格納されます。

1. ワークフローを保存します。

メタデータの変更は、アセットのレンディションレンディションthumbnail.140.100.pngおよびthumbnail.319.319.pngに反映され、他のレンディションレンディションレンディションには反映されません。

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

### XMPメタデータのフィルター {#filtering-xmp-metadata}

AEM Assetsは、アセットバイナリから読み取られ、アセットの取り込み時にJCRに保存されるXMPメタデータのプロパティ/ノードのブラックリストフィルターとホワイトリストフィルターの両方をサポートしています。

ブラックリストフィルターは、除外するよう指定されたプロパティを除く、すべての XMP メタデータプロパティを読み込みます。ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブラックリストフィルターで、大量の XMP メタデータを含む膨大な量のアセットを読み込むと、監視キューの遅滞など、安定性に関する問題が、AEM インスタンス／クラスターで発生する可能性があります。

この問題は、XMP メタデータのホワイトリストフィルターで解決できます。このフィルターは、読み込む XMP プロパティを定義するので、そこに定義されていない XMP プロパティや不明な XMP プロパティは無視されます。これらのプロパティをいくつかブラックリストフィルターに追加することで、後方互換性を確保できます。

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。AEM では、この値を `exif:DateTimeOriginal`.という名前のメタデータフィールドに格納します。この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. Configuration Managerを開くには、にアクセスしま `https://[aem_server]:[port]/system/console/configMgr`す。
1. Open the **[!UICONTROL Adobe CQ DAM XmpFilter]** configuration.
1. To apply whitelist filtering, select **[!UICONTROL Apply Whitelist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Whitelisted XML Names for XMP filtering]** box.

1. To filter out blacklisted XMP properties after applying whitelist filtering, specify them in the **[!UICONTROL Blacklisted XML Names for XMP filtering]** box.

   >[!NOTE]
   >
   >「**[!UICONTROL Apply Blacklist to XMP Properties]**」チェックボックスは、デフォルトでオンになっています。つまり、ブラックリストフィルターは、デフォルトで有効になっています。To disable blacklist filtering, unselect the **[!UICONTROL Apply Blacklist to XMP Properties]** option.

1. 変更内容を保存します。

>[!MORELIKETHIS]
>
>* [アドビのXMP仕様](https://www.adobe.com/devnet/xmp.html)