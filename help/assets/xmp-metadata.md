---
title: XMP メタデータ
description: メタデータ管理のための XMP（Extensible Metadata Platform）メタデータ規格について説明します。メタデータの作成、処理、交換のための標準化された形式として AEM で使用されます。
contentOwner: AG
feature: メタデータ
role: Business Practitioner,Administrator
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 212e4e7cfb93d5765f80003c42ba6afb9af45c13
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 74%

---

# XMP メタデータ {#xmp-metadata}

XMP（Extensible Metadata Platform）は、AEM Assets であらゆるメタデータ管理に使用されるメタデータ規格です。XMP で提供される標準形式によって、多様なアプリケーションに対応したメタデータの作成、処理およびやり取りができます。

XMP では、すべてのファイル形式に埋め込むことができる共通のメタデータエンコーディングのほか、リッチ[コンテンツモデル](#xmp-core-concepts)も提供され、[アドビによるサポート](#advantages-of-xmp)やその他各社のサポートがあるので、XMP を AEM Assets と組み合わせて使用すると強力なプラットフォームを構築できます。

## XMP の概要とエコシステム {#xmp-ecosystem}

AEM Assets は、XMP メタデータ標準をネイティブにサポートしています。XMP は、デジタルアセット内の標準化されたメタデータと独自メタデータを処理および格納するための規格です。XMP は、複数のアプリケーションでメタデータを効率的に使用するための共通規格となるよう設計されています。

例えば制作のプロフェッショナルは、アドビのアプリケーションに組み込まれた XMP サポートを使用して、複数のファイル形式に情報を渡します。AEM Assets リポジトリーでは、XMP メタデータを抽出し、そのデータをコンテンツのライフサイクルの管理に使用します。自動化ワークフローを作成することもできます。

XMP が提供するデータモデル、ストレージモデルおよびスキーマを使用して、メタデータの定義、作成および処理方法を規格化できます。これらの概念は、すべてこの節で説明します。

EXIF、ID3、Microsoft Office などの従来のメタデータは、すべて自動的に XMP に解釈され、製品カタログなどの顧客固有のメタデータスキーマをサポートするよう拡張することができます。

XMP のメタデータは、一連のプロパティで構成されます。これらのプロパティは、常にリソースと呼ばれる特定のエンティティに関連付けられます。つまり、プロパティはリソースの「説明」です。XMP の場合、リソースとなるのは常にアセットです。

XMP によって定義される[メタデータ](https://en.wikipedia.org/wiki/Metadata)モデルは、任意の定義済みメタデータ項目のセットと併用できます。また、XMP によって、リソースで複数の処理手順がおこなわれる際にその履歴を記録するうえで便利な基本的なプロパティに対して、特定の[スキーマ](https://en.wikipedia.org/wiki/XML_schema)も定義されます。処理手順は、撮影、[スキャン](https://en.wikipedia.org/wiki/Image_scanner)またはテキスト作成から、画像編集手順（[切り抜き](https://en.wikipedia.org/wiki/Cropping_%28image%29)やカラー調整など）を経て、最終的な画像へのアセンブリまでです。XMP の処理中に、各ソフトウェアプログラムまたはデバイスでデジタルリソースに独自の情報を付加できます。この情報は、最終的なデジタルファイルで保持されます。

XMP のシリアライズおよび格納は、通常 [W3C](https://ja.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://ja.wikipedia.org/wiki/Resource_Description_Framework)（RDF）のサブセットを使用して実行され、[XML](https://ja.wikipedia.org/wiki/XML) で表記されます。

### XMP の利点 {#advantages-of-xmp}

XMP には、他のエンコーディング規格およびエンコーディングスキーマに比べて次の利点があります。

* XMP ベースのメタデータは利便性が高く、細かく分類されています。
* XMP では 1 つのプロパティに複数の値を指定できます。
* XMP の規格化されたエンコーディングによって、メタデータを簡単にやり取りできます。
* XMP は拡張可能です。アセットに詳細情報を追加できます。

XMP 規格は拡張できるように設計されていて、カスタムタイプのメタデータを XMP データに追加できます。一方、EXIF は拡張できません。EXIF のプロパティのリストは固定されていて、拡張することはできません。

>[!NOTE]
>
>XMP では通常、バイナリデータタイプを埋め込むことはできません。XMP でバイナリデータ（サムネール画像など）を扱う場合、XML に対応するフォーマット（`Base64` など）でエンコーディングする必要があります。

### XMP の中心概念 {#xmp-core-concepts}

**名前空間とスキーマ**

XMP スキーマは、一連のプロパティ名を共通の XML 名前空間で定義したものです。
名前空間には、データタイプや識別情報が含まれます。XMP スキーマは、そのスキーマの XML 名前空間 URI によって識別されます。名前空間を使用すると、異なるスキーマに存在する、名前が同じで意味が異なるプロパティとの競合を防ぐことができます。

例えば、別個に設計された 2 つのスキーマにある **Creator** プロパティは、アセットを作成した個人を意味する場合と、アセットの作成元アプリケーション（Adobe Photoshop など）を意味する場合があります。

**XMP のプロパティと値**

XMP には、1 つ以上のスキーマからプロパティを選択し含めることができます。多くのアドビアプリケーションで使用される一般的なサブセットに含まれるプロパティの例を示します。

* Dublin Core スキーマ：`dc:title`、`dc:creator`、`dc:subject`、`dc:format`、`dc:rights`
* XMP 基本スキーマ：`xmp:CreateDate`、`xmp:CreatorTool`、`xmp:ModifyDate`、`xmp:metadataDate`
* XMP Rights Management スキーマ：`xmpRights:WebStatement`、`xmpRights:Marked`
* XMP Media Management スキーマ：`xmpMM:DocumentID`

**代替言語**

XMP には、`xml:lang` プロパティをテキストプロパティに追加して、テキストの言語を指定する機能があります。

## レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

[!DNL Adobe Experience Manager Assets]のこのXMPの書き戻し機能は、メタデータの変更を元のアセットのレンディションにレプリケートします。
[!DNL Assets]内から、またはアセットのアップロード中に、アセットのメタデータを変更すると、変更は最初にアセット階層のメタデータノードに保存されます。  の書き戻し機能によって、メタデータの変更が、アセットのすべてのレンディションまたは特定のレンディションに反映されます。この機能は、`jcr`名前空間を使用するメタデータプロパティ（`dc:title`という名前のプロパティは書き戻されますが、`mytitle`という名前のプロパティは書き戻されません）のみを書き戻します。

例えば、「`Classic Leather`」というタイトルのアセットの[!UICONTROL Title]プロパティを`Nylon`に変更するシナリオを考えてみましょう。

![メタデータ](assets/metadata.png)

この場合、[!DNL Assets]は、 **[!UICONTROL Title]**&#x200B;プロパティに対する変更を、アセット階層に格納されたアセットメタデータ用の`dc:title`パラメーターに保存します。

![リポジトリのアセットノードに格納されたメタデータ](assets/metadata_stored.png)

>[!IMPORTANT]
>
>[!DNL Assets]では、書き戻し機能はデフォルトで有効になっていません。 [メタデータの書き戻しを有効にする方法](#enable-xmp-writeback)を参照してください。 MSM for digital assetsは、メタデータの書き戻しが有効になっている場合は機能しません。 書き戻し時に、継承が中断されます。

### XMPの書き戻し{#enable-xmp-writeback}を有効にする

[!UICONTROL DAMメタデータの書き戻] しワークフローは、アセットのメタデータの書き戻しに使用されます。書き戻しを有効にするには、次の3つの方法のいずれかを実行します。

* ランチャーを使用します。
* `DAM MetaData Writeback`ワークフローを手動で開始します。
* 後処理の一部としてワークフローを設定します。

ランチャーを使用するには、次の手順に従います。

1. 管理者は、**[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL ランチャー]**&#x200B;にアクセスします。
1. [!UICONTROL Launcher]を選択します。このランチャーで、**[!UICONTROL Workflow]**&#x200B;列に&#x200B;**[!UICONTROL DAM MetaDataの書き戻し]**&#x200B;が表示されます。 ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。

   ![「 DAMメタデータの書き戻しランチャー」を選択して、そのプロパティを変更し、アクティブ化します。](assets/launcher-properties-metadata-writeback1.png)

1. **[!UICONTROL ランチャーのプロパティ]**&#x200B;ページで「**[!UICONTROL アクティブ化]**」を選択します。 「**[!UICONTROL 保存して閉じる]**」をクリックします。

ワークフローを手動で1回だけアセットに適用するには、左側のレールから[!UICONTROL DAMメタデータの書き戻し]ワークフローを適用します。

アップロードされたすべてのアセットにワークフローを適用するには、後処理プロファイルにワークフローを追加します。

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->
