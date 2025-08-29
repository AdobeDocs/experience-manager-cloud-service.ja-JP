---
title: Formsのルールエディターへの API の統合
description: フォームデータモデルを使用せずに、コアコンポーネントに基づくアダプティブFormsの API を統合する方法など、ルールエディターでの呼び出しサービスの最新の機能強化について説明します。
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: api をルールエディターに統合し、サービスを起動する機能を強化
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: 80dde7ddaa08d752391b4004d7c93e5baac9716e
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# ルールエディターでの API の統合

<span> ルールエディターへの API の統合は、早期導入プログラムの一環です。 公式メール ID から `aem-forms-ea@adobe.com` に書き込んで、早期導入プログラムに参加し、機能へのアクセスをリクエストできます。</span>

アダプティブFormsのビジュアルルールエディターでは、フォームデータモデルを作成せずに API を直接統合できます。 API エンドポイントに接続するには、API の URL （JSON 形式）を入力するか、cURL コマンドを使用して設定を読み込みます。 統合すると、**サービスを呼び出し** アクションを使用して API を呼び出すことができます。

フォームフィールドは、API 設定で定義された入力パラメーターに直接マッピングできます。 同様に、対応する API 応答の **イベントペイロード** オプションを使用して、出力パラメーターをフォームフィールドにマッピングできます。

また、ビジュアルルールエディターを使用すると、サービスを呼び出す際に **成功** ハンドラーと **失敗ハンドラー** を定義できます。 サクセスハンドラーは、API 呼び出しが成功した後に実行するアクションを指定し、エラーハンドラーは、エラーが発生した場合のフォームの応答方法を定義します。

>[!NOTE]
>
> ルールエディターでの API 統合は、[ ユニバーサルエディターで作成されたEdge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) にも適用できます。

## 比較：API 統合メソッド

| 項目 | フォームデータモデル（FDM）との API 統合 | 直接 API 統合（*Create API 統合* を使用） |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **目的** | 複数のフォームにわたる、再利用可能な API の一元的な統合 | フォーム固有の API の迅速な統合 |
| **セットアップの場所** | フォームデータモデルエディターで作成および編集（AEM コンソール） | アダプティブフォームのルールエディターで直接作成および編集 |
| **複雑性** | セットアップ作業が多い（マッピングと設定が必要） | シンプルで軽量 |
| **最適な対象** | 複数のフォームを使用した大規模法人またはユースケース | 小さなフォーム、プロトタイプまたは 1 回限りの API 呼び出し |

## API 統合設定

以下のスクリーンショットは、API 統合設定ウィンドウを示しています。

![API 統合設定 ](/help/forms/assets/api-integration-configuration.png)

### 主要な設定オプション

**API 統合設定**

* **cURL から読み込み**:API の URL、HTTP メソッド、ヘッダー、パラメーターなどの詳細を手動で入力する代わりに、既に作成されている cURL コマンドを貼り付けて、API 統合を設定します。
* **表示名**:API サービスのカスタム名。
* **API URL**:API サービスのエンドポイント。
* **HTTP メソッドを選択**: API の呼び出しに使用される HTTP リクエストメソッド。
* **コンテンツタイプ**：リクエストと応答の形式を定義します。
* **暗号化が必要**:（オプション）送信中に機密データが暗号化されるようにします。
* **クライアントで実行**：有効にすると、API 呼び出しはサーバーではなくクライアント（ブラウザー）から行われます。

**認証タイプ**

* **オプション**：なし、基本、API キー、OAuth 2.0。

**入力パラメーター**

* **入力用に JSON をアップロード**：サンプルの JSON ファイルをアップロードして、入力マッピングを自動入力します。
   * **Name**:API に必要な入力パラメーター名。
   * **タイプ**：入力のデータタイプ（文字列、数値、ブール値など）。
   * **In**：パラメーターの場所（クエリ、ヘッダーまたは本文）。
   * **デフォルト値**：ユーザーから提供されない場合、事前入力された値。
   * **追加**：入力パラメーターを追加するオプション。

**出力パラメーター**

* **出力用に JSON をアップロード**：マッピングを自動生成するためのサンプル API 応答をアップロードします。
   * **Name**: API 応答からの出力パラメーター名。
   * **Type**：出力パラメーターで想定されるデータタイプ（文字列、数値など）。
   * **In**：マッピングされた値を格納する場所を定義します。
   * **追加/削除**：新しいマッピングを追加するか、既存のマッピングを削除します。

## ユースケース：Visa 申請フォームの国フィールドへの入力

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**シナリオ**：政府機関が、次のフィールドを含むオンラインのビザ申請フォームを提供します。

1. フルネーム （テキスト）
2. 生年月日（日付）
3. 国籍国（ドロップダウン）
4. パスポート番号（テキスト）
5. パスポート発行国（ドロップダウン）
6. 宛先の国（ドロップダウン）
7. 到着予定日（Date）

フォームは、国の静的なリストを管理する代わりに、**getcountryname API** を使用して、国に関する情報（大陸、資本、ISO Alpha コードなど）を動的に取得します。

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

これにより、申込者がフォームに入力する際に、常に最新かつ正確な国のリストを確認できます。

### ルールエディターで API 統合を使用した実装

ルールエディターで「**API 統合を作成**」ボタンをクリックすると、フォームデータモデルを作成せずに API を統合できます。

![API 統合の作成 ](/help/forms/assets/create-api-integration.png)

**getcountryname** という名前の API サービスは、ルールエディターの **API 統合設定** の下で設定されます。

![API REST エンドポイントの設定 ](/help/forms/assets/api-restendpoint.png)

* **API エンドポイント URL** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* **HTTP メソッド** → GET
* **コンテンツタイプ** → JSON
* **入力** →クエリパラメーターとして渡 `username` れます（`aemforms`）。
* **出力**`continent`、`capital`、`countrynames`、`isoAlpha3`、`languages` などの→応答フィールドは、フォームフィールドにマッピングされます。

**ビザ申請フォーム** では、3 つのドロップダウンフィールド **国籍国**、**パスポート発行国**、および **発送先国** は、**サービスの呼び出し** アクションにバインドされています。

フォームが読み込まれると、**サービスを呼び出し** は API から国のリストを取得します。 次に、応答がマッピングされ、ドロップダウンオプションに自動的に入力されます。

例えば、ユーザーが **国籍国** を開くと、国のリストは API 応答から動的に表示されます。

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![API 統合出力 ](/help/forms/assets/api-integration-output.png)

同様に、**パスポート発行国** と **宛先国** は同じ API 呼び出しを使用し、3 つのフィールドすべてで一貫性のある最新のデータを確保します。

## API 障害の再試行メカニズムの実装

API リクエストが失敗した場合は、ユーザーにエラーをレポートする前にリクエストを再試行すると便利なことがよくあります。 **function.js** ファイルにカスタムコードを記述することで、ポーリングおよび再試行メカニズムを実装できます。

次の例は、最大 2 回の再試行時および再試行間の指数関数的なバックオフを伴う API 失敗を処理する方法を示しています。

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

上記のコードでは、**retryHandler** 関数は、失敗した場合に自動再試行で API リクエストを管理します。 リクエスト関数（requestFn）を受け取り、リクエストを最大 2 回試み、再試行ごとにメタデータを追加します。

>[!NOTE]
>
> カスタム関数の追加方法の手順について詳しくは、[ コアコンポーネントに基づくアダプティブFormsのカスタム関数の概要 ](/help/forms/create-and-use-custom-functions.md) を参照してください。

## よくある質問

* **アダプティブFormsで API を統合するには、フォームデータモデルを作成する必要がありますか？**\
  いいえ。ビジュアルルールエディターを使用すると、フォームデータモデルを作成することなく、「**Create API Integration**」オプションを使用して API を直接統合できます。 このアプローチは、軽量またはフォーム固有のユースケースに最適です。

* **ルールエディターから行われる API 呼び出しを保護できますか？**\
  はい。API 統合設定は、**基本、API キー、OAuth 2.0** などの認証オプションを提供します。 また、**暗号化が必要** を有効にして、機密データを安全に送信することもできます。
