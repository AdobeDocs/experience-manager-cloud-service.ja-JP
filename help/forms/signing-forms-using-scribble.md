---
title: 手書き署名を使用したフォームへの電子サインの適用方法
description: 手書き署名を使用したフォームに電子サインを適用する方法を説明します。
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: ad28fd933a85c8b5ba1cdad4927f0a0a45ad478d
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 74%

---

# 手書き署名を使用したフォームの電子サイン{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/creating-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html?lang=ja#) |
| AEM as a Cloud Service | この記事 |


**手書き署名** コンポーネントを使用すると、アダプティブフォームに手書きで署名できます。<!-- The Signature step component displays a PDF version of the Adaptive Form. You require a Document of Record option enabled or form template based Adaptive Forms to use the Signature step component. -->

![手書き署名ダイアログ](assets/scribble-signature.png)

## 署名ウィンドウで使用できる様々なオプション

* **A：** **ペイントブラシ**&#x200B;アイコンをクリックして、キャンバスに署名を描きます。
* **B：** **消去**&#x200B;アイコンをクリックして、キャンバス上の署名を消去します。
* **C：** **位置情報**&#x200B;アイコンをクリックして、署名とともに位置情報を追加します。
* **D：** **キーボード**&#x200B;アイコンをクリックして、キャンバスに名前を入力します。

手書き署名ウィンドウで「完了」![aem_forms_save](assets/aem_forms_save.png) アイコンを選択すると、署名を編集できなくなります。署名を編集する場合は、現在の署名を無視して、上記のペイントブラシ／キーボードオプションを使用して再署名する必要があります。

「**設定**」![設定アイコン](assets/configure.png) アイコンを選択して、手書き署名キャンバスのアスペクト比を設定できます。
* 手書き署名キャンバスのアスペクト比が 1 未満の場合、位置情報は手書き署名キャンバスの下部に追加されます。


* 手書き署名キャンバスのアスペクト比が 1 を超える場合、位置情報は手書き署名キャンバスの右側に追加されます。


![手書き署名 -下部](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>署名は常に PNG 形式で保存されます。
>

## 手書き署名を使用するためのアダプティブフォームの設定 {#configure-an-adaptive-form-to-use-scribble-signature}

1. アダプティブフォームを編集モードで開きます。
1. **手書き署名**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。
1. 「**設定**」![設定](assets/configure.png) アイコンを選択します。この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。次の節で説明するように [ 手書き署名のプロパティを設定 ](#properties-of-scribble-signature-component) します。

   ![ 手書き署名 ](/help/forms/assets/scribblesig.png)

1. 「完了」![aem_forms_save](assets/aem_forms_save.png) アイコンを選択して、変更を保存します。署名が正常に設定されます。

## 手書き署名コンポーネントのプロパティの設定

設定ダイアログでは、訪問者による手書き署名コンポーネントのカスタマイズを簡単に行えます。

### 「基本」タブ

![「基本」タブ](/help/forms/assets/scribblesig-basic.png)

* **名前** - フォームコンポーネントは、フォーム内とルールエディター内の両方で一意の名前で簡単に識別できますが、名前にスペースや特殊文字を含めることはできません。

* **タイトル** - タイトルを使用すると、フォーム内のコンポーネントを簡単に識別できます。デフォルトでは、コンポーネントの上にタイトルが表示されます。 タイトルを追加しない場合、コンポーネントの名前がタイトルテキストの代わりに表示されます。

* **タイトルのリッチテキストを許可** - この機能により、ユーザーは、太字、斜体、下線付きのテキスト、様々なフォント、フォントサイズ、カラー、追加オプションなどの機能を組み込んで、プレーンテキストのタイトルを書式設定でき、視覚的なプレゼンテーションとカスタマイズが強化されます。 これにより、ドキュメント、web サイト、アプリケーション内でタイトルを目立たせる際の柔軟性とクリエイティブなコントロールが向上します。\
  「**タイトルのリッチテキストを許可**」 チェックボックスをオンにすると、コンポーネントのタイトルをスタイル設定するための書式設定オプションが表示されます。 使用可能なすべての書式設定オプションにアクセスするには、![全画面表示アイコン](/help/forms/assets/fullscreen-icon.png) タブをクリックします。

  ![リッチテキストのサポート](/help/forms/assets/richtext-support-title.png)

* **タイトルを非表示** - コンポーネントのタイトルを非表示にするには、このオプションを選択します。
* **必須フィールド** - フィールドを必須にするには、このオプションを選択します。
* **必須フィールドメッセージ** - **必須フィールドメッセージ** は、必須フィールドに入力せずにフォームを送信しようとすると、ユーザーに表示されるカスタマイズ可能なメッセージです。
* **データモデル連結参照** – 連結参照は、外部データソースに保存され、フォーム内で使用されるデータ要素への参照です。 バインド参照を使用すると、データをフォームフィールドに動的にバインドして、フォームにデータソースの最新のデータを表示できます。 例えば、フォームに入力された顧客 ID に基づいて、顧客の名前と住所をフォームに表示できます。 さらに、フォームに入力されたデータでデータソースを更新することもできます。 このようにして、AEM Forms で外部データソースとやり取りするフォームを作成し、データの収集と管理においてシームレスなユーザーエクスペリエンスを提供できます。
* **オブジェクトを非表示** - フォームでコンポーネントを非表示にする場合に、このオプションを選択します。 このコンポーネントは、他の目的（ルールエディターでの計算に使用するなど）にも利用できます。 これは、ユーザーが表示する必要のない情報や直接変更した情報を保存する必要がある場合に役立ちます。
* **オブジェクトの無効化** - コンポーネントを無効にする場合に、このオプションを選択します。 エンドユーザーは、無効になっているコンポーネントをアクティブにしたり、編集したりすることはできません。 ユーザーはフィールドの値を表示できますが、変更することはできません。 このコンポーネントは、他の目的（ルールエディターでの計算に使用するなど）にも利用できます。
* **アスペクト比** – 手書き署名コンポーネントのアスペクト比により、幅と高さの比例関係が定義されます。
* **フィールドレイアウト** - 「**フィールドレイアウト**」オプションでは、ラベル（キャプション）やエラーメッセージなどのフォーム要素をコンポーネントに対して配置する方法を指定します。 **ウィジェットの上部としてのキャプションとエラー** は、フィールドのキャプション（ラベル）とエラーメッセージをコンポーネントの上に配置します。 **アダプティブフォーム設定から継承** は、アダプティブフォーム設定で指定されたデフォルトのフィールドレイアウト設定を使用します。
* **CSS クラス** - **CSS クラス** を使用すると、スタイルシートで定義された 1 つ以上の CSS クラスを割り当てることで、コンポーネントにカスタムスタイルを適用できます。 これにより、アダプティブフォーム全体で一貫したスタイル設定とレイアウトのカスタマイズが可能になります。

### ヘルプの目次

![「ヘルプコンテンツ」タブ](/help/forms/assets/scribblesig-help.png)

* **短い説明** - 短い説明は、特定のフォームフィールドの目的に関する追加の情報や説明を提供する簡単な説明文です。 これにより、ユーザーは、フィールドに入力するデータの種類を理解しやすくなります。また、入力された情報が有効で目的の条件を満たしていることを確認できるように、ガイドラインや例を提供できます。 デフォルトでは、短い説明は非表示になっています。 「**短い説明を常に表示**」オプションを有効にすると、コンポーネントの下に説明が表示されます。

* **短い説明を常に表示** - このオプションを有効にすると、コンポーネントの下に短い説明が表示されます。

* **詳細な説明** - フォームフィールドの正しい入力を支援するために、ユーザーに提供される追加の情報やガイダンスを指します。 コンポーネントの横に配置されているヘルプアイコン（i）をクリックすると表示されます。 これは、フォームフィールドのラベルやプレースホルダーテキストよりも詳細な情報を提供し、ユーザーがフィールドの要件や制約を理解できるように設計されています。 また、フォームへの入力をより簡単かつ正確にするための提案や例を提供することも可能です。

### 「アクセシビリティ」タブ {#accessibility}

![「アクセシビリティ」タブ](/help/forms/assets/scribblesig-acc.png)

「**アクセシビリティ** 」タブでは、コンポーネントの [ARIA アクセシビリティ](https://www.w3.org/WAI/standards-guidelines/aria/)ラベルの値を設定できます。 スクリーンリーダー用のテキストを使用する場合は、次の様々なオプションを使用できます。

* **スクリーンReaderの優先順位** - スクリーンReaderの優先順位とは、視覚に障害のあるユーザーが使用する、支援テクノロジー（スクリーンリーダーなど）によって読み上げられる追加のテキストを指します。 このテキストでは、フォームフィールドの目的に関するオーディオの説明が提供され、フィールドのタイトル、説明、名前および関連するメッセージ（カスタムテキスト）に関する情報を含めることができます。 スクリーンリーダー用のテキストを使用すると、視覚に障害のあるユーザーを含むすべてのユーザーがフォームに確実にアクセスして、フォームフィールドとその要件を完全に理解できるようになります。

   * **カスタムテキスト**：ARIA アクセシビリティラベルにカスタムテキストを使用する場合は、このオプションを選択します。 このオプションを選択すると、「カスタムテキスト」ダイアログボックスが表示されます。 関連情報は、「カスタムテキスト」ダイアログボックスで追加できます。
   * **簡単な説明**:ARIA アクセシビリティラベルの説明を使用する場合は、このオプションを選択します。
   * **タイトル**：ARIA アクセシビリティラベルのタイトルを使用する場合は、このオプションを選択します。
   * **名前**：ARIA アクセシビリティラベルの名前を使用する場合は、このオプションを選択します。
   * **なし**：ARIA アクセシビリティラベルに追加しない場合は、このオプションを選択します。

<!--

 * **Element Name**: Specify name of the component.

    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.

    * **CSS Class**: Specify CSS class of the client library, if any. Adobe recommends using [themes](themes.md) and [in-line styles](inline-style-adaptive-forms.md) instead of CSS Class.
## Sign an Adaptive Form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an Adaptive Form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![aem_forms_save](assets/aem_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.png)

1. Click complete to finish the signing process.

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel. -->

## 関連トピック {#see-also}

{{see-also}}