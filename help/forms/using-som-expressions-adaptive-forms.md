---
title: アダプティブFormsで SOM 式を使用するにはどうすればよいですか？
description: アダプティブFormsでパネルの SOM 式を抽出する方法を説明します。
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 75%

---


# アダプティブフォームでの SOM 式の使用 {#using-som-expressions-in-adaptive-forms}

アダプティブフォームは AEM ページとしてモデル化され、AEM リポジトリーで JCR コンテンツ構造で表示されます。コンテンツ構造のキー要素は guideContainer ノードです。 guideContainer の下に、ネストされたパネルとフィールドを含む rootPanel があります。

スクリプティングオブジェクトモデル (SOM) を使用して、特定のドキュメントオブジェクトモデル (DOM) 内の値、プロパティ、およびメソッドを参照できます。 DOM は、メモリオブジェクトとプロパティをツリー階層で整理します。 SOM 式は、フィールド/描画要素とパネルを参照します。

以下の画像は、コンポーネントをフォームに追加する際にアダプティブフォームが変換するノード構造を示しています。例えば、パネルをルートパネルに追加し、実行時に DOM に変換されるパネルにラジオボタンを追加できます。アダプティブフォームのラジオボタンフィールドには、`guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]` のように SOM 式を指定します。

![DOM ツリー](assets/hierarchy.png)

DOM ツリー

アダプティブフォーム内のすべての要素の SOM 式には、`guide[0].guide1[0]` というプレフィックスが付けられます。ノード構造階層のコンポーネントの場所は SOM 式の派生に使用されます。

![2 つのラジオボタンを持つ DOM ツリー](assets/hierarchy_radio_button.png)

2 つのラジオボタンを持つ DOM ツリー

アダプティブフォームでラジオボタンの位置を変更すると、SOM 式が変更されます。オーサリングモードでは、「SOM 式を表示」オプションを使用して [!DNL AEM Forms] 内のフィールドや要素の SOM 式を表示できます。このオプションはフィールドや要素を右クリックするとパネル上に表示されます。

![アダプティブフォームでの SOM 式の抽出](assets/som-expressions.png)

アダプティブフォームでの SOM 式の抽出

パネル内では、この機能にパネルツールバーからアクセスできます。この機能はアダプティブフォーム作成者のスクリプティングを促進します。

![パネルツールバーを使用した SOM 式の抽出](assets/som-expression.png)

パネルツールバーを使用した SOM 式の抽出

[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) に一覧表示されている API の一部は、要素の SOM 式を使用します。例えば、アダプティブフォーム内の特定のフィールドにフォーカスを移動するには、対応する SOM 式を `guideBridge` の `getFocus` API に渡します。
