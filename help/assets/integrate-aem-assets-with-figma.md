---
title: ' [!DNL AEM Assets]  と  [!DNL Figma] を統合します。'
description: ' [!DNL AEM Assets]  を  [!DNL Figma]  と統合して、 [!DNL Figma]  デザインワークフロー内で組織のアセットにアクセスして使用する方法について説明します。'
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: 3603a98dfee62db49f3201c8d75aa8eee4909cc1
workflow-type: ht
source-wordcount: '450'
ht-degree: 100%

---


# [!DNL AEM Assets] と [!DNL Figma] の統合{#integrate-aem-assets-with-figma}

[!DNL AEM Assets] は [!DNL Figma] とネイティブに統合されているので、[!DNL AEM Assets] に保存されているアセットに [!DNL Figma] ユーザーインターフェイスから直接アクセスできます。[!DNL AEM Assets] で管理されているコンテンツを [!DNL Figma] キャンバスに配置し、新しいコンテンツや編集したコンテンツを [!DNL AEM Assets] リポジトリに保存できます。

## 始める前に{#prerequisites-for-aem-assets-and-figma-integration}

* AEM のリリースバージョン `19149` 以上が必要です。

* [!DNL AEM Assets] を [!DNL Figma] と統合するには、有効な [!DNL AEM Assets] および [!DNL Figma] ライセンスが必要です。

## [!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]へのアクセス{#access-aem-assets-connector}

[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]にアクセスするには、次の手順を実行します。

1. [!DNL Figma] ホームページで、キャンバスの下部にあるツールバーの「**[!UICONTROL アクション]**」をクリックし、ダイアログボックスの検索バーで [!DNL Adobe Experience Manager (AEM) Assets Connector] を検索します。
1. [!DNL Adobe Experience Manager (AEM) Assets Connector] を選択して、[!DNL Adobe Experience Manager (AEM) Assets Connector] パネルを表示します。このパネルを使用して、[ [!DNL AEM]  アセットを  [!DNL Figma]  キャンバス](#import-aem-assets-into-figma-workflow)に読み込みます。
   ![アクション](/help/assets/assets/actions-on-figma.png)
または、[!DNL Figma] コミュニティで利用可能な [[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) にアクセスし、「**[!UICONTROL 開く...]**」をクリックし、最近使用したファイルを選択するか、新しいファイルを作成して「**[!UICONTROL 実行]** 」をクリックし、[!DNL Adobe Experience Manager (AEM) Assets Connector] パネルにアクセスします。
   ![Figma コミュニティのプラグインページ](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [!DNL AEM] 環境にログインした後に&#x200B;**[!UICONTROL ネットワークエラー]**&#x200B;メッセージが表示される場合は、[アドビサポートにお問い合わせ](https://helpx.adobe.com/jp/contact.html)ください。

## [!DNL AEM] アセットの [!DNL Figma] キャンバスへの読み込み{#import-aem-assets-into-figma-workflow}

[!DNL Figma] デザインインターフェイス内で [[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]パネルにアクセス](#access-aem-assets-connector)し、次の操作を行います。

1. [!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]パネルでアセットを検索します。詳しくは、[アセットセレクターの使用](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector)を参照してください。

1. アセットをキャンバスにドラッグ＆ドロップするか、アセットを選択して「**[!UICONTROL 選択]**」をクリックし、アセットをキャンバス上に配置します。

1. フォルダーパス内の ![3 つのドット](/help/assets/assets/three-dots.svg) をクリックして、現在の階層内のすべての親フォルダーと子フォルダーを表示します。フォルダーを選択して、その場所に移動します。
   ![3 つのドット](/help/assets/assets/assets-folder-structure.png)

Figma の準備が整ったら、[アセットを AEM Assets リポジトリに書き出す](#export-figma-design-to-aem-assets-folder)ことができます。

## [!DNL AEM Assets] リポジトリへのアセットの書き出し{#export-figma-design-to-aem-assets-folder}

[!DNL Figma] デザインインターフェイス内の [[!UICONTROL Adobe Experience Manager（AEM）Assets コネクタ]パネルにアクセス](#access-aem-assets-connector)し、次の手順を実行してデザインを [!DNL AEM Assets] リポジトリに書き出します。

1. [!DNL Figma] デザインを保存する宛先フォルダーに移動します。既にフォルダー内にいる場合は、フォルダーパスのその他のオプション（![3 つのドット](/help/assets/assets/three-dots.svg)）をクリックして、別の宛先フォルダーを選択します。
1. オプション：キャンバス上のアセットをグループ化し、これらを 1 つのユニットとして選択してフォルダーにアップロードします。
1. ![ファイルのアップロード](/help/assets/assets/upload-icon.svg) **[!UICONTROL アップロード]** をクリックして、**[!UICONTROL アセットをアップロード]**&#x200B;ダイアログボックスを表示します。
1. ダイアログボックスで、ファイル名を指定し、ファイル形式を選択し、「**[!UICONTROL 選択した項目]**」または「**[!UICONTROL ページ]**」のいずれかを選択して、「**[!UICONTROL アップロード]**」をクリックし、選択したアセットまたはデザイン全体を宛先フォルダーにアップロードします。
   ![Figma デザインをアップロード](/help/assets/assets/upload-figma-design.png)

## 重要な注意点{#Limitations-of-using-aem-assets-into-figma}

この統合には現在、次の制限があります。

* [!DNL AEM] Assets を Figma に読み込む場合、サポートされる形式は **JPEG**、**PNG** です。
* [!DNL Figma] から [!DNL AEM Assets] にデザインを書き出す場合、サポートされる形式は **PNG**、**PDF**、**JPG**、**SVG** です。
