---
title: フォームのフィールドのための文脈依存ヘルプの作成
seo-title: Authoring in-context help for form fields
description: AEM Forms では、文脈依存ヘルプをテキストまたはビデオなどのリッチメディアの形でアダプティブフォームフィールドやパネルに追加することができます。
seo-description: AEM Forms allows you to add in-context help to Adaptive Form fields and panels, as text or rich media, including videos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---


# フォームのフィールドのための文脈依存ヘルプの作成{#authoring-in-context-help-for-form-fields}

## はじめに {#introduction}

エンドユーザーがフォームに記入しているときに、特定のフォームフィールドへの記入方法がわからない場合があります。そのような問題を解決するために、アダプティブフォームでは、テキストのまたは高度な文脈依存ヘルプをフォームフィールドに追加できるようにしています。これにより、フォーム入力エクスペリエンスを向上し、エンドユーザーにとっての曖昧さを回避することができます。

この記事では、アダプティブフォームの作成中に文脈依存ヘルプを追加する方法を説明します。

## 文脈依存ヘルプの追加 {#add-in-context-help}

文脈依存ヘルプは、サイドバーにある「プロパティ」タブの「ヘルプコンテンツ」セクションで、次のオプションを利用して指定できます。

* [簡単な説明](authoring-in-field-help.md#p-short-description-p)
* [詳細な説明](authoring-in-field-help.md#p-long-description-p)

![フォームのフィールドのための文脈依存ヘルプ](assets/descriptions.png)

>[!NOTE]
>
>詳細な説明は簡単な説明をオーバーライドします。両方を指定した場合は、詳細な説明のみが表示されます。

### 簡単な説明 {#short-description}

簡単な説明フィールドは、フォームフィールドの記入に関する短く簡単なヒントを提供するためにあります。簡単な説明内で指定されたテキストは、フィールドの上にカーソルを移動させると、ツールヒントとして表示されます。

![フォームフィールドへの文脈依存ヘルプの追加の簡単な説明](assets/tooltip.png)

>[!NOTE]
>
>ヘルプテキストを常にフィールドの下に表示するには、「**簡単な説明を常に表示する**」を選択します。

![フィールドの下に永久的に表示される簡単な文脈依存ヘルプ](assets/short1.png)

### 詳細な説明 {#long-description}

「詳細な説明」フィールドを使って、文脈依存ヘルプに長いテキストを指定したり、ビデオなどのリッチメディアコンテンツを埋め込んだりすることができます。例えば、次の画像では文脈依存ヘルプとしてビデオを埋め込む方法を示しています。

![フォームフィールドのための文脈依存ヘルプとしてのリッチメディアの追加](assets/long-descriptions.png)

詳細な説明を追加すると、**が表示されますか？** アイコンがフィールドの隣に表示されます。アイコンをクリックすると、「詳細な説明」セクションに追加されたコンテンツが表示されます。

![リッチメディアを使用した文脈依存ヘルプの例](assets/photoshop.png)

### パネルレベルのヘルプ {#panel-level-help}

フォームフィールドの文脈依存ヘルプに加え、パネル編集ダイアログの「ヘルプコンテンツ」タブから、パネルレベルでヘルプを指定することができます。

![フォームパネルへの文脈依存ヘルプの追加](assets/panel-level-help.png)

パネルにヘルプを追加すると、**が表示されますか？** アイコンがパネルの説明の隣に表示されます。アイコンをクリックすると、パネル編集ダイアログの「ヘルプコンテンツ」セクションに追加されたコンテンツが表示されます。

![フォームパネルレベルでの文脈依存ヘルプの例](assets/photoshop-1.png)

