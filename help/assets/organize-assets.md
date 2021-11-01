---
title: デジタルアセットを整理します
description: Experience Managerを使用して、デジタルアセット、画像、ファイル、フォルダーなどを整理します。
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 843d6660fc2a2048d138601b4b74ee9f2faa54c9
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 7%

---

# デジタルアセットを整理します {#organize-digital-assets}

Microsoft® Office ドキュメントとPDFドキュメントのすべてのデジタルアセット、メタデータ、コンテンツが抽出され、検索可能になります。 検索することでアセットの高度なフィルター処理が可能になり、適切な権限を完全に活用できます。メタデータについて詳しくは、「デジタルアセット管理」の「メタデータ」で説明しています。

[!DNL Experience Manager Assets] は、コンテンツを複数の方法で整理できます。 フォルダーを使用して階層形式で整理したり、タグなどの順序なしのアドホック方法で整理したりできます。 ユーザーは、DAM アセットエディターでタグを編集できます。このエディターでは、サブアセット、レンディションおよびメタデータが表示されます。

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them more easy to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## フォルダー内のアセットの整理 {#organize-using-folders}

アセットを整理する最も基本的な方法は、アセットをフォルダーに保存することです。 これは、ローカルファイルシステム内のフォルダー内のファイルを整理する場合と似ています。 フォルダーの作成および管理方法について詳しくは、 [アセットの管理](manage-digital-assets.md). ファイルやフォルダーの命名方法、サブフォルダーの配置方法、これらのフォルダー内のファイルの処理方法は、アセットの処理方法に大きな影響を与える可能性があります。 一貫性のある適切なファイルおよびフォルダーの命名戦略を使用すると、優れたメタデータプラクティスと共に、デジタルアセットリポジトリを最大限に活用できます。

* 通常、デジタルアセットリポジトリは常に成長しています。 したがって、コンテンツ作成サイクルの早い段階で、メタデータの使用、フォルダー構造およびファイル名を形式化することが重要です。
* フォルダーは、デジタルアセットに対して一貫性のあるストレージ構造を適用する目的のみで使用します。この一貫性により、プロセスが向上し、アセットの管理が向上します。 例えば、次のタイプのフォルダーに配置されたアセットは、アセットの区別に役立ちます。

   * **開発フォルダー**:には、現在作業中のデジタルアセットが含まれています。
   * **クライアントフォルダー**:には、クライアント名またはプロジェクト名に基づくデジタルアセットが含まれます。
   * **プライマリフォルダー**:には、オリジナルのソースデジタルアセットが含まれています。
   * **レンディションフォルダー**:には、オリジナルのソースデジタルアセットのレンディションとコピーが含まれます。
   * **ファイルサイズフォルダー**:には、ファイルサイズの大、中、小に応じてデジタルアセットを格納します。
   * **ステージングフォルダー**:には、Web サイトへの公開の準備ができたデジタルアセットが含まれています。
   * **MIME タイプフォルダー**:には、画像、ドキュメント、マルチメディアなど、MIME タイプに固有のデジタルアセットが含まれます。
   * **フォルダーをアーカイブ**:には、公開を終了したデジタルアセットが含まれています。
   * **日付ベースのフォルダー**:は、作成日または最終変更日に基づいてデジタルアセットを格納します。

* カスタマイズや自動化が引き続き機能するように、変更される可能性の低いフォルダのディレクトリを作成します。 例えば、割り当てられた処理プロファイルは引き続き機能します。
* アセットが既に公開されている場合は、 [!DNL Experience Manager] をクリックして、アセットを別のフォルダーに移動し、新しい場所から再公開します。 元の公開済みアセットの場所は、新しく再公開されたアセットと共に引き続き使用できます。 ただし、元の公開済みアセットは *消失* から [!DNL Experience Manager] およびを非公開にすることはできません。 したがって、ベストプラクティスとして、まずアセットを非公開にしてから、別のフォルダーに移動します。

## タグを使用してアセットを整理する {#use-tags-to-organize-assets}

タグをメタデータとして使用すると、アセットの検索、検索結果を使用したコレクションの作成、一部のアセットの検索ランキングの上昇、アセット検出用のAdobe Senseiの AI アルゴリズムの適用を簡単におこなえます。

[!DNL Adobe Experience Manager Assets] は、自己学習アルゴリズムを使用して、非常に説明的なタグを作成し、数回のクリックで適切なアセットを見つけることができます。 スマートタグは、Adobe Sensei、人工知能および機械学習フレームワークを使用します。これらは、標準タグとビジネス固有のタグの両方を画像に認識し、適用するようにトレーニングできます。 スマートタグでは、コンテンツ、個々の単語またはフレーズを識別し、アセットに対して説明タグを自動的に適用することもできます

詳しくは、次の記事を参照してください。

* [アセットメタデータの編集](meta-edit.md)
* [アセットのスマートタグ](smart-tags.md)

## コレクションとして整理 {#organize-as-collections}

内のアセットコレクションを使用 [!DNL Experience Manager Assets]を使用すると、ユーザー間でアセットを作成、編集および共有する機能を合理化できます。 使用方法に基づいて複数のタイプのコレクションを作成します。例えば、アセット、フォルダー、コレクションの静的な参照リストを含むコレクションや、検索条件に基づいてアセットを取り込むコレクションなどです。 様々な場所のアセットを使用してコレクションを作成し、様々なレベルのアクセス、表示および編集権限を持つ複数のユーザーと共有できます。

詳しくは、 [コレクションの管理](manage-collections.md)


## プロファイルを使用したアセットの整理 {#organize-to-use-profiles}

処理プロファイルには [!DNL Assets] 事前定義済みフォルダーにアップロードされるアセットに適用される処理コマンド。 プロファイルは、フォルダーのコンテンツや新しくアップロードされたアセットの処理を自動化するために使用されます。 プロファイルを使用すると、アセットをより整理できます。

メタデータの使用、ファイル名、フォルダー構造を標準化することで、デジタルアセットのプールが増えるにつれて、より高い精度と一貫性を保ってフォルダーに処理プロファイルを適用できます。

>[!MORELIKETHIS]
>
>* [アセットマイクロサービスと処理プロファイルの使用](asset-microservices-configure-and-use.md)
>* [メタデータプロファイル](metadata-profiles.md)
>* [ビデオプロファイル](/help/assets/dynamic-media/video-profiles.md)
>* [Dynamic Mediaイメージプロファイル](/help/assets/dynamic-media/image-profiles.md)


