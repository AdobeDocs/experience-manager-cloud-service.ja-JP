---
title: ブランド承認済みアセットのアップロード先  [!DNL Content Hub]
description: ブランド承認済みアセットをContent Hubにアップロードする方法を学ぶ
role: User
exl-id: f1be7cfc-1803-4c17-bb58-947104aa883c
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 7%

---

# コンテンツハブへのブランド承認済みアセットのアップロード {#upload-brand-approved-assets-content-hub}

>[!CONTEXTUALHELP]
>id="upload_assets_content_hub"
>title="コンテンツハブへのブランド承認済みアセットのアップロード"
>abstract="ローカルファイルシステムからコンテンツハブに承認済みアセットを追加するか、OneDrive データソースまたは Dropbox データソースからアセットを読み込みます。検索機能を強化するために、フォルダー構造に関係なく、すべてのアセットがコンテンツハブの最上位に表示されます。"

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

[ アセットを追加する権限を持つContent Hub ユーザー ](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)、ローカルファイルシステムからContent Hubにアセットを追加したり、OneDrive またはDropboxのデータソースからアセットを読み込んだりできます。 ローカルファイルシステムで使用可能なフォルダー構造や、検索機能を強化するための OneDrive およびDropboxデータソースに関係なく、すべてのアセットがContent Hubの最上位に表示されます。

Assetsのas a Cloud Serviceで `Approved` とマークされたアセットは、Content Hubで自動的に使用できるようになります。 詳しくは、[Content Hubのアセットを承認 ](/help/assets/approve-assets-content-hub.md) を参照してください。

アセット検索をさらに強化するために、Content Hubでは次の操作を実行できます。

* キャンペーン名、キーワード、チャネルなど、アセットのアップロードに関連する重要な詳細を定義します。

* ファイルサイズ、形式、解像度、その他のプロパティなど、アップロードに成功した場合に、各アセットのその他のプロパティを自動的に生成します。

* [Adobe Sensei](https://www.adobe.com/jp/sensei.html) が提供する人工知能を使用して、アップロードされたすべてのアセットに適切なタグを自動的に適用します。 スマートタグと呼ばれるこれらのタグは、関連するアセットをすばやく見つけるのに役立つので、プロジェクトのコンテンツベロシティ（コンテンツ創出の速度）が向上します。

[ ブランドで承認されたアセットのみをContent Hub](/help/assets/approve-assets.md) にアップロードしてください。

![ ブランド承認済みアセットのアップロード ](assets/upload-brand-approved-assets.png)

## 前提条件 {#prerequisites-add-assets}

[ アセットを追加する権限を持つContent Hub ユーザー ](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)、Content Hubにアセットをアップロードできます。

## ローカルファイルシステムからContent Hubへのアセットの追加 {#add-assets-local-file-system}

Content Hubにアセットを追加するには、次の手順を実行します。

1. **[!UICONTROL Assetsを追加]** をクリックして **[!UICONTROL 承認済みアセットを追加]** ダイアログボックスを表示し、アップロードを作成します。

1. 右側のペインにある「**[!UICONTROL ファイルまたはフォルダーをここにドラッグします]**」セクションで、ローカルのファイルシステムからアセットをドラッグするか、**[!UICONTROL 参照]** をクリックして、ローカルのファイルシステムで使用可能なファイルまたはフォルダーを手動で選択します。 アップロードに含まれるファイルのリストは、リストとして使用できます。


   また、サムネールを使用して選択した画像をプレビューし、X アイコンをクリックして、リストから特定の画像を削除することもできます。 X アイコンは、画像の名前またはサイズの上にマウスを置いた場合にのみ表示されます。 また、「**[!UICONTROL すべてを削除]**」をクリックして、アップロードリストからすべての項目を削除することもできます。

   アップロードプロセスを完了し **[!UICONTROL アップロードボタン]** を有効にするには、アセットをキャンペーン名でグループ化する必要があります。

   ![Content Hubへのアセットのアップロード ](assets/upload-assets-content-hub.png)

1. 「**[!UICONTROL キャンペーン名]**」フィールドを使用して、アップロードする名前を定義します。 既存の名前を使用することも、新しい名前を作成することもできます。 Content Hubには、名前を入力する際に表示される追加のオプションが用意されています。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   ベストプラクティスとして、Adobeでは残りのフィールドに値を指定し、アップロードしたアセットの検索エクスペリエンスを強化することをお勧めします。

1. 同様に、「**[!UICONTROL キーワード]**」、「**[!UICONTROL チャネル]**」、「**[!UICONTROL 期間]**」、「**[!UICONTROL 地域]** の各フィールドの値を定義します。 キーワード、チャネル、場所別にアセットのタグ付けとグループ化を行うと、承認済みの会社コンテンツを使用するすべてのユーザーがこれらのアセットを検索し、整理しておくことができます。

1. **[!UICONTROL アップロード]** をクリックして、Content Hubにアセットをアップロードします。 [!UICONTROL  詳細を確認 ] 確認ボックスが表示されます。 「[!UICONTROL 続行]」をクリックします。

1. Assetsがアップロードを開始します。 [!UICONTROL  新規アップロード ] をクリックして、アップロード手順を再開します。 「[!UICONTROL  完了 ]」をクリックしてアップロードを完了します。

また、管理者は、アセットのアップロード時に表示される必須フィールドとオプションフィールド（キャンペーン名、キーワード、チャネルなど）を設定することもできます。 詳しくは、[Content Hub ユーザーインターフェイスの設定 ](configure-content-hub-ui-options.md#configure-upload-options-content-hub) を参照してください。


## OneDrive またはDropboxのデータソースからContent Hubへのアセットの追加 {#add-assets-onedrive-dropbox}

OneDrive またはDropboxのデータソースからContent Hubにアセットを追加するには：

1. **[!UICONTROL Assetsを追加]** をクリックして、OneDrive またはDropboxからアセットを読み込むことができる **[!UICONTROL 承認済みアセットを追加]** ダイアログボックスを表示します。

1. **[!UICONTROL OneDrive]** または **[!UICONTROL Dropbox]** をクリックして、読み込みプロセスを開始します。 Content Hubでは、OneDrive またはDropboxアカウントにログオンするように求めるメッセージが表示され、左側のウィンドウに OneDrive またはDropboxフォルダー構造が表示されます。

1. ファイル名またはフォルダー名の横にある「+」アイコンをクリックすると、選択した項目のリストに項目が表示されます。 Content Hub ポータルに追加する必要のあるすべてのファイルを選択したら、[ ローカルファイルシステムからContent Hubへのアセットの追加 ](#add-assets-local-file-system) の手順 3 ～ 6 を繰り返し、アップロードプロセスを完了します。

   ![OneDrive またはDropboxからContent Hubへのアセットのアップロード ](assets/add-assets-onedrive-dropbox.png)

また、管理者は、アセットのアップロード時に表示される必須フィールドとオプションフィールド（キャンペーン名、キーワード、チャネルなど）を設定することもできます。 詳しくは、[Content Hub ユーザーインターフェイスの設定 ](configure-content-hub-ui-options.md#configure-upload-options-content-hub) を参照してください。

## Content Hubを使用してアップロードされたアセットの管理 {#manage-assets-uploaded-using-content-hub}

[ アセットを追加する権限を持つContent Hub ユーザー ](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets)、ローカルファイルシステムから [Content Hubにアセットを追加 ](/help/assets/upload-brand-approved-assets.md) するか、OneDrive またはDropboxのデータソースからアセットを読み込むことができます。 ローカルファイルシステムで使用可能なフォルダー構造や、検索機能を強化するための OneDrive およびDropboxデータソースに関係なく、すべてのアセットがContent Hubの最上位に表示されます。

Content Hubを使用してアップロードされたアセットの表示は、[ 自動承認切り替えを有効 ](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) にしたかどうかによって異なります。

* **[!UICONTROL 自動承認]** 切替スイッチが有効になっている場合は、Content Hubを使用してアップロードしたアセットを自動的に利用できます。

* **[!UICONTROL 自動承認]** の切り替えが無効になっている場合、Content Hubを使用してアップロードしたアセットは自動的には表示されません。 アセットは、Assetsas a Cloud Serviceの `hydrated-assets` フォルダーで使用できます。 フォルダーに移動して、Content Hubに表示するアセットのステータスを `Approved` 定する [ 一括編集 ](#bulk-approve-assets-content-hub) を行います。

![Content Hub承認プロセス ](/help/assets/assets/content-hub-approval.png)
