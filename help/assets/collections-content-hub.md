---
title: コンテンツハブでのコレクションの管理
description: コンテンツハブでのコレクションの管理方法について説明します。
role: User
exl-id: ea74456c-f980-4a02-b26b-d7c46dac6aee
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 95%

---

# [!DNL Content Hub] でのコレクションの管理 {#manage-collections}

| [検索のベストプラクティス](/help/assets/search-best-practices.md) | [メタデータのベストプラクティス](/help/assets/metadata-best-practices.md) | [コンテンツハブ](/help/assets/product-overview.md) | [OpenAPI 機能を備えた Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開発者向けドキュメント](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Manage collections](assets/manage-collections.jpg) -->
![コレクションの管理](assets/manage-collection.png)

>[!AVAILABILITY]
>
>Content Hub ガイドがPDF形式で利用できるようになりました。 ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えます。
>
>[!BADGE Content Hub ガイドのPDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

コレクションとは、ユーザー間で共有できる一連のアセットを指します。参照整合性を維持しながら、1 つのコレクションに異なる複数の場所のアセットを含めることができます。

[!DNL Content Hub] では、公開コレクションを作成できます。これらのコレクションは、資格を持つすべてのユーザーがアクセス可能で、複数のユーザーが効率的にコンテンツにアクセスして利用できる共有スペースが作成されます。コレクションは、リソースの共同使用を促進し、効率性と利便性を高めます。コレクションの参照ページ内では、次の操作を実行できます。

* **作成**：1 つ以上のコレクションを作成します。
* **表示**：アセットとそのプロパティを表示します。
* **共有**：アセットをリンクとして他のユーザーと共有します。
* **ダウンロード**：アセットをダウンロードします。
* **除去**：コレクションから特定のアセットを除去します。
* **削除**：コレクション全体を削除します。

これにより、ユーザーは [!DNL Content Hub] 内で使用可能な様々なアセットに簡単にアクセスして管理できます。

## 前提条件 {#prerequisites}

[コンテンツハブユーザー](deploy-content-hub.md#onboard-content-hub-users)は、この記事で説明されているアクションを実行できます。

## コレクションの作成{#create-collections}

[新しいコレクションを作成](#create-new-collection)するか、[既存のコレクションにアセットを追加](#add-assets-to-existing-collection)するかを選択できます。

### 新しいコレクションの作成{#create-new-collection}

コレクションに追加する必要があるアセットを選択し、「**[!UICONTROL コレクションに追加]**」をクリックします。

![コレクションの作成](assets/add-assets-collection.jpg)

新しいコレクションを作成するには、「**[!UICONTROL コレクション]**」タブに移動し、「**[!UICONTROL 新しいコレクションを作成]**」をクリックします。アセットの&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力し、オプションで&#x200B;**[!UICONTROL 説明]**&#x200B;を入力します。「**[!UICONTROL 作成]**」をクリックします。

### 既存のコレクションへのアセットの追加{#add-assets-to-existing-collection}

既存のコレクションにアセットを追加するには、コレクションに追加する必要があるアセットを選択します。「**[!UICONTROL コレクションに追加]**」をクリックします。コレクションを選択するプロンプトが表示されます。

![新しいコレクションの作成](assets/create-add-collection.jpg)

アセットを追加する必要があるコレクションを選択します。また、検索バーを使用して既存のコレクションを検索することもできます。<br>アセットを追加するコレクションを選択し、「**[!UICONTROL コレクションに追加]**」をクリックします。

## コレクションの表示{#view-collections}

「**[!UICONTROL コレクション]**」タブに移動し、コレクション名を検索します。コレクションで使用可能なアセットのリストを表示するには、コレクション名をクリックします。また、コレクション内でフィルターを適用して、アセットの結果を絞り込むこともできます。

コレクション内で表示する必要があるアセットをクリックします。[!DNL Content Hub] には、アセットの詳細ビューが表示されます。[詳しくは、アセットの詳細を参照してください](asset-properties-content-hub.md)。

<!--
![Asset details](assets/view-collection.jpg)

* **A**: Details and metadata of the asset 
* **B**: Zoom In or Zoom Out the asset 
* **C**: Reset Zoom view 
* **D**: View the previous or next asset 
* **E**: Download the asset 
* **F**: Open the asset in Adobe Express 
* **G**: Hide the metadata of the asset 
* **H**: Share the asset as a link 
-->

## コレクション内での使用可能なアセットのダウンロード{#download-assets-within-collection}

コレクション内で使用可能なアセットをダウンロードするには、「**[!UICONTROL コレクション]**」タブに移動します。\
コレクションカードの ![ダウンロードアイコン](assets/download-icon.svg) アイコンをクリックします。

![「コレクション」タブ](assets/download-collection.jpg)

コレクションのすべてのアセットがダウンロードされます。

また、コレクションを開いて、アセットを個別にダウンロードすることもできます。ダウンロードする必要があるアセットを含むコレクションをクリックします。アセットを選択し、「**[!UICONTROL ダウンロード]**」をクリックします。

詳しくは、[ [!DNL Content Hub]](download-assets-content-hub.md) からアセットをダウンロードする方法を参照してください。

## コレクション内での使用可能なアセットの共有 {#share-assets-available-within-collection}

コレクション内で使用可能なアセットを共有することもできます。「**[!UICONTROL コレクション]**」タブに移動します。コレクションカードの ![共有アイコン](assets/share.svg) アイコンを選択します。共有リンクがコピーされます。コピーしたリンクを受信者と共有できます。詳しくは、[ [!DNL Content Hub]](share-assets-content-hub.md) でのアセットの共有を参照してください。

## コレクションの詳細の編集 {#edit-details-of-collection}

コレクションの&#x200B;**[!UICONTROL タイトル]**&#x200B;と&#x200B;**[!UICONTROL 説明]**&#x200B;を編集するには、コレクション名をクリックし、![情報アイコン](assets/info-icon.svg) アイコンをクリックします。[!UICONTROL コレクションの詳細]画面が表示され、コレクションの&#x200B;**[!UICONTROL タイトル]**&#x200B;と&#x200B;**[!UICONTROL 説明]**&#x200B;を編集できます。「**[!UICONTROL 変更を保存]**」をクリックして変更を確定します。

![コレクションの詳細](assets/collection-details.png)

## コレクションからのアセットの削除{#remove-assets-from-a-collection}

コレクションから 1 つまたは複数のアセットを削除できます。コレクションからアセットを削除するには、アセットを削除する必要があるコレクションをクリックし、アセットを選択して「**[!UICONTROL コレクションから削除]**」をクリックします。

![コレクションの削除](assets/remove-collection-new.jpg)

アセットの削除を確認するプロンプトが表示されます。「**[!UICONTROL 削除]**」をクリックします。\
選択したアセットはコレクションから正常に削除されました。

## コレクションの削除{#delete-collection}

コレクションを削除するには、「**[!UICONTROL コレクション]**」タブに移動し、削除するコレクションをクリックします。![削除アイコン](assets/remove-icon.svg) アイコンをクリックして、コレクションを削除します。
