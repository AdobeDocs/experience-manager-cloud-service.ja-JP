---
title: AEM Sites ページで使用する前にアセットをプレビューする
description: OpenAPI 機能を備えた Dynamic Media を使用すると、Adobe Experience Manager（AEM） Sites のプレビューページでアセットをプレビューできます。 このアセットプレビューを使用すると、アセットを公開する前に（更新されたアセットを含む）作成者ページを公開前に、作成者および関係者がアセットの更新を確認および検証できます。
role: Admin, User
source-git-commit: e343cc5754ec5565e57a5a932d59d7bfe78c6027
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---


# AEM Sites ページで使用する前にアセットをプレビューする {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] を使用すると、[!DNL Adobe Experience Manager (AEM) Sites] オーサーページで使用可能なアセットを、公開する前にプレビューできます。 アセットのプレビューは、サイトのオーサー層とプレビュー層で使用できます。

[AEM Sites プレビューページでアセットをプレビュー ](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) するには、プレビューするアセットを追加するか、ライブサイトページで使用可能な既存のアセットを置き換えて、サイトのオーサーページを更新します。 次に、更新されたオーサーページをプレビュー層に公開して、プレビュー URL を生成します。

プレビューページを関係者と共有して、更新されたアセットの視覚的な品質とコンテキストの整合性に関するフィードバックを収集します。 フィードバックに基づいてアセットを絞り込みます。 レビューサイクル中に、アセットの複数のバージョンを作成および管理します。

公開するためにアセットを最終決定したら、オーサーページでアセットを更新し、公開アクセス用にページをパブリッシュ層に公開します。

## 開始する前に{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

次の点を確認します。

* [!DNL AEM Assets as a Cloud Service] にアクセスします。
* アセットのステータスプロパティを編集する権限。
* プレビューするアセットを含むフォルダーに適用されたメタデータフォームの [ 基本 [!UICONTROL  タブ ] で使用可能な [!UICONTROL  ステータス ] メタデータプロパティに [!UICONTROL  プレビュー ]](/help/assets/metadata-assets-view.md#edit-metadata-forms) 値を追加しました。
  ![ 「プレビューを追加」オプション ](/help/assets/assets/metedata-form-preview.png)
* プレビュートークンを生成するためのキー。 [Adobe サポートに問い合わせ ](https://helpx.adobe.com/in/contact.html)、キーのリクエストを発行します。

## Sites プレビューページでのアセットのプレビュー {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

新しいアセットや既に承認されているアセットをプレビューできます。 承認済みアセットは、ライブサイトページにのみ表示されます。

次の手順を実行して、アセットのステータスを [!DNL Assets View] でプレビューに設定し、Sites オーサリングページをプレビュー層に公開してページのプレビュー URL を生成します。

1. 次の手順を実行して、アセットのステータスを **[!UICONTROL プレビュー]** に設定します。

   1. [!DNL Assets View] で **[!UICONTROL Assets]** を選択し、フォルダーに移動します。
   1. プレビューするアセットを選択します
   1. **[!UICONTROL 詳細]** をクリックします。
   1. [!UICONTROL  情報パネル ] で、**[!UICONTROL ステータス]** を **[!UICONTROL プレビュー]** に設定し、「**[!UICONTROL 保存]**」をクリックします。
      ![プレビュー](/help/assets/assets/preview-boat-at-bay.png)

1. Sites オーサリングページに移動します。 [AEM ページエディターでリモートアセットにアクセス ](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) の手順を実行し、アセットセレクターパネルを使用して最近プレビュー（ステータス）に設定したアセットを選択します。

   >[!NOTE]
   >
   > アセットセレクターに、最新のステータス更新が承認済みまたはプレビューに設定されたアセットが表示されます。

1. 「**[!UICONTROL 公開を管理]** オプションを使用して、ページをプレビュー層に公開します。 [ プレビューへのコンテンツの公開 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content) セクションの手順を実行して、ページをプレビュー層に公開します。 公開後、ページのプレビュー URL を生成します。 プレビューページには、Sites ページのアセット（最新のステータス更新）が表示されます。

レビューおよびフィードバックのために、関係者とこのプレビュー URL を共有します。 関係者が、プレビューページにアクセスできることを確認します。 プレビューページへのアクセスを提供する方法について詳しくは、[ プレビューサービスへのアクセス ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service) を参照してください。

>[!NOTE]
>
>[ 画像 V3 コアコンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility) は、デフォルトでアセットのプレビューバージョンをサポートしています。 [ アセットセレクター ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload) パネルを使用してアセットのプレビューバージョン（プレビューステータスのアセット）を選択すると、画像 V3 コンポーネントは、プレビュー層（Sites オーサーページのプレビューバージョン）でアセットを自動的にレンダリングします。

アセットのバージョンを最終決定した後、公開するために [ ページをパブリッシュ層に公開 ](#publish-your-pages-to-publish-tier) します。

## 承認済みアセットを使用してページを公開し、一般に使用する{#publish-your-pages-to-publish-tier}

公開するアセットのバージョンを最終決定した後、アセットのステータスを **[!UICONTROL 承認済み]** に設定します。 次に、ページをパブリッシュ層に公開します。 ページを公開するには、次の手順を実行します。

1. 前述の [ サイトプレビューページでアセットをプレビューする ](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) セクションの手順 1 に従って、アセットのステータスを **[!UICONTROL 承認済み]** に変更します。
1. Sites オーサーページに移動し、[!DNL Publish tier] に公開します。 [ ページエディターからの公開 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor) セクションの手順を実行して、ページを公開します。
または、[Sites コンソールからのページの公開 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console) の節の手順に従って、サイトのコンソールからページを公開します。

   >[!NOTE]
   >
   > パブリッシュ層では、承認済みのアセットのみを配信できます。 ページをパブリッシュ層に公開して公開する前に、アセットを承認します。

   ![ ページが公開されました ](/help/assets/assets/the-page-has-been-publushed.png)
公開に成功すると、確認メッセージ **[!UICONTROL ページが公開されました]** が表示されます。 パブリッシュ層で公開済みのページに移動して、更新がライブであり、コンテンツが期待どおりに表示されることを確認します。

