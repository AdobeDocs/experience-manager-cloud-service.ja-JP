---
title: コンテンツハブでのコレクションの管理
description: コンテンツハブでのコレクションの管理方法について説明します。
role: User
exl-id: ea74456c-f980-4a02-b26b-d7c46dac6aee
source-git-commit: 5c275b305dc128f158dfdac035595e4bb77960a9
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 77%

---

# [!DNL Content Hub] でのコレクションの管理 {#manage-collections}

<!-- ![Manage collections](assets/manage-collections.jpg) -->
![コレクションの管理](assets/manage-collection.png)

コレクションとは、ユーザー間で共有できる一連のアセットを指します。参照整合性を維持しながら、1 つのコレクションに異なる複数の場所のアセットを含めることができます。

[!DNL Content Hub] では、公開コレクションを作成できます。これらのコレクションは、資格を持つすべてのユーザーがアクセス可能で、複数のユーザーが効率的にコンテンツにアクセスして利用できる共有スペースが作成されます。コレクションは、リソースの共同使用を促進し、効率性と利便性を高めます。コレクションの参照ページ内では、次の操作を実行できます。

* **作成**：1 つ以上のコレクションを作成します。
* **表示**：アセットとそのプロパティを表示します。
* **共有**：アセットをリンクとして他のユーザーと共有します。
* **ダウンロード**：アセットをダウンロードします。
* **除去**：コレクションから特定のアセットを除去します。
* **削除**：コレクション全体を削除します。
* **ピン留め/ピン留めを解除**：コレクションをピン留めまたはピン留めを解除します。
* **お気に入り**：コレクションをお気に入りに登録します。

これにより、ユーザーは [!DNL Content Hub] 内で使用可能な様々なアセットに簡単にアクセスして管理できます。

## 前提条件 {#prerequisites}

[Content Hub ユーザー](deploy-content-hub.md#onboard-content-hub-users)は、この記事で説明されているアクションを実行できます。

## コレクションの作成{#create-collections}

ガバナンスを管理しながら、[新しいコレクションを作成](#create-new-collection)するか、[既存のコレクションにアセットを追加](#add-assets-to-existing-collection)するかを選択できます。

### 新しいコレクションの作成{#create-new-collection}

コレクションの作成時にアクセスを制御するには、次の手順を実行します。

1. 「**[!DNL Collections]**」タブに移動し、「**[!UICONTROL コレクションを作成]**」をクリックします。新しいコレクション ウィンドウが表示されます。

1. コレクションに「**[!UICONTROL タイトル]**」と「**[!UICONTROL 説明]**」を追加します。

   ![コレクション権限](assets/collection-permissions.png)

1. **[!UICONTROL アクセスできるユーザー]**&#x200B;ドロップダウンで、アクセス制御のタイプを選択します。以下のオプションが利用できます。

   | アクセス方法 | アクセスタイプ | 説明 |
   |---|---|---|
   | **自分と管理者のみが編集可能** | プライベート | このコレクションを編集およびコレクションにアクセスできるのは、作成者と管理者のみです。 |
   | **誰でも表示可能** | パブリック | すべてのユーザーがこのコレクションにアクセスできますが、編集できるのは作成者と管理者のみです。 |
   | **誰でも表示して編集可能** | パブリック | このコレクションは誰でも利用でき、制限なくフルアクセスと編集権限が付与されます。 |

   >[!NOTE]
   >
   > [!DNL Content Hub] 管理者は、**[!UICONTROL アクセスできるユーザー]**&#x200B;ドロップダウンで使用可能なすべてのオプションを表示できますが、通常のユーザーの場合は、アクセスできるオプションを[指定して設定](configure-content-hub-ui-options.md)する必要があります。

1. 「**[!UICONTROL 作成]**」をクリックします。完了したら、[コレクションにアセットを追加](#add-assets-to-existing-collection)できます。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

<!--
>[!NOTE]
>
>Collections governance is a limited availability feature. You can get it enabled  by creating a support ticket. Once enabled, you need to [Configure Collections in Content Hub](configure-content-hub-ui-options.md#configure-collections-content-hub).-->

<!--To create a new collection, navigate to the **[!UICONTROL Collections]** tab and click **[!UICONTROL Create new collection]**. Enter the **[!UICONTROL Title]** and provide an optional **[!UICONTROL Description]** for the assets. Click **[!UICONTROL Create]**.
![Create collection](assets/add-assets-collection.jpg)          
-->

### 既存のコレクションへのアセットの追加{#add-assets-to-existing-collection}

既存のコレクションにアセットを追加するには、コレクションに追加する必要があるアセットを選択します。「**[!UICONTROL コレクションに追加]**」をクリックします。コレクションを選択するプロンプトが表示されます。

![新しいコレクションの作成](assets/create-add-collection.jpg)

アセットを追加する必要があるコレクションを選択します。また、検索バーを使用して既存のコレクションを検索することもできます。<br>アセットを追加するコレクションを選択し、「**[!UICONTROL コレクションに追加]**」をクリックします。

## コレクションの表示{#view-collections}

「**[!UICONTROL コレクション]**」タブに移動し、コレクション名を検索します。フィルターを使用すると、特定の条件を選択して検索結果を絞り込み、最も関連性の高いコレクションをすばやく見つけることができます。

コレクションで使用可能なアセットのリストを表示するには、コレクション名をクリックします。また、コレクション内でフィルターを適用して、アセットの結果を絞り込むこともできます。コレクション内で表示する必要があるアセットをクリックします。[!DNL Content Hub] には、アセットの詳細ビューが表示されます。[詳しくは、アセットの詳細を参照してください](asset-properties-content-hub.md)。

### コレクション表示のフィルタリング {#filter-collections-view}

Content Hub では、環境設定に基づいてオプションを絞り込み、コレクションビューをフィルタリングして、探しているものを正確に簡単に見つけることができます。[Content Hub 内のコレクションの設定](configure-content-hub-ui-options.md#configure-collections-content-hub)を確認します。

コレクションビューをフィルタリングするには、「**[!DNL Collections]**」タブに移動し、「コレクション」ドロップダウンに移動します。次のいずれかのオプションを選択します。

* **[!UICONTROL すべてのコレクション]：**&#x200B;非公開または共有されているすべてのコレクションを表示および編集するには、このオプションを選択します。
* **[!UICONTROL 自分のみ]：**&#x200B;アクセス可能なコレクションを表示する場合は、このオプションを選択します。
* **[!UICONTROL すべてのユーザーが表示可能]：**&#x200B;このオプションでは、すべてのユーザーがアクセス可能で作成者のみが編集できるコレクションをフィルタリングできます。
* **[!UICONTROL すべてのユーザーが編集可能]：**&#x200B;すべてのユーザーがアクセス可能かつ編集可能なコレクションをフィルタリングする場合は、このオプションを選択します。

  ![コレクション表示のフィルタリング](assets/filter-collection-view.png)

さらに、アクセス権限に基づいてコレクションビューをフィルタリングするには、「**[!DNL Collections]**」タブに移動し、次のいずれかのオプションに移動します。

* **[!UICONTROL 任意のユーザーが作成]：**&#x200B;このフィルターを使用すると、任意のユーザーが作成したコレクションを表示できます。

* **[!UICONTROL 自分で作成]:**&#x200B;このフィルターは、自分が作成したコレクションを表示するように制限します。

  ![コレクション表示のフィルタリング](assets/filter-collection-view1.png)

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

詳しくは、[&#x200B; [!DNL Content Hub]](download-assets-content-hub.md) からアセットをダウンロードする方法を参照してください。

## コレクション内での使用可能なアセットの共有 {#share-assets-available-within-collection}

コレクション内で使用可能なアセットを共有することもできます。必ず [Content Hub で公開リンク共有を有効にする](configure-content-hub-ui-options.md#enable-public-link-sharing)ようにします。「**[!UICONTROL コレクション]**」タブに移動します。コレクションカードの ![共有アイコン](assets/share.svg) アイコンを選択します。共有リンクがコピーされます。コピーしたリンクを受信者と共有できます。詳しくは、[&#x200B; [!DNL Content Hub]](share-assets-content-hub.md) でのアセットの共有を参照してください。

Content Hub コレクションには、カスタマイズ可能な共有権限や共同作業機能など、効果的なアセット管理を行うための包括的なガバナンスツールが用意されています。読み取り専用アクセスから完全な管理制御に至るまで、これらの設定はアセット配布に対する微調整のガバナンスをサポートします。アセットを個別に、またはコレクションの一部として共有する場合、アクセス範囲は、ユーザーに割り当てられたコレクションの現在のアクセスレベルによって決定されます。また、プライベートコレクションを共有することはできません。

## コレクションの詳細の編集 {#edit-details-of-collection}

コレクションの&#x200B;**[!UICONTROL タイトル]**&#x200B;と&#x200B;**[!UICONTROL 説明]**&#x200B;を編集するには、コレクション名をクリックし、![情報アイコン](assets/info-icon.svg) アイコンをクリックします。[!UICONTROL コレクションの詳細]画面が表示され、コレクションの&#x200B;**[!UICONTROL タイトル]**&#x200B;と&#x200B;**[!UICONTROL 説明]**&#x200B;を編集できます。「**[!UICONTROL 変更を保存]**」をクリックして変更を確定します。さらに、コレクションへのアクセス権は、設定に応じて、コレクションを編集ダイアログで更新できます。

![コレクションの詳細](assets/collection-details.png)

## コレクションからのアセットの削除{#remove-assets-from-a-collection}

次のユーザーは、コレクションから 1 つまたは複数のアセットを削除できます。

* 管理者
* コレクションの所有者
* 編集権限を持つ管理者以外のユーザー

コレクションからアセットを削除するには、アセットを削除する必要があるコレクションをクリックし、アセットを選択して「**[!UICONTROL コレクションから削除]**」をクリックします。

![コレクションの削除](assets/remove-collection-new.jpg)

アセットの削除を確認するプロンプトが表示されます。「**[!UICONTROL 削除]**」をクリックします。\
選択したアセットはコレクションから正常に削除されました。

## コレクションの削除{#delete-collection}

コレクションを削除できるのは、管理者と作成者のみです。コレクションを削除するには、「**[!UICONTROL コレクション]**」タブに移動し、削除するコレクションをクリックします。![削除アイコン](assets/delete-icon.svg) アイコンをクリックして、コレクションを削除します。

## コレクションをピン留めまたはピン留めを解除 {#pin-unpin-collection}

Content Hub管理者は、クイックアクセス用にContent Hub内のコレクションをピン留めできます。 ピン留めされたコレクションは、コレクションのホームページの専用のピン留めセクションに表示されるので、重要なコレクションを手の届くところに簡単に保持できます。 クイックアクセス用に、次の手順を実行して、コレクションをピン留めまたはピン留めを解除できます。

1. ピン留めまたはピン留めを解除するコレクションを参照します。

1. **[!UICONTROL その他のアクション]**![&#x200B; その他のアクションアイコン &#x200B;](assets/do-not-localize/more-actions.png) をクリックし、**[!UICONTROL クイックアクセスにピン留め]** を選択します。 確認ボックスが表示されます。

   ![&#x200B; ピン コレクション &#x200B;](assets/pin-collection.png)

1. 「**[!UICONTROL ピン留め]**」をクリックして確定します。 非公開コレクションをピン留めすると、警告メッセージが表示されます。

   ![&#x200B; ピン留めの収集を確認 &#x200B;](assets/confirm-pin-collection.png)

   ピン留めされたコレクションは、クイックアクセスのために上部に表示されます。 または、コレクションのピン留めを解除するには、**[!UICONTROL その他のアクション]**![&#x200B; その他のアクション アイコン &#x200B;](assets/do-not-localize/more-actions.png) をクリックし、「**[!UICONTROL ピン留めを解除]** を選択します。

   ![&#x200B; ピン留めされたコレクションを表示 &#x200B;](assets/pinned-collections.png)

## コレクションをお気に入りとしてマーク {#favorite-collection}

Content Hubでコレクションをお気に入りに登録すると、コレクションの整理と取得が簡単になります。 追加すると、お気に入りのコレクションをContent Hub ホームページの「お気に入り」タブから簡単に使用できます。 さらに、お気に入りコレクション内でアセットを検索できます。 コレクションをお気に入りとしてマークするには、次の手順に従います。

1. ピン留めまたはピン留めを解除するコレクションを参照します。

1. **[!UICONTROL その他のアクション]**![&#x200B; その他のアクション &#x200B;](assets/do-not-localize/more-actions.png) アイコンをクリックし、**[!UICONTROL お気に入りに追加]** を選択して、コレクションをお気に入りに登録します。

   ![&#x200B; コレクションをお気に入りに登録 &#x200B;](assets/mark-favorite-collection.png)

   「お気に入り」としてマークされたコレクションが「**[!UICONTROL お気に入り]** タブに表示されるようになりました。 または、「お気に入り **[!UICONTROL からコレクションを削除することもでき]** す。 これを行うには、**[!UICONTROL その他のアクション]**![&#x200B; その他のアクション アイコン &#x200B;](assets/do-not-localize/more-actions.png) をクリックし、**[!UICONTROL お気に入りから削除]** を選択します。

   ![&#x200B; コレクションをお気に入りとして削除 &#x200B;](assets/remove-favorite-collection.png)

>[!NOTE]
>
>[&#x200B; コレクションをピン留めまたはピン留めを解除 &#x200B;](#pin-unpin-collection) および [&#x200B; コレクションをお気に入りとしてマーク &#x200B;](#favorite-collection) は、使用制限のある機能です。 Adobe カスタマーサポートケースを [&#x200B; 作成して送信 &#x200B;](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) して、デプロイメントで有効にすることができます。

