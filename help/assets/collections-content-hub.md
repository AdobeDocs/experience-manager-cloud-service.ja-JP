---
title: Content Hubでのコレクションの管理
description: Content Hubでコレクションを管理する方法を学ぶ
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 3%

---

# でのコレクションの管理 [!DNL Content Hub] {#manage-collections}

<!-- ![Manage collections](assets/manage-collections.jpg) -->
![コレクションの管理](assets/manage-collection.png)

コレクションとは、ユーザー間で共有できる一連のアセットを指します。 コレクションには、参照整合性を維持しながら、様々な場所のアセットを含めることができます。

[!DNL Content Hub] 公開コレクションを作成できます。 これらのコレクションには、資格を持つすべてのユーザーがアクセスでき、複数のユーザーが効率的にコンテンツにアクセスして利用できる共有スペースを作成します。 コレクションは、効率と利便性を高めるために、リソースの共同利用を促進します。 コレクションの参照ページでは、次の操作を実行できます。

* **作成**:1 つ以上のコレクションを作成します。
* **表示**：アセットとそのプロパティを表示します。
* **共有**：アセットをリンクとして他のユーザーと共有します。
* **Download**：アセットのダウンロード
* **削除**：コレクションから特定のアセットを削除します。
* **削除**：コレクション全体を削除します。

これにより、ユーザーは、内で使用可能な様々なアセットに簡単にアクセスして管理できます [!DNL Content Hub].

## 前提条件 {#prerequisites}

[Content Hub ユーザー](deploy-content-hub.md#onboard-content-hub-users) この記事で取り上げるアクションを実行できます。

## コレクションの作成{#create-collections}

次のいずれかを選択できます。 [新しいコレクションを作成](#create-new-collection) または [既存のコレクションへのアセットの追加](#add-assets-to-existing-collection).

### 新しいコレクションを作成{#create-new-collection}

コレクションに追加する必要があるアセットを選択し、 **[!UICONTROL コレクションに追加]**.

![コレクションの作成](assets/add-assets-collection.jpg)

新しいコレクションを作成するには、に移動します **[!UICONTROL コレクション]** tab キーを押してクリック **[!UICONTROL 新しいコレクションを作成]**. を入力 **[!UICONTROL タイトル]** およびオプションを指定 **[!UICONTROL 説明]** アセット用。 「**[!UICONTROL 作成]**」をクリックします。

### 既存のコレクションへのアセットの追加{#add-assets-to-existing-collection}

既存のコレクションにアセットを追加するには、コレクションに追加する必要のあるアセットを選択します。 クリック **[!UICONTROL コレクションに追加]**. コレクションを選択するよう求められます。

![新しいコレクションを作成](assets/create-add-collection.jpg)

アセットを追加する必要があるコレクションを選択します。 検索バーを使用して既存のコレクションを検索することもできます。 <br>アセットを追加する必要があるコレクションを選択し、 **[!UICONTROL コレクションに追加]**.

## コレクションの表示{#view-collections}

に移動します。 **[!UICONTROL コレクション]** tab キーを押して、コレクション名を検索します。 コレクションで使用可能なアセットのリストを表示するには、コレクション名をクリックします。 コレクション内でフィルターを適用して、アセットの結果を絞り込むこともできます。

コレクション内で表示する必要があるアセットをクリックします。 [!DNL Content Hub] アセットの詳細表示を表示します。 [アセットの詳細を参照](asset-properties-content-hub.md).

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

## コレクション内で使用可能なアセットのダウンロード{#download-assets-within-collection}

コレクション内で使用可能なアセットをダウンロードするには、に移動します。 **[!UICONTROL コレクション]** タブ。\
クリック ![ダウンロードアイコン](assets/download-icon.svg) アイコンがコレクションカードに表示されます。

![「コレクション」タブ](assets/download-collection.jpg)

コレクション内のすべてのアセットがダウンロードされます。

コレクションを開いて、アセットを個別にダウンロードすることもできます。 ダウンロードするアセットを含んだコレクションをクリックします。 アセットを選択し、 **[!UICONTROL Download]**.

方法を学ぶ [からのアセットのダウンロード [!DNL Content Hub]](download-assets-content-hub.md).

## コレクション内で使用可能なアセットの共有 {#share-assets-available-within-collection}

コレクション内で使用可能なアセットを共有することもできます。 に移動します。 **[!UICONTROL コレクション]** タブ。 「」を選択します ![共有アイコン](assets/share.svg) アイコンがコレクションカードに表示されます。 共有リンクがコピーされます。 コピーしたリンクは受信者と共有できます。 の詳細情報 [でのアセットの共有 [!DNL Content Hub]](share-assets-content-hub.md).

## コレクションの詳細の編集 {#edit-details-of-collection}

を編集します **[!UICONTROL タイトル]** および **[!UICONTROL 説明]** コレクションのコレクション名をクリックし、 ![情報アイコン](assets/info-icon.svg) アイコン。 [!UICONTROL コレクションの詳細] 画面が表示され、 **[!UICONTROL タイトル]** および **[!UICONTROL 説明]** コレクションの。 クリック **[!UICONTROL 変更を保存]** 変更を確認します。

![コレクションの詳細](assets/collection-details.png)

## コレクションからのアセットの削除{#remove-assets-from-a-collection}

コレクションから 1 つまたは複数のアセットを削除できます。 コレクションからアセットを削除するには、アセットを削除するコレクションをクリックし、アセットを選択して、 **[!UICONTROL コレクションから削除]**.

![コレクションを削除](assets/remove-collection-new.jpg)

アセットの削除を確認するプロンプトが表示されます。 「**[!UICONTROL 削除]**」をクリックします。\
選択したアセットはコレクションから正常に削除されました。

## コレクションの削除{#delete-collection}

コレクションを削除するには、に移動します **[!UICONTROL コレクション]** tab キーを押しながら、削除するコレクションをクリックします。 クリック ![アイコンを削除](assets/remove-icon.svg) アイコンをクリックしてコレクションを削除します。
