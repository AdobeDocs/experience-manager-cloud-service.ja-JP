---
title: バージョン、コメント、注釈をフォームに追加します。
description: アダプティブフォームのコアコンポーネントを使用して、アダプティブフォームにコメント、注釈、バージョンを追加します。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Adaptive Forms, Core Components
exl-id: 84b95a19-c804-41ad-8f4b-5868c8444cc0
role: User, Developer, Admin
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# アダプティブフォームのバージョン管理、レビューおよびコメント

<!--Before you can use versionings, comments, and annotations in an Adaptive Form, you must ensure you have [enabled Adaptive Form Core Components](
https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components).-->

<!--Adaptive Form Core Components facilitates to add versionings, comments, and annotations to a form. These features helps form authors and users to enhance the form development process where they can create multiple versions of a form, collaborate and add their comments to a form, and add annotations to form components.-->

<span class="preview"> これはプレリリース機能で、 [プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja#new-features). </span>


アダプティブフォームのコアコンポーネントは、フォーム作成者がバージョン管理、コメント、注釈をフォームに組み込むための機能を提供します。 これらの機能を使用すると、ユーザーはフォームの複数のバージョンを作成および管理したり、コメントを通じて共同ディスカッションを行ったり、特定のフォームコンポーネントに注釈を添付したりできるので、フォーム作成プロセスが合理化され、フォーム作成全体のエクスペリエンスが向上します。


## アダプティブフォームのバージョン管理 {#adaptive-form-versioning}

アダプティブフォームのバージョン管理は、フォームにバージョンを追加するのに役立ちます。 フォーム作成者は、フォームの複数のバージョンを簡単に作成し、最終的にビジネス目標に適したバージョンを使用できます。 また、フォームユーザーは、フォームを以前のバージョンに戻すこともできます。 また、作成者は、フォームの 2 つのバージョンをプレビューして比較することが容易になり、UI の観点からフォームをより適切に分析できます。 次に、アダプティブフォームの各バージョン管理機能について詳しく説明します。

### フォームバージョンの作成 {#create-a-form-version}

フォームのバージョンを作成するには、次の手順に従います。

1. フォームを作成するか、既存のフォームを使用します。
1. AEM UI で、に移動します。 **[!UICONTROL フォーム]**>>**[!UICONTROL Formsとドキュメント]** を選択します **フォーム**.
1. 左パネルの選択ドロップダウンで、次を選択します **[!UICONTROL バージョン]**.
   ![フォームを選択](select-a-form.png)
1. 「」をクリックします **3 つのドット** 左側の下部パネルにある「」をクリックします。 **[!UICONTROL バージョンとして保存]**.
1. ここで、フォームバージョンにラベルを指定します。コメントを通じてフォームに関する情報を指定できます。
   ![フォームバージョンの作成](create-a-form-version.png)

### フォームバージョンの更新 {#update-a-form-version}

アダプティブフォームを編集および更新する際に、新しいバージョンをフォームに追加します。 最後の節で示した手順に従って、画像に示すようにフォームの新しいバージョンに名前を付けます。

![フォームバージョンの更新](update-a-form-version.png)

### フォームのバージョンを元に戻す {#revert-a-form-version}

フォームのバージョンを以前のバージョンに戻すには、フォームのバージョンを選択し、 **[!UICONTROL このバージョンに戻る]**.

![フォームのバージョンを元に戻す](revert-form-version.png)

### フォームのバージョンの比較 {#compare-form-versions}

フォーム作成者は、プレビュー目的で 2 つの異なるバージョンのフォームを比較できます。 バージョンを比較するには、任意のフォームバージョンを選択し、 **[!UICONTROL 現在と比較]**. プレビューモードで 2 つの異なるフォームバージョンが表示されます。

![フォームのバージョンの比較](compare-form-versions.png)

## コメントを追加 {#add-comments}

レビューとは、1 人または複数のレビュー担当者にフォームに対するコメントを許可するメカニズムです。 フォームユーザーは誰でも、コメントを使用してフォームにコメントしたり、フォームをレビューしたりできます。 フォームにコメントするには、 **[!UICONTROL フォーム]**&#x200B;を追加し、 **[!UICONTROL コメント]** をフォームに追加します。

>[!NOTE]
> 前述のように、アダプティブフォームのコアコンポーネントでコメントを使用する場合は、フォームの機能が有効になります [フォームに対するレビューの作成と管理](/help/forms/create-reviews-forms.md) が無効になっています。


![フォームへのコメントの追加](form-comments.png)

## 注釈を追加 {#adaptive-form-annotations}

多くの場合、フォームグループユーザーは、レビュー目的で（フォームの特定のタブやフォームのコンポーネントなど）、フォームに注釈を追加する必要があります。 このような場合、作成者は注釈を使用できます。 フォームに注釈を追加するには、次の手順を実行します。

1. でフォームを開きます **[!UICONTROL 編集]** モード。

1. 「」をクリックします **アイコンを追加** 画像に示すように右上のレールに配置されます。
   ![注釈](annotation.png)

1. 「」をクリックします **アイコンを追加** 注釈を追加するために、画像で示されているように左上のパネルに配置します。
   ![注釈を追加](add-annotation.png)

1. これで、コメントを追加したり、複数の色でスケッチを描画してフォームコンポーネントを作成したりできます。

1. フォームに追加されたすべての注釈を表示するには、フォームを選択すると、画像に示すように、左側のパネルに追加された注釈が表示されます。

   ![追加された注釈を参照](see-annotations.png)

## 関連トピック {#see-also}

{{see-also}}
