---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST エンドポイント、REST エンドポイントへの送信、REST URL へのデータの投稿、REST エンドポイントアクションの設定
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 62%

---


# 送信アクション「REST エンドポイント用のアダプティブフォームの設定」

以下を使用します。 **[!UICONTROL REST エンドポイントに送信]** 送信されたデータを REST URL に投稿するアクション。 URL は、内部（フォームがレンダリングされるサーバー）または外部サーバーのどちらのものでも使用できます。

AEM as a Cloud Serviceには、フォーム送信を処理するための標準の様々な送信アクションが用意されています。 これらのオプションについて詳しくは、 [アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)  記事。

## メリット

の設定の利点の一部 **[!UICONTROL REST エンドポイントに送信]** アダプティブFormsの送信アクションは次のとおりです。

* これにより、RESTful API を使用して、フォームデータを外部のシステムやサービスとシームレスに統合できます。
* アダプティブFormsからのデータ送信を柔軟に処理でき、動的で複雑なデータ構造をサポートできます。
* フォームフィールドの動的マッピングを REST エンドポイント URL 内のパラメーターに対してサポートしており、適応可能でカスタマイズ可能なデータ送信が可能です。


## 送信アクション「REST エンドポイントへの送信」の設定 {#steps-to-configure-submit-to-restendpoint-submit-action}

送信アクションを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. 次から： **[!UICONTROL 送信アクション]** ドロップダウンリストで、「 **[!UICONTROL Rest エンドポイントに送信]**.
   ![REST エンドポイントへの送信のアクション設定](/help/forms/assets/submit-action-restendpoint.png)

   内部サーバーにデータを POST 送信するには、リソースのパスを指定します。データは、リソースのパスに POST されます。例えば、`/content/restEndPoint` のようになります。このような POST リクエストには、送信リクエストの認証情報が使用されます。

   外部サーバーにデータを POST 送信するには、URL を指定します。URL の形式は、`https://host:port/path_to_rest_end_point` です。POST リクエストを匿名で処理するためのパスを設定してください。

   ![「ありがとうございます」ページのパラメーターとして渡されたフィールド値のマッピング](assets/post-enabled-actionconfig.png)

   上の例で、ユーザーが `textbox` に入力した情報は、パラメーター `param1` を使用して取得されます。`param1` を使用して取得されるデータを POST するための構文を以下に示します。

   `String data=request.getParameter("param1");`

   同様に、XML データと添付ファイルの POST に使用するパラメーターは、`dataXml` および `attachments` です。

   例えば、この 2 つのパラメーターをスクリプト中で使用して、REST エンドポイントに送信されたデータを解析できます。データを格納および解析するための構文を以下に示します。

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   この例では、`data` が XML データを格納し、`att` が添付ファイルデータを格納します。

   **[!UICONTROL REST エンドポイントへの送信]**&#x200B;送信アクションでは、フォームに入力されたデータを HTTP GET リクエストの一部として設定済みの確認ページに送信します。リクエストするフィールドの名前を追加できます。 リクエストのフォーマットを以下に示します。

   `{fieldName}={request parameter name}`

   以下の画像に示されているように、`param1` および `param2` が、**textbox** フィールドおよび **numericbox** フィールドからコピーされた値を持つパラメーターとして、次のアクションに向けて渡されます。

   ![REST エンドポイント送信アクションの設定](assets/action-config.png)

   **[!UICONTROL POST リクエストを有効にする]**&#x200B;ことで、リクエストを POST する URL を指定することもできます。フォームをホストする AEM サーバーにデータを送信するには、AEM サーバーのルートパスに対応する相対パスを使用します。例えば、`/content/forms/af/SampleForm.html` のようになります。他のサーバーにデータを送信するには、絶対パスを使用します。

1. 「**[!UICONTROL 完了]**」をクリックします。

## ベストプラクティス

* 外部サーバーにデータを投稿する場合は、URL がセキュリティで保護されていることを確認し、機密情報を保護するために、匿名でPOSTリクエストを処理するようにパスを設定します。
* フィールドを REST URL 内のパラメーターとして渡すには、すべてのフィールドが異なる要素名を持っている必要があります。これは、異なるパネルに置かれているフィールドにも適用されます。

## 関連記事

{{af-submit-action}}

