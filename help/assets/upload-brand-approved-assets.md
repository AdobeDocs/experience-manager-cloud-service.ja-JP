---
title: ブランド承認済みアセットのへのアップロード [!DNL Content Hub]
description: ブランド承認済みアセットをContent Hubにアップロードする方法を学ぶ
role: User
source-git-commit: c85b4e1c828ed1fb7f4063f965fe116215ca0244
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# ブランド承認済みアセットのContent Hubへのアップロード {#upload-brand-approved-assets-content-hub}

[アセットを追加する権限を持つContent Hub ユーザー](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) は、ローカルファイルシステムからContent Hubにアセットを追加するか、OneDrive またはDropboxのデータソースからアセットを読み込むことができます。 ローカルファイルシステムで使用可能なフォルダー構造や、検索機能を強化するための OneDrive およびDropboxデータソースに関係なく、すべてのアセットがContent Hubの最上位に表示されます。

アセット検索をさらに強化するために、Content Hubでは次の操作を実行できます。

* キャンペーン名、キーワード、チャネルなど、アセットのアップロードに関連する重要な詳細を定義します。

* ファイルサイズ、形式、解像度、その他のプロパティなど、アップロードに成功した場合に、各アセットのその他のプロパティを自動的に生成します。

* 提供される人工知能を利用する [Adobe Sensei](https://www.adobe.com/jp/sensei.html) アップロードされたすべてのアセットに関連するタグを自動的に適用します。 スマートタグと呼ばれるこれらのタグは、関連するアセットをすばやく見つけるのに役立つので、プロジェクトのコンテンツベロシティ（コンテンツ創出の速度）が向上します。

必ず [Content Hubへのブランド承認アセット](/help/assets/approve-assets.md).

![ブランド承認済みアセットのアップロード](assets/upload-brand-approved-assets.png)

## 前提条件 {#prerequisites-add-assets}

[アセットを追加する権限を持つContent Hub ユーザー](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) は、Content Hubにアセットをアップロードできます。

## ローカルファイルシステムからContent Hubへのアセットの追加 {#add-assets-local-file-system}

Content Hubにアセットを追加するには、次の手順を実行します。

1. クリック **[!UICONTROL Assetsを追加]** を表示するには **[!UICONTROL 承認済みアセットの追加]** アップロードを作成できるダイアログボックス。

1. が含まれる **[!UICONTROL ここにファイルまたはフォルダーをドラッグ]** セクション右側のウィンドウで使用できます。ローカルファイルシステムからアセットをドラッグするか、をクリックします **[!UICONTROL 参照]** ローカルファイルシステム上で使用可能なファイルまたはフォルダーを手動で選択する。 アップロードに含まれるファイルのリストは、リストとして使用できます。


   また、サムネールを使用して選択した画像をプレビューし、X アイコンをクリックして、リストから特定の画像を削除することもできます。 X アイコンは、画像の名前またはサイズの上にマウスを置いた場合にのみ表示されます。 次をクリックすることもできます **[!UICONTROL すべて削除]** をクリックして、アップロードリストからすべての項目を削除します。

   アップロード処理を完了し、を有効にするには **[!UICONTROL アップロードボタン]**&#x200B;の場合は、アセットをキャンペーン名の下にグループ化する必要があります。

   ![Content Hubへのアセットのアップロード](assets/upload-assets-content-hub.png)

1. を使用してアップロードの名前を定義する **[!UICONTROL キャンペーン名]** フィールド。 既存の名前を使用することも、新しい名前を作成することもできます。 Content Hubには、名前を入力する際に表示される追加のオプションが用意されています。 <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   ベストプラクティスとして、Adobeでは残りのフィールドに値を指定し、アップロードしたアセットの検索エクスペリエンスを強化することをお勧めします。

1. 同様に、の値を定義します **[!UICONTROL キーワード]**, **[!UICONTROL チャネル]**, **[!UICONTROL 期間]**、および **[!UICONTROL 地域]** フィールド。 キーワード、チャネル、場所別にアセットのタグ付けとグループ化を行うと、承認済みの会社コンテンツを使用するすべてのユーザーがこれらのアセットを検索し、整理しておくことができます。

1. クリック **[!UICONTROL Upload]** Content Hubにアセットをアップロードする場合 [!UICONTROL 詳細を確認] 確認ボックスが表示されます。 「[!UICONTROL 続行]」をクリックします。

1. Assetsがアップロードを開始します。 クリック [!UICONTROL 新規アップロード] をクリックして、アップロード手順を再開します。 クリック [!UICONTROL 完了] アップロードを完了します。

また、管理者は、アセットのアップロード時に表示される必須フィールドとオプションフィールド（キャンペーン名、キーワード、チャネルなど）を設定することもできます。 詳しくは、を参照してください [Content Hub ユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## OneDrive またはDropboxのデータソースからContent Hubへのアセットの追加 {#add-assets-onedrive-dropbox}

OneDrive またはDropboxのデータソースからContent Hubにアセットを追加するには：

1. クリック **[!UICONTROL Assetsを追加]** を表示するには **[!UICONTROL 承認済みアセットの追加]** onedrive またはDropboxからアセットを読み込むことができるダイアログボックス。

1. クリック **[!UICONTROL OneDrive]** または **[!UICONTROL Dropbox]** をクリックして読み込みプロセスを開始します。 Content Hubでは、OneDrive またはDropboxアカウントにログオンするように求めるメッセージが表示され、左側のウィンドウに OneDrive またはDropboxフォルダー構造が表示されます。

1. ファイル名またはフォルダー名の横にある「+」アイコンをクリックすると、選択した項目のリストに項目が表示されます。 Content Hub ポータルに追加する必要のあるファイルをすべて選択したら、手順 3 ～ 6 を繰り返します [ローカルファイルシステムからContent Hubへのアセットの追加](#add-assets-local-file-system) をクリックしてアップロードプロセスを完了します。

   ![OneDrive またはDropboxーからContent Hubへのアセットのアップロード](assets/add-assets-onedrive-dropbox.png)

また、管理者は、アセットのアップロード時に表示される必須フィールドとオプションフィールド（キャンペーン名、キーワード、チャネルなど）を設定することもできます。 詳しくは、を参照してください [Content Hub ユーザーインターフェイスの設定](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

