---
title: フォームにバージョン、コメント、注釈を追加します。
description: アダプティブフォームのコアコンポーネントを使用して、アダプティブフォームにコメント、注釈、バージョンを追加します。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Adaptive Forms, Core Components
hidefromtoc: true
source-git-commit: 4e60d7315fe7a92d608f0858a7108f7590e9aefa
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# アダプティブフォームのバージョン管理、レビュー、コメント作成

<!--Before you can use versionings, comments, and annotations in an Adaptive Form, you must ensure you have [enabled Adaptive Form Core Components](
https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components).-->

<!--Adaptive Form Core Components facilitates to add versionings, comments, and annotations to a form. These features helps form authors and users to enhance the form development process where they can create multiple versions of a form, collaborate and add their comments to a form, and add annotations to form components.-->

<span class="preview"> これはプレリリース機能で、 [プレリリースチャネル](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=ja?cloud-environments). </span>


アダプティブフォームのコアコンポーネントには、フォーム作成者がバージョン管理、コメント、注釈をフォームに組み込むことができる機能が用意されています。 これらの機能を使用すると、複数のバージョンのフォームの作成と管理、コメントによる協調ディスカッション、特定のフォームコンポーネントへの注釈の付加が可能になり、フォーム開発プロセスを合理化できます。


## アダプティブフォームのバージョン管理 {#adaptive-form-versioning}

アダプティブフォームのバージョン管理は、フォームにバージョンを追加する場合に役立ちます。 フォーム作成者は、複数のバージョンのフォームを簡単に作成し、最後に、ビジネス目標に適したフォームを使用できます。 また、フォームユーザーは以前のバージョンに戻すこともできます。 また、作成者は、フォームをプレビューして、2 つのバージョンのフォームを比較でき、UI の観点からフォームをより適切に分析できます。 各アダプティブフォームのバージョン管理機能について詳しく説明します。

### フォームバージョンの作成 {#create-a-form-version}

フォームのバージョンを作成するには、次の手順に従います。

1. フォームを作成するか、既存のフォームを使用します。
1. AEM UI で、 **[!UICONTROL フォーム]**>>**[!UICONTROL Forms &amp; Documents]** を選択し、 **フォーム**.
1. 左側のパネルの選択ドロップダウンで、「 」を選択します。 **[!UICONTROL バージョン]**.
   ![フォームを選択](select-a-form.png)
1. 次をクリック： **三点** 左側の下のパネルにある、 **[!UICONTROL バージョンとして保存]**.
1. 次に、フォームバージョンのラベルを指定し、コメントを通じてフォームに関する情報を指定できます。
   ![フォームバージョンの作成](create-a-form-version.png)

### フォームのバージョンを更新する {#update-a-form-version}

アダプティブフォームを編集して更新する場合、新しいバージョンをフォームに追加します。 最後の節で示す手順に従って、画像に示すようにフォームの新しいバージョンに名前を付けます。

![フォームのバージョンを更新する](update-a-form-version.png)

### フォームのバージョンを元に戻す {#revert-a-form-version}

フォームのバージョンを以前のバージョンに戻すには、フォームのバージョンを選択して、 **[!UICONTROL このバージョンに戻る]**.

![フォームのバージョンを元に戻す](revert-form-version.png)

### フォームのバージョンの比較 {#compare-form-versions}

フォーム作成者は、プレビュー用に 2 つの異なるバージョンのフォームを比較できます。 バージョンを比較するには、任意のフォームバージョンを選択して、 **[!UICONTROL 現在と比較]**. プレビューモードでは、2 つの異なるフォームバージョンが表示されます。

![フォームのバージョンの比較](compare-form-versions.png)

## コメントを追加 {#add-comments}

レビューとは、1 人または複数のレビュー担当者がフォームにコメントすることを許可するメカニズムです。 フォームのユーザーは誰でも、コメントを使用してフォームにコメントしたり、フォームをレビューしたりできます。 フォームにコメントを付けるには、 **[!UICONTROL フォーム]**&#x200B;をクリックし、 **[!UICONTROL コメント]** をフォームに追加します。

>[!NOTE]
> 上記の説明に従ってアダプティブフォームのコアコンポーネントでコメントを使用すると、フォームの機能が使用されます [フォームのレビューの作成と管理](/help/forms/create-reviews-forms.md) は無効です。


![フォームにコメントを追加する](form-comments.png)

## 注釈の追加 {#adaptive-form-annotations}

多くの場合、フォームグループのユーザーは、レビュー目的で、フォームの特定のタブやフォームのコンポーネントなどに注釈を追加する必要があります。 その場合、作成者は注釈を使用できます。 フォームに注釈を追加するには、次の手順を実行します。

1. でフォームを開く **[!UICONTROL 編集]** モード。

1. 次をクリック： **アイコンを追加** は、画像内で指定された右上のレールに配置されます。
   ![注釈](annotation.png)

1. 次をクリック： **アイコンを追加** は、画像内の左上のレールに配置され、表記を追加します。
   ![注釈を追加](add-annotation.png)

1. コメントを追加し、複数の色でスケッチを描画して、コンポーネントを形成できるようになりました。

1. フォームに追加されたすべての注釈を表示するには、フォームを選択し、画像に示すように、左側のパネルに追加された注釈を表示します。

   ![追加された注釈を参照](see-annotations.png)











