---
title: コアコンポーネントに基づくフォームの呼び出しサービス VREの機能強化は何ですか？
description: ルールエディターのInvoke サービスの機能強化
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: vreでのサービス機能強化の呼び出し、呼び出しサービスを使用したドロップダウンオプションの入力、呼び出しサービスの出力を使用した繰り返し可能なパネルの設定、呼び出しサービスの出力を使用したパネルの設定、呼び出しサービスの出力パラメーターを使用した他のフィールドの検証。
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: e69201c40b72f4eaabe3da634ecf05bd04769f6b
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 2%

---

# コアコンポーネント Formsのビジュアルルールエディターへの外部APIの統合

アダプティブフォームのビジュアルルールエディターは、**呼び出しサービス**&#x200B;機能をサポートしており、インスタンスに設定されたフォームデータモデル（FDM）を介して外部APIに接続できます。 フォームフィールドをサービスの入力パラメーターに直接マッピングし、イベントペイロードオプションを使用して出力パラメーターをマッピングできます。 ビジュアルルールエディターでは、サービスの応答に基づいて成功ハンドラーと失敗ハンドラーのルールを定義することもできます。成功ハンドラーは成功したAPI呼び出しを処理し、失敗ハンドラーはエラーを管理します。

これにより、フォームからAPI リクエストを簡単に送信し、API レスポンスを処理し、返されたデータをフォーム内で動的に表示または使用できます。 これにより、アダプティブフォームと外部システムやデータソースとのシームレスな統合が保証されます。


## フォームのルールエディターで呼び出しサービスを使用する利点

Adobe フォームのルールエディターでサービス呼び出し操作を使用する利点を以下に示します。

* **合理化されたAPI統合**：ビジュアルルールエディターにより、外部サービスまたはAPIをAdaptive Formsに統合するプロセスが簡素化されます。 **呼び出しサービス**&#x200B;を使用すると、複雑なコーディングを必要とせずに、フォームをさまざまなデータソースやサービスに簡単に接続でき、フォームの統合がより効率的になります。

* **動的な応答の処理**: **呼び出しサービス**&#x200B;の出力応答に基づいて成功とエラーの応答を管理し、フォームを異なるシナリオに動的に反応させることができます。 これにより、フォームがさまざまな条件を適切に処理することが保証され、柔軟性とコントロールが向上します。

* **ユーザーインタラクションの強化**: ルールエディターで&#x200B;**呼び出しサービス**&#x200B;を使用すると、フォーム内でのリアルタイムの検証が可能になり、ユーザーエクスペリエンスが向上します。 また、データがサーバーサイドで正確に検証されるため、エラーが減り、フォームの信頼性が向上します。

## 成功および失敗応答のサービスハンドラーを呼び出す

>[!NOTE]
>
> コアコンポーネントに基づくフォームに対してのみ、**Invoke Service**&#x200B;の成功ハンドラーと失敗ハンドラーを使用できます。 基盤コンポーネントに基づくFormsでは、**呼び出しサービス**&#x200B;の成功ハンドラーと失敗ハンドラーはサポートされていません。

視覚的なルールエディターを使用すると、出力の応答に基づいて&#x200B;**Invoke Service**&#x200B;操作の成功ハンドラーと失敗ハンドラーのルールを作成できます。 次の画像は、アダプティブフォームのビジュアルルールエディターの&#x200B;**呼び出しサービス**&#x200B;を示しています。

![ サービスハンドラーの呼び出し](/help/forms/assets/invoke-service-rule-editor.png)

### 成功ハンドラーと失敗ハンドラーの追加

成功ハンドラーまたは失敗ハンドラーを追加するには、それぞれ&#x200B;**[!UICONTROL 成功ハンドラーを追加]**&#x200B;または&#x200B;**[!UICONTROL 失敗ハンドラーを追加]**&#x200B;をクリックします。

「**[!UICONTROL 成功ハンドラーを追加]**」をクリックすると、**[!UICONTROL サービス成功ハンドラー]** ルールエディターが表示され、操作が成功したときに&#x200B;**サービスを呼び出し**&#x200B;の出力応答を管理するためのルールまたはロジックを指定できます。 条件を定義しなくてもルールを指定できますが、**[!UICONTROL 条件を追加]** オプションをクリックして、成功ハンドラーの条件を追加できます。

![ サービス成功ハンドラーを呼び出す](/help/forms/assets/invoke-service-success-handler.png)

**呼び出しサービス**&#x200B;操作に対する正常な応答を処理するために、複数のルールを追加できます。

![複数の成功ハンドラー](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%, height=50%}

同様に、操作が成功しなかった場合に&#x200B;**Invoke Service**&#x200B;の出力応答を処理するルールを追加できます。 次の画像は、**[!UICONTROL Invoke Service Failure Handler]** ルールエディターを示しています。

![呼び出しサービス エラーのハンドラー](/help/forms/assets/invoke-service-failue-handler.png)

また、複数のルールを追加して、**サービスの呼び出し**&#x200B;操作からの失敗した応答を処理することもできます。

サーバー&#x200B;**でエラー検証を有効にする**&#x200B;機能を使用すると、アダプティブフォームの設計中に作成者が追加した検証をサーバーでも実行できます。

## ルールエディターで呼び出しサービスを使用するための前提条件

ルール エディターで&#x200B;**呼び出しサービス**&#x200B;を使用する前に満たす必要がある前提条件は次のとおりです。

* データソースが設定されていることを確認します。 データソースの設定手順については、[ここをクリック ](/help/forms/configure-data-sources.md)してください。
* 設定されたデータソースを使用して、フォームデータモデルを作成します。 フォームデータモデルの作成に関するガイダンスについては、[ここをクリック ](/help/forms/create-form-data-models.md)してください。

## 様々なユースケースを通じたInvoke Serviceの探索

ビジュアルルールエディターの&#x200B;**呼び出しサービス**&#x200B;を使用すると、いくつかの便利な操作を実行できます。 ドロップダウンオプションの入力、繰り返し可能またはシンプルなパネルの設定、フォームフィールドの検証など、すべて&#x200B;**呼び出しサービス**&#x200B;の出力応答に基づいて使用できます。 フォームの柔軟性とインタラクティブ性を向上させます。

次の表は、**呼び出しサービス**&#x200B;を使用できるいくつかのシナリオを示しています。

| **ユースケース** | **説明** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **呼び出しサービスの出力を使用してドロップダウンオプションを設定** | 「サービスを呼び出し」出力から取得したデータに基づいて、ドロップダウンオプションを動的に入力します。 [実装を確認するには、ここをクリック ](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service)してください。 |
| **呼び出しサービスの出力を使用して繰り返し可能なパネルを設定** | Invoke Service出力のデータを使用して繰り返し可能なパネルを設定し、ダイナミックパネルを使用できるようにします。 [実装を確認するには、ここをクリック ](#use-case-2-set-repeatable-panel-using-output-of-invoke-service)してください。 |
| **呼び出しサービスの出力を使用してパネルを設定** | Invoke Service出力の特定の値を使用して、パネルのコンテンツまたは表示を設定します。 [実装を確認するには、ここをクリック ](#use-case-3-set-panel-using-output-of-invoke-service)してください。 |
| **呼び出しサービスの出力パラメーターを使用して、他のフィールドを検証する** | 呼び出しサービスの特定の出力パラメーターを使用して、フォームフィールドを検証します。 [実装を確認するには、ここをクリック ](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields)してください。 |
| **呼び出しサービスのアクションに移動でイベント ペイロードを使用** | イベントペイロードを使用して、成功と失敗の応答を処理し、ナビゲーション中にデータを「移動先」アクションに渡します。 [実装を確認するには、ここをクリック ](#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service)してください。 |

`Get Information` テキストボックスに入力された入力に基づいて値を取得する`Pet ID` フォームを作成します。 以下のスクリーンショットは、これらのユースケースで使用されるフォームを示しています。

![情報フォームを取得](/help/forms/assets/get-information-form.png)

**フォームフィールド**

フォームに次のフィールドを追加します。

* **ペット IDを入力**: Textbox
* **写真のURLを選択**: ドロップダウン
* **タグ**: パネル
   * 名前：Textbox
   * ID: Textbox
* **カテゴリ**: パネル
   * 名前：Textbox
* **送信**：送信ボタン

>[!NOTE]
>
> フォームフィールドの&#x200B;**プロパティ** ダイアログの&#x200B;**バインド参照** フィールドで、![foldersearch_18](assets/folder-search-icon.svg)を選択し、フォームデータモデル（FDM）に追加したバイナリプロパティを移動して選択します。

**パネルの設定**

次の制約を使用して、パネルを繰り返しとして設定します。

* 最小値：1
* 最大値：4

必要に応じて、繰り返しパネルの値を調整できます。

**データソース**

この例では、[Swagger Petstore](https://petstore.swagger.io/) APIを使用してデータソースを設定しています。 [ フォームデータモデル ](/help/forms/create-form-data-models.md)は、[getPetById](https://petstore.swagger.io/#/pet/getPetById) サービス用に設定されており、入力されたIDに基づいてペットの詳細を取得します。

[Swagger Petstore](https://petstore.swagger.io/#/pet/addPet) APIの[addPet](https://petstore.swagger.io/) サービスを使用して、次のJSONを投稿してみましょう。

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```

ルールとロジックは、**テキストボックスのルールエディターの** サービスを呼び出す`Pet ID` アクションを使用して実装され、前述のユースケースを示します。

それでは、各ユースケースの実装を詳しく見ていきましょう。

### ユースケース 1：呼び出しサービスの出力を使用してドロップダウン値を入力する

この使用例では、`Invoke Service`の出力に基づいてドロップダウンオプションを動的に入力する方法を示します。

#### 実装

これを実現するには、`Pet ID` テキストボックスにルールを作成して、`getPetById` サービスを呼び出します。 ルールで、`enum`成功ハンドラーを追加`photo-url`の`photoUrls` ドロップダウンの&#x200B;**[!UICONTROL プロパティを]**&#x200B;に設定します。

![ ドロップダウン値を設定](/help/forms/assets/set-dropdownoption.png)

>[!NOTE]
>
> 成功ハンドラーと失敗ハンドラーの設定方法については、[成功ハンドラーと失敗ハンドラーの追加](#adding-success-handler-and-failure-handler)の節を参照してください。

#### 出力

「`101`」テキストボックスに「`Pet ID`」と入力すると、入力した値に基づいてドロップダウンオプションが動的に入力されます。

![結果](/help/forms/assets/output1.png)

>[!NOTE]
>
> ドロップダウンオプションは、サービスを呼び出し、JSON応答を解析し、カスタム関数を適用することで、動的に入力することもできます。 詳しくは、[このセクション ](#retrieve-property-values-from-a-json-array)を参照してください。

### ユースケース 2：呼び出しサービスの出力を使用した繰り返し可能なパネルの設定

この使用例では、**呼び出しサービス**&#x200B;の出力に基づいて、繰り返し可能なパネルを動的に入力する方法を示します。

#### 考慮事項

* 繰り返し可能なパネルの名前が、パネルを設定する&#x200B;**呼び出しサービス**&#x200B;のパラメーターと一致していることを確認します。
* パネルは、対応する&#x200B;**呼び出しサービス** フィールドによって返される値の数に対して繰り返されます。

#### 実装

`Pet ID` テキストボックスにルールを作成して、`getPetById` サービスを呼び出します。 **[!UICONTROL 成功ハンドラーを追加]**&#x200B;で、別の成功ハンドラー応答を追加します。 ルールの`tags` パネルの値を`tags`に設定します。

![繰り返し可能なパネルのルールを作成](/help/forms/assets/create-rule-repeatable-panel.png)

>[!NOTE]
>
> 成功ハンドラーと失敗ハンドラーの設定方法については、[成功ハンドラーと失敗ハンドラーの追加](#adding-success-handler-and-failure-handler)の節を参照してください。

#### 出力

「`101`」テキストボックスに「`Pet ID`」と入力すると、入力値に基づいて繰り返し可能なパネルが動的に入力されます。

![出力](/help/forms/assets/output2.png)

### ユースケース 3：呼び出しサービスの出力を使用したパネルの設定

この使用例では、**呼び出しサービス**&#x200B;の出力に基づいて、パネルの値を動的に設定する方法を示します。

#### 考慮事項

* パネルの名前が、パネルを設定する&#x200B;**呼び出しサービス**&#x200B;のパラメーターと一致していることを確認します。
* パネルは、対応する「サービスを呼び出し」フィールドによって返される値の数に対して繰り返されます。

#### 実装

`Pet ID` テキストボックスにルールを作成して、`getPetById` サービスを呼び出します。 **[!UICONTROL 成功ハンドラーを追加]**&#x200B;で、別の成功ハンドラー応答を追加します。 ルールの`categoryname` テキストボックスの値を`category.name`に設定します。

>[!NOTE]
>
> 成功ハンドラーと失敗ハンドラーの設定方法については、[成功ハンドラーと失敗ハンドラーの追加](#adding-success-handler-and-failure-handler)の節を参照してください。

![繰り返し可能なパネルのルールを作成](/help/forms/assets/set-panel-values.png)

#### 出力

「`101`」テキストボックスに「`Pet ID`」と入力すると、入力値に基づいてパネルに動的に入力されます。

![出力](/help/forms/assets/output3.png)

### ユースケース 4：呼び出しサービスの出力パラメーターを使用して、他のフィールドを検証する

この使用例では、**呼び出しサービス**&#x200B;の出力を使用して、他のフォームフィールドを動的に検証する方法を示します。

#### 実装

`Pet ID` テキストボックスにルールを作成して、`getPetById` サービスを呼び出します。 **[!UICONTROL 失敗ハンドラーを追加]**&#x200B;で、失敗ハンドラー応答を追加します。 誤った&#x200B;**が入力された場合は、**&#x200B;送信`Pet ID` ボタンを非表示にします。

![失敗ハンドラー](/help/forms/assets/create-rule-failure-handler.png)

#### 出力

`102` テキストボックスに`Pet ID`と入力すると、**送信** ボタンは非表示になります。

![出力](/help/forms/assets/output4.png)

### ユースケース 5：呼び出しサービスのアクションに移動でのイベントペイロードの使用

この使用例では、**呼び出しサービス**&#x200B;を呼び出す&#x200B;**送信** ボタンでルールを設定し、**移動先** アクションを使用してユーザーを別のページにリダイレクトする方法を示します。

#### 実装

**送信** ボタンにルールを作成して、`redirect-api` API サービスを呼び出します。 このサービスは、ユーザーを&#x200B;**お問い合わせ** フォームにリダイレクトする責任があります。

以下に示すJSON データを使用して、APIを`redirect-api` API サービスとしてルールエディターに直接統合できます。

```json
{
  "id": "1",
  "path": "/content/dam/formsanddocuments/contact-detail/jcr:content?wcmmode=disabled"
}
```

>[!NOTE]
>
> ルールエディターのインターフェイスにAPIを直接統合する方法については、定義済みのフォームデータモデルを使用せずに[ここをクリック ](/help/forms/api-integration-in-rule-editor.md)してください。

**[!UICONTROL 成功ハンドラーを追加]**&#x200B;で、**移動先** アクションを設定して、**パラメーターを使用してユーザーを**&#x200B;お問い合わせ`Event Payload` ページにリダイレクトします。 ここで、ユーザーは連絡先の詳細を送信できます。

![ イベントペイロード ](/help/edge/docs/forms/assets/navigate-to-eventpayload.png)

オプションで、サービスコールが失敗した場合にエラーメッセージを表示するようにエラーハンドラーを設定します。

#### 出力

**送信** ボタンをクリックすると、`redirect-api` API サービスが呼び出されます。 成功すると、ユーザーは&#x200B;**お問い合わせ** ページにリダイレクトされます。

![ イベントペイロード出力](/help/forms/assets/output5.gif)

## JSON配列からのプロパティ値の取得

<span class="preview">これはアーリーアダプター機能です。 興味がある場合は、仕事用アドレスからmailto:aem-forms-ea@adobe.comにクイックメールを送信して、機能</a>へのアクセスをリクエストしてください。</span>

アダプティブ Formsでは、サービスの呼び出し、JSON応答の処理、フォームフィールドの動的な入力がサポートされています。 この節では、JSON配列からプロパティ値を抽出し、フォームフィールドにバインドする方法について説明します。

### JSON応答のサンプル

次の例は、米国の販売地域と販売担当者のリストを表しています。


```json
[
  {
    "region": "East",
    "salesPerson": "Emily Carter"
  },
  {
    "region": "South",
    "salesPerson": "Michael Brown"
  },
  {
    "region": "Midwest",
    "salesPerson": "Sophia Martinez"
  },
  {
    "region": "Southwest",
    "salesPerson": "David Johnson"
  },
  {
    "region": "West",
    "salesPerson": "Linda Walker"
  }
]
```

### プロパティ値を抽出するカスタム関数

JSON配列からプロパティ値を抽出するには、次のカスタム関数を使用します。

```js
/**
 * Returns an array of values for a specific property from an array of objects.
 *
 * @name getPropertyValues
 * @param {Object[]} jsonArray An array of objects
 * @param {string} propertyName The property whose values should be extracted
 * @returns {Array} An array containing the values of the specified property
 *
 */

function getPropertyValues(jsonArray, propertyName)
{
    return jsonArray.map((obj) => obj[propertyName]);

}
```

カスタム関数は次を受け入れます。

* **jsonArray**: サービスから返されたJSON配列
* **propertyName**：値を抽出するプロパティ

カスタム関数は、値の単純な配列を返します。

>[!NOTE]
>
> カスタム関数を追加する方法の詳細な手順については、「[ コアコンポーネントに基づくアダプティブ Formsのカスタム関数の概要](/help/forms/create-and-use-custom-functions.md)」を参照してください。


### ルールエディターでの関数の使用

JSON配列から特定の値を取得するには：

```
event.payload.invokeServiceResponse.rawPayloadBody
```

次の例は、この応答を使用して`Sales Department` フォームに入力する方法を示しています。

例えば、`Sales Department`と`Select Region`のドロップダウンを含む`Select Sales Representative` フォームを作成します。

**手順1: フォームの初期化でサービスを呼び出す**

```
WHEN
    Form is initialized
THEN
    Invoke Service → salesdeptinfo
```

>[!NOTE]
>
> ビジュアルルールエディターでフォームデータモデルを作成せずにAPIを統合する方法については、[ここをクリック ](/help/forms/api-integration-in-rule-editor.md)してください。

**手順2：地域ドロップダウンを設定**

サービスコールにサクセスハンドラーを追加し、次のアクションを設定します。

```
Set enum → Region dropdown
getPropertyValues(
    event.payload.invokeServiceResponse.rawPayloadBody,
    "region"
)
```

このルールは、JSON配列を読み取り、`region` プロパティ値を抽出し、値を`Select Region` ドロップダウンに割り当てます。

同様に、成功ハンドラーの`Select Sales Representative` ドロップダウンのアクションを設定します。

![JSON配列のイベントペイロード ](/help/forms/assets/event-payload.png)

フォームがJSON データを読み込むと、カスタム関数がプロパティ値を抽出し、ドロップダウンが自動的に入力されます。

![ イベントペイロードフォーム ](/help/forms/assets/event-payload-form.png)

## よくある質問

**Q: Invoke サービスを使用してルールを作成し、コアコンポーネントの最新バージョンにアップグレードするとどうなりますか？**

**A:** コアコンポーネントの最新バージョンにアップグレードすると、**呼び出しサービス** ルールは、下位互換性があるため、最新のユーザーインターフェイスに自動的に更新されます。

**Q: サービスの呼び出し操作の成功または失敗の応答を処理するために、複数のルールを追加できますか？**

**A:**&#x200B;はい、**呼び出しサービス**&#x200B;操作の成功または失敗の応答を処理するために、複数のルールを追加できます。

## 関連記事

* [データソースの設定](configure-data-sources.md)
* [フォームデータモデル（FDM）の作成](create-form-data-models.md)
* [フォームデータモデル（FDM）の操作](work-with-form-data-model.md)
* [フォームデータモデル（FDM）の使用](using-form-data-model.md)


## その他のリソース

{{see-also-rule-editor}}
