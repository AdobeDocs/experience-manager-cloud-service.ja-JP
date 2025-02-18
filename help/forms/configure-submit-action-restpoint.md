---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: AEM Forms REST エンドポイント、REST エンドポイントへの送信、REST URL へのデータの POST、REST エンドポイントアクションの設定
feature: Adaptive Forms, Core Components
title: アダプティブフォームの送信アクションの設定方法
role: User, Developer
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
source-git-commit: cc9b72fbebc673aeb29032915f371c8f5e156b28
workflow-type: ht
source-wordcount: '703'
ht-degree: 100%

---

# REST エンドポイントへの送信アクションのアダプティブフォームを設定する

**[!UICONTROL REST エンドポイントへの送信]**&#x200B;アクションを使用して、送信されたデータを REST URL に POST できます。URL は、内部（フォームがレンダリングされるサーバー）または外部サーバーのどちらのものでも使用できます。

AEM as a Cloud Service では、フォーム送信を処理するための様々な送信アクションが標準で提供されます。これらのオプションについて詳しくは、[アダプティブフォーム送信アクション](/help/forms/configure-submit-actions-core-components.md)の記事をご覧ください。

## メリット

アダプティブフォームの **[!UICONTROL REST エンドポイントへの送信]**&#x200B;の送信アクションを設定するメリットは次のとおりです。

* RESTful API を通じて、フォームデータと外部システムおよびサービスをシームレスに統合できます。
* アダプティブフォームからのデータ送信を柔軟に処理し、動的で複雑なデータ構造をサポートできます。
* REST エンドポイント URL のパラメーターへのフォームフィールドの動的マッピングをサポートし、適応可能でカスタマイズ可能なデータ送信を行うことができます。


## REST エンドポイントへの送信の送信アクションを設定する {#steps-to-configure-submit-to-restendpoint-submit-action}

Swagger Open API 仕様に基づいて送信アクションを設定するには：

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから、「**[!UICONTROL REST エンドポイントへの送信]**」を選択します。
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

   **[!UICONTROL REST エンドポイントへの送信]**&#x200B;送信アクションでは、フォームに入力されたデータを HTTP GET リクエストの一部として設定済みの確認ページに送信します。リクエストにフィールド名を追加できます。リクエストのフォーマットを以下に示します。

   `{fieldName}={request parameter name}`

   以下の画像に示されているように、`param1` および `param2` が、**textbox** フィールドおよび **numericbox** フィールドからコピーされた値を持つパラメーターとして、次のアクションに向けて渡されます。

   ![REST エンドポイント送信アクションの設定](assets/action-config.png)

   **[!UICONTROL POST リクエストを有効にする]**&#x200B;ことで、リクエストを POST する URL を指定することもできます。フォームをホストする AEM サーバーにデータを送信するには、AEM サーバーのルートパスに対応する相対パスを使用します。例えば、`/content/forms/af/SampleForm.html` のようになります。他のサーバーにデータを送信するには、絶対パスを使用します。

1. 「**[!UICONTROL 完了]**」をクリックします。

### サービス REST エンドポイントに基づく送信アクションの設定 {#config-service-endpoint-auth}

<span class="preview"> サービスエンドポイント機能は早期導入プログラムの対象であり、コアコンポーネントにのみ適用されます。早期導入プログラムに登録し、機能へのアクセスをリクエストするには、公式メール ID から aem-forms-ea@adobe.com にメールを送信してください。</span>

1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブをクリックします。
1. **[!UICONTROL 送信アクション]**&#x200B;ドロップダウンリストから、「**[!UICONTROL REST エンドポイントへの送信]**」を選択します。
1. POST リクエストを有効にします。
1. REST エンドポイント URL を指定します。
1. サービス REST エンドポイント認証タイプおよびコンテンツタイプ用に作成した設定を選択します。認証タイプとコンテンツタイプについて詳しくは、[データソースの設定](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)を参照してください。
   ![REST エンドポイントの設定](assets/rest-service-endpoint-config.png)
1. 「完了」をクリックします。

## ベストプラクティス

* 外部サーバーにデータを POST する場合は、URL がセキュリティで保護されていることを確認し、POST リクエストを匿名で処理して機密情報を保護するパスを設定します。
* フィールドを REST URL 内のパラメーターとして渡すには、すべてのフィールドが異なる要素名を持っている必要があります。これは、異なるパネルに置かれているフィールドにも適用されます。

## 関連記事

{{af-submit-action}}
