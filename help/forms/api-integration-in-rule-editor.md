---
title: FormsのルールエディターでのAPIの統合
description: フォームデータモデルを使用せずに、コアコンポーネントに基づいてアダプティブFormsのAPIを統合する方法など、ルールエディターの呼び出しサービスの最新の機能強化について説明します。
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: ルールエディターでの API の統合, サービス拡張機能の呼び出し
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: af79899657fc8f1d7a8b8037889af5c2dbb2cdcf
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 4%

---

# ルールエディターでのAPIの統合

<span> ルールエディターでのAPIの統合は、アーリーアダプタープログラムの下にあります。 公式メール ID から `aem-forms-ea@adobe.com` に送信して早期導入プログラムに参加し、機能へのアクセスをリクエストできます。</span>

>[!NOTE]
>
> ビジュアルルールエディターは、コアコンポーネントに基づくアダプティブFormsでのAPI統合と、ユニバーサルエディターで作成された[Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)をサポートしています。

アダプティブ Formsのビジュアルルールエディターは、フォームデータモデルを作成せずに直接API統合をサポートしています。 API エンドポイントに接続するには、API URL （JSON形式）を入力するか、cURL コマンドを使用して設定を読み込みます。 統合が完了すると、**サービスを呼び出し** アクションを使用してAPIを呼び出すことができます。

フォームフィールドは、API設定で定義された入力パラメーターに直接マッピングできます。 同様に、出力パラメーターは、対応するAPI応答に&#x200B;**イベントペイロード** オプションを使用してフォームフィールドにマッピングできます。

さらに、ビジュアルルールエディターでは、サービスの呼び出し時に&#x200B;**成功**&#x200B;および&#x200B;**失敗ハンドラー**&#x200B;を定義できます。 成功ハンドラーは、API呼び出しが成功した後に実行するアクションを指定し、失敗ハンドラーは、エラーが発生したときにフォームがどのように応答するかを定義します。

## 比較：API統合方法

| 項目 | フォームデータモデル（FDM）によるAPI統合 | ダイレクト API統合（*Create API Integration*&#x200B;経由） |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **目的** | 複数のフォームを一元化し、再利用可能なAPIを統合 | フォームに特化したAPIを迅速に統合 |
| **設定の場所** | フォームデータモデルエディター（AEM コンソール）で作成および編集 | アダプティブフォームルールエディターで直接作成および編集 |
| **複雑性** | より高いセットアップ労力（マッピングと設定が必要） | シンプルで軽量 |
| **最適な用途：** | 複数のフォームを持つ大規模なユースケース | 小さなフォーム、プロトタイプ、または1回限りのAPI呼び出し |

## API 統合の設定

以下のスクリーンショットは、API統合設定ウィンドウを表示します。

![API統合設定](/help/forms/assets/api-integration-configuration.png)

### 主要な設定オプション

**API統合設定**

* **cURLからインポート**: API URL、HTTP メソッド、ヘッダー、パラメーターなどの詳細を手動で入力する代わりに、既製のcURL コマンドを貼り付けて、API統合を設定します。
* **表示名**: API サービスのカスタム名。
* **API URL**: API サービスのエンドポイント。
* **HTTP メソッドを選択**: APIの呼び出しに使用されるHTTP リクエストメソッド。
* **コンテンツの種類**：要求と応答の形式を定義します。
* **暗号化が必要**: （オプション）送信中に機密データが暗号化されるようにします。
* **クライアントで実行**：有効にすると、API呼び出しはサーバーではなくクライアント（ブラウザー）から行われます。

**認証タイプ**

* **オプション**：なし、基本、API キー、OAuth 2.0。

**入力パラメーター**

* **入力用にJSONをアップロード**：入力マッピングを自動入力するためのサンプル JSON ファイルをアップロードします。
   * **名前**: APIに必要な入力パラメーター名。
   * **Type**：入力データ型（文字列、数値、ブール値など）。
   * **In**: パラメーター（クエリ、ヘッダー、または本文）の場所。
   * **デフォルト値**：ユーザーが指定しない場合は、事前入力された値。
   * **追加**：追加の入力パラメーターを追加するオプション。

**出力パラメーター**

* **出力用にJSONをアップロード**: マッピングを自動生成するためのサンプル API応答をアップロードします。
   * **名前**: API応答からパラメーター名を出力します。
   * **型**：出力パラメーターの想定されるデータ型（文字列、数値など）。
   * **In**: マッピングされた値が期待される場所を定義します。
   * **追加/削除**：新しいマッピングを追加するか、既存のマッピングを削除します。

## ユースケース：ビザ申請フォームの国フィールドの入力

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**シナリオ**：官公庁が、次のフィールドを含むオンラインビザ申請フォームを提供します。

1. 氏名（テキスト）
2. 生年月日（Date）
3. 国籍（ドロップダウン）
4. パスポート番号（テキスト）
5. パスポート発行国（ドロップダウン）
6. 宛先の国（ドロップダウン）
7. 到着予定日（日付）

国の静的なリストを管理する代わりに、フォームは&#x200B;**getcountryname API**&#x200B;を使用して国の情報（大陸、大文字、ISO Alpha コードなど）を動的に取得します。

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

これにより、応募者はフォームに入力しながら、常に最新かつ正確な国リストを確認できます。

### ルールエディターでのAPI統合を使用した実装

フォームデータモデルを作成せずにAPIを統合するには、ルールエディターの「**API統合を作成**」ボタンをクリックします。

![API統合の作成](/help/forms/assets/create-api-integration.png)

**getcountryname**&#x200B;という名前のAPI サービスは、ルールエディターの&#x200B;**API統合設定**&#x200B;で設定されています。

![API rest Endpoint Configuration](/help/forms/assets/api-restendpoint.png)

* **API エンドポイント URL** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* **HTTP メソッド** → GET
* **コンテンツタイプ** → JSON
* **Input** → `username`がクエリパラメーター（`aemforms`）として渡されました。
* **Output** →応答フィールド（`continent`、`capital`、`countrynames`、`isoAlpha3`、`languages`など）は、フォームフィールドにマッピングされます。

**ビザ申請フォーム**&#x200B;では、**国籍の国**、**パスポート発行国**、**宛先国**&#x200B;の3つのドロップダウンフィールドが&#x200B;**サービスの呼び出し** アクションにバインドされています。

フォームが読み込まれると、**サービスを呼び出し**&#x200B;がAPIから国のリストを取得します。 その後、応答がマッピングされ、ドロップダウンオプションが自動的に入力されます。

例えば、ユーザーが&#x200B;**国籍の国**&#x200B;を開くと、国のリストがAPI応答から動的に表示されます。

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![API統合出力](/help/forms/assets/api-integration-output.png)

同様に、**パスポート発行の国**&#x200B;と&#x200B;**宛先国**&#x200B;は、同じAPI呼び出しを使用し、3つのフィールドすべてで一貫性のある最新のデータを確保します。

>[!NOTE]
>
> APIを呼び出し、カスタム関数[を使用して、JSON配列からプロパティ値を](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array)取得できます。 このアプローチにより、値を抽出し、フォームフィールドに直接結び付けることができます。

## API障害に対する再試行メカニズムの実装

API リクエストが失敗した場合、ユーザーにエラーを報告する前にリクエストを再試行すると便利です。 ポーリングと再試行のメカニズムを実装するには、**function.js** ファイルにカスタムコードを記述します。

次の例は、最大2回の再試行と再試行間の指数関数的なバックオフを伴うAPI エラーを処理する方法を示しています。

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

上記のコードでは、**retryHandler**&#x200B;関数は、失敗した場合に自動再試行を使用してAPI要求を管理します。 リクエスト関数（requestFn）を受け取り、リクエストを最大2回試行し、再試行ごとにメタデータを追加します。

## よくある質問

* **アダプティブ FormsにAPIを統合するには、フォームデータモデルを作成する必要がありますか？**\
  いいえ。ビジュアルルールエディターを使用すると、フォームデータモデルを作成することなく、**API統合を作成** オプションを使用してAPIを直接統合できます。 このアプローチは、軽量なユースケースや、フォーム固有のユースケースに最適です。

* **ルールエディターから作成されたAPI呼び出しを保護できますか？**\
  はい。API統合設定には、**Basic、API Key、OAuth 2.0**&#x200B;などの認証オプションが用意されています。 また、**暗号化必須**&#x200B;を有効にして、機密データが安全に送信されるようにすることもできます。
