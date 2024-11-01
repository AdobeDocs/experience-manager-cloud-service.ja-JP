---
title: 手書き署名を使用したフォームへの電子サインの適用方法
description: 手書き署名を使用したフォームに電子サインを適用する方法を説明します。
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 100%

---

# 手書き署名を使用したフォームの電子サイン{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/creating-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html?lang=ja#) |
| AEM as a Cloud Service | この記事 |


**手書き署名**&#x200B;コンポーネントや&#x200B;**署名ステップ**&#x200B;コンポーネントを使用すると、アダプティブフォームに手書きで署名できます。署名ステップコンポーネントでは、アダプティブフォームの PDF バージョンが表示されます。署名ステップコンポーネントを使用するには、「レコードのドキュメント」オプションが有効なアダプティブフォームか、フォームテンプレートベースのアダプティブフォームが必要です。

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

1. 「レコードのドキュメント」オプションが有効なアダプティブフォームか、フォームテンプレートベースのアダプティブフォームを作成します。詳しい手順については、「[アダプティブフォームの作成](creating-adaptive-form.md)」を参照してください。
1. **手書き署名**&#x200B;コンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。
1. 「**設定**」![設定](assets/configure.png) アイコンを選択します。この操作により、手書き署名コンポーネントのプロパティを表示するプロパティブラウザーが開きます。手書き署名コンポーネントのプロパティを設定します。
1. 署名ステップコンポーネントを、コンポーネントブラウザーからアダプティブフォームにドラッグ＆ドロップします。

   >[!NOTE]
   >
   >署名ステップコンポーネントは、フォームの幅いっぱいに表示されます。そのため、署名ステップコンポーネントが含まれているセクションに他のコンポーネントを配置しないようにすることをお勧めします。

1. コンテンツブラウザーで「**フォームコンテナ**」を選択し、「**設定**」![設定アイコン](assets/configure.png) アイコンをクリックします。この操作により、アダプティブフォームのコンテナプロパティを表示するプロパティブラウザーが開きます。**アダプティブフォームコンテナ**／**電子サイン**&#x200B;に移動して、「**Adobe Sign を有効にする**」オプションを選択解除します。「完了」![aem_forms_save](assets/aem_forms_save.png) アイコンを選択して、変更を保存します。

   >[!NOTE]
   >
   >署名ステップコンポーネントをアダプティブフォームに追加すると、「Adobe Sign を有効にする」オプションが自動的に選択されます。

1. 「**設定**」![設定](assets/configure.png) アイコンを選択します。この操作により、署名ステップのプロパティを表示するプロパティブラウザーが開きます。以下のプロパティを設定します。

   * **要素名**：コンポーネントの名前を指定します。

   * **タイトル：**&#x200B;コンポーネントの一意のタイトルを指定します。
   * **テンプレートメッセージ：**&#x200B;署名 PDF の読み込み中に表示するメッセージを指定します。Adobe Sign サービスによる署名 PDF の準備と読み込みには、ある程度の時間がかかります。
   * **署名サービス：**「**手書き署名**」オプションを選択します。

   * **CSS クラス**：クライアントライブラリの CSS クラスを指定します（存在する場合）。CSS クラスの代わりに[テーマ](themes.md)や[インラインスタイル](inline-style-adaptive-forms.md)の使用をお勧めします。

   「完了」![aem_forms_save](assets/aem_forms_save.png) アイコンを選択して、変更を保存します。署名が正常に設定されます。

   これで、フォームを記入する際に、PDF バージョンのアダプティブフォームが表示され、PDF ドキュメントの署名オプションが提供されます。詳しくは、「[手書き署名を使用したアダプティブフォームの署名](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)」を参照してください。

## 手書き署名を使用したアダプティブフォームの署名 {#sign-an-adaptive-form-using-scribble-signature}

1. フォームへの記入を完了して署名ステップページに到達すると、署名画面が表示されます。

   ![EchoSign ページの署名画面](assets/esignscribblesign.jpg)

1. 「**[!UICONTROL 署名]**」をクリックします。手書き署名ダイアログが表示されます。フォームに署名し、完了 ![aem_forms_save](assets/aem_forms_save.png) アイコンをクリックして、変更内容を保存します。

   ![手書き署名ダイアログ](assets/scribblewidget.png)

1. 「完了」をクリックして署名プロセスを完了します。

   ![署名プロセスの完了](assets/scribblecomplete.jpg)

署名がフォームに追加され、フォームコントロールが次のパネルに移動します。

## 関連トピック {#see-also}

{{see-also}}