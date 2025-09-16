---
title: AEM Sites ページで使用する前にアセットをプレビュー
description: OpenAPI 機能を備えた Dynamic Media を使用すると、Adobe Experience Manager（AEM）Sites プレビューページでアセットをプレビューできます。このアセットプレビューを使用すると、オーサーページ（更新されたアセットを含む）を公開して一般公開する前に、ユーザーと関係者がアセットの更新内容を確認および検証できます。
role: Admin, User
exl-id: 6f071ca9-0f84-45fc-a6b3-047cca9d5e65
source-git-commit: 3f3e091d09b94418fc2cda0bd3b3ce950555b7a9
workflow-type: ht
source-wordcount: '731'
ht-degree: 100%

---


# AEM Sites ページで使用する前にアセットをプレビュー {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] を使用すると、[!DNL Adobe Experience Manager (AEM) Sites] オーサーページで使用可能なアセットを公開前にプレビューできます。アセットプレビューは、サイトのオーサー層とプレビュー層で使用できます。

[AEM Sites のプレビューページでアセットをプレビュー](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities)するには、プレビューするアセットを追加するか、ライブ Sites ページで使用可能な既存のアセットを置き換えて、サイトのオーサーページを更新します。更新したオーサーページをプレビュー層に公開して、プレビュー URL を生成します。

プレビューページを関係者と共有し、更新したアセットのビジュアルの品質やコンテキストへの適合性についてフィードバックを収集します。フィードバックに基づいてアセットを絞り込みます。レビューサイクル中に、アセットの複数のバージョンを作成および管理します。

アセットを公開用に確定したら、オーサーページでアセットを更新し、公開アクセス用にパブリッシュ層にページを公開します。

## 始める前に{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

次の点を確認します。

* [!DNL AEM Assets as a Cloud Service] にアクセスします。
* アセットのステータスプロパティを編集する権限。
* プレビューするアセットを含むフォルダーに適用されるメタデータフォームの[「[!UICONTROL 基本]」タブで使用可能な[!UICONTROL ステータス]メタデータプロパティに、[!UICONTROL プレビュー]値が追加されました](/help/assets/metadata-assets-view.md#edit-metadata-forms)。
  ![プレビューオプションを追加](/help/assets/assets/metedata-form-preview.png)
* プレビュートークンを生成するためのキー。 [アドビサポートに問い合わせて](https://helpx.adobe.com/jp/contact.html)、キーのリクエストを発行します。

## Sites プレビューページでのアセットのプレビュー {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

新しいアセットや既に承認されているアセットをプレビューできます。承認済みアセットは、ライブ Sites ページにのみ表示されます。

[!DNL Assets View] でアセットのステータスをプレビューに設定し、Sites オーサリングページをプレビュー層に公開して、ページのプレビュー URL を生成するには、次の手順を実行します。

1. 次の手順を実行して、アセットのステータスを&#x200B;**[!UICONTROL プレビュー]**&#x200B;に設定します。

   1. [!DNL Assets View] で「**[!UICONTROL Assets]**」を選択し、フォルダーに移動します。
   1. プレビューするアセットを選択します。
   1. 「**[!UICONTROL 詳細]**」をクリックします。
   1. [!UICONTROL 情報パネル]で&#x200B;**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL プレビュー]**&#x200B;に設定し、「**[!UICONTROL 保存]**」をクリックします。
      ![プレビュー](/help/assets/assets/preview-boat-at-bay.png)

1. Sites オーサリングページに移動します。 最近プレビュー（ステータス）に設定したアセットの選択に対してアセットセレクターパネルを使用するには、[AEM ページエディターでのリモートアセットへのアクセス](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor)の節の手順を実行します。

   >[!NOTE]
   >
   > アセットセレクターには、最新のステータス更新が承認済みまたはプレビューに設定されたアセットが表示されます。

1. 「**[!UICONTROL 公開を管理]**」オプションを使用して、ページをプレビュー層に公開します。[プレビューへのコンテンツの公開](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content)の節の手順を実行して、ページをプレビュー層に公開します。公開後、ページのプレビュー URL を生成します。プレビューページには、Sites ページのアセット（最新のステータス更新を含む）が表示されます。

このプレビュー URL を関係者と共有し、レビューとフィードバックを得ます。関係者がプレビューページにアクセスできることを確認します。プレビューページへのアクセスを提供する方法について詳しくは、[プレビューサービスへのアクセス](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service)を参照してください。

>[!NOTE]
>
>[画像 V3 コアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility)は、デフォルトでアセットのプレビューバージョンをサポートします。[アセットセレクター](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload)パネルを使用してアセットのプレビューバージョン（プレビューステータスのアセット）を選択すると、画像 V3 コンポーネントにより、プレビュー層（Sites オーサーページのプレビューバージョン）に自動的にレンダリングされます。

アセットバージョンを確定したら、[ページをパブリッシュ層に公開](#publish-your-pages-to-publish-tier)して一般公開します。

## 公開用に承認されたアセットを使用したページの公開{#publish-your-pages-to-publish-tier}

公開用のアセットのバージョンを確定したら、アセットのステータスを「**[!UICONTROL 承認済み]**」に設定します。次に、ページをパブリッシュ層に公開します。ページを公開するには、次の手順を実行します。

1. 上記の「[サイトプレビューページでアセットをプレビューする](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities)」セクションの手順 1 に従って、アセットのステータスを 「**[!UICONTROL 承認済み]**」に変更します。
1. Sites オーサーページに移動し、[!DNL Publish tier] に公開します。「[ページエディターからの公開](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor)」セクションの手順を実行して、ページを公開します。または、「[Sites コンソールからのページの公開 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console)」セクションの手順に従って、サイトのコンソールからページを公開します。

   >[!NOTE]
   >
   > パブリッシュ層では、承認済みのアセットのみを配信できます。ページをパブリッシュ層に公開して一般公開する前に、アセットを承認します。

   ![ページが公開されました](/help/assets/assets/the-page-has-been-publushed.png)
公開に成功すると、「**[!UICONTROL ページが公開されました]**」という確認メッセージが表示されます。パブリッシュ層で公開済みのページに移動し、更新がライブであり、コンテンツが期待どおりに表示されることを確認します。
