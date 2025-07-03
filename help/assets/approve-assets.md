---
title: Experience Manager でのアセットの承認
description: ' [!DNL Experience Manager] でアセットを承認する方法について説明します。'
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: ht
source-wordcount: '1063'
ht-degree: 100%

---

# [!DNL Experience Manager] でのアセットの承認

ブランドマネージャーとマーケターは、ブランドアセットを厳密に管理します。承認済みの最新バージョンのアセットのみが使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性が確保されます。

AEM Assets でアセットを承認すると、アセット管理が効率化され、アセットを処理するための制御された効率的なプロセスが確保されます。

## 始める前に {#pre-requisites}

AEM Assets as a Cloud Service へのアクセス権と、アセットの&#x200B;**[!UICONTROL レビューステータス]**&#x200B;プロパティを編集する権限が必要です。

## 設定

アセットを承認する前に、管理ビューで該当するメタデータスキーマを 1 回更新する必要があります。Assets ビューでは、この設定をスキップできます。メタデータスキーマを設定するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. 該当するメタデータスキーマを選択し、「**[!UICONTROL 編集]**」をクリックします。<br>**[!UICONTROL メタデータスキーマフォームエディター]**&#x200B;が開き、「**[!UICONTROL 基本]**」タブがハイライト表示されます。
1. 下にスクロールして、「**[!UICONTROL レビューステータス]**」をクリックします。
1. 右側のサイドパネルにある「**[!UICONTROL ルール]**」タブをクリックします。
1. 「**[!UICONTROL 編集を無効にする]**」をオフにします。
「**[!UICONTROL レビューステータス]**」フィールドのマッピング先のプロパティを表示する必要がある場合は、「**[!UICONTROL 設定]**」タブに移動し、「**[!UICONTROL プロパティにマッピング]**」フィールドで `./jcr:content/metadata/dam:status` 値を表示します。
1. 右側の「**[!UICONTROL フォームを作成]**」セクションから「**[!UICONTROL ドロップダウン]**」フィールドをフォームの「メタデータ」セクションにドラッグ＆ドロップします。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]**&#x200B;パネルで次の更新を行います。
   1. **[!UICONTROL フィールドラベル]**&#x200B;を「_承認ターゲット_」に変更します。
   1. 「**[!UICONTROL プロパティにマッピング]**」を _./jcr:content/metadata/dam:activationTarget_ に更新します。
   1. オプション値として `contenthub` と `delivery` の選択肢を追加します。

   >[!NOTE]
   >
   >アセットビューを使用して承認ターゲットをコンテンツハブとして選択すると、アセットは同じ組織に属するユーザーがコンテンツハブで使用できるようになります。承認ターゲットを配信として選択すると、アセットはすべてのユーザーが使用できるようになります。

1. 「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>アセットまたはフォルダーのデフォルトのスキーマが異なる場合は、その特定のスキーマでこの更新を行います。

## アセットの承認 {#approve-assets}

[!DNL Experience Manager Admin view] でアセットを承認するには、次の手順に従います。

1. アセットを選択し、上部のパネルで「**[!UICONTROL プロパティ]**」をクリックします。
1. 「**[!UICONTROL 基本]**」タブで、「**[!UICONTROL レビューステータス]**」まで下にスクロールします。
1. レビューステータスを「**[!UICONTROL 承認済み]**」に変更します。
   ![画像](/help/assets/assets/approve-old-ui.png)
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同様に、[新しいアセットビュー](/help/assets/manage-organize-assets-view.md)を使用してアセットを承認できます。

## アセットの一括承認 {#bulk-approve-assets}

複数のアセットを一度にすばやく承認して、ワークフローを効率化します。アセットを一括承認して、承認プロセスを迅速化し、時間を節約し、生産性を向上させることができます。
<br>[!DNL Experience Manager Admin view] で一括アセットを承認するには、次の手順に従います。

1. オーサー環境（https://author-pXXX-eYYY.adobeaemcloud.com）にフォルダーを作成します。_XXX_ をプログラム ID に置き換え、_YYY_ を Experience Manager の環境 ID に置き換えます。
1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL メタデータプロファイル]**&#x200B;に移動します。
1. ページの右上にある「**[!UICONTROL 作成]**」をクリックします。
1. プロファイルのタイトルを追加し、「**[!UICONTROL 作成]**」をクリックします。メタデータプロファイルが正常に作成されました。
1. 新しく作成したメタデータプロファイルを選択して、「**[!UICONTROL 編集&#x200B;_（e）_]**」をクリックします。<br>**[!UICONTROL メタデータプロファイルを編集]**フォームが開き、「**[!UICONTROL 基本]**」タブがハイライト表示されます。
1. 右側の「**[!UICONTROL フォームを作成]**」セクションから **[!UICONTROL 1 行のテキストフィールド]**&#x200B;をフォームの「メタデータ」セクションにドラッグ＆ドロップします。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]**&#x200B;パネルで次の更新を行います。
   1. **[!UICONTROL フィールドラベル]**&#x200B;を「_承認済みアセット_」に変更します。
   1. **[!UICONTROL マッピング先のプロパティ]**&#x200B;を _.jcr:content/metadata/dam:status_ に更新します。
   1. デフォルト値を「_承認済み_」に変更します。

1. 右側の「**[!UICONTROL フォームを作成]**」セクションから「**[!UICONTROL ドロップダウン]**」フィールドをフォームの「メタデータ」セクションにドラッグ＆ドロップします。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]**&#x200B;パネルで次の更新を行います。
   1. **[!UICONTROL フィールドラベル]**&#x200B;を「_承認ターゲット_」に変更します。
   1. 「**[!UICONTROL プロパティにマッピング]**」を _./jcr:content/metadata/dam:activationTarget_ に更新します。
   1. オプション値として `contenthub` と `delivery` の選択肢を追加します。

   >[!NOTE]
   >
   >アセットビューを使用して承認ターゲットをコンテンツハブとして選択すると、アセットは同じ組織に属するユーザーがコンテンツハブで使用できるようになります。承認ターゲットを配信として選択すると、アセットはすべてのユーザーが使用できるようになります。
1. 「**[!UICONTROL 保存]**」をクリックします。
1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、新しく作成したメタデータプロファイルを選択します。
1. 上部のアクションバーから「**[!UICONTROL フォルダーにメタ―データプロファイルを適用]**」をクリックします。
1. 承認する必要があるフォルダーを選択し、「**[!UICONTROL 適用]**」をクリックします。
   <br>フォルダー全体の権限が承認用に設定され、このフォルダーにアップロードされたアセットはすべて自動的に承認されます。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>このアプローチでは、フォルダー内に新しく作成したアセットが承認されます。フォルダー内の既存のアセットについては、手動で選択して承認する必要があります。<br>または、「**[!UICONTROL 再処理]**」オプションを使用して、メタデータプロファイルの変更を以前のアセットに適用することもできます。

同様に、アセットビューのフォルダー内でアセットを一括承認するには、次の手順を実行します。

1. アセットを選択し、「**[!UICONTROL 一括メタデータ編集]**」をクリックします。

1. 右側のパネルの「[!UICONTROL プロパティ]」セクションにある「**[!UICONTROL ステータス]**」フィールドで「**[!UICONTROL 承認済み]**」を選択します。

   ステータスを `Approved` として選択し、Experience Manager Assets に対して [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) や[コンテンツハブ](/help/assets/product-overview.md)、または両方が有効になっている場合は、「**[!UICONTROL 承認ターゲット]**」フィールドで使用できる「`Delivery`」および「`Content Hub`」オプションを表示できます。

   * 「**[!UICONTROL 配信]**」を選択すると、アセットが OpenAPI 機能を備えた Dynamic Media とコンテンツハブの両方で使用できるようになります。コンテンツハブが有効になっていない場合、このオプションを選択すると、アセットは OpenAPI 機能を備えた Dynamic Media でのみ使用できるようになります。
   * アセットをコンテンツハブで使用できるようにするには、「**[!UICONTROL コンテンツハブ]**」を選択します。

   ![承認ステータス](/help/assets/assets/approval-status-delivery.png)

   デフォルトのメタデータフォームを使用しておらず、「**[!UICONTROL 承認ターゲット]**」フィールドを表示できない場合は、[メタデータフォームを編集](/help/assets/metadata-assets-view.md#metadata-forms)して、「**[!UICONTROL 承認対象]**」フィールドを使用できるコンポーネントからメタデータフォームにドラッグし、「**[!UICONTROL 保存]**」をクリックします。

   >[!NOTE]
   >
   >組織内でアセットビューを使用して承認ターゲットを `Content Hub` として選択すると、アセットは同じ組織に属するユーザーがコンテンツハブで使用できるようになります。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 承認済みアセットの配信 URL のコピー {#copy-delivery-url-approved-assets}

AEM as a Cloud Service インスタンスで [!UICONTROL OpenAPI 機能を備えた Dynamic Media] が有効になっている場合は、リポジトリ内のすべての承認済みアセットの配信 URL が使用できます。

リポジトリ内の承認済みアセットの配信 URL をコピーするには：

1. アセットを選択し、「**[!UICONTROL 詳細]**」をクリックします。

1. 右側のパネルで使用可能な Dynamic Media アイコンをクリックします。

1. **[!UICONTROL Dynamic Media]** パネルで「**[!UICONTROL OpenAPI 機能を備えた Dynamic Media]**」を選択します。

1. 「**[!UICONTROL URL をコピー]**」をクリックして、アセットの配信 URL をコピーします。
   ![動的レンディション](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   >承認済みアセットの配信 URL をコピーするオプションは、アセットビューでのみ使用できます。

Dynamic Media パネル内に表示される他のレンディションについて詳しくは、[Dynamic Media レンディションの表示とダウンロード](/help/assets/renditions.md#view-download-dm-renditions)を参照してください。
