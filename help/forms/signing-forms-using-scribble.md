---
title: 手書き署名を使用したフォームへの電子署名の適用
seo-title: Apply electronic signatures to a form using scribble signatures
description: 手書きを使用したフォームへの署名
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 79%

---

# 手書き署名を使用したフォームへの電子署名の適用{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

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

手書き署名ウィンドウで、完了 ![aem_forms_save](assets/aem_forms_save.png) アイコンをタップすると、署名を編集できなくなります。署名を編集する場合は、現在の署名を無視して、上記の「ペイントブラシ」や「キーボード」オプションを使用して再署名する必要があります。

次をタップします。 **設定** ![設定アイコン](assets/configure.png) アイコンをクリックして、手書き署名キャンバスの縦横比を設定します。
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
1. **設定**（![設定](assets/configure.png)）アイコンをタップします。この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 署名ステップコンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームで使用できる全幅を取ります。 署名ステップコンポーネントを含むセクションには、他のコンポーネントを含めないことをお勧めします。

1. コンテンツブラウザーで、 **フォームコンテナ**&#x200B;をクリックし、 **設定** ![設定アイコン](assets/configure.png) アイコン この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。に移動します。 **アダプティブフォームコンテナ** > **電子署名** を選択し、選択を解除します。 **Adobe Signを有効にする** オプション。 完了 ![aem_forms_save](assets/aem_forms_save.png) アイコンをタップして、変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「Adobe Sign を有効にする」オプションが自動的に選択されます。

1. **設定**（![設定](assets/configure.png)）アイコンをタップします。これにより、プロパティブラウザーが開き、署名ステップのプロパティが表示されます。 以下のプロパティを設定します。

   * **要素名**：コンポーネントの名前を指定します。

   * **タイトル：** コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：** 署名メッセージの読み込み中に表示するPDFを指定します。 Adobe Signサービスでは、署名PDFの準備と読み込みに時間がかかります。
   * **署名サービス：**「**手書き署名**」オプションを選択します。

   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。CSS クラスの代わりに[テーマ](themes.md)や[インラインスタイル](inline-style-adaptive-forms.md)を使用することをお勧めします。

   完了 ![aem_forms_save](assets/aem_forms_save.png) アイコンをタップして、変更を保存します。署名が正常に設定されます。

   これで、フォームを記入する際に、PDF バージョンのアダプティブフォームが表示され、PDF ドキュメントの署名オプションが提供されます。詳しくは、「[手書き署名を使用したアダプティブフォームの署名](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. フォームへの記入を完了して署名ステップページに到達すると、署名画面が表示されます。

   ![EchoSign ページの署名画面](assets/esignscribblesign.jpg)

1. クリック **[!UICONTROL 署名]**. 手書き署名ダイアログが表示されます。 フォームに署名し、完了 ![aem_forms_save](assets/aem_forms_save.png) アイコンをクリックして、変更内容を保存します。

   ![手書き署名ダイアログ](assets/scribblewidget.png)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。
