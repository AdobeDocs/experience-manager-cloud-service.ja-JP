---
title: Experience Managerでのアセットの承認
description: ' [!DNL Experience Manager] でアセットを承認する方法について説明します。'
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 5%

---

# [!DNL Experience Manager] でのアセットの承認

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>OpenAPI 機能ガイドのDynamic MediaがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE OpenAPI 機能ガイドPDFのDynamic Media]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

ブランドマネージャーとマーケターは、ブランドアセットを厳格に管理しています。 アセットの承認済みの最新バージョンのみを使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性を確保できます。

AEM Assetsでアセットを承認してアセット管理を効率化し、アセットを処理するための制御された効率的なプロセスを確保できます。

## 事前準備 {#pre-requisites}

アセットの **[!UICONTROL レビューステータス]** プロパティを編集するには、AEM Assetsのas a Cloud Serviceへのアクセス権と権限が必要です。

## 設定

アセットを承認するには、管理表示で該当するメタデータスキーマを 1 回更新する必要があります。 Assets ビューの場合は、この設定をスキップできます。 メタデータスキーマを設定するには、次の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL メタデータスキーマ]**&#x200B;に移動します。
1. 該当するメタデータスキーマを選択し、「**[!UICONTROL 編集]**」をクリックします。 <br> 基本 **[!UICONTROL タブがハイライト表示された状態で]** メタデータスキーマフォームエディター **[!UICONTROL が開き]** す。
1. 下にスクロールして、**[!UICONTROL レビューステータス]** をクリックします。
1. 右側のパネルにある「**[!UICONTROL ルール]**」タブをクリックします。
1. **[!UICONTROL 編集を無効にする]** のチェックを外し、「**[!UICONTROL 保存]** をクリックします。
**[!UICONTROL レビューステータス]** フィールドのマッピング先のプロパティを表示する必要がある場合は、「**[!UICONTROL 設定]** タブに移動し、「**[!UICONTROL プロパティにマッピング]**」フィールドの `./jcr:content/metadata/dam:status` 値を表示します。

>[!NOTE]
>
アセットまたはフォルダーのデフォルトのスキーマが異なる場合は、その特定のスキーマでこの更新を行ってください。

## アセットの承認 {#approve-assets}

[!DNL Experience Manager Admin view] でアセットを承認するには、次の手順に従います。

1. アセットを選択し、上部のペインで **[!UICONTROL プロパティ]** をクリックします。
1. 「**[!UICONTROL 基本]**」タブで、下にスクロールして **[!UICONTROL レビューステータス]** を表示します。
1. レビューステータスを **[!UICONTROL 承認済み]** に変更します。
   ![画像](/help/assets/assets/approve-old-ui.png)
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同様に、[ 新しいAssets表示 ](/help/assets/manage-organize-assets-view.md) を使用してアセットを承認できます。

## アセットの一括承認 {#bulk-approve-assets}

複数のアセットを一度にすばやく承認することで、ワークフローを効率化します。 アセットを一括承認して、承認プロセスを迅速化し、時間を節約し、生産性を向上させることができます。
<br>[!DNL Experience Manager Admin view] で一括アセットを承認するには、次の手順に従います。

1. オーサー環境でフォルダーを作成します（https://author-pXXX-eYYY.adobeaemcloud.com）。 _XXX_ をプログラム ID に、_YYY_ をExperience Managerの環境 ID に置き換えます。
1. **[!UICONTROL ツール]** / **[!UICONTROL Assets]** / **[!UICONTROL メタデータプロファイル]** に移動します。
1. ページの右上にある「**[!UICONTROL 作成]**」をクリックします。
1. プロファイルのタイトルを追加し、「**[!UICONTROL 作成]**」をクリックします。 メタデータプロファイルが正常に作成されました。
1. 新しく作成されたメタデータプロファイルを選択し、「**[!UICONTROL 編集 _（e）_]**」をクリックします。 <br> 基本&#x200B;**[!UICONTROL タブがハイライト表示された状態で]**メタデータプロファイルを編集&#x200B;**[!UICONTROL フォームが開き]**す。
1. **[!UICONTROL 1 行のテキストフィールド]** を、右側の **[!UICONTROL フォームを作成]** セクションからフォームのメタデータセクションにドラッグ&amp;ドロップします。
1. 新しく追加されたフィールドをクリックし、**[!UICONTROL 設定]** パネルで次の更新を行います。
   1. **[!UICONTROL フィールドラベル]** を _承認済みAssets_ に変更します。
   1. **[!UICONTROL プロパティにマッピング]** を _に更新します。/jcr:content/metadata/dam:status_。
   1. デフォルト値を _approved_ に変更します。

1. 「**[!UICONTROL 保存]**」をクリックします。
1. **[!UICONTROL メタデータプロファイル]** ページで、新しく作成したメタデータプロファイルを選択します。
1. 上部のアクションバーの「**[!UICONTROL メタデータプロファイルをフォルダーに適用]**」をクリックします。
1. 承認する必要があるフォルダーを選択し、「**[!UICONTROL 適用]**」をクリックします。
   <br> フォルダー全体に対する権限が承認用に設定され、このフォルダーにアップロードされたアセットが自動的に承認されます。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
この方法では、フォルダー内に新しく作成されたアセットが承認されます。 フォルダー内の既存のアセットの場合、手動で選択して承認する必要があります。 <br> または、「**[!UICONTROL 再処理]**」オプションを使用して、メタデータプロファイルから古いアセットに変更を適用します。

同様に、Assets ビューでフォルダー内のアセットを一括承認するには、次の手順を実行します。

1. アセットを選択し、**[!UICONTROL 一括メタデータ編集]** をクリックします。

1. 右側のペインの **[!UICONTROL プロパティ]** セクションで使用可能な **[!UICONTROL ステータス]** フィールドの [!UICONTROL  承認済み ] を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 承認済みアセットの配信 URL をコピー {#copy-delivery-url-approved-assets}

リポジトリー内のすべての承認済みアセットの配信 URL は、AEM as a Cloud Service インスタンスで [!UICONTROL OpenAPI 機能 ] が有効になっているDynamic Mediaがある場合に使用できます。

リポジトリ内の承認済みアセットの配信 URL をコピーするには：

1. アセットを選択し、「**[!UICONTROL 詳細]**」をクリックします。

1. 右側のパネルに表示されている「Dynamic Media」アイコンをクリックします。

1. **[!UICONTROL Dynamic Media]** パネルにある「**[!UICONTROL Dynamic Media with OpenAPI]**」を選択します。

1. **[!UICONTROL URL をコピー]** をクリックして、アセットの配信 URL をコピーします。
   ![ 動的レンディション ](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   承認済みアセットの配信 URL をコピーするオプションは、Assets ビューでのみ使用できます。

Dynamic Media パネル内に表示されるその他のレンディションについて詳しくは、[Dynamic Media レンディションの表示とダウンロード ](/help/assets/renditions.md#view-download-dm-renditions) を参照してください。
