---
title: アダプティブフォームでのカスタム関数の作成と追加
description: AEM Formsはカスタム関数をサポートしており、ルールエディター内で独自の関数を作成および使用できます。
keywords: ルールエディターでカスタム関数を使用して、カスタム関数の追加、カスタム関数の使用、カスタム関数の作成をおこないます。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: f5c17382052b4d116deaae564f1a2b9fdbb5ea0a
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 11%

---


# コアコンポーネントに基づくアダプティブフォームのカスタム関数の作成

コアコンポーネントに基づくアダプティブFormsは、ユーザー入力に基づいてコンテンツと動作を調整することで、動的なユーザーエクスペリエンスを提供します。 カスタム関数を使用すると、開発者は機能を拡張して、フォームが特定の要件を満たすことができるようにします。 カスタム機能を統合することで、開発者は複雑なロジックを実装し、プロセスを自動化し、特定のビジネス要件やユーザーの期待に沿った独自のインタラクションを導入できます。 これにより、フォームが様々な条件に適合するだけでなく、様々なユースケースに対してより正確で効果的なソリューションを提供できるようになります。
この記事では、コアコンポーネントを使用してアダプティブFormsのカスタム関数を作成する手順を説明します。

## 考慮事項

* `parameter type` と `return type` は `None` をサポートしていません。

* カスタム関数リストでサポートされていない関数は次のとおりです。
   * ジェネレーター関数
   * 非同期/待機関数
   * メソッドの定義
   * クラスメソッド
   * デフォルトのパラメーター
   * REST パラメーター

## カスタム関数を作成するための前提条件

アダプティブFormsへのカスタム関数の追加を開始する前に、次のことを確認してください。

**ソフトウェア：**

* **プレーンテキストエディター（IDE）**：任意のプレーンテキストエディターも使用できますが、Microsoft Visual Studio Code などの統合開発環境（IDE）は、編集を容易にする高度な機能を提供します。

* **Git:** このバージョン管理システムは、コードの変更を管理するために必要です。 インストールされていない場合は、https://git-scm.comからダウンロードします。


## カスタム関数の作成 {#create-custom-function}

ルールエディターでカスタム関数を呼び出すクライアントライブラリを作成します。 詳しくは、「[クライアント側ライブラリの使用](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=ja#developing)」を参照してください。

カスタム関数の作成手順は次のとおりです。
1. [クライアントライブラリの作成](#create-client-library)
1. [アダプティブフォームへのクライアントライブラリの追加](#use-custom-function)

### クライアントライブラリの作成 {#create-client-library}

クライアントライブラリを追加することで、カスタム関数を追加できます。 クライアントライブラリを作成するには、次の手順を実行します。

**リポジトリのクローンを作成**

[AEM Formsas a Cloud Serviceリポジトリ ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=jp#accessing-git) のクローン：

1. コマンドラインまたはターミナルウィンドウを開きます。

1. リポジトリを保存するマシン上の目的の場所に移動します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   `git clone [Git Repository URL]`

このコマンドは、リポジトリをダウンロードし、複製されたリポジトリのローカルフォルダーをコンピューターに作成します。 このガイド全体では、このフォルダーを [AEMaaCS プロジェクトディレクトリ ] と呼びます。

**クライアントライブラリフォルダーの追加**

[AEMaaCS プロジェクトディレクトリ ] に新しいクライアントライブラリフォルダーを追加するには、次の手順に従います。

1. [AEMaaCS プロジェクトディレクトリ ] をエディターで開きます。

   ![ カスタム関数のフォルダー構造 ](/help/forms/assets/custom-library-folder-structure.png)

1. `ui.apps` を見つけます。
1. 新規フォルダーを追加します。 例えば、`experience-league` というフォルダーを追加します。
1. フォルダー `/experience-league/` 移動し、`ClientLibraryFolder` を追加します。 例えば、`customclientlibs` という名前のクライアントライブラリフォルダーを作成します。

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**クライアントライブラリフォルダーへのファイルとフォルダーの追加**

追加したクライアントライブラリフォルダーに次の内容を追加します。

* .content.xml ファイル
* js.txt ファイル
* js フォルダー

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. `.content.xml` で次のコード行を追加します。

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > `client library folder` および `categories` プロパティには、任意の名前を付けることができます。

1. `js.txt` で次のコード行を追加します。

   ```javascript
         #base=js
       function.js
   ```
1. `js` フォルダーに、Javascript ファイルをとして追加します。これには、カスタム関数が含まれ `function.js` います。

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```
1. ファイルを保存します。

![ カスタム関数のフォルダー構造 ](/help/forms/assets/custom-function-added-files.png)

**新規フォルダーを filter.xml に含めます**:

1. [AEMaaCS プロジェクトディレクトリ]内の `/ui.apps/src/main/content/META-INF/vault/filter.xml` ファイルに移動します。

1. ファイルを開き、最後に次の行を追加します。

   `<filter root="/apps/experience-league" />`
1. ファイルを保存します。

![ カスタム関数フィルター xml](/help/forms/assets/custom-function-filterxml.png)

**新しく作成したクライアントライブラリフォルダーをAEM環境にデプロイします**。

AEM as a Cloud Service の [AEMaaCS プロジェクトディレクトリ]を Cloud Service 環境にデプロイします。Cloud Service 環境にデプロイするには：

1. 変更をコミットする

   1. 次のコマンドを使用して、リポジトリに変更を追加、コミット、プッシュします。

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. 更新されたコードをデプロイします。

   1. 既存のフルスタックパイプラインを使用してコードのデプロイメントをトリガーします。 これにより、更新されたコードが自動的にビルドおよびデプロイされます。

パイプラインをまだ設定していない場合は、[AEM Forms as a Cloud Service のパイプラインの設定方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#setup-pipeline)のガイドを参照してください。

パイプラインが正常に実行されると、クライアントライブラリに追加されたカスタム関数が [ アダプティブフォームのルールエディター ](/help/forms/rule-editor-core-components.md) で使用できるようになります。

### アダプティブフォームへのクライアントライブラリの追加{#use-custom-function}

クライアントライブラリをForms CS 環境にデプロイしたら、アダプティブフォームでその機能を使用します。 アダプティブフォームにクライアントライブラリを追加するには、次の手順に従います

1. フォームを編集モードで開きます。フォームを編集モードで開くには、フォームを選択し、「**[!UICONTROL 編集]**」を選択します。
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナプロパティ ![ガイドプロパティ](/help/forms/assets/configure-icon.svg) アイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 基本]**」タブを開き、ドロップダウンリストから **[!UICONTROL クライアントライブラリカテゴリ]** の名前を選択します（この場合は「`customfunctionscategory`」を選択します）。

   ![カスタム関数をクライアントライブラリを追加する](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > 「**[!UICONTROL クライアントライブラリカテゴリ]**」フィールドにコンマ区切りのリストを指定することで、複数のカテゴリを追加できます。

1. 「**[!UICONTROL 完了]**」をクリックします。

カスタム関数は、[JavaScript注釈 [ を使用して ](/help/forms/rule-editor-core-components.md) アダプティブフォームのルールエディター ](##js-annotations) で使用できます。

## アダプティブフォームでのカスタム関数の使用

アダプティブフォームでは、[ ルールエディター内のカスタム関数 ](/help/forms/rule-editor-core-components.md) を使用できます。 JavaScriptのファイル（`Function.js` ファイル）に次のコードを追加して、生年月日（YYYY-MM-DD）に基づいて年齢を計算しましょう。 生年月日を入力として取得し、年齢を返すカスタム関数を `calculateAge()` として作成します。

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

上記の例では、ユーザーが誕生日を（YYYY-MM-DD）形式で入力すると、カスタム関数 `calculateAge` が呼び出され、年齢が返されます。

![ ルールエディター内の Calcualte Agae カスタム関数 ](/help/forms/assets/custom-function-calculate-age.png)

フォームをプレビューして、ルールエディターを介してカスタム関数がどのように実装されているかを確認します。

![ ルールエディターフォームプレビューでの Agae カスタム関数の計算 ](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 次の [ カスタム関数 ](/help/forms/assets//customfunctions.zip) フォルダーを参照できます。 [ パッケージマネージャー ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager) を使用して、このフォルダーをダウンロードし、AEM インスタンスにインストールします。

## カスタム関数の機能

AEM forms のカスタム関数は、フォームの機能を拡張およびパーソナライズするための堅牢なソリューションを提供します。 カスタム関数を使用すると、組織固有のニーズを満たすことができます。

これらの関数は、特定フィールドの操作、グローバルフィールドの使用、非同期操作、キャッシュメカニズムの組み込みなど、様々な機能をサポートします。 この柔軟性により、フォームを複雑な要件に適応させ、効率的にカスタマイズされたユーザーエクスペリエンスを提供できるようになります。 これらの高度な機能を活用することで、フォームのインタラクションを強化し、パフォーマンスを最適化して、AEM フォームをより機能的でレスポンシブなものにすることができます。

カスタム関数の機能について説明します。

### カスタム関数での非同期のサポート {#support-of-async-functions}

非同期カスタム関数がルールエディターリストに表示されない。 ただし、同期関数式を使用して作成されたカスタム関数内で、非同期関数を呼び出すことができます。

![Sync および async カスタム関数 ](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> カスタム関数で非同期関数を呼び出す利点は、非同期関数を使用すると、複数のタスクを同時に実行でき、カスタム関数内で各関数の結果を使用できる点です。

カスタム関数を使用して非同期関数を呼び出す方法については、以下のコードを参照してください。

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

上記の例では、asyncFunction 関数は `asynchronous function` です。 `https://petstore.swagger.io/v2/store/inventory` に対して `GET` リクエストを実行することで、非同期操作を実行します。 `await` を使用して応答を待ち、`response.json()` を使用して応答本文を JSON として解析し、データを返します。 `callAsyncFunction` 関数は、`asyncFunction` 関数を呼び出してコンソールに応答データを表示する同期カスタム関数です。 `callAsyncFunction` 関数は同期していますが、非同期の asyncFunction 関数を呼び出し、`then` 文と `catch` 文で結果を処理します。

動作を確認するには、ボタンを追加し、ボタンクリック時に非同期関数を呼び出すボタンのルールを作成します。

![async 関数のルールを作成しています ](/help/forms/assets/rule-for-async-funct.png)

ユーザーが「`Fetch`」ボタンをクリックすると、カスタム関数 `callAsyncFunction` が呼び出され、非同期関数 `asyncFunction` が呼び出されることを示すには、以下のコンソールウィンドウの図を参照してください。 コンソールウィンドウをInspectして、ボタンクリックに対する応答を表示します。

![ コンソールウィンドウ ](/help/forms/assets/async-custom-funct-console.png)


### フィールドおよびグローバルスコープのオブジェクトは、カスタム関数でサポートされています。 {#support-field-and-global-objects}

フィールドオブジェクトは、テキストフィールド、チェックボックスなど、フォーム内の個々のコンポーネントまたは要素を参照します。 Globals オブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するメソッドなどの読み取り専用変数が含まれています。

>[!NOTE]
>
> `param {scope} globals` は最後のパラメーターである必要があり、アダプティブフォームのルールエディターには表示されません。

### カスタム関数でのキャッシュサポート

アダプティブFormsは、カスタム関数のキャッシュを実装して、ルールエディターでカスタム関数のリストを取得する際の応答時間を短縮します。 `error.log` ファイルに `Fetched following custom functions list from cache` のようなメッセージが表示されます。

![ キャッシュをサポートするカスタム関数 ](/help/forms/assets/custom-function-cache-error.png)

カスタム関数が変更されると、キャッシュが無効化され、解析されます。

## トラブルシューティング

* カスタム関数のコードを含んだJavaScript ファイルにエラーがある場合、カスタム関数はアダプティブフォームのルールエディターに表示されません。 カスタム関数のリストを確認するには、エラーの `error.log` ファイルに移動します。 エラーが発生すると、カスタム関数のリストは空で表示されます。

  ![ エラーログファイル ](/help/forms/assets/custom-function-list-error-file.png)

  エラーがない場合、カスタム関数が取得され、`error.log` ファイルに表示されます。 `error.log` ファイルに `Fetched following custom functions list` のようなメッセージが表示されます。

  ![ 適切なカスタム関数を持つエラーログファイル ](/help/forms/assets/custom-function-list-fetched-in-error.png)

## 次の手順

次に、様々な [ コアコンポーネントに基づくアダプティブフォームのカスタム関数の例 ](/help/forms/custom-function-core-components-use-cases.md) を見てみましょう。

## 関連トピック

{{see-also-rule-editor}}