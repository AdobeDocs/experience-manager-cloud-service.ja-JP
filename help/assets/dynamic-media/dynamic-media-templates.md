---
title: テンプレート  [!DNL Dynamic Media]  管理方法
description: WYSIWYG テンプレートエディターを使用して  [!DNL Dynamic Media]  テンプレートを作成する方法と、複数の画像やテキストレイヤーを含めて、バナーやチラシをすばやく作成し、下流のアプリケーションで使用する方法について説明します。
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 184149144d1f8d204241fcc477f937fa7c225895
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 55%

---

# [!DNL Dynamic Media] テンプレート{#dynamic-media-templates}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

WYSIWYG テンプレートエディターである [!DNL Dynamic Media] テンプレートを使用して、バナーやチラシ用にリアルタイムのカスタマイズ可能なテンプレートを作成します。 [!DNL Dynamic Media] テンプレートを公開し、ダウンストリームアプリケーションで使用します。 [!DNL Dynamic Media] テンプレートには、画像レイヤーとテキストレイヤーが含まれます。 テンプレートの画像レイヤーとテキストレイヤーにパラメーターを追加し、[[!DNL Dynamic Media] URL](https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) を使用してリアルタイムにレイヤーの位置やサイズを変更し、コンテンツを更新します。

主な機能は次のとおりです。

* **[!DNL Dynamic Media]WYSIWYG テンプレートエディター：** 画像レイヤーとテキストレイヤーを使用してカスタマイズ可能なバナーを作成します。
* **レイヤーのパラメーター化：**&#x200B;レイヤーの動的なキーと値のペアを定義して、リアルタイム更新を実現します。
* **[!DNL Dynamic Media]URL サポート：** テンプレートに [!DNL Dynamic Media] URL を使用して、ファーストパーティアプリケーションまたはサードパーティアプリケーションからパーソナライズされた値を統合します。
* **レイヤー表示コントロール：**&#x200B;必要に応じて、レイヤーを動的に非表示または表示します。
* **スマートテキストのサイズ変更：**&#x200B;指定された領域に合わせて、テキストのサイズを自動的に調整します。

[!DNL Dynamic Media] のテンプレートの主なメリットには、次のようなものがあります。

* **1:1 パーソナライゼーションを最適化：**&#x200B;リアルタイムの顧客シグナルに合わせて、コンテンツを調整します。
* **手作業を削減：**&#x200B;コンテンツの作成と管理を自動化および高速化します。
* **一貫したオムニチャネルエクスペリエンスを確保：**&#x200B;チャネル全体でブランドの一貫性を維持します。
* **コンテンツを効果的に再利用：** 1 回使用のコンテンツを避け、動的なパラメーター化されたテンプレートを使用して拡大します。
* **リスクを軽減：**&#x200B;価格、割引、リンクをリアルタイムで更新します。
* **顧客エンゲージメントを強化：**&#x200B;インタラクティブでコンテキストに関連のあるエクスペリエンスを推進します。

>[!NOTE]
>
>セキュリティ強化 SKU を購読しているお客様は、[!DNL Dynamic Media] テンプレートを含む [!DNL Dynamic Media] の機能を Cloud Services プログラムで使用できません。

## 始める前に{#prerequisites-for-dynamic-media-wysiwyg-template}

[!DNL Dynamic Media] テンプレートを作成するには、次の条件を満たす必要があります。

1. [!DNL Dynamic Media] へのアクセス。
1. [ インスタンスで使用可能な画像を  [!DNL AEM Assets]  で同期して  [!DNL Dynamic Media]  テンプレートの作成に使用 ](/help/assets/dynamic-media/config-dm.md)
1. タッチ UI で次の内容を確認しました。
   * **[!UICONTROL [!DNL Dynamic Media] 設定を編集ページ]****[!UICONTROL [!DNL Dynamic Media]で、同期モード]** が **[!UICONTROL デフォルトで無効]** に設定されている場合、すべてのAEM フォルダーに適用されるわけではありません（**[!UICONTROL すべてのコンテンツを同期]** がオフになっています）。 詳しくは、[Dynamic Media Cloud Service の設定](/help/assets/dynamic-media/config-dm.md)を参照してください。
   * 作成後 **[!UICONTROL [!DNL Dynamic Media]テンプレートを保存する宛先フォルダーまたはサブフォルダーに対して、同期モード]** が **[!UICONTROL サブフォルダーに対して有効にする]** に設定されています。 詳しくは、[Cloud Serviceの設定  [!DNL Dynamic Media] ](/help/assets/dynamic-media/config-dm.md) を参照してください。

## WYSIWYG テンプレート [!DNL Dynamic Media] 作成{#how-to-create-dynamic-media-wysiwyg-template}

[!DNL Dynamic Media] テンプレートを作成するには、次の手順を実行します。

1. [!DNL Assets View] に移動し、![Assets[4}Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) で「フォルダーを作成 ]**します。 ](/help/assets/assets/Asset-icon.svg)**[!UICONTROL ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** のフォルダーツリーは **[!UICONTROL Dynamic Media Assets]** にレプリケートされます。 [!DNL Dynamic Media] テンプレートをこの [!UICONTROL Dynamic Media Assets] フォルダーに保存します。
1. 「![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets ]**」を選択し、画像を [ アップロードして  [!DNL AEM]  および同時に公開 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) してテンプレートの作成に使用します  [!DNL Dynamic Media]  画像の公開は、ダウンストリームアプリケーションで使用できる、テンプレートの配信 URL を生成するために必要です。
1. [空のキャンバスを作成](#create-a-canvas)
1. [キャンバスに画像を追加](#add-images-to-the-canvas)
1. [キャンバスにテキストレイヤーを追加](#add-text-to-the-canvas)
1. [レイヤーを編集または削除](#edit-or-delete-a-layer)
1. [レイヤーをパラメーター化](#parameterise-a-layer)

### 空のキャンバスを作成{#create-a-canvas}

空のキャンバスを作成するには、次の手順を実行します。

1. [!DNL Assets View] に移動し、左側のパネルで使用可能な **[!UICONTROL Dynamic Media Assets]** を選択し、フォルダーに移動してそのフォルダーにテンプレートを保存します。

   ![Dynamic Media テンプレート](/help/assets/assets/DM-Assets1.png)

1. 「**[!UICONTROL テンプレートを作成]**」を選択します。 **[!UICONTROL 新規テンプレート]**ダイアログボックスが表示されます。
   ![ リアルタイムでカスタマイズできる動的テンプレートの作成方法 ](/help/assets/assets/new-template.png)
   >[!NOTE]
   >
   >  テンプレートは、作成した場所に保存されます。 ホ [!DNL Assets View] ムページで **[!UICONTROL Dynamic Media Assets]** を選択し、**[!UICONTROL テンプレートを作成]** をクリックして、**[!UICONTROL Dynamic Media Assets]** ルートフォルダーにテンプレートを保存します。

1. テンプレート名を指定し、キャンバスの幅と高さを定義して、「**[!UICONTROL 作成]**」をクリックします。空白のキャンバスが表示され、テンプレートの作成に使用するメニューオプションが両側に表示されます。メニューオプションにポインタを合わせると、ツールチップが表示されます。
   ![リアルタイムのカスタマイズ可能なテンプレート](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > 許容される幅と高さの範囲は 50～5000 です。

**右側のパネルのメニューオプション：**&#x200B;これらのオプションを使用して、必要な画像とテキストレイヤーをキャンバスに追加します。

* ![DM テンプレート](/help/assets/assets/add-image.svg)：クリックして、画像をキャンバスに追加します。
* ![カスタマイズ可能なテンプレート](/help/assets/assets/add-text.svg)：クリックして、テキストをキャンバスに追加します。
* ![カスタマイズ可能なテンプレート](/help/assets/assets/show-layers-list.svg)：クリックして、キャンバス上のすべてのレイヤー（画像とテキスト）のリストを表示します。キャンバスに追加されたすべての画像とテキストは、個別のレイヤーとして表されます。

**左側のウィンドウのメニューオプション：** これらのオプションは、次の一般的なエディターアクションに使用します。

* ![DM テンプレート ](/help/assets/assets/layer-selector.svg): ![DM テンプレート ](/help/assets/assets/layer-selector.svg) を選択し、キャンバス上のレイヤーをクリックして選択します。
* ![ カスタマイズをサポートするテンプレート ](/help/assets/assets/bring-forward.svg): クリック ![ カスタマイズをサポートするテンプレート ](/help/assets/assets/bring-forward.svg) またはキーボードショートカット **Ctrl** + **]** （Windows）または **Cmd** + **]** （Mac）を使用して、選択したレイヤーを前面に移動します。
* ![ 簡単にカスタマイズできるテンプレートを作成する方法 ](/help/assets/assets/send-backward.svg): ![ 簡単にカスタマイズできるテンプレートを作成する方法 ](/help/assets/assets/send-backward.svg) をクリックするか、キーボードショートカット、**Ctrl** + **[** （Windows）または **Cmd** + **[** （Mac））を使用して、選択したレイヤーを後方に移動します。
* ![ すぐにカスタマイズできるテンプレートを作成 ](/help/assets/assets/undo.svg):「![ すぐにカスタマイズできるテンプレートを作成 ](/help/assets/assets/undo.svg)」をクリックするか、キーボードショートカットを使用して、**Ctrl**+**Z** （Windows）または **Cmd**+**Z** （Mac）を使用して最後の操作を元に戻します。
* ![ テンプレートを使用して横断幕をすばやく作成 ](/help/assets/assets/redo.svg):![ テンプレートをクリックして横断幕をすばやく作成 ](/help/assets/assets/redo.svg) するか、キーボードショートカット **Ctrl** + **Y** （Windows）または **Cmd** + **Y** （Mac）を使用して最後の操作をやり直します。
* ![ テンプレートを使用すると、チラシをすばやく作成できます ](/help/assets/assets/zoom-in.svg):![ テンプレートをクリックすると ](/help/assets/assets/zoom-in.svg) チラシをすばやく作成できます。または、キーボードショートカット **Ctrl** + **+** （Windows）または **Cmd** + **+** （Mac）を使用してキャンバスをズームします。
* ![ テンプレートを使用して横断幕をすばやく作成 ](/help/assets/assets/Zoom-out.svg):![ テンプレートをクリックして横断幕をすばやく作成するか ](/help/assets/assets/Zoom-out.svg) キーボードショートカット **Ctrl** + **-** （Windows）または **Cmd** + **-** （Mac）を使用してキャンバスをズームアウトします。
* テキストやプロパティが編集されていない場合は、**Backspace** キーまたは **Delete** キーを押すと、選択したレイヤーが削除されます。

![ テンプレートをクリックしてチラシをすばやく作成 ](/help/assets/assets/show-layers-list.svg)、キャンバスレイヤーでその他のオプション（![](/help/assets/assets/three-dots.svg)）を選択して、テンプレートの作成中にいつでもキャンバスの寸法を編集できます。
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> テンプレートでは、キャンバスを含めて最大 20 個のレイヤーを使用できます。

### キャンバスに画像を追加{#add-images-to-the-canvas}

キャンバスに画像を追加するには、次の手順を実行します。

1. ![ すぐにバナーを作成 ](/help/assets/assets/add-image.svg) をクリックして [ アセットセレクター ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector) パネルを開きます。 このパネルには、[!DNL Dynamic Media] に同期されたAEM Assets インスタンス内の画像が表示されます。
1. パネルを参照するか、検索バーでキーワードを使用して、特定の画像を見つけます。
1. 画像をキャンバス上にドラッグ＆ドロップして使用します。キャンバス上のレイヤーのサイズ変更や再配置について詳しくは、[**[!UICONTROL プロパティパネル]**](#reposition-resize-delete-a-layer)を参照してください。
   ![数秒以内にバナーを作成](/help/assets/assets/add-image-to-canvas.png)

### キャンバスにテキストレイヤーを追加{#add-text-to-the-canvas}

キャンバスにテキストレイヤーを追加するには、次の手順を実行します。

1. 「![新しいバナーをすばやく作成](/help/assets/assets/add-text.svg)」をクリックして、キャンバスにテキストレイヤーを追加し、プロパティパネルを開きます。
1. レイヤーを選択し、テキストをクリックして更新します。
1. プロパティパネルの「**[!UICONTROL スマートテキストのサイズ変更]**」を選択すると、指定した領域に最適に収まるようにテキストの長さとフォントサイズが自動的に調整されます。
   ![カスタマイズ可能な最適なバナー](/help/assets/assets/add-text-layer.png)

レイヤーの再配置、サイズ変更、回転または削除について詳しくは、[**[!UICONTROL プロパティパネル]**](#reposition-resize-delete-a-layer)を参照してください。パネルの「**[!UICONTROL テキスト]**」セクションの下にあるそれぞれのフィールドの値を変更して、必要なフォント、サイズ、色、スタイル、配置（レイヤー内）にテキストを書式設定します。

>[!NOTE]
>
> デフォルトのAdobe Sans F2 フォントファミリー以外のフォントを使用するには、フォントファイルをアップロードして ]0}Assets} および [!DNL Dynamic Media] に公開する必要があります。 [!AEM インスタンスに古いフォントがある場合、テンプレートエディターで表示するには、必ず[再処理](/help/assets/reprocessing-assets-view.md)します。

### レイヤーを編集または削除 {#edit-or-delete-a-layer}

キャンバスレイヤーを編集または削除するには、次の手順を実行します。

1. 「![動的更新をサポートするテンプレート](/help/assets/assets/show-layers-list.svg)」をクリックして、キャンバスまたはレイヤーリストからレイヤーを選択します。
1. 「**[!UICONTROL その他のオプション]**」（![リアルタイムの更新をサポートするテンプレート](/help/assets/assets/three-dots.svg)）をクリックして、レイヤーを編集または削除します。
1. 「**[!UICONTROL 削除]**」をクリックして、レイヤーを削除します。
1. 「**[!UICONTROL 編集]**」をクリックして、[**[!UICONTROL プロパティパネル]**](#reposition-resize-delete-a-layer)を使用してレイヤーを編集します。
   ![迅速なバナー作成](/help/assets/assets/dm-templates/edit-delete-layer.png)

### プロパティパネル{#properties-panel}

レイヤーのプロパティパネルに移動するには：

1. 「![迅速なコンテンツ作成](/help/assets/assets/show-layers-list.svg)」をクリックします。
1. リストからレイヤーを選択します。

このパネルには、キャンバスプレーン上のレイヤーの中心点の位置（X 値と Y 値）とレイヤーの寸法（幅と高さ）が、テキストの書式設定オプションと共に表示されます。

![迅速なコンテンツ作成](/help/assets/assets/properties-panel.png)

レイヤーのプロパティパネルからキャンバス上の別のレイヤーを選択して、そのプロパティパネルに移動します。


#### レイヤーの再配置、サイズ変更、回転または削除{#reposition-resize-delete-a-layer}

テキストまたは画像レイヤーを編集するには、次の一般的なレイヤー編集アクションを参照してください。

* **レイヤーを再配置：**&#x200B;レイヤーをドラッグして、キャンバス上の任意の場所に移動します。このアクションにより、プロパティパネルの X 値と Y 値が更新されます。
* **レイヤーをサイズ変更：**&#x200B;レイヤーを選択し、エッジハンドルをドラッグしてサイズ変更します。このアクションにより、プロパティパネルの W（幅）値と H（高さ）値が更新されます。
* **レイヤーを回転：**&#x200B;レイヤーの上に垂直に配置された正方形のハンドルをドラッグして、レイヤーを中心に回転させます。このアクションにより、プロパティパネルの角度値が更新されます。
* **レイヤーを削除**：**Backspace** キーまたは **Delete** キーを押し、「**[!UICONTROL 確認]**」をクリックして、選択したレイヤーを削除します。

#### テキストの書式設定オプション{#text-formatting-options-on-properties-panel}

パネルの「**[!UICONTROL テキスト]**」セクションの下にあるそれぞれのフィールドの値を変更して、必要なフォント、サイズ、色、スタイル、配置（レイヤー内）にテキストを書式設定します。
**[!UICONTROL スマートテキストのサイズ変更]** を必ず含めてください。 [!UICONTROL  スマートテキストのサイズ変更 ] は、[ 自動調整 ](https://experienceleague.adobe.com/ja/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting) アルゴリズムを使用してテキスト領域のテキストを最適に埋め込み、テキストのオーバーフローを防いで、テキスト下部の余分なスペースを最小限に抑えます。

![すぐにコンテンツを作成](/help/assets/assets/smart-text-resize.png)

### レイヤーをパラメーター化 {#parameterise-a-layer}

複数の画像とテキストのレイヤーを含むテンプレートを作成したら、選択したレイヤーをパラメーター化します。レイヤーまたはそのプロパティをパラメーター化すると、キーと値のペア（パラメーターとも呼ばれる）が取得されます。このパラメーターをテンプレートの URL に含めると、レイヤーの位置、サイズまたはコンテンツをリアルタイムで更新できるので、テンプレートのカスタマイズをすぐに行うことができます。

レイヤーをパラメーター化するには：

1. 「![即時コンテンツ作成](/help/assets/assets/show-layers-list.svg)」をクリックし、レイヤーを選択して「**[!UICONTROL パラメーター]**」をクリックします。**[!UICONTROL パラメーター]**&#x200B;パネルが表示されます。
1. **[!UICONTROL パラメーターを含める]**&#x200B;を切り替えて、プロパティをパラメーター化します。パラメーター化後のプロパティの動作については、[ パラメーターパネルオプション ](#parameterisation-options-or-allowed-parameters) を参照してください。
1. **オプション：**&#x200B;パラメーター名を変更します。パラメーター名には、レイヤー名の後に接尾辞が続きます。選択したレイヤーでは、そのすべてのパラメーター化されたプロパティは同じレイヤー名を共有し、その後に様々な接尾辞が続きます。セマンティックの命名規則に従ってレイヤー名を変更すると、URL にパラメーターを含める際に、パラメーター名自体がレイヤーのコンテンツや目的についての説明となります。
1. 「**[!UICONTROL 保存]**」をクリックします。
   ![即時コンテンツ作成](/help/assets/assets/parameterise-a-layer.png)
画像とテキストレイヤーのパラメーターパネルを切り替えるには、キャンバス上でレイヤーを選択し、「**[!UICONTROL パラメーター]**」をクリックします。

#### パラメーターパネルオプション {#parameterisation-options-or-allowed-parameters}

パラメーター化されたプロパティをテンプレートの URL に URL パラメーターとして含めることで、URL を使用してテンプレートをリアルタイムで編集できます。

**画像パラメーター：**

**[!UICONTROL X]:** URL のパラメーターの値を変更することで、テンプレート平面の X 軸に平行な中心線に沿ってレイヤーを水平方向に移動するには、このプロパティを含めます。
**[!UICONTROL Y]:** URL のパラメーターの値を変更することで、テンプレート平面の Y 軸に平行な中心線に沿ってレイヤーを垂直に移動するには、これを含めます。
**[!UICONTROL 幅 ]:** URL のパラメーターの値を変更してレイヤーの幅を調整する場合に含めます。
**[!UICONTROL 高さ ]:**URL のパラメーターの値を変更してレイヤーの高さを調整する場合に含めます。
**[!UICONTROL 非表示 ]:**0 （表示）と 1 （非表示）を使用して、テンプレート内のレイヤーの表示と非表示を切り替えるには、含めます。
**[!UICONTROL Source]:** URL のパラメーターの値の画像パスを変更することで、レイヤーの画像を新しい画像に置き換える場合に含めます。

**テキストの書式設定パラメーター：**

URL のパラメーター値を更新して、URL からテキスト、フォント、カラー、サイズを編集するには、以下のパラメーターを含めます。

**[!UICONTROL テキスト ]:**URL からテキストを更新する場合に含めます。
**[!UICONTROL フォントファミリー ]:**URL からテキストのフォントを更新する場合に含めます。
**[!UICONTROL フォントサイズ ]:**URL からテキストのフォントサイズを更新する場合に含めます。
**[!UICONTROL テキストカラー ]:** URL からテキストのフォントカラーを更新する場合に含めます。

### レイヤーをグループ化して同時に表示をコントロール{#group-layers}

テンプレートの柔軟性を維持するもう 1 つの方法は、単一のパラメーター名を使用して複数のレイヤーを制御することです。この戦略は、表示（レイヤーを非表示または表示）パラメーターで、単一のテンプレートからデザインまたはグラフィックを更新する場合に役立ちます。

複数のレイヤーの非表示パラメーター（![高速コンテンツ作成](/help/assets/assets/Visibility-icon.svg)）に同じ名前を割り当て、同時に非表示または表示できるようにするには、次の手順に従います。

1. レイヤーの[**[!UICONTROL プロパティパネル]**](#parameterise-a-layer)に移動します。
1. 以前にパラメーター化していない場合は、**[!UICONTROL 非表示]**&#x200B;パラメーターを切り替えます。
1. **オプション：** **[!UICONTROL Hide]** パラメーターの名前を変更します。
1. **[!UICONTROL 非表示]** パラメーター名をコピーします。
1. キャンバスから他のレイヤーを選択して、そのレイヤーのパラメーターパネルに移動し、パラメーター化されていない場合は、**[!UICONTROL 非表示]**&#x200B;パラメーターを切り替えます。
1. **[!UICONTROL 非表示パラメーター]**&#x200B;の名前を、コピーした名前に置き換えます。
1. 「**[!UICONTROL 保存]**」をクリックして、レイヤーをグループ化します。
1. [**[!UICONTROL プレビューと公開]**](#preview-and-publish-template-and-copy-template-deliver-url)の節の手順 3 と 4 を実行して、変更を確認します。

## テンプレートをプレビューおよび公開し、配信 URL をコピー{#preview-and-publish-template-and-copy-template-deliver-url}

テンプレートをプレビューおよび公開し、配信 URL をコピーするには、次の手順を実行します。

1. キャンバスページで、「**[!UICONTROL プレビュー]**」をクリックします。また、**[!UICONTROL アセットビュー]****／****[!UICONTROL Dynamic Media アセット]****に移動して、**&#x200B;テンプレートを見つけて選択し&#x200B;**、**「**[!UICONTROL テンプレートを編集]**」をクリックして&#x200B;**、**「**[!UICONTROL プレビュー]**」をクリックすることもできます。プレビューページには、テンプレート、そのパラメーター（パラメーター化されたレイヤとプロパティ）、公開ステータスおよび「**[!UICONTROL 公開]**」オプションが表示されます。
1. **[!UICONTROL テンプレートパラメーター]**&#x200B;パネルからパラメーターを選択して値を編集すると、プレビューの対応するテンプレートレイヤーのコンテンツ、サイズ、位置、またはテキストの書式設定が即座に更新されます。例：
   1. テキストレイヤーを選択してテキストを編集するか、
   1. 画像レイヤーを選択し、「![その場でコンテンツを作成](/help/assets/assets/add-image.svg)」をクリックし、アセットセレクターから画像を選択して、「**[!UICONTROL 更新]**」をクリックします。

   テンプレートはすぐに更新され、編集されたテキストが表示され、以前の画像が新しい画像に置き換えられます。また、画像パラメーターの値には、新しい画像のパスが反映されます。同様に、レイヤーの値を調整してサイズ変更すると、その変更がリアルタイムでテンプレートに適用されます。
1. リストから **[!UICONTROL グループ化されたレイヤー ](#group-layers) の [ 非表示]** パラメーターを選択して、テンプレート内でそれらを表示または非表示にします。
1. **オプション：****[!UICONTROL 非表示]**&#x200B;パラメーターの値を 0 と 1 の間で変更し、「**[!UICONTROL 更新]**」をクリックして変更を確認します。同じ **[!UICONTROL Hide]** パラメーターを持つレイヤーは、非表示または同時に表示されます。 同様に、URL からレイヤーの表示をコントロールできます。

   ![その場でのコンテンツの作成](/help/assets/assets/dm-templates-publish-status.png)
また、**[!UICONTROL すべてのパラメーターを含める]**を切り替えて、表示されているすべてのパラメーター値を編集し、テンプレートのプレビューで更新を確認することもできます。
   <br>
1. プレビューページでテンプレートを公開するには、「**[!UICONTROL 公開]**」をクリックして公開を確定します。**[!UICONTROL 公開完了]** メッセージが表示され、公開ステータスが **[!UICONTROL 公開済み]** に更新されます。

>[!NOTE]
>
>テンプレートを公開するには、まずテンプレート画像を公開する必要があります。

### 配信 URL をコピー

**[!UICONTROL プレビュー]**&#x200B;ページで選択したパラメーターは、テンプレートの URL の URL パラメーターになります。

プレビューに表示されている公開済みテンプレートの URL をコピーするには：

1. 「**[!UICONTROL URL をコピー]**」をクリックします。**[!UICONTROL URL をコピー]**&#x200B;ダイアログボックスが表示されます。表示されている URL を選択してコピーします。URL の最初のパラメーターが疑問符 **（[!UICONTROL ?]）** キーと値のペアは **[!UICONTROL $]** で始まり、**[!UICONTROL &amp;]** で終わります。 キーと値は等号 **（[!UICONTROL =]）** で区切られ、キーは左側、値は右側に表示されます。
1. この URL をブラウザーのタブにペーストして、ライブテンプレートを表示します。**プレビューと公開**&#x200B;の節の[手順 2](#preview-and-publish-template-and-copy-template-deliver-url) の説明に従って、URL の必要なパラメーターの値（キーの値）を直接更新して、テンプレートをリアルタイムでカスタマイズします。
1. 製品やサービスの迅速なマーチャンダイジングには、この URL を使用します。この URL を顧客と共有することや、web サイトやダウンストリームのサードパーティアプリケーションに統合してバナーを表示することや、継続的なオファーを反映するようにリアルタイムで更新することができます。

このビデオでは、[!DNL Dynamic Media] テンプレートの作成方法を手順を追って説明します。
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## URL からテンプレートをリアルタイムで更新{#update-the-template-from-the-url}

URL 内でパラメーターを直接編集するのは面倒な場合があります。簡素化するには：

1. URL をコピーして、メモ帳にペーストします。
1. Cmd + F キー（Mac）または Ctrl + F キー（Windows）を使用して、パラメーター値を見つけて編集します。例：
   * 画像レイヤーの画像パスを検索して置換します。
   * レイヤーの [ パラメーター化 ](#parameterise-a-layer) 座標、幅および高さを検索して、値を調整します。
   * テキストレイヤーのテキスト、フォント、カラー、サイズ、位置を編集します。
   * 表示値を 0 と 1 の間で変更します。

この更新された URL をブラウザーにペーストして、変更を表示します。

## テンプレートを編集{#edit-the-template}

テンプレートを編集するには、次の手順に従います。

1. [!DNL Assets view] で、「**[!UICONTROL Dynamic Media Assets]**」をクリックします。
2. テンプレートの場所に移動します。
3. テンプレートを選択します。
4. 「**[!UICONTROL テンプレートを編集]**」をクリックします。テンプレートキャンバスには、テンプレートと、レイヤーパネル内のすべてのレイヤーのリストが表示されます。必要に応じて、テンプレートの編集を開始します。

## テンプレートレイヤーにコールトゥアクション（CTA）リンクを追加します{#add-CTA-in-dynamic-media-templates}

[!DNL Dynamic Media] テンプレートにターゲットページに誘導するCTA リンクを追加して、テンプレートの画像やテキストレイヤーをハイパーリンクに変換します。 レイヤーにCTA リンクを追加するには、次の手順を実行します。

1. テンプレートの場所に移動してテンプレートを選択し、![ 編集 ](/help/assets/assets/edit-pen-icon.svg)**[!UICONTROL テンプレートを編集]** をクリックします。 テンプレートがキャンバスに表示されます。
1. テンプレートレイヤーを選択し [ そのプロパティパネルに移動 ](#edit-or-delete-a-layer)、そこにCTA リンクを追加します。
1. プロパティパネルで「**[!UICONTROL CTAを追加]**」を選択し、「**[!UICONTROL URL]**」フィールドに公開先 URL を指定して、「**[!UICONTROL 保存]**」をクリックします。

   ![CTAを追加 ](/help/assets/assets/add-cta.png)

1. **[!UICONTROL プレビュー]** をクリックして、テンプレートをプレビューし、定義されたパラメーターを確認します。
1. **[!UICONTROL 公開]** をクリックし、**[!UICONTROL はい]** を選択してテンプレートを公開します（まだ公開していない場合）。
1. このテンプレートが保存されているフォルダーに移動し、このテンプレートを選択して ![ 詳細ページ ](/help/assets/assets/details-page-icon.svg)**[!UICONTROL 詳細]** をクリックします。
1. **[!UICONTROL コピーオプション]** をクリックし、「**[!UICONTROL 埋め込みコードをコピー]**」を選択します。

   ![ 埋め込みコードのコピー ](/help/assets/assets/copy-options1.png)

   埋め込みコードの例を次に示します。

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    </map>
    </div>
   ```

1. コピーした埋め込みコードをサイトのHTML ファイルに追加し、ブラウザーで実行してテンプレートを表示します。

テンプレートのCTA要素をクリックして、移動先ページに移動します。

テンプレートレイヤーにCTA リンクを追加する方法については、この手順のビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## 重要な注意点 {#important-points-to-note}

* 動的更新用にパラメーター化された画像レイヤーを含むテンプレートを作成したら、今後の更新を予定している画像がパラメーター化された画像と同じ寸法を共有していることを確認します。これにより、画像がオーバーフローしたり、空のスペースが残ったりすることなく、レイヤー内に完全に収まります。現在、テンプレートは、画像をレイヤーに収める自動寸法調整をサポートしていません。
* テキストレイヤーでは、部分文字列はサポートされません。ユーザーは、テキストレイヤーの部分文字列に異なるフォントプロパティを適用できません。
* 現在、[!DNL Dynamic Media] テンプレートでは複数の [!DNL Dynamic Media] 会社をサポートしていません。
* コピーまたは移動の場合、宛先セレクターにすべてのフォルダー（[!DNL Dynamic Media] 以外の同期フォルダーを含む）が表示されます。 また、現在のところ、[!DNL Dynamic Media] テンプレートアセットは表示されません（どちらも宛先セレクターの制限です）。
* Assets セクションからフォルダー（公開、削除など）に対して行う更新処理は、そのフォルダー内で使用可能な [!DNL Dynamic Media] テンプレートに影響します。
* ごみ箱は、[!DNL Dynamic Media] のテンプレートでは機能しません。 アセットがごみ箱に移動された後に復元された場合、そのアセットはAEMで復元されますが、[!DNL Dynamic Media] では復元されません。 同じことが [!DNL Dynamic Media] テンプレートにも有効です。

## 関連トピック

1. [[!DNL Dynamic Media]  とその機能 ](/help/assets/dynamic-media/dynamic-media.md) を探索
1. [[!DNL Dynamic Media] OpenAPI 機能を使用 ](/help/assets/dynamic-media-open-apis-overview.md) て
