---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 37b20a97942f381b46ce36a6a3f72ac019bba5b7
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 9%

---

# Edge Delivery Services Formsを使用したForms送信サービス

<span class="preview">この機能は、早期アクセスプログラムを通じて使用できます。アクセス権をリクエストするには、GitHub 組織名とリポジトリ名を記載したメールを公式アドレスから <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> に送信してください。例えば、リポジトリ URL が https://github.com/adobe/abc の場合、組織名は「adobe」、リポジトリ名は「abc」になります。</span>

Forms送信サービスを使用すると、フォーム送信データを OneDrive、SharePoint、Google Sheets などの任意のスプレッドシートに保存でき、目的のスプレッドシートプラットフォーム内でフォームデータに簡単にアクセスして管理できます。

![Forms送信サービス ](/help/forms/assets/form-submission-service.png)

## Forms Submission サービスを使用するメリット

スプレッドシートでForms送信サービスを使用する利点は次のとおりです。

* **直接統合**：指定したスプレッドシートにデータを直接送信するようにフォームを設定できるので、手動でデータを転送する必要がなくなります。
* **データ構造**：送信を設定する際に、フォームフィールドを対応するスプレッドシートの列にマッピングして、整理されたデータストレージを使用できます。
* **アクセス制御**：既存の権限を活用して、選択したスプレッドシートサービスに応じて、送信されたフォームデータにアクセスして変更できるユーザーを制御できます。

## 前提条件

Forms Submission サービスを使用するための前提条件を以下に示します。

* AEM プロジェクトに最新のアダプティブフォームブロックが含まれていることを確認します。
* Forms送信サービスを使用するには、Git リポジトリが許可リストに追加されていることを確認してください。 Forms送信サービスを使用する [許可リストに追加するには、](mailto:aem-forms-ea@adobe.com)mailto:aem-forms-ea@adobe.com} と、GitHub の組織名およびリポジトリ名を入力してください。

## Forms送信サービスの設定

アダプティブ AEM ブロックが設定された新しいForms プロジェクトを作成します。 新しいAEM プロジェクトの作成方法については、[ はじめに – 開発者向けチュートリアル ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) を参照してください。 プロジェクトの `fstab.yaml` ファイルを更新します。 既存の参照を、`forms@adobe.com` と共有したフォルダーのパスに置き換えます。

[Forms Submission サービスを手動で設定する ](#configuring-the-forms-submission-service-manually) または [API を使用するForms Submission サービスを設定する ](#configuring-the-forms-submission-service-using-api) ことができます。

### 手動によるForms送信サービスの設定

![Forms 送信サービスのワークフロー ](/help/forms/assets/forms-submission-service-workflow.png)

#### &#x200B;1. フォーム定義を使用してフォームを作成する

Google シートまたはMicrosoft Excel を使用してフォームを作成します。 Microsoft Excel またはGoogle Sheets のフォーム定義を使用してフォームを作成する方法については、[ ここをクリック ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms) してください。

次のスクリーンショットは、フォームの作成に使用されたフォーム定義を示しています。

![ フォームの定義 ](/help/forms/assets/form-submission-definition.png)

>[!IMPORTANT]
>
>**フォームを作成するシートには、名前の付け方に制限があります。シート名として使用できるのは `helix-default` と `shared-aem` のみです。**

#### &#x200B;2. スプレッドシートを有効にしてデータを受け入れます。

フォームを作成してプレビューしたら、対応するスプレッドシートを有効にしてデータの受信を開始します。 新しいシートを `incoming` のように追加します。 [ スプレッドシートを手動で有効にしてデータを受け入れる ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data) ことができます。

![ 受信シート ](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> `incoming` シートが存在しない場合、AEMではこのブックにデータが送信されません。

#### &#x200B;3. スプレッドシートを共有し、リンクを生成します。

スプレッドシートを `forms@adobe.com` アカウントと共有してリンクを生成するには、次の手順を実行します。

1. Excel またはGoogle Sheets で、右上隅の **共有** ボタンをクリックします。
1. `forms@adobe.com` アカウントと
目のアイコンをクリックし、**編集** アクセスを選択して、**送信** をクリックします。

   ![ 受信シートの共有 ](/help/forms/assets/form-submission-share-incoming.png)

1. スプレッドシートリンクをコピーするには、右上隅の **共有** ボタンをクリックし、「**リンクをコピー**」を選択します。

   ![ 受信シートのリンクをコピー ](/help/forms/assets/form-submission-copy-link.png)

#### &#x200B;4. フォーム定義でスプレッドシートをリンクする

Forms Submission サービスをGoogle Sheets またはMicrosoft Excel で設定するには、次の手順を実行します。

1. フォーム定義を含むスプレッドシートを開きます。
1. **送信** フィールドに対応する行の **アクション** 列にコピーしたスプレッドシートリンクを貼り付けます。

   ![ スプレッドシートをリンクする ](/help/forms/assets/form-submission-sheet-linking.png)

1. 更新されたフォーム送信サービスで [AEM Sidekick](https://www.aem.live/docs/sidekick) を使用して、シートをプレビューして公開します。

>[!NOTE]
>
> [ スプレッドシート ](/help/forms/assets/spreadsheet.xlsx) を参照して、Forms送信サービスを使用できます。

### API を使用したForms Submission サービスの設定

また、フォームに **POST** リクエストを送信して、`incoming` シートをデータで更新することもできます。

>[!NOTE]
>
> * `incoming` シートが存在しない場合、AEMではこのブックにデータが送信されません。
> * `incoming` シートをAdobe Experience Manager `forms@adobe.com` と共有し、編集アクセス権を付与します。
> * サイドキックで `incoming` シートをプレビューして公開します。

シート設定のための POST リクエストのフォーマット方法については、[API ドキュメント ](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/) を参照してください。 以下に例を示します。

以下に示すように、curl やPostmanなどのツールを使用してこの POST リクエストを実行できます。

* **Postmanを使用する場合**:

例えば、を置き換えた後、Postmanで以下のリクエストを送信します。
* フォーム ID を `{id}` 用
* GitHub リポジトリまたはサイト名を `site or repository` します
* GitHub ユーザー名を `organization` します。

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

Postmanで「**送信**」ボタンをクリックすると、`201 Created` の応答が返され、送信されたデータで `incoming` シートが更新されます。

![postman 画面 ](/help/forms/assets/postman-api.png)

* **Curl コマンドの使用**:

例えば、を置き換えた後で、ターミナルまたはコマンドプロンプトで次のコマンドを実行します。
* フォーム ID を `{id}` 用
* GitHub リポジトリまたはサイト名を `site or repository` します
* GitHub ユーザー名を `organization` します。


>[!BEGINTABS]

>[!TAB macOSの場合 ]

    &quot;&#39;json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
    —header &quot;Content-Type: application/json&quot; \
    —header &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; \
     – データ &#39;{
    &quot;data&quot;: {
    &quot;startDate&quot;: &quot;2025-01-20&quot;,
    &quot;endDate&quot;: &quot;2025-01-25&quot;,
    &quot;destination&quot;: &quot;Australia&quot;,
    &quot;class&quot;:&quot;First First class&quot;,
    &quot;budget&quot;: &quot;2000&quot;,
    &quot;amount&quot;: &quot;1000000&quot;,
    &quot;name&quot;: &quot;Joe&quot;,
    &quot;age&quot;: &quot;35&quot;,
    &quot;subscribe&quot;: null,
    &quot;email&quot;: &quot;mary@gmail.com&quot;
    }
     
    
     
}&#39;s
>[!TAB Windows OS の場合 ]

    &quot;&#39;json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
     – ヘッダー&quot;Content-Type: application/json&quot; ^
     – ヘッダー&quot;x-adobe-routing: tier=live,bucket=main—[ サイト/リポジトリ ]—[ 組織 ]&quot; ^
     – データ &quot;{\&quot;data\&quot;: {\&quot;startDate\&quot;: \&quot;2025-01-10\&quot;, \&quot;endDate\&quot;: \&quot;2025-01-25\&quot;, \&quot;destination\&quot;: \&quot;Australia\&quot;, \&quot;class\&quot;: \&quot;First Class\&quot;, \&quot;budget\&quot;: \&quot;2000\&quot;, \&quot;amount\&quot;: \&quot;1000000\&quot;, \&quot;name\&quot;: \&quot;Joe\&quot;, \&quot;age\&quot;: \&quot;35\&quot;, \&quot;subscribe\&quot;: null, \&quot;email\&quot;: \&quot;mary@gmail.com\&quot;}}&quot;
    
    &quot;&#39;

>[!ENDTABS]

上記の POST リクエストでは、`incoming` シートが下記の応答で更新されます。

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

次の画面は、API を使用してデータ送信によって更新された `incoming` シートのスクリーンショットを示しています。

![ 更新されたシート ](/help/forms/assets/updated-sheet.png)

## 関連トピック

{{see-more-forms-eds}}