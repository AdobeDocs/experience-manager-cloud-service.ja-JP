---
title: インタラクティブ通信同期 API の設定方法
description: Adobe Experience Manager Forms as a Cloud Service用のインタラクティブ通信同期 API の開発環境のセットアップ
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: cb69041ff59ba1ff586e8c1c71090cc2eb9ad453
workflow-type: tm+mt
source-wordcount: '2573'
ht-degree: 2%

---


# AEM Forms as a Cloud Service通信の同期 API 処理

このガイドでは、AEM Forms Communications Synchronous API の設定と使用に関する包括的な手順を説明します。

OAuth サーバー間認証を使用して、AEM as a Cloud Service環境を設定し、API アクセスを有効にし、通信 API を呼び出す方法について説明します。

## 前提条件

AEM Forms Communications API の実行とテストを行うための環境を設定するには、以下が揃っていることを確認してください。

### アクセスと権限

通信 API の設定を開始する前に、必要なアクセス権と権限があることを確認してください。

**ユーザーおよび役割の権限**

- Adobe IDは [https://account.adobe.com/](https://account.adobe.com/) で作成されました
- 組織のメールに関連付けられたAdobe ID
- Adobe Managed Services製品コンテキストの割り当て
- Adobe Admin Consoleで割り当てられた開発者の役割
- Adobe Developer Consoleでプロジェクトを作成する権限

>[!NOTE]
>
> 役割の割り当ておよびユーザーへのアクセス権の付与について詳しくは、記事 [&#x200B; ユーザーと役割の追加 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/users-and-roles) を参照してください。

**Cloud Manager アクセス**

- [Cloud Manager](https://my.cloudmanager.adobe.com) のログイン資格情報
- プログラムの環境を表示および管理するためのアクセス
- CI/CD パイプラインを作成および実行する権限
- 環境の詳細および設定へのアクセス

**Git リポジトリへのアクセス**

- Cloud Manager Git リポジトリーへのアクセス
- クローン作成と変更のプッシュのための Git 資格情報

### 開発ツール

- サンプルアプリケーションの実行用の **Node.js**
- **Git** の最新バージョン
- **ターミナル/コマンドライン** へのアクセス
- 設定ファイル編集用の **テキストエディターまたは IDE** （VS Code、IntelliJ など）
- **Postman** または API テスト用の同様のツール

>[!NOTE]
>
> これは、環境ごとに 1 回限りのプロセスです。AEM Forms Communications API の設定を進める前に、このプロセスを完了する必要があります。

次に、各手順を詳しく説明します。

### 手順 1:AEM インスタンスの更新

AEM インスタンスを更新するには：

1. **Adobe Cloud Managerへのログイン**
   1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) に移動します。
   2. Adobe IDでログイン

2. **プログラムの概要に移動**
   1. リストからプログラムを選択します。 プログラムの概要ページにリダイレクトされます

3. **環境の詳細を見つける**
   1. 環境名の横にある「`ellipsis` （...）」アイコンを選択し、「**更新**」をクリックします
   2. **送信** ボタンをクリックし、提案されたフルスタックパイプラインを実行します。

      ![&#x200B; 環境の更新 &#x200B;](/help/forms/assets/update-env.png)

### 手順 2:Git リポジトリの複製

Cloud Manager Git リポジトリーをクローンして、API 設定ファイルを管理します。

1. **リポジトリセクションを見つける**
   1. **プログラムの概要** ページで、「**リポジトリ**」タブをクリックします
   2. リポジトリ名を見つけ、省略記号メニュー（...）をクリックします。
   3. リポジトリー URL をコピー

      >[!NOTE]
      >
      > 通常、URL 形式は `https://git.cloudmanager.adobe.com/<org>/<program>/` です

2. **Git コマンドを使用したクローン**

   1. コマンドプロンプトまたはターミナルを開きます
   2. `git clone` コマンドを実行して、Git リポジトリを複製します。

      ```bash
      git clone [repository-url]
      ```

      >[!NOTE]
      >
      > Git リポジトリを複製するには、Adobe Cloud Managerから提供された資格情報を使用します。

      例えば、Git リポジトリーをクローンするには、次のコマンドを実行します。

      ```bash
      https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-p43162-uk59167/
      ```

      ![Git リポジトリのクローン作成 &#x200B;](/help/forms/assets/repo-clone.png)


**Git リポジトリ統合オプション**

Adobe Cloud Managerでは、次の両方のリポジトリオプションをサポートしています。

- **Cloud Manager Git リポジトリの直接使用**
   - Cloud Managerのネイティブ Git リポジトリを使用
   - パイプラインとの組み込み統合

- **顧客管理 Git リポジトリーとの統合**
   - 独自の Git リポジトリ（GitHub、GitLab、Bitbucket など）を接続
   - Adobe Cloud Managerとの同期の設定

Adobe Cloud ManagerとAdobe Cloud Managerの統合方法について詳しくは、[Git 統合に関するドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html) を参照してください。

### 手順 3:AEM Cloud Service 環境とAEM Forms エンドポイントへのアクセス

AEM Cloud Service 環境の詳細にアクセスして、API 設定に必要な URL と識別子を取得します。

1. **Adobe Cloud Managerへのログイン**
   1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) に移動します。
   2. Adobe IDでログイン

2. **プログラムの概要に移動**
リストからプログラムを選択します。 プログラムの概要ページにリダイレクトされます

3. **AEM Cloud Service 環境へのアクセスと表示**

   AEM Cloud Service 環境の詳細の表示またはアクセスには、次の 2 つのオプションのいずれかを使用できます。

   - **オプション 1：概要ページから**

      1. **プログラムの概要** ページで、次の操作を行います
      2. 左側のメニューで **「環境」** クリックします。  すべての環境のリストが表示されます

         ![&#x200B; すべての環境を表示 &#x200B;](/help/forms/assets/all-env.png)

      3. 特定の環境名をクリックすると詳細を表示できます

         ![&#x200B; オプション 1 – 環境の詳細 &#x200B;](/help/forms/assets/option1-env.png)

   - **オプション 2：環境セクションから**

      1. プログラムの概要ページで、次の操作を行います
      2. 「**環境** セクションを見つけます
      3. **「すべて表示」** をクリックして、すべての環境を表示します
      4. 環境の横にある **省略記号メニュー（...）** をクリックします
         ![&#x200B; オプション 1 – 環境の詳細 &#x200B;](/help/forms/assets/option2-env-details.png)
      5. 「詳細 **表示」を選択し** す。

         ![&#x200B; オプション 1 – 環境の詳細 &#x200B;](/help/forms/assets/option1-env.png)

4. **AEM Forms エンドポイントの検索**

   **環境** 詳細ページから、次の詳細に注意してください。

   **オーサーサービス URL**

   - URL：`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`
   - バケット：author-pXXXXX-eYYYY
例：`https://author-p43162-e177398.adobeaemcloud.com`

   **パブリッシュサービス URL**

   - URL：`https://publish-pXXXXX-eYYYYY.adobeaemcloud.com`
   - バケット：publish-pXXXXX-eYYYY
例：`https://publish-p43162-e177398.adobeaemcloud.com`

>[!NOTE]
>
> AEM Cloud Service 環境およびAEM Forms エンドポイントにアクセスする方法については、[&#x200B; 環境の管理に関するドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=ja) を参照してください。

### 手順 4:API アクセスの設定

次の手順を実行して、AEM Forms Communications API を設定します。

#### 4.1 Adobe Developer Console プロジェクトのセットアップ

1. **Adobe Developer Consoleへのアクセス**
   1. [Adobe Developer Console](https://developer.adobe.com/console) に移動します
   2. Adobe IDでログイン

2. **新規プロジェクトを作成**
   1. 「**クイックスタート**」セクションで、「**新規プロジェクトを作成**」をクリックします
   2. デフォルト名で新しいプロジェクトが作成されます

      ![ADC プロジェクトの作成 &#x200B;](/help/forms/assets/adc-home.png)

   3. 右上隅の **プロジェクトを編集** をクリックします

      ![&#x200B; プロジェクトを編集 &#x200B;](/help/forms/assets/adc-edit-project.png)

   4. 意味のある名前を指定（例：「formsproject」）
   5. 「**保存**」をクリックします。

      ![&#x200B; プロジェクト名を編集 &#x200B;](/help/forms/assets/adc-edit-projectname.png)

#### 4.2 Forms Communication API の追加

要件に応じて、様々なAEM Forms通信 API を追加できます。

**A.ドキュメントサービス API の場合**

1. 「**API を追加**」をクリックします。

   ![API を追加 &#x200B;](/help/forms/assets/adc-add-api.png)

2. **Forms Communication API** を選択
   1. _API を追加_ ダイアログで、**Experience Cloudでフィルタリングします**
   2. 「Forms Communication API **を選択し** す。

   ![Forms Communication API の追加 &#x200B;](/help/forms/assets/adc-add-forms-api.png)


3. **OAuth サーバー間** 認証方法を選択します

   ![&#x200B; 認証方法の選択 &#x200B;](/help/forms/assets/adc-add-authentication-method.png)

**B.Forms Runtime API の場合**

1. **「API を追加」をクリック**
   - プロジェクトで「**API を追加**」ボタンをクリックします

   ![API を追加 &#x200B;](/help/forms/assets/adc-add-api.png)

2. **AEM Forms配信およびランタイム API を選択**
   - _API を追加_ ダイアログで、**Experience Cloudでフィルタリングします**
   - **AEM Forms配信およびランタイム API」を選択** ます。
   - 「**次へ**」をクリックします。

   ![&#x200B; ランタイム API を追加 &#x200B;](/help/forms/assets/add-runtime-api.png)


3. **認証方法**
   - **OAuth サーバー間**&#x200B;認証方式を選択します。


   ![&#x200B; 認証方法の選択 &#x200B;](/help/forms/assets/add-authentication-for-runtime-apis.png)

#### 4.3 製品プロファイルの追加

製品プロファイルを追加するには、次の手順に従います。

1. 必要なアクセスレベルに基づいて適切な **製品プロファイル** を選択します。

   | アクセスタイプ | 製品プロファイル |
   |------------------|----------------------|
   | 読み取り専用アクセス | `AEM Users - author - Program XXX - Environment XXX` |
   | 読み取り/書き込みアクセス | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
   | 完全な管理アクセス | `AEM Administrators - author - Program XXX - Environment XXX` |

2. オーサーサービス URL （**）に一致する** 製品プロファイル `https://author-pXXXXX-eYYYYY.adobeaemcloud.com` を選択します。 例：select `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`。

3. 「**設定済み API を保存**」をクリックします。API と製品プロファイルがプロジェクトに追加されます

   ![&#x200B; プロジェクト設定の選択 &#x200B;](/help/forms/assets/adc-add-product-profile.png)

#### 4.4 資格情報の生成と保存

1. **認証情報へのアクセス**

   1. Adobe Developer Consoleでプロジェクトに移動します
   2. **OAuth サーバー間** 資格情報をクリックします。
   3. 「**資格情報の詳細** セクションを表示します

   ![資格情報の表示](/help/forms/assets/adc-view-credential.png)

2. **レコード API 資格情報**

   ```text
   API Credentials:
   ================
   Client ID: <your_client_id>
   Client Secret: <your_client_secret>
   Technical Account ID: <tech_account_id>
   Organization ID: <org_id>
   Scopes: AdobeID,openid,read_organizations
   ```

#### 4.5 アクセストークンの生成

**A.テスト用**

Adobe Developer Consoleで手動でアクセストークンを生成します。

1. **プロジェクトへの移動**
   1. Adobe Developer Consoleで、プロジェクトを開きます
   2. **OAuth サーバー間** をクリックします。

2. **アクセストークンの生成**
   1. プロジェクトの「API」セクションで **「アクセストークンを生成」** ボタンをクリックします
   2. 生成されたアクセストークンのコピー

   ![&#x200B; アクセストークンの生成 &#x200B;](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > アクセストークンは **24 時間有効**

**B.実稼動の場合**

cURL コマンドを使用してプログラムでトークンを生成します。

**必要な資格情報：**

- クライアント ID
- クライアントの秘密鍵
- 範囲（通常：`AdobeID,openid,read_organizations`）

**トークン エンドポイント：**

```
https://ims-na1.adobelogin.com/ims/token/v3
```

**サンプルリクエスト （curl）:**

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=client_credentials' \
  -d 'client_id=<YOUR_CLIENT_ID>' \
  -d 'client_secret=<YOUR_CLIENT_SECRET>' \
  -d 'scope=AdobeID,openid,read_organizations'
```

**応答：**

```json
{
  "access_token": "eyJhbGciOiJSUz...",
  "token_type": "bearer",
  "expires_in": 86399
}
```

#### 4.6 クライアント ID のAEMへの登録

ADC プロジェクトのクライアント ID がAEM インスタンスと通信できるようにするには、YAML 設定ファイルを使用して登録し、設定パイプラインを介してデプロイする必要があります。

1. **Config ディレクトリの検索または作成**

   1. AEM プロジェクトリポジトリのクローンに移動し、`config` フォルダーに移動します
   2. 存在しない場合は、プロジェクトのルートレベルで作成します。

   ```bash
   mkdir config
   ```

2. `api.yaml` ディレクトリに `config` という名前の新しいファイルを作成します。

   ```bash
   touch config/api.yaml
   ```

3. `api.yaml` ファイルに次のコードを追加します。

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

   設定パラメーターを次に説明します。

   - **kind**：常に `"API"` に設定します（API 設定として識別します）
   - **version**:API バージョン（通常は `"1"` または `"1.0"`）
   - **envTypes**：この設定が適用される環境タイプの配列
      - `["dev"]` – 開発環境のみ
      - `["stage"]` - ステージング環境のみ
      - `["prod"]` – 実稼動環境のみ
   - **allowedClientIDs**:AEM インスタンスへのアクセスが許可されたクライアント ID
      - **オーサー**：オーサー層のクライアント ID
      - **パブリッシュ**：パブリッシュ層のクライアント ID
      - **preview**：プレビュー層のクライアント ID

   例えば、`allowedClientIDs` を `6bc4589785e246eda29a545d3ca55980` として、envTypes を `dev` として追加します。

   ![&#x200B; 設定ファイルの追加 &#x200B;](/help/forms/assets/create-api-yaml-file.png)

4. **変更のコミットとプッシュ**

   1. クローンしたリポジトリのルートフォルダーに移動して、以下のコマンドを実行します。


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![Git の変更のプッシュ &#x200B;](/help/forms/assets/push-yaml-changes-in-git.png)


5. **設定パイプラインをセットアップ**

   1. **Cloud Managerへのログイン**
      1. [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) に移動します。
      2. Adobe IDでログイン

   2. **プログラムに移動**
リストからプログラムを選択すると、プログラムの概要ページにリダイレクトされます

   3. **パイプラインカードを見つける**
      1. プログラムの概要ページで **パイプライン** カードを見つけます
      1. 「追加 **ボタンをクリ** ク

   4. **パイプラインタイプを選択**

      - **開発環境の場合**:**「実稼動以外のパイプラインを追加」** を選択します。 実稼動以外のパイプラインは、開発環境とステージング環境用です

      - **実稼動環境の場合**:**「実稼動パイプラインを追加」** を選択します。 実稼動パイプラインには追加の承認が必要です

        >[!NOTE]
        >
        > この場合、開発環境が使用可能なので、実稼動以外のパイプラインを作成します。

   5. **パイプラインの設定 – 「設定」タブ**

      「**設定**」タブで、次のように設定します。

      a. **パイプラインタイプ**
      - 「デプロイメントパイプライン **を選択**

      b. **パイプライン名**
      - わかりやすい名前を指定（例：パイプラインに `api-config-pipieline` という名前を付ける）

      c. **導入トリガー**
      - **手動**：手動でトリガーされた場合にのみデプロイします（初期設定で推奨）
      - **Git の変更時**：変更がブランチにプッシュされると自動デプロイされます

      d. **重要な指標のエラー動作**
      - **毎回確認する**：失敗時にアクションを要求する（デフォルト）
      - **直ちに失敗**：指標の失敗時にパイプラインを自動的に失敗します
      - **直ちに続行**：失敗しても続行します

      e. 「**続行」をクリックして** 「**Source コード**」タブに進みます

      ![&#x200B; 設定パイプライン &#x200B;](/help/forms/assets/add-config-pipeline.png)

   6. **パイプラインを設定 – 「Source コード」タブ**

      「**Source コード**」タブで、次のように設定します。

      a. **デプロイメントタイプ**
      - 「ターゲットデプロイメント **を選択**

      b. **デプロイメントオプション**
      - 「**Config」** を選択します（設定ファイルのみをデプロイします）。 これは、Cloud Managerに config デプロイメントであることを示しています。

      c. **適格なデプロイメント環境を選択**
      - 設定をデプロイする環境を選択します。 この場合、これは `dev` 環境です。

      d. **Source コードの詳細を定義**

      - **リポジトリ**:`api.yaml` ファイルを含むリポジトリを選択します。 例えば、`AEMFormsInternal-ReleaseSanity-p43162-uk59167` リポジトリを選択します。
      - **Git ブランチ**：ブランチを選択します。 例えば、この場合、コードは `main` ブランチにデプロイされます。
      - **コードの場所**：ディレクトリへのパス `config` 入力します。 `api.yaml` はルートのフォルダーにあ `config` ので、`/config` と入力します

      e. 「**保存」** をクリックして、パイプラインを作成します

      ![&#x200B; 設定パイプライン &#x200B;](/help/forms/assets/confirm-pipeline-1.png)

6. **設定をデプロイ**

   パイプラインが作成されたら、`api.yaml` 設定をデプロイします。

   1. **パイプラインの概要から**
      1. プログラムの概要ページで、「**パイプライン** カードを見つけます
      2. リストで新しく作成した設定パイプラインに移動します。 例えば、作成したパイプライン名（「api-config-pipeline」など）を探します。 ステータスや前回の実行を含むパイプラインの詳細を確認できます。

   2. **デプロイメントの開始**
      1. パイプラインの横にある **「ビルド」** ボタン（または再生アイコン ▶）をクリックします
      2. プロンプトが表示されたらデプロイメントを確認し、パイプラインの実行を開始します

      ![&#x200B; パイプラインを実行 &#x200B;](/help/forms/assets/run-config-pipeline.png)

   3. **デプロイメントの成功の確認**
      - パイプラインが完了するのを待ちます。
         - 成功すると、ステータスが「成功」（緑色のチェックマーク ✓）に変わります。
         - 失敗した場合は、ステータスが「失敗」（赤十字 ✗）に変わります。 **ログをダウンロード** をクリックして、エラーの詳細を表示します。

           ![&#x200B; パイプライン成功 &#x200B;](/help/forms/assets/pipeline-suceess.png)

      これで、Forms Communications API のテストを開始できます。 テストの目的で、Postman、curl、またはその他の REST クライアントを使用して、API を呼び出すことができます。

### 手順 5:API の仕様とテスト

これで環境が設定されたので、[Swagger UI](#a-using-swagger-ui-for-api-testing) を使用して、または NodeJS アプリケーションを開発してプログラムで、AEM Forms Communication API のテストを開始できます。

この例では、テンプレートと XDP ファイルを使用して Document Services API を使用してPDFを生成します。

#### A. API テストへの Swagger UI の使用

Swagger UI は、コードを記述せずに API をテストするためのインタラクティブなインターフェイスを備えています。**試す** 機能を使用して、[PDFを生成 &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) ドキュメントサービス API を呼び出してテストします。

1. API ドキュメントへの移動
   - Forms API:[Forms API リファレンス &#x200B;](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
   - ドキュメントサービス：[&#x200B; ドキュメントサービス API リファレンス &#x200B;](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
ブラウザーで [Document Services API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document) ドキュメントを開きます。
2. 「**ドキュメントの生成**」セクションを展開し、「[XDP またはPDF テンプレートから入力可能なPDF フォームを生成します（オプションでデータ結合も可能 &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm)」を選択します。
3. 右側のウィンドウで、「試す **をクリックし** す。

   ![API の Swagger テスト &#x200B;](/help/forms/assets/api-doc-generation.png)
4. 以下の値を入力します。

   | **セクション** | **パラメーター** | **値** |
   |--------------|---------------|------------|
   | バケット | AEM インスタンス | AEM インスタンス名（Adobe ドメイン名（`.adobeaemcloud.com`）を除いたもの。例えば、`p43162-e177398` をバケットとして使用します。 |
   | セキュリティ | ベアラートークン | Adobe Developer Console プロジェクトの OAuth サーバー間資格情報からのアクセストークンの使用 |
   | 本文 | テンプレート | XDP をアップロードしてPDF フォームを生成します。 例えば、[&#x200B; この XDP](/help/forms/assets/ClosingForm.xdp) を使用してPDFを生成できます。 |
   | 本文 | data | 事前入力されたPDF フォームを生成するためにテンプレートと結合されるデータを含む、オプションの XML ファイル。 例えば、[&#x200B; この XML](/help/forms/assets/ClosingForm.xml) を使用してPDFを生成できます。 |
   | パラメーター | X-Adobe-Accept-Experimental | 1 |

5. 「**送信**」をクリックして、API を呼び出します

   ![&#x200B; 送信 API](/help/forms/assets/api-send.png)

6. 「**応答** タブで応答を確認します。
   - 応答コードが `200` の場合は、PDFが正常に作成されたことを意味します。
   - 応答コードが `400` の場合は、リクエストパラメーターが無効か、形式が正しくないことを意味します。
   - 応答コードが `500` の場合は、内部サーバーエラーがあることを意味します。

   この場合、応答コードは `200` です。これは、PDFが正常に生成されたことを意味します。

   ![&#x200B; レビューの回答 &#x200B;](/help/forms/assets/api-success.png)

   これで、「[&#x200B; ダウンロード &#x200B;](/help/forms/assets/create-pdf.pdf) ボタンを使用して **作成したPDF** をダウンロードし、PDF ビューアで表示できます。

   ![PDFを表示 &#x200B;](/help/forms/assets/create-pdf.png)

>[!NOTE]
>
> テストの目的で、[Postman](https://www.postman.com/)、[curl](https://curl.se/) またはその他の REST クライアントを使用して、AEM API を呼び出すこともできます。

#### B. NodeJS アプリケーションをプログラムで開発する

**Document Services API を使用して、** XDP **テンプレートおよび** XML **データファイルから入力可能なPDF フォームを生成するための Node.js アプリケーションを開発** ます。

##### 前提条件

- システムにインストールされている Node.js
- アクティブなAEM as a Cloud Service インスタンス
- Adobe Developer Consoleからの API 認証用のベアラートークン
- サンプル XDP ファイル：[ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- サンプル XML ファイル：[ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

Node.js アプリケーションを開発するには、以下の開発手順に従います。

##### 手順 1：新しい Node.js プロジェクトの作成

cmd/terminal を開き、次のコマンドを実行します。

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![&#x200B; 新しい node js プロジェクトの作成 &#x200B;](/help/forms/assets/api-1.png)

##### 手順 2：必要な依存関係のインストール

**node-fetch**、**dotenv**、**form-data** ライブラリをインストールして、HTTP リクエストを行い、環境変数を読み取り、フォームデータを処理します。

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![npm 依存関係のインストール &#x200B;](/help/forms/assets/api-2.png)

##### 手順 3:package.json の更新

1. cmd/terminal を開き、コマンドを実行します。

   ```bash
   code .
   ```

   ![&#x200B; エディターでプロジェクトを開く &#x200B;](/help/forms/assets/api-3.png)

   コードエディターでプロジェクトが開きます。

2. `package.json` ファイルを更新して、`type` を `module` に追加します。

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![&#x200B; パッケージ ファイルの更新 &#x200B;](/help/forms/assets/api-4.png)

##### 手順 4:.env ファイルの作成

1. プロジェクトのルートレベルに.env ファイルを作成します
2. 次の設定を追加し、プレースホルダーを ADC プロジェクトの OAuth サーバー間資格情報の実際の値に置き換えます。

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![&#x200B; 環境ファイルを作成 &#x200B;](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > `CLIENT_ID`、`CLIENT_SECRET` および `SCOPES` をAdobe Developer Console プロジェクトからコピーできます。

##### 手順 5:src/index.jsを作成

1. プロジェク `index.js` のルートレベルにファイルを作成します
2. 次のコードを追加し、プレースホルダーを実際の値に置き換えます。

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![index.js を作成 &#x200B;](/help/forms/assets/api-6.png)

##### 手順 6：アプリケーションの実行

```bash
node src/index.js
```

![&#x200B; アプリケーションの実行 &#x200B;](/help/forms/assets/api-7.png)

`demo-nodejs-generate-pdf` フォルダーにPDFが作成されます。 フォルダーに移動して、`generatedForm.pdf` という名前の生成されたファイルを見つけます。

![&#x200B; 作成された pdf を表示 &#x200B;](/help/forms/assets/api-8.png)

[&#x200B; 生成されたPDF](/help/forms/assets/create-pdf.png) を開いて確認できます。

## トラブルシューティング

### 一般的な問題と考えられる原因

#### 問題 1:403 Forbidden エラー

**症状：**

- API リクエストの戻り `403 Forbidden`
- エラーメッセージ：*アクセスが拒否されました* または *権限が不十分です*
- 有効なアクセストークンでも発生

**考えられる原因：**

- OAuth サーバー間資格情報にリンクされた製品プロファイルの権限が不十分です
- AEM オーサーのサービスユーザーグループに、必要なコンテンツパスに対する必要な権限がありません

#### 問題 2:401 Unauthorized エラー

**症状：**

- API リクエストの戻り `401 Unauthorized`
- エラーメッセージ：*トークンが無効または期限切れです*

**考えられる原因：**

- アクセストークンが期限切れです（24 時間のみ有効）
- クライアント ID とクライアント秘密鍵が正しくないか、一致しません
- API リクエストに認証ヘッダーがないか、形式が正しくありません

#### 問題 3:404 エラーが見つからない

**症状：**

- API リクエストの戻り `404 Not Found`
- エラーメッセージ：*リソースが見つかりません* または *API エンドポイントが見つかりません*

**考えられる原因：**

- クライアント ID がAEM インスタンスの `api.yaml` 設定に登録されていません
- バケットパラメーターが正しくありません（AEM インスタンスの識別子と一致しません）
- リソース ID （フォームまたはアセット）が無効または存在しません

#### 問題 4：サーバー間認証オプションを使用できない

**症状：**

- Adobe Developer Consoleで OAuth サーバー間オプションが見つからないか無効になっている

**考えられる原因：**

- 統合を作成するユーザーは、関連する製品プロファイルに **開発者** として追加されません

#### 問題 5：パイプラインのデプロイメントに失敗する

**症状：**

- 設定パイプラインの実行に失敗
- デプロイメントログに、`api.yaml` に関連するエラーが表示される

**考えられる原因：**

- YAML 構文（インデント、引用符、または配列形式の問題）が無効です
- `api.yaml` が間違ったディレクトリに配置されています
- 設定のクライアント ID の形式が正しくないか、正しくありません


## 関連記事

バッチ（非同期 API）用の環境を設定する方法については、[AEM Forms as a Cloud Serviceとのバッチ処理 &#x200B;](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) を参照してください。
