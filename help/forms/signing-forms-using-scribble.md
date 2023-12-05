---
title: 手書き署名を使用してフォームに電子署名を適用する方法を教えてください。
description: 手書き署名を使用してフォームに電子署名を適用する方法を説明します。
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 75%

---

# 手書き署名を使用したフォームの E 署名{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/creating-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | この記事 |


**手書き署名**&#x200B;コンポーネントや&#x200B;**署名ステップ**&#x200B;コンポーネントを使用すると、アダプティブフォームに手書きで署名できます。署名ステップコンポーネントでは、アダプティブフォームの PDF バージョンが表示されます。署名ステップコンポーネントを使用するには、「レコードのドキュメント」オプションが有効なアダプティブフォームか、フォームテンプレートベースのアダプティブフォームが必要です。

![手書き署名ダイアログ](assets/scribble-signature.png)

## 署名ウィンドウで使用できる様々なオプション

* **A：** **ペイントブラシ**&#x200B;アイコンをクリックして、キャンバスに署名を描きます。
* **B：** **消去**&#x200B;アイコンをクリックして、キャンバス上の署名を消去します。
* **C：** **位置情報**&#x200B;アイコンをクリックして、署名とともに位置情報を追加します。
* **D：** **キーボード**&#x200B;アイコンをクリックして、キャンバスに名前を入力します。

「完了」を選択したら、 ![aem_forms_save](assets/aem_forms_save.png) 手書き署名ウィンドウのアイコンを使用すると、署名を編集できません。 署名を編集する場合は、現在の署名を無視して、上記のペイントブラシ／キーボードオプションを使用して再署名する必要があります。

次の項目を選択できます。 **設定** ![設定アイコン](assets/configure.png) アイコンをクリックして、手書き署名キャンバスの縦横比を設定します。
* 手書き署名キャンバスのアスペクト比が 1 未満の場合、位置情報は手書き署名キャンバスの下部に追加されます。


* 手書き署名キャンバスのアスペクト比が 1 を超える場合、位置情報は手書き署名キャンバスの右側に追加されます。


![手書き署名 -下部](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>署名は常に PNG 形式で保存されます。
>

## 手書き署名を使用するためのアダプティブフォームの設定 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 「レコードのドキュメント」オプションが有効なアダプティブフォームか、フォームテンプレートベースのアダプティブフォームを作成します。詳しい手順については、「[アダプティブフォームの作成](creating-adaptive-form.md)」を参照してください。
1. **手書き署名**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。
1. を選択します。 **設定** ![設定](assets/configure.png) アイコン。 この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 署名ステップコンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

1. コンテンツブラウザーで、「 」を選択します。 **フォームコンテナ**&#x200B;をクリックし、 **設定** ![設定アイコン](assets/configure.png) アイコン。 この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。に移動します。 **アダプティブフォームコンテナ** > **電子署名** を選択し、選択を解除します。 **Adobe Signを有効にする** オプション。 「完了」を選択します。 ![aem_forms_save](assets/aem_forms_save.png) アイコンをクリックして変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「Adobe Sign を有効にする」オプションが自動的に選択されます。

1. を選択します。 **設定** ![設定](assets/configure.png) アイコン。 この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名**：コンポーネントの名前を指定します。

   * **タイトル：** コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：** 署名メッセージの読み込み中に表示するPDFを指定します。 Adobe Signサービスでは、署名PDFの準備と読み込みに時間がかかります。
   * **署名サービス：**「**手書き署名**」オプションを選択します。

   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。Adobeは、 [テーマ](themes.md) および [インラインスタイル](inline-style-adaptive-forms.md) を使用します。

   「完了」を選択します。 ![aem_forms_save](assets/aem_forms_save.png) アイコンをクリックして変更を保存します。 署名が正常に設定されました。

   これで、フォームを記入する際に、PDF バージョンのアダプティブフォームが表示され、PDF ドキュメントの署名オプションが提供されます。詳しくは、「[手書き署名を使用したアダプティブフォームの署名](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. フォームへの記入を完了して署名ステップページに到達すると、署名画面が表示されます。

   ![EchoSign ページの署名画面](assets/esignscribblesign.jpg)

1. クリック **[!UICONTROL 署名]**. 手書き署名ダイアログが表示されます。 フォームに署名し、完了 ![aem_forms_save](assets/aem_forms_save.png) アイコンをクリックして、変更内容を保存します。

   ![手書き署名ダイアログ](assets/scribblewidget.png)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。

## 関連トピック {#see-also}

{{see-also}}