---
title: コンテンツハブでのコレクションの管理
description: コンテンツハブでのコレクションの管理方法について説明します。
role: User
exl-id: ea74456c-f980-4a02-b26b-d7c46dac6aee
source-git-commit: 6bc838ff76edda3e03cbde8da4a28f65cba3b36a
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 57%

---

# [!DNL Content Hub] でのコレクションの管理 {#manage-collections}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime と Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets と Edge Delivery Services の統合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新規</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Dynamic Media Prime と Ultimate の有効化</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

<!-- ![Manage collections](assets/manage-collections.jpg) -->
![コレクションの管理](assets/manage-collection.png)

>[!AVAILABILITY]
>
>コンテンツハブガイドを PDF 形式で利用できるようになりました。ガイド全体をダウンロードし、Adobe Acrobat AI アシスタントを使用して質問に答えてください。
>
>[!BADGE コンテンツハブガイドの PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

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

[Content Hub ユーザー ](deploy-content-hub.md#onboard-content-hub-users) は、この記事で説明されるアクションを実行できます。

## コレクションの作成{#create-collections}

ガバナンスを管理しながら、[ 新しいコレクションを作成 ](#create-new-collection) または [ 既存のコレクションにアセットを追加 ](#add-assets-to-existing-collection) を選択できます。

### 新しいコレクションの作成{#create-new-collection}

コレクションの作成時にアクセスを制御するには、次の手順を実行します。

1. 「**[!DNL Collections]**」タブに移動し、「**[!UICONTROL コレクションを作成]** をクリックします。 新規コレクション ウィンドウが表示されます。

1. コレクションに **[!UICONTROL タイトル]** と **[!UICONTROL 説明]** を追加します。

   ![ コレクション権限 ](assets/collection-permissions.png)

1. **[!UICONTROL アクセスできるユーザー]** ドロップダウンで、アクセス制御のタイプを選択します。 以下のオプションが利用できます。

   | アクセス方法 | アクセスタイプ | 説明 |
   |---|---|---|
   | **自分と管理者のみがアクセスできます** | プライベート | このコレクションを編集してアクセスできるのは、作成者と管理者のみです。 |
   | **誰でもアクセス可能** | Public | すべてのユーザーがこのコレクションにアクセスできますが、編集できるのは作成者と管理者のみです。 |
   | **誰でもアクセスして編集できます** | Public | このコレクションは誰でも利用でき、制限なくフルアクセスと編集権限が付与されます。 |

1. 「**[!UICONTROL 作成]**」をクリックします。 完了したら、[ コレクションにアセットを追加 ](#add-assets-to-existing-collection) できます。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>コレクションガバナンスは限定提供の機能です。 有効にするには、サポートチケットを作成します。 有効にしたら、[Content Hubでコレクションを設定 ](configure-content-hub-ui-options.md#configure-collections-content-hub) する必要があります。

<!--To create a new collection, navigate to the **[!UICONTROL Collections]** tab and click **[!UICONTROL Create new collection]**. Enter the **[!UICONTROL Title]** and provide an optional **[!UICONTROL Description]** for the assets. Click **[!UICONTROL Create]**.
![Create collection](assets/add-assets-collection.jpg)          
-->

### 既存のコレクションへのアセットの追加{#add-assets-to-existing-collection}

既存のコレクションにアセットを追加するには、コレクションに追加する必要があるアセットを選択します。「**[!UICONTROL コレクションに追加]**」をクリックします。コレクションを選択するプロンプトが表示されます。

![新しいコレクションの作成](assets/create-add-collection.jpg)

アセットを追加する必要があるコレクションを選択します。また、検索バーを使用して既存のコレクションを検索することもできます。<br> アセットを追加する必要があるコレクションを選択し、**[!UICONTROL コレクションに追加]** をクリックします。

## コレクションの表示{#view-collections}

「**[!UICONTROL コレクション]**」タブに移動し、コレクション名を検索します。フィルターを使用すると、特定の条件を選択して検索結果を絞り込み、最も関連性の高いコレクションをすばやく見つけることができます。

コレクションで使用可能なアセットのリストを表示するには、コレクション名をクリックします。コレクション内でフィルターを適用して、アセットの結果を絞り込むこともできます。 コレクション内で表示する必要があるアセットをクリックします。[!DNL Content Hub] には、アセットの詳細ビューが表示されます。[詳しくは、アセットの詳細を参照してください](asset-properties-content-hub.md)。

### コレクション表示のフィルタリング {#filter-collections-view}

Content Hubでは、環境設定に基づいてオプションを絞り込むことで、コレクションビューをフィルタリングして、探しているものを正確に簡単に見つけることができます。 [Content Hub内のコレクションの設定 ](configure-content-hub-ui-options.md#configure-collections-content-hub) を確認します。

コレクションビューをフィルタリングするには、「」タブ **[!DNL Collections]** 移動し、「コレクション」ドロップダウンに移動します。 次のいずれかのオプションを選択します。

* **[!UICONTROL すべてのコレクション &#x200B;]:** 非公開で共有されているすべてのコレクションを表示するには、このオプションを選択します。
* **[!UICONTROL 自分のみ &#x200B;]:** アクセス可能なコレクションを表示する場合は、このオプションを選択します。
* **[!UICONTROL すべてのユーザーが表示 &#x200B;]:** すべてのユーザーがアクセスできるが、作成者のみが編集できるコレクションをフィルタリングできます。
* **[!UICONTROL すべてのユーザーが編集できます &#x200B;]:** すべてのユーザーがアクセス可能かつ編集可能なコレクションをフィルタリングする場合は、このオプションを選択します。

  ![ コレクション表示のフィルタリング ](assets/filter-collection-view.png)

さらに、アクセス権限に基づいてコレクションビューをフィルタリングするには、「**[!DNL Collections]**」タブに移動し、次のいずれかのオプションに移動します。

* **[!UICONTROL 任意のユーザーが作成 &#x200B;]:** このフィルターを使用すると、任意のユーザーが作成したコレクションを表示できます。

* **[!UICONTROL 自分で作成 &#x200B;]:** このフィルターは、自分が作成したコレクションを表示するように制限します。

  ![ コレクション表示のフィルタリング ](assets/filter-collection-view1.png)

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

![「コレクション」タブ](assets/download-collection.png)

コレクションのすべてのアセットがダウンロードされます。

また、コレクションを開いて、アセットを個別にダウンロードすることもできます。ダウンロードする必要があるアセットを含むコレクションをクリックします。アセットを選択し、「**[!UICONTROL ダウンロード]**」をクリックします。

詳しくは、[ [!DNL Content Hub]](download-assets-content-hub.md) からアセットをダウンロードする方法を参照してください。

## コレクション内での使用可能なアセットの共有 {#share-assets-available-within-collection}

コレクション内で使用可能なアセットを共有することもできます。必ず [Content Hubで公開リンク共有を有効にする ](configure-content-hub-ui-options.md#enable-public-link-sharing) ようにします。 「**[!UICONTROL コレクション]**」タブに移動します。コレクションカードの ![共有アイコン](assets/share.svg) アイコンを選択します。共有リンクがコピーされます。コピーしたリンクを受信者と共有できます。詳しくは、[ [!DNL Content Hub]](share-assets-content-hub.md) でのアセットの共有を参照してください。

Content Hubでコレクションを共有する際に、システム内のデジタルリソースに対して受信者が実行できるアクセス範囲とアクションを定義できます。 Content Hub Collections には、カスタマイズ可能な共有権限や共同作業機能など、効果的なアセット管理を行うための包括的なガバナンスツールが用意されています。 読み取り専用アクセスから完全な管理制御に至るまで、これらの設定はアセット配布に対する微調整のガバナンスをサポートします。

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



