---
title: Dynamic Media テンプレートの管理方法
description: Dynamic Media テンプレートエディターを使用してWYSIWYG テンプレートを作成し、複数の画像やテキストレイヤーを含めて、バナーやチラシをすばやく作成して下流のアプリケーションで使用する方法を説明します。
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: f5fa8f1f23d35d239f7bb0e22e104627f9f84317
workflow-type: tm+mt
source-wordcount: '2722'
ht-degree: 0%

---

# Dynamic Media テンプレート{#dynamic-media-templates}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

Dynamic Media テンプレートエディターを使用してWYSIWYG テンプレートを作成し、複数の画像とテキストレイヤーを含めることで、バナーやチラシをすばやく作成してダウンストリームのアプリケーションで使用できます。 また、テンプレートに含まれる画像レイヤーやテキストレイヤーにパラメーターを追加し、[Dynamic Media URL](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) を使用して、これらのレイヤーの値をリアルタイムで更新することもできます。

主な機能の一部を次に示します。

* **Dynamic Media WYSIWYG テンプレートエディター：** 画像レイヤーとテキストレイヤーを使用して、カスタマイズ可能なバナーを作成します。
* **レイヤーパラメーター化：** レイヤーの動的キー値ペアを定義して、リアルタイムの更新を可能にします。
* **Dynamic Media URL のサポート：** テンプレートにDynamic Media URL を使用し、ファーストパーティアプリケーションまたはサードパーティアプリケーションからパーソナライズされた値を統合します。
* **レイヤ表示コントロール：** 必要に応じて、レイヤをダイナミックに非表示または表示します。
* **スマートテキストのサイズ変更：** 指定された領域に合わせて、テキストのサイズを自動的に調整します。

Dynamic Media テンプレートの主なメリットには、次のようなものがあります。

* **1:1 の最適化Personalization:** リアルタイムの顧客シグナルに合わせてコンテンツを調整します。
* **手作業の削減：** コンテンツの作成と管理を自動化および迅速化します。
* **一貫したオムニチャネルエクスペリエンスの確保：** チャネル間でブランドの一貫性を維持します。
* **コンテンツを効果的に再利用：** 動的でパラメーター化されたテンプレートを使用すると、コンテンツを 1 回使用するのを避け、拡大することができます。
* **リスクの軽減：** 価格、割引、リンクをリアルタイムで更新します。
* **顧客エンゲージメントの強化：** 文脈的に関連性の高いインタラクティブなエクスペリエンスを促進します。

>[!NOTE]
>
>セキュリティ強化 SKU を購読しているお客様は、Dynamic Media テンプレートを含むDynamic Media機能をCloud Serviceプログラムで使用できません。

## 始める前に{#prerequisites-for-dynamic-media-wysiwyg-template}

Dynamic Mediaテンプレートを作成するには、次の要件を満たす必要があります。

1. Dynamic Mediaへのアクセス。
1. [AEM Assets インスタンスで使用可能な画像をDynamic Mediaと同期して、テンプレートの作成に使用します ](/help/assets/dynamic-media/config-dm.md)。

## Dynamic Media WYSIWYG テンプレートの作成{#how-to-create-dynamic-media-wysiwyg-template}

DM テンプレートを作成するには、次の手順に従います。

1. [空のキャンバスの作成](#create-a-canvas)
1. [キャンバスへの画像の追加](#add-images-to-the-canvas)
1. [キャンバスへのテキストレイヤーの追加](#add-text-to-the-canvas)
1. [レイヤーの編集または削除](#edit-or-delete-a-layer)
1. [パラメーターレイヤー](#parameterise-a-layer)

### 空のキャンバスの作成{#create-a-canvas}

空のキャンバスを作成するには、次の手順を実行します。

1. Assets ビューに移動し、左側のパネルで使用可能な **[!UICONTROL Dynamic Media Assets]** をクリックします。

   ![Dynamic Media テンプレート ](/help/assets/assets/dm-templates/DM-Assets1.png)

1. **[!UICONTROL テンプレートを作成]** をクリックして、Dynamic Media Assetsの下にテンプレートを保存するか、フォルダーに移動して **[!UICONTROL テンプレートを作成]** をクリックします。 **[!UICONTROL 新規テンプレート]** ダイアログボックスが表示されます。
   ![ リアルタイムでカスタマイズできる動的テンプレートの作成方法 ](/help/assets/assets/dm-templates/new-template.png)
[ フォルダーを作成 ](/help/assets/add-delete-assets-view.md) するには、**[!UICONTROL Dynamic Media AssetsAssets]** の下にフォルダーを作成します ]**。**[!UICONTROL **[!UICONTROL Assets]** の下のフォルダーツリーは、**[!UICONTROL Dynamic Media Assets]** の下に複製されます。
1. テンプレート名を指定し、キャンバスの幅と高さを定義して、「**[!UICONTROL 作成]**」をクリックします。 テンプレートの作成に使用するメニューオプションが両側に表示された、空のキャンバス。 メニューオプションにカーソルを合わせると、ツールチップが表示されます。
   ![ リアルタイムのカスタマイズ可能なテンプレート ](/help/assets/assets/dm-templates/blank-canvas-page.png)

>[!NOTE]
>
> 許容される幅と高さの範囲は 50 ～ 5000 です。

**右側のパネルのメニューオプション：** これらのオプションを使用して、必要な画像とテキストレイヤーをキャンバスに追加します。

* ![DM テンプレート ](/help/assets/assets/dm-templates/add-image.svg)：クリックしてキャンバスに画像を追加します。
* ![ カスタマイズ可能なテンプレート ](/help/assets/assets/dm-templates/add-text.svg)：クリックしてキャンバスにテキストを追加します。
* ![ カスタマイズ可能なテンプレート ](/help/assets/assets/dm-templates/show-layers-list.svg)：クリックして、キャンバス上のすべてのレイヤー（画像とテキスト）のリストを表示します。 キャンバスに追加されたすべての画像とテキストは、個別のレイヤーとして表されます。

**左側のペインのメニューオプション：** 以下に示すように、一般的なエディターアクションにこれらのオプションを使用します。

* ![DM テンプレート ](/help/assets/assets/dm-templates/layer-selector.svg): レイヤーを選択します。
* ![ カスタマイズをサポートするテンプレート ](/help/assets/assets/dm-templates/bring-forward.svg)：クリックして、選択したレイヤーを前面に移動するか、**Ctrl** + **]** （Windows）または **Cmd** + **]** （Mac）を押します。
* ![ 簡単にカスタマイズできるテンプレートを作成する方法 ](/help/assets/assets/dm-templates/send-backward.svg)：選択したレイヤーを後ろに移動するにはクリックするか、**Ctrl** + **[** （Windows）または **Cmd** + **[** （Mac）を押します。
* ![ すぐにカスタマイズできるテンプレートを作成 ](/help/assets/assets/dm-templates/undo.svg): クリックして最後の操作を取り消すか、**Ctrl** + **Z** （Windows）または **Cmd** + **Z** （Mac）を押します。
* ![ テンプレートを使用してバナーをすばやく作成 ](/help/assets/assets/dm-templates/redo.svg)：クリックして最後の操作をやり直すか、**Ctrl** + **Y** （Windows）または **Cmd** + **Y** （Mac）を押します。
* ![ テンプレートを使用してチラシをすばやく作成 ](/help/assets/assets/dm-templates/zoomin.svg)：クリックしてカンバスをズームするか、**Ctrl** + **+** （Windows）または Cmd + **+** （Mac）を押します。
* ![ テンプレートを使用して横断幕をすばやく作成 ](/help/assets/assets/dm-templates/zoomout.svg)：クリックしてキャンバスをズームアウトするか、**Ctrl** + **-** （Windows）または **Cmd** + **-** （Mac）を押します。
* テキストまたはプロパティが編集されていない場合に、選択したレイヤーを削除するには、**Backspace** または **delete** を押します。

![ テンプレートをクリックすると ](/help/assets/assets/dm-templates/show-layers-list.svg) チラシをすばやく作成できます **> キャンバスレイヤーにさらにオプション（![](/help/assets/assets/dm-templates/three-dots.svg)）を** 加すると、テンプレートの作成中にいつでもキャンバスの寸法を編集できます。
![](/help/assets/assets/dm-templates/edit-canvas1.png)

>[!NOTE]
>
> テンプレートでは、キャンバスを含めて最大 20 個のレイヤーを使用できます。

### キャンバスへの画像の追加{#add-images-to-the-canvas}

以下の手順を実行して、キャンバスに画像を追加します。

1. ![ バナーをすぐに作成 ](/help/assets/assets/dm-templates/add-image.svg) をクリックして [ アセットセレクター ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector) パネルを表示します。 パネルには、Dynamic Mediaに同期されたAEM Assets インスタンス内の画像が表示されます。
1. パネルを参照するか、検索バーのキーワードを使用して、特定の画像を検索します。
1. 画像をキャンバスにドラッグ&amp;ドロップして使用します。 キャンバス上のレイヤーのサイズ変更や再配置については、[**[!UICONTROL  プロパティパネル ]**](#reposition-resize-delete-a-layer) を参照してください。
   ![ 秒以内にバナーを作成 ](/help/assets/assets/dm-templates/add-image-to-canvas.png)

### キャンバスへのテキストレイヤーの追加{#add-text-to-the-canvas}

以下の手順を実行して、キャンバスにテキストレイヤーを追加します。

1. ![ 新しいバナーを fastly で作成 ](/help/assets/assets/dm-templates/add-text.svg) をクリックしてテキストレイヤーをキャンバスに追加し、プロパティパネルを開きます。
1. レイヤーを選択し、テキストをクリックして更新します。
1. プロパティパネルで **[!UICONTROL スマートテキストサイズ変更]** を有効にして、指定した領域に最適に収まるようにテキストの長さとフォントサイズを自動的に調整します。
   ![ カスタマイズ可能な最適なバナー ](/help/assets/assets/dm-templates/add-text-layer.png)

[**[!UICONTROL  プロパティパネル ]**](#reposition-resize-delete-a-layer) を参照して、レイヤーの再配置、サイズ変更、回転、削除を行います。 パネルの「**[!UICONTROL テキスト]**」セクションの下にあるそれぞれのフィールドの値を変更して、目的のフォント、サイズ、色、スタイル、配置（レイヤー内）にテキストを書式設定します。

>[!NOTE]
>
> デフォルトのAdobe Sans F2 フォントファミリー以外のフォントを使用するには、フォントファイルをAEM AssetsとDynamic Mediaにアップロードして公開する必要があります。 インスタンスに古いフォントがある場合は、テンプレートエディターに表示するために ](/help/assets/reprocessing-assets-view.md) 再処理 [ してください。

### レイヤーの編集または削除 {#edit-or-delete-a-layer}

キャンバスレイヤーを編集または削除するには、以下の手順を実行します。

1. ![ 動的更新をサポートするテンプレート ](/help/assets/assets/dm-templates/show-layers-list.svg) をクリックし、キャンバスまたはレイヤーリストからレイヤーを選択します。
1. **その他のオプション** （![ リアルタイムの更新をサポートするテンプレート ](/help/assets/assets/dm-templates/three-dots.svg)）をクリックして、レイヤーを編集または削除します。
1. **[!UICONTROL 削除]** をクリックして、レイヤーを削除します。
1. **[!UICONTROL 編集]** をクリックし、[**[!UICONTROL  プロパティパネル ]**](#reposition-resize-delete-a-layer) を使用してレイヤーを編集します。
   ![ バナーの迅速な作成 ](/help/assets/assets/dm-templates/edit-delete-layer.png)

### プロパティパネル{#properties-panel}

レイヤーのプロパティパネルに移動するには：

1. ![ コンテンツの迅速な作成 ](/help/assets/assets/dm-templates/show-layers-list.svg) をクリックします。
1. リストから画層を選択します。

このパネルには、キャンバスプレーン上のレイヤーの中心点の位置（X 値と Y 値）、レイヤーの寸法（幅と高さ）がテキストフォーマットオプションと共に表示されます。

![ コンテンツの迅速な作成 ](/help/assets/assets/dm-templates/properties-panel.png)

レイヤーのプロパティパネルで、キャンバス上の別のレイヤーを選択して、そのプロパティパネルに移動します。


#### レイヤーの再配置、サイズ変更、回転、削除{#reposition-resize-delete-a-layer}

テキストまたは画像レイヤーを編集するための一般的なレイヤー編集アクションを次に示します。

* **レイヤーの位置を変更：** レイヤーをドラッグしてキャンバス上の任意の場所に移動します。 プロパティパネルの X と Y の値を更新します。
* **レイヤーのサイズを変更：** レイヤーを選択し、エッジハンドルをドラッグしてサイズを変更します。 プロパティパネルの W （幅）と H （高さ）の値が更新されます。
* **レイヤーを回転：** レイヤーの上に配置された正方形のハンドルをドラッグして、レイヤーを中心に回転させます。 この操作により、プロパティパネルの角度の値が更新されます。
* **レイヤーを削除** 選択したレイヤーを削除するには、**Backspace** または **削除** を押し、**[!UICONTROL 確認]** をクリックします。

#### テキストの書式設定オプション{#text-formatting-options-on-properties-panel}

パネルの「**[!UICONTROL テキスト]**」セクションの下にあるそれぞれのフィールドの値を変更して、目的のフォント、サイズ、色、スタイル、配置（レイヤー内）にテキストを書式設定します。

**[!UICONTROL スマートテキストのサイズ変更]** 指定した領域にテキストが収まるように、フォントサイズと長さを適切に調整して **[!UICONTROL スマートテキストのサイズ変更]** （[ 自動調整 ](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting)）を必ず含めてください。 この機能により、テキストのオーバーフローを防いだり、テキストの下部にある余分なスペースを最小限に抑えたりできます。
![ コンテンツをすぐに作成 ](/help/assets/assets/dm-templates/smart-text-resize.png)

### パラメーターレイヤー {#parameterise-a-layer}

画像とテキストの複数のレイヤーを含んだテンプレートを作成したら、選択したレイヤーのパラメーターを設定します。 レイヤーまたはそのプロパティがパラメーター化されると、キーと値のペア（パラメーターとも呼ばれます）を取得します。 このパラメーターをテンプレートの URL に含めることで、レイヤーの位置、サイズまたはコンテンツをリアルタイムで更新し、テンプレートのカスタマイズを即時に行うことができます。

レイヤーをパラメーター化するには：

1. ![ コンテンツの即時作成 ](/help/assets/assets/dm-templates/show-layers-list.svg) をクリックし、レイヤーを選択して **[!UICONTROL パラメーター]** をクリックします。 **[!UICONTROL パラメーター]** パネルが表示されます。
1. **[!UICONTROL パラメーターを含める]** を切り替えて、プロパティをパラメーター化します。 パラメーター化後のプロパティの動作については、[this](#parameterisation-options-or-allowed-parameters) を参照してください。
1. **オプション：** パラメーター名を変更します。 パラメーター名には、レイヤー名の後にサフィックスが付きます。 選択した画層では、すべてのパラメータ化されたプロパティが同じ画層名を共有し、その後に異なる接尾辞が続きます。 セマンティックの命名規則に従って、レイヤー名の名前を変更します。これにより、URL にパラメーターを含めると、パラメーター名 self でレイヤーのコンテンツや目的が説明されるようになります。
1. 「**[!UICONTROL 保存]**」をクリックします。
   ![ コンテンツの即時作成 ](/help/assets/assets/dm-templates/parameterise-a-layer.png)
画像レイヤーとテキストレイヤーのパラメーターパネルを切り替えるには、キャンバスでレイヤーを選択して **[!UICONTROL パラメーター]** をクリックします。

#### パラメーターパネルオプション {#parameterisation-options-or-allowed-parameters}

パラメーター化されたプロパティをテンプレート URL の URL パラメーターとして含めることで、URL を使用してリアルタイムにテンプレートを編集できます。

**画像パラメーター：**

**X:** URL のパラメーターの値を変更することで、テンプレート平面の X 軸に平行な中心線に沿ってレイヤーを水平方向に移動するには、このプロパティを含めます。
**Y:** URL のパラメーターの値を変更することで、テンプレート平面の Y 軸に平行な中心線に沿ってレイヤーを垂直に移動するには、このオプションを含めます。
**幅：**URL のパラメーターの値を変更してレイヤーの幅を調整する場合に含めます。
**高さ：**URL のパラメーターの値を変更してレイヤーの高さを調整する場合に含めます。
**非表示：**0 （表示）と 1 （非表示）を使用して、テンプレート内のレイヤーの表示と非表示を切り替えるには、「含める」をクリックします。
**Source:** URL のパラメーターの値の画像パスを変更することで、レイヤーの画像を新しい画像に置き換える場合に含めます。

**テキストフォーマットパラメーター：**

URL のパラメーター値を更新して、URL のテキスト、フォント、カラー、サイズを編集するには、以下のパラメーターを含めます。

**テキスト：**URL からテキストを更新する場合に含めます。
**フォントファミリー：**URL からテキストのフォントを更新する場合に含めます。
**フォントサイズ：**URL からテキストのフォントサイズを更新するために含めます。
**テキストカラー：** URL からテキストのフォントカラーを更新するために含めます。

### 画層をグループ化して表示/非表示を同時にコントロールする{#group-layers}

テンプレートの柔軟性を維持するもう 1 つの方法は、単一のパラメーター名を利用して複数のレイヤーを制御することです。 この方法は、表示（画層を非表示または表示）パラメータで、1 つのテンプレートからデザインまたはグラフィックスを更新する場合に役立ちます。

次の手順に従って、複数のレイヤーの非表示パラメーター（![ コンテンツの高速作成 ](/help/assets/assets/dm-templates/Visibility-icon.svg)）に同じ名前を割り当てると、それらを同時に非表示または表示できます。

1. レイヤーの [**[!UICONTROL  プロパティパネル ]**](#parameterise-a-layer) に移動します。
1. 以前にパラメーター化されていない場合は、**[!UICONTROL 非表示]** パラメーターを切り替えます。
1. **オプション：** 非表示パラメーターの名前を変更します。
1. Hide Parameter の名前をコピーします。
1. 他のレイヤーをキャンバスから選択して他のレイヤーのパラメーターパネルに移動し、パラメーター化されていない場合は **[!UICONTROL 非表示]** パラメーターを切り替えます。
1. **[!UICONTROL パラメーターを非表示]** の名前を、コピーした名前に置き換えます。
1. 「**[!UICONTROL 保存]**」をクリックして、レイヤーをグループ化します。
1. 「[**[!UICONTROL  プレビューとPublish]**](#preview-and-publish-template-and-copy-template-deliver-url)」セクションの手順 3 ～ 4 を実行して、変更内容を確認します。

## テンプレートをプレビューおよび公開して、配信 URL をコピーします{#preview-and-publish-template-and-copy-template-deliver-url}

テンプレートをプレビューして公開し、配信 URL をコピーするには、次の手順を実行します。

1. キャンバスページで「**[!UICONTROL プレビュー]**」をクリックします。 また、**[!UICONTROL Assets ビュー]****>****[!UICONTROL Dynamic Media Assets]****> でテンプレートを見つけて選択**>**「**[!UICONTROL  テンプレートを編集 ]****>**「プレビュー**」をクリックします ****。 プレビューページには、テンプレート、テンプレートのパラメーター（パラメーター化されたレイヤーとプロパティ）、公開ステータス、**[!UICONTROL Publish]** オプションが表示されます。
1. **[!UICONTROL テンプレートパラメーター]** パネルからパラメーターを選択して、その値を編集し、プレビューで対応するテンプレートレイヤーのコンテンツ、サイズ、位置、テキストの書式を即座に更新できます。 次に例を示します。
   1. テキストレイヤーを選択してテキストを編集する
   1. 画像レイヤーを選択し、「![ その場でのコンテンツの作成 ](/help/assets/assets/dm-templates/add-image.svg) をクリックして、アセットセレクターから画像を選択して、「**[!UICONTROL 更新]**」をクリックします。

   テンプレートは直ちに更新され、編集されたテキストが表示され、前の画像が新しい画像に置き換えられます。 また、画像パラメーターの値には、新しい画像のパスが反映されます。 同様に、レイヤーの値を調整してサイズを変更すると、その変更がリアルタイムでテンプレートに適用されます。
1. リストから [ グループ化されたレイヤー ](#group-layers) の非表示パラメーターを選択して、テンプレート内でそれらを表示または非表示にします。
1. **オプション：****[!UICONTROL 非表示]** パラメーターの値を 0 ～ 1 の間で変更し、「**[!UICONTROL 更新]**」をクリックして変更を確認します。 同じ非表示パラメーターを持つレイヤーは、非表示または一緒に表示されます。 同様に、URL からレイヤーの表示を制御できます。

   ![ その場でのコンテンツの作成 ](/help/assets/assets/dm-templates-publish-status.png)
**[!UICONTROL すべてのパラメーターを含める]** を切り替えて、表示されているすべてのパラメーター値を編集し、テンプレートプレビューで更新内容を確認することもできます。
   <br>
1. プレビューページでテンプレートを公開するには、**[!UICONTROL Publish]** をクリックして、公開を確定します。 Publishの完了メッセージが表示され、公開ステータスが公開済みに更新されます。

>[!NOTE]
>
>テンプレートを公開するには、まずテンプレート画像を公開する必要があります。

### 配信 URL をコピー

**[!UICONTROL プレビュー]** ページで選択したパラメーターが、テンプレート URL の URL パラメーターになります。

プレビューに表示されている公開済みテンプレートの URL をコピーするには：

1. **[!UICONTROL URL をコピー]** をクリックします。 **[!UICONTROL URL をコピー]** ダイアログボックスが表示されます。 表示された URL を選択してコピーします。 URL の最初のパラメーターが疑問符 **（?）の後に始まることを確認します** とキーと値のペアは **$** で始まり、**&amp;** で終わります。 キーと値は等号 **（=）** で区切られ、キーは左側、値は右側に表示されます。
1. この URL をブラウザータブにペーストし、ライブテンプレートを表示します。 「**プレビューとPublish**」セクションの [ 手順 2](#preview-and-publish-template-and-copy-template-deliver-url) で説明されているように、URL で必要なパラメーターの値（キーの値）を直接更新して、テンプレートをリアルタイムでカスタマイズします。
1. 製品やサービスの迅速なマーチャンダイジングには、この URL を使用します。 この URL を顧客と共有したり、web サイトやダウンストリームのサードパーティアプリケーションに統合してバナーを表示したり、継続的なオファーを反映するようにリアルタイムで更新したりできます。

このビデオでは、Dynamic Media テンプレートの作成方法を手順を追って説明します。
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## URL からテンプレートに対してリアルタイムの更新を行う{#update-the-template-from-the-url}

URL 内でパラメーターを直接編集するのは面倒な場合があります。 シンプル化するには：

1. URL をコピーしてメモ帳に貼り付けます。
1. Cmd + F （Mac）または Ctrl + F （Windows）を使用して、パラメーター値を検索および編集します。 例：
   * 画像レイヤーの画像パスを置き換えます。
   * レイヤーの寸法と位置を調整します（[ パラメーター化 ](#parameterise-a-layer) れている場合）。
   * テキストレイヤーのテキスト、フォント、カラー、サイズ、配置を編集します。
   * 表示値を 0 ～ 1 の間で変更します。

この更新された URL をブラウザーに貼り付けて、変更を表示します。

## テンプレートの編集{#edit-the-template}

次の手順に従って、テンプレートを編集します。

1. Assets ビューで、**[!UICONTROL Dynamic Media Assets]** をクリックします。
2. テンプレートの場所に移動します。
3. テンプレートを選択します。
4. **[!UICONTROL テンプレートを編集]** をクリックします。 テンプレートキャンバスには、テンプレートと、そのテンプレートに含まれるすべてのレイヤーのリストがレイヤーパネルに表示されます。 必要に応じてテンプレートの編集を開始します。

## 留意点 {#important-points-to-note}

* 動的更新用にパラメーター化された画像レイヤーを含むテンプレートを作成したら、今後の更新を見据えた画像が、パラメーター化された画像と同じサイズであることを確認します。 これにより、画像がレイヤー内に完全に収まり、オーバーフローしたり、空のスペースを残したりしなくなります。 現在、このテンプレートは、画像をレイヤーに収めるための自動寸法調整をサポートしていません。
* テキストレイヤーでは部分文字列はサポートされません。 ユーザーは、テキストレイヤーの部分文字列に異なるフォントプロパティを適用できません。
* 現在、複数のDynamic Media会社は、Dynamic Media テンプレートではサポートされていません。
* コピーまたは移動の場合、宛先セレクターにすべてのフォルダー（Dynamic Mediaと同期されていないフォルダーを含む）が表示されます。 また、現在のところ、Dynamic Media テンプレートアセットは表示されません（どちらも宛先セレクターの制限です）。
* Assets セクションからフォルダー（Publishや削除など）に対して行う更新処理は、そのフォルダー内で使用できるDynamic Media テンプレートに影響します。
* ごみ箱は、Dynamic Media テンプレートには機能しません。 アセットがごみ箱に移動された後に復元された場合、そのアセットはAEMで復元されますが、Dynamic Mediaでは復元されません。 同じことがDynamic Media テンプレートにも有効です。

## 関連トピック

1. [Dynamic Mediaとその機能を探索する ](/help/assets/dynamic-media/dynamic-media.md)
1. OpenAPI 機能を使用した [Dynamic Mediaの探索 ](/help/assets/dynamic-media-open-apis-overview.md)
