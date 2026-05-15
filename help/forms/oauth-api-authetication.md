---
title: OAuth サーバー間認証の設定方法
description: Adobe Experience Manager Forms as a Cloud ServiceのOAuth サーバー間認証を設定する方法について説明します
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 24fa5751-c006-4c39-bdc3-b46a4974638e
hide: true
hidefromToC: true
index: false
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 11%

---

# OAuth サーバー間認証

OAuth Server-to-Server Authenticationにより、ユーザーの操作を必要とせずに、AEM Forms Communications APIへのトークンベースの安全なアクセスが可能になります。 OAuth サーバー間認証は、Adobe Developer Consoleでサポートされています。

## 前提条件

開始する前に、次の前提条件が満たされていることを確認してください。

* 使用している環境に固有の[Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/access-rights)へのアクセス権があることを確認してください。
* [Adobe Developer Consoleへのアクセスを有効にするには、Adobe Admin Console](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions)でシステム管理者または開発者の役割を割り当てます。

## OAuth サーバー間認証を使用してアクセストークンを生成する方法を教えてください。

次の手順に従って、Adobe Developer コンソールからアクセストークンを生成し、OAuth Server-to-Server Authenticationを介して最初のAPI呼び出しを行います。

### &#x200B;1. Adobe Developer Console プロジェクト設定

1. [Adobe Developer Console](https://developer.adobe.com/console)に移動します
2. Adobe IDでログイン

3. 新規プロジェクトを作成するか、既存のプロジェクトに移動します

>[!BEGINTABS]

>[!TAB 新しいプロジェクトを作成するには]

1. **クイックスタート** セクションで、**新規プロジェクトの作成**&#x200B;をクリックします
2. 新しいプロジェクトがデフォルト名で作成されます

   ![ADC プロジェクトの作成](/help/forms/assets/adc-home.png)

3. 右上隅の「**プロジェクトを編集**」をクリックします

   ![ プロジェクトを編集](/help/forms/assets/adc-edit-project.png)

4. 意味のある名前を指定します（例：「formsproject」）。
5. 「**保存**」をクリックします。

   ![ プロジェクト名を編集](/help/forms/assets/adc-edit-projectname.png)

>[!TAB 既存のプロジェクトに移動するには]

1. Adobe Developer Consoleから&#x200B;**すべてのプロジェクト**&#x200B;をクリックします

   ![ プロジェクトを検索](/help/forms/assets/search-adc-project.png)

2. プロジェクトを見つけて、クリックして開きます。

   ![ プロジェクトの検索](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

### &#x200B;2. Forms APIの追加

次の操作に基づいてForms APIを追加します。

* **AEM Forms Communications API**：ドキュメント（PDFおよび関連する形式）の生成、変換、組み立て、またはセキュリティ保護が必要な場合に使用します。
* **アダプティブ Forms ランタイム API** – 実行時にアダプティブ Formsをレンダリング、送信、処理する必要がある場合に使用します。

>[!BEGINTABS]

>[!TAB AEM Forms Communications API]の場合

1. 「**APIを追加**」をクリックします

   ![Apiを追加](/help/forms/assets/adc-add-api.png)

2. **Forms Communication API**&#x200B;を選択
   1. _Add API_ ダイアログで、**Experience Cloud**&#x200B;でフィルタリングします
   2. **「Forms Communication API」を選択**

      ![Forms Communication APIを追加](/help/forms/assets/adc-add-forms-api.png)

   3. 「**次へ**」をクリックします。
   4. **OAuth サーバー間**&#x200B;認証方法を選択

      ![認証方法を選択](/help/forms/assets/adc-add-authentication-method.png)

>アダプティブ Forms ランタイム API]の[!TAB 

1. **「APIを追加」をクリック**

   ![Apiを追加](/help/forms/assets/adc-add-api.png)

2. **AEM Forms Delivery and Runtime APIを選択**
   1. _Add API_ ダイアログで、**Experience Cloud**&#x200B;でフィルタリングします
   2. **「AEM Forms Delivery and Runtime API」を選択**
      ![Forms Communication APIを追加](/help/forms/assets/adc-add-runtime-api.png)

   3. 「**次へ**」をクリックします。
   4. **OAuth サーバー間**認証方式を選択します。
      ![認証方法を選択](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

既存のプロジェクトにAPIと認証方法を追加するには、**プロジェクトに追加** > **API**&#x200B;をクリックします\
![既存のプロジェクトにAPIを追加](/help/forms/assets/add-api-existing-project.png)

### &#x200B;3. 製品プロファイルを追加

製品プロファイルは、AEM リソースにアクセスするための資格情報に対する権限（または権限）を提供します。

1. AEM インスタンス URL （`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`）に一致する&#x200B;**製品プロファイル**&#x200B;を選択します。

   * **サービスタイプ** - AEM インスタンスに関連付けられているサービスまたは権限を指定します

   * **環境タイプ** – 環境がオーサーサービスとパブリッシュサービスのどちらであるかを指定します

   * **プログラム XXX** - Cloud Manager プログラム IDを識別します

   * **環境XXX** – そのプログラム内の特定の環境IDを識別します

   >[!NOTE]
   >
   > 製品プロファイルは、特定のAEM インスタンス（プログラムと環境）に関連付けられます。 インスタンス URLに一致するプロファイルを必ず選択してください。

2. 「**設定済み API を保存**」をクリックします。 APIと製品プロファイルがプロジェクトに追加されます

   ![ プロジェクト設定を選択](/help/forms/assets/adc-add-product-profile.png)

### &#x200B;4. 資格情報の生成と保存

1. Adobe Developer Consoleでプロジェクトに移動します
2. **OAuth サーバー間**&#x200B;資格情報をクリックします
3. **資格情報の詳細** セクションを表示

   ![資格情報の表示](/help/forms/assets/adc-view-credential.png)

**レコード API資格情報**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

### &#x200B;5. アクセストークン生成

アクセストークンを手動またはプログラムで生成します。

>[!BEGINTABS]

>[!TAB  テスト用]

Adobe Developer Consoleでアクセストークンを手動で生成する：

1. **プロジェクトに移動**
   1. Adobe Developer Consoleで、プロジェクトを開きます
   2. **OAuth サーバー間**&#x200B;をクリックします

2. **アクセストークンを生成**
   1. プロジェクトのAPI セクションで「**&quot;アクセストークンを生成&quot;**」ボタンをクリックします
   2. 生成されたアクセストークンをコピー

   ![ アクセストークンを生成](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > アクセストークンは&#x200B;**24時間**&#x200B;のみ有効です

>[!TAB 実稼動用]

[Adobe IMS](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) APIを使用してプログラムでトークンを生成します：

**必要な資格情報：**

* クライアント ID
* クライアントの秘密鍵
* スコープ （通常：`openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

**トークンエンドポイント：**

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

>[!ENDTABS]

生成されたアクセストークンを使用して、開発環境、ステージ環境または実稼動環境のAPI呼び出しを行えるようになりました。

## ベストプラクティス：開発、ステージング、実稼動用の資格情報の管理

* 開発、ステージング、実稼動では、常に別々の資格情報を使用します。

* 各資格情報を正しいAEM環境URLにマッピングします。

* 秘密鍵を安全に保管し、それらをソース管理に委ねないでください。

* トークンは24時間のみ有効なので、アクセストークンの有効性を追跡します。

## 次の手順

同期Forms Communication APIの環境を設定する方法については、[AEM Forms as a Cloud Service Communications同期処理](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)を参照してください。


## 関連記事

同期（オンデマンド）および非同期（バッチ）Forms Communications APIの環境を設定する方法について説明します。

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同期API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同期API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API – 同期">AEM Forms Communications API – 同期</a>
                    </p>
                    <p class="is-size-6">ドキュメントを即座に生成または処理する同期（オンデマンド）Forms Communications APIの環境を設定する方法について説明します。 </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API – 非同期" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="非同期API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="非同期API">AEM Forms Communications API – 非同期（バッチ） </a>
                    </p>
                    <p class="is-size-6">複数のドキュメントをスケジュールされた方法で生成または処理する非同期（バッチ）Forms Communications APIの環境を設定する方法について説明します。</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">詳細情報</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service の概要](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [アダプティブフォームおよび通信 API 用のAEM Forms as a Cloud Service アーキテクチャ](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信処理 - 同期 API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信処理 - バッチ API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Forms Communications API - チュートリアル ](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
