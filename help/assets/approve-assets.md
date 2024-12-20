---
title: Experience Manager でのアセットの承認
description: ' [!DNL Experience Manager] でアセットを承認する方法について説明します。'
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 90%

---

# [!DNL Experience Manager] でのアセットの承認

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

ブランドマネージャーとマーケターは、ブランドアセットを厳密に管理します。承認済みの最新バージョンのアセットのみが使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性が確保されます。

AEM Assets でアセットを承認すると、アセット管理が効率化され、アセットを処理するための制御された効率的なプロセスが確保されます。

## 事前準備 {#pre-requisites}

AEM Assets as a Cloud Service へのアクセス権と、アセットの&#x200B;**[!UICONTROL レビューステータス]**&#x200B;プロパティを編集する権限が必要です。

## 設定

アセットを承認する前に、管理ビューで該当するメタデータスキーマを 1 回更新する必要があります。Assets ビューでは、この設定をスキップできます。メタデータスキーマを設定するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. 該当するメタデータスキーマを選択し、「**[!UICONTROL 編集]**」をクリックします。<br>**[!UICONTROL メタデータスキーマフォームエディター]**&#x200B;が開き、「**[!UICONTROL 基本]**」タブがハイライト表示されます。
1. 下にスクロールして、「**[!UICONTROL レビューステータス]**」をクリックします。
1. 右側のサイドパネルにある「**[!UICONTROL ルール]**」タブをクリックします。
1. 「**[!UICONTROL 編集を無効にする]**」をオフにし、「**[!UICONTROL 保存]**」をクリックします。
「**[!UICONTROL レビューステータス]**」フィールドのマッピング先のプロパティを表示する必要がある場合は、「**[!UICONTROL 設定]**」タブに移動し、「**[!UICONTROL プロパティにマッピング]**」フィールドで `./jcr:content/metadata/dam:status` 値を表示します。

>[!NOTE]
>
アセットまたはフォルダーのデフォルトのスキーマが異なる場合は、その特定のスキーマでこの更新を行います。

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

1. 「**[!UICONTROL 保存]**」をクリックします。
1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、新しく作成したメタデータプロファイルを選択します。
1. 上部のアクションバーから「**[!UICONTROL フォルダーにメタ―データプロファイルを適用]**」をクリックします。
1. 承認する必要があるフォルダーを選択し、「**[!UICONTROL 適用]**」をクリックします。
   <br>フォルダー全体の権限が承認用に設定され、このフォルダーにアップロードされたアセットはすべて自動的に承認されます。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
このアプローチでは、フォルダー内に新しく作成したアセットが承認されます。フォルダー内の既存のアセットについては、手動で選択して承認する必要があります。<br>または、「**[!UICONTROL 再処理]**」オプションを使用して、メタデータプロファイルの変更を以前のアセットに適用することもできます。

同様に、アセットビューのフォルダー内でアセットを一括承認するには、次の手順を実行します。

1. アセットを選択し、「**[!UICONTROL 一括メタデータ編集]**」をクリックします。

1. 右側のパネルの「[!UICONTROL プロパティ]」セクションにある「**[!UICONTROL ステータス]**」フィールドで「**[!UICONTROL 承認済み]**」を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 承認済みアセットの配信 URL のコピー {#copy-delivery-url-approved-assets}

AEM as a Cloud Service インスタンスで [!UICONTROL OpenAPI 機能を備えた Dynamic Media] が有効になっている場合は、リポジトリ内のすべての承認済みアセットの配信 URL が使用できます。

リポジトリ内の承認済みアセットの配信 URL をコピーするには：

1. アセットを選択し、「**[!UICONTROL 詳細]**」をクリックします。

1. 右側のパネルに表示されている「Dynamic Media」アイコンをクリックします。

1. **[!UICONTROL Dynamic Media]** パネルにある「**[!UICONTROL Dynamic Media with OpenAPI]**」を選択します。

1. 「**[!UICONTROL URL をコピー]**」をクリックして、アセットの配信 URL をコピーします。
   ![動的レンディション](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   承認済みアセットの配信 URL をコピーするオプションは、アセットビューでのみ使用できます。

Dynamic Media パネル内に表示されるその他のレンディションについて詳しくは、[Dynamic Media レンディションの表示とダウンロード ](/help/assets/renditions.md#view-download-dm-renditions) を参照してください。
