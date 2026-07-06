---
title: ' [!DNL AEM Assets]  と  [!DNL Figma] を統合します。'
description: ' [!DNL AEM Assets]  を  [!DNL Figma]  と統合して、 [!DNL Figma]  デザインワークフロー内で組織のアセットにアクセスして使用する方法について説明します。'
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="AEM Assetsに適用）。"
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 28%

---


# [!DNL AEM Assets] と [!DNL Figma] の統合{#integrate-aem-assets-with-figma}

[!DNL AEM Assets] は [!DNL Figma] とネイティブに統合されているので、[!DNL AEM Assets] に保存されているアセットに [!DNL Figma] ユーザーインターフェイスから直接アクセスできます。 [!DNL AEM Assets] で管理されているコンテンツを [!DNL Figma] キャンバスに配置し、新しいコンテンツや編集したコンテンツを [!DNL AEM Assets] リポジトリに保存できます。

## 始める前に{#prerequisites-for-aem-assets-and-figma-integration}

* AEM のリリースバージョン `19149` 以上が必要です。

* [!DNL AEM Assets] を [!DNL Figma] と統合するには、有効な [!DNL AEM Assets] および [!DNL Figma] ライセンスが必要です。

## サポートされているファイル形式 {#supported-file-formats-integration-figma}


* [!DNL AEM]個のアセットをFigmaに読み込む場合、サポートされる形式は、画像アセット（JPEG、PNG）、ビデオファイル（MP4、MOV、WebM）、アニメーションファイル（GIF）、ベクターファイル（SVG）です。
* [!DNL Figma] から [!DNL AEM Assets] にデザインを書き出す場合、サポートされる形式は **PNG**、**PDF**、**JPG**、**SVG** です。

## [!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]へのアクセス{#access-aem-assets-connector}

[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]にアクセスするには、次の手順を実行します。

1. [!DNL Figma] ホームページで、キャンバスの下部にあるツールバーの「**[!UICONTROL アクション]**」をクリックし、ダイアログボックスの検索バーで [!DNL Adobe Experience Manager (AEM) Assets Connector] を検索します。
1. [!DNL Adobe Experience Manager (AEM) Assets Connector] を選択して、[!DNL Adobe Experience Manager (AEM) Assets Connector] パネルを表示します。 このパネルを使用して、[&#x200B; [!DNL AEM]  アセットを  [!DNL Figma]  キャンバス](#import-aem-assets-into-figma-workflow)に読み込みます。   ![&#x200B; アクション](/help/assets/assets/actions-on-figma.png)
または、[!DNL Figma] コミュニティで利用可能な[[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)にアクセスし、**[!UICONTROL で開く…]**&#x200B;をクリックし、最近のファイルを選択するか、新しいファイルを作成し、**[!UICONTROL 実行]**&#x200B;をクリックして[!DNL Adobe Experience Manager (AEM) Assets Connector] パネルにアクセスします。   ![Figma コミュニティのプラグインページ](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [!DNL AEM] 環境にログインした後に&#x200B;**[!UICONTROL ネットワークエラー]**&#x200B;メッセージが表示される場合は、[アドビサポートにお問い合わせ](https://helpx.adobe.com/jp/contact.html)ください。

## [!DNL AEM] アセットの [!DNL Figma] キャンバスへの読み込み{#import-aem-assets-into-figma-workflow}

[!DNL Figma] デザインインターフェイス内で [[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]パネルにアクセス](#access-aem-assets-connector)し、次の操作を行います。

1. [!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]パネルでアセットを検索します。 詳しくは、[&#x200B; コンテンツアドバイザーの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector)を参照してください。

1. アセットをキャンバスにドラッグ＆ドロップするか、アセットを選択して「**[!UICONTROL 選択]**」をクリックし、アセットをキャンバス上に配置します。

1. フォルダーパス内の ![3 つのドット](/help/assets/assets/three-dots.svg) をクリックして、現在の階層内のすべての親フォルダーと子フォルダーを表示します。 フォルダーを選択して、その場所に移動します。   ![3 つのドット](/help/assets/assets/figma-v2-plugin.png)

1. [ オプション ] 「**[!UICONTROL アップデートを確認]**」をクリックします。 現在のFigma ドキュメントで使用されているアセットは、AEMに存在するアセットと比較されます。 更新はすべて別のウィンドウに表示されます。 「**[!UICONTROL 更新]**」をクリックして、更新されたアセットをAEMからFigma ドキュメントに取り込みます。

Figma の準備が整ったら、[アセットを AEM Assets リポジトリに書き出す](#export-figma-design-to-aem-assets-folder)ことができます。

## [!DNL AEM Assets] リポジトリへのアセットの書き出し{#export-figma-design-to-aem-assets-folder}

[!DNL Figma] デザインインターフェイス内の [[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]パネルにアクセス](#access-aem-assets-connector)し、次の手順を実行してデザインを [!DNL AEM Assets] リポジトリに書き出します。

1. [!DNL Figma] デザインを保存する宛先フォルダーに移動します。 既にフォルダー内にいる場合は、フォルダーパスのその他のオプション（![3 つのドット](/help/assets/assets/three-dots.svg)）をクリックして、別の宛先フォルダーを選択します。
1. オプション：キャンバス上のアセットをグループ化し、これらを 1 つのユニットとして選択してフォルダーにアップロードします。
1. ![ファイルのアップロード](/help/assets/assets/upload-icon.svg) **[!UICONTROL アップロード]** をクリックして、**[!UICONTROL アセットをアップロード]**&#x200B;ダイアログボックスを表示します。
1. ダイアログボックスで、**[!UICONTROL 選択したアイテム]**&#x200B;または&#x200B;**[!UICONTROL ページ]**&#x200B;のいずれかを選択し、ファイルまたはページ名を指定して書き出し設定を定義し、**[!UICONTROL アップロード]**&#x200B;をクリックして、選択したアセットまたはデザイン全体を宛先フォルダーにアップロードします。

   書き出し設定は、ファイル形式、スケール、品質で構成されます。 例えば、ファイル形式として「JPG」を選択した場合、画像の拡大・縮小と画質を指定することもできます。 同様に、ファイル形式としてPNGを選択した場合は、画像スケールを定義することもできます。   ![Figma デザインをアップロード](/help/assets/assets/upload-figma-design.png)


## よくある質問 {#frequently-asked-questions-aem-assets-figma-integration}

### AEM AssetsとFigmaの統合により、デザイナーは何ができるようになりますか？ {#aem-assets-figma-integration-overview}

FigmaとのAEM Assets統合により、デザイナーはツールを切り替えることなく、Figma ユーザーインターフェイス内からAdobe Experience Managerに保存されているアセットに直接アクセスできます。 デザイナーは、AEM Assetsから画像、ビデオ、アニメーションファイル、ベクターを検索してFigma キャンバスに読み込み、完成または編集したデザインをサポートされているフォーマットでAEM Assets リポジトリに書き出すことができます。 この統合はネイティブで、Figma コミュニティで利用可能なAdobe Experience Manager AEM Assets コネクタを超えるサードパーティコネクタは必要ありません。

### AEM AssetsとFigmaを統合するための前提条件は何ですか？ {#aem-assets-figma-prerequisites}

AEM AssetsとFigmaを統合するには、AEMの最小リリース版の19149と、AEM AssetsとFigmaの両方の有効なライセンスの2つの前提条件が必要です。 Adobe Experience Manager AEM Assets コネクタにアクセスしてFigma内で使用するには、両方の条件を満たす必要があります。 設定中にAEM環境にログインした後にネットワークエラーメッセージが表示される場合は、Adobe サポートにお問い合わせください。

### FigmaでAdobe Experience Manager AEM Assets コネクタにアクセスするにはどうすればよいですか？ {#access-aem-assets-connector-figma}

Adobe Experience Manager AEM Assets コネクタには、Figma内から2つの方法でアクセスできます。 Figmaのホームページから、キャンバス下部のツールバーにある&#x200B;**アクション**&#x200B;をクリックし、ダイアログボックスでAdobe Experience Manager AEM Assets コネクタを検索して選択し、コネクタパネルを開きます。 または、Figma コミュニティページから直接コネクタにアクセスし、**で開く**&#x200B;をクリックし、最近のファイルを選択するか新しいファイルを作成し、**実行**&#x200B;をクリックしてコネクタパネルを起動します。

### AEM AssetsからFigmaに読み込むことができるファイル形式は何ですか？ {#aem-assets-figma-import-formats}

AEM AssetsをFigmaに読み込むには、JPEGおよびPNG形式の画像アセット、MP4、MOVおよびWebM形式のビデオファイル、GIF形式のアニメーションファイル、SVG形式のベクターファイルがサポートされています。 これらのフォーマットのAssetsは、Adobe Experience Manager AEM Assets Connector パネル内で検索し、ドラッグ&amp;ドロップするか、アセットを選択して「選択」をクリックすることで、Figma キャンバスに直接配置できます。

### AEM AssetsからFigma キャンバスにアセットを読み込むにはどうすればよいですか？ {#import-aem-assets-figma-canvas}

AEM AssetsからFigmaにアセットを読み込むには、Figma デザインインターフェイス内のAdobe Experience Manager AEM Assets コネクタパネルを開きます。 コネクタパネル内でコンテンツアドバイザーを使用してアセットを検索します。 アセットが見つかったら、キャンバスにドラッグ&amp;ドロップするか、アセットを選択し、**選択**&#x200B;をクリックしてキャンバスに配置します。 リポジトリ内のフォルダーを移動するには、フォルダーパスの3点アイコンをクリックして、現在の階層の親フォルダーと子フォルダーを表示して移動します。

### Figma ドキュメントで使用されているAEM Assetsが更新されたかどうかを確認するにはどうすればよいですか？ {#check-aem-assets-updates-figma}

FigmaのAdobe Experience Manager AEM Assets コネクタには、開いているFigma ドキュメントで現在使用されているアセットとAEM Assetsのバージョンを比較する&#x200B;**更新プログラムの確認** オプションが含まれています。 これを使用するには、コネクタパネルを開き、**アップデートの確認**&#x200B;をクリックします。 AEMで更新されたアセットは、別のウィンドウに表示されます。 「**更新**」をクリックして、更新された各アセットの最新バージョンをAEMからFigma ドキュメントに取り込みます。

### Figma デザインをAEM Assetsに書き出す際にサポートされるファイル形式は何ですか？ {#figma-export-aem-assets-formats}

Figma デザインをAEM Assets リポジトリに書き出す場合、PNG、PDF、JPG、SVGの4つのファイル形式がサポートされます。 書き出し設定では、選択したフォーマットに応じて追加の設定を定義することもできます。JPGの書き出しでは、画像の拡大・縮小と画質を指定できます。PNGの書き出しでは、画像の拡大・縮小を定義できます。 これらの設定は、書き出し処理中にアセットをアップロード ダイアログボックスで設定します。

### Figma デザインをAEM Assets リポジトリに書き出すにはどうすればよいですか？ {#export-figma-design-aem-assets}

Figma デザインをAEM Assetsに書き出すには、Figma内のAdobe Experience Manager AEM Assets コネクタパネルを開き、AEM Assets リポジトリの保存先フォルダーに移動します。 アップロードアイコンをクリックして、アセットをアップロードダイアログボックスを開きます。 ダイアログボックスで、「選択した項目」を選択して特定のアセットまたはページをアップロードし、デザインページ全体をアップロードします。ファイルまたはページ名を指定して、形式、スケール、品質を含む書き出し設定を定義し、「アップロード」をクリックします。 デザインは、選択したAEM Assetsの保存先フォルダーに保存されます。

### AEM Assetsに書き出す前にFigmaでアセットをグループ化できますか？ {#group-assets-figma-export-aem}

Figma デザインは、AEM Assets リポジトリに書き出す前に、カンバス上でグループ化できます。 アセットをグループ化すると、アセットを1つのユニットとして選択し、1回の操作で宛先フォルダーにアップロードできます。 グループ化が完了したら、Adobe Experience Manager AEM Assets コネクタパネルを開き、保存先フォルダーに移動して「アップロード」をクリックし、アセットのアップロードダイアログボックスでグループ化されたアイテムを選択して、書き出し設定を行い、「アップロード」をクリックします。

### Figma内からAEM Assets リポジトリ内のフォルダーを移動するにはどうすればよいですか？ {#navigate-aem-folders-figma}

AEM Assets リポジトリ内のフォルダーナビゲーションは、FigmaのAdobe Experience Manager AEM Assets コネクタパネル内で直接使用できます。 フォルダーパスの3点アイコンをクリックすると、現在の階層のすべての親フォルダーと子フォルダーが表示されます。 リストから任意のフォルダーを選択して、その場所に移動します。 デザインを別の保存先フォルダーに書き出す場合は、フォルダーパスの「その他のオプション」をクリックして、AEM Assets リポジトリー内の別のフォルダーを選択します。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
