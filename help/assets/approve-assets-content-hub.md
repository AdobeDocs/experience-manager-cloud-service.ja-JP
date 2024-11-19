---
title: コンテンツハブ向けアセットの承認
description: Assetsのas a Cloud Serviceでアセットを承認して、Content Hubで使用できるようにする方法を説明します。
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 6%

---

# コンテンツハブ向けアセットの承認 {#approve-assets-content-hub}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Content Hub用のアセットの承認 ](assets/content-hub-approve-assets.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

ブランドマネージャーとマーケターは、ブランドアセットを厳格に管理しています。 Content Hub内では、承認済みの最新バージョンのアセットのみを使用できるので、すべてのチャネルとアプリケーションでブランドの一貫性を確保できます。

AEM Assetsのas a Cloud Service機能を使用してアセットを承認することで、アセット管理を効率化し、アセットを処理するための制御された効率的なプロセスを確保できます。

## 事前準備 {#pre-requisites}

開始する前に、次のものが必要です。

* AEM Assetsのas a Cloud Serviceへのアクセス

* アセットの **[!UICONTROL アセットプロパティ]** で使用可能な [ ステータス ](/help/assets/manage-organize-assets-view.md##manage-asset-status) フィールドを編集できるように、アセットメタデータを編集する権限を書き込みます。

## コンテンツハブ向けアセットの承認{#approve-assets-for-content-hub}

Assetsのas a Cloud Serviceで `approved` とマークされたアセットは、Content Hubで自動的に使用できるようになります。

>[!NOTE]
>
Assetsのas a Cloud ServiceおよびContent HubがContent Hubに表示されるアセットと同じ組織を使用する必要があります。

AEM as a Cloud Service内でAssets表示を使用して、アセットのステータスを `approved` に設定するには：

1. アセットを選択し、ツールバーの「**[!UICONTROL 詳細]**」をクリックします。

1. 「**[!UICONTROL 基本]**」タブで、「**[!UICONTROL ステータス]**」ドロップダウンリストからアセットのステータスを `approved` のように選択します。
1. 「**[!UICONTROL 保存]**」をクリックします。

   >[!VIDEO](https://video.tv.adobe.com/v/3433172)

管理者ビューを使用してアセットを承認する必要がある場合は、[ 管理者ビューを使用したアセットの承認 ](/help/assets/approve-assets.md#approve-assets) を参照してください。

## Assets ビューを使用したContent Hubのアセットの一括承認 {#bulk-approve-assets-content-hub}

AEM Assetsのas a Cloud Service用のAssets ビューを使用したアセットの一括承認。 すべてのアセットが一括承認された後で、Content Hubで使用できるようになります。

Assets ビューでフォルダー内のアセットを一括承認するには：

1. アセットを選択し、**[!UICONTROL 一括メタデータ編集]** をクリックします。

1. 右側のペインの **[!UICONTROL プロパティ]** セクションで使用可能な **[!UICONTROL ステータス]** フィールドの [!UICONTROL  承認済み ] を選択します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## 管理ビューで新しく取り込んだアセットの承認の自動化 {#automate-approval-newly-ingested-assets}

Assets表示から管理者表示に切り替えた後は、フォルダー設定を指定して、そのフォルダーに追加されたすべての新しいアセットが自動的に承認されるようにできます。

管理者ビューとAssets ビューは、次の方法で切り替えることができます。
![My Workspaceの概要 ](assets/assets-view.png)

[!DNL Experience Manager Admin view] に新しく取り込んだアセットの承認を自動化するには、次の手順に従います。

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
この方法では、フォルダー内に新しく作成されたアセットが承認されます。 フォルダー内の既存のアセットの場合、手動で選択して承認する必要があります。

## Content Hubを使用してアップロードされたアセットの管理 {#manage-assets-uploaded-using-content-hub}

[ アセットを追加する権限を持つContent Hub ユーザー ](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)、ローカルファイルシステムから [Content Hubにアセットを追加 ](/help/assets/upload-brand-approved-assets.md) するか、OneDrive またはDropboxのデータソースからアセットを読み込むことができます。 ローカルファイルシステムで使用可能なフォルダー構造や、検索機能を強化するための OneDrive およびDropboxデータソースに関係なく、すべてのアセットがContent Hubの最上位に表示されます。

Content Hubを使用してアップロードされたアセットの表示は、[ 自動承認切り替えを有効 ](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) にしたかどうかによって異なります。

* **[!UICONTROL 自動承認]** 切替スイッチが有効になっている場合は、Content Hubを使用してアップロードしたアセットを自動的に利用できます。

* **[!UICONTROL 自動承認]** の切り替えが無効になっている場合、Content Hubを使用してアップロードしたアセットは自動的には表示されません。 アセットは、Assetsas a Cloud Serviceの `hydrated-assets` フォルダーで使用できます。 フォルダーに移動して、Content Hubに表示するアセットのステータスを `Approved` 定する [ 一括編集 ](#bulk-approve-assets-content-hub) を行います。

![Content Hub承認プロセス ](/help/assets/assets/content-hub-approval.png)
