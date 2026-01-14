---
title: OAuth サーバー間認証の設定方法
description: Adobe Experience Manager Forms as a Cloud Service用に OAuth サーバー間認証を設定する方法を説明します
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 7%

---


# OAuth サーバー間認証

OAuth サーバー間認証を使用すると、ユーザーの操作を必要とせずに、AEM Forms Communications API への安全なトークンベースのアクセスが可能になります。 Adobe Developer Consoleでは、OAuth サーバー間認証がサポートされています。

## 前提条件

開始する前に、次の前提条件が満たされていることを確認してください。

* 使用する環境に固有の [Adobe Developer Consoleへのアクセス &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/access-rights) があることを確認します。
* [Adobe Admin Consoleでシステム管理者または開発者の役割を割り当て &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions)Adobe Developer Consoleへのアクセスを有効にします。

## OAuth サーバー間認証を使用してアクセストークンを生成する方法

次の手順に従って、Adobe Developer コンソールからアクセストークンを生成し、OAuth サーバー間認証を使用して最初の API 呼び出しを行います。

### &#x200B;1. Adobe Developer Console プロジェクトのセットアップ

1. [Adobe Developer Console](https://developer.adobe.com/console) に移動します
2. Adobe IDでログイン

3. 新しいプロジェクトを作成するか、既存のプロジェクトに移動します

>[!BEGINTABS]

>[!TAB  新しいプロジェクトを作成するには ]

1. 「**クイックスタート**」セクションで、「**新規プロジェクトを作成**」をクリックします
2. デフォルト名で新しいプロジェクトが作成されます

   ![ADC プロジェクトの作成 &#x200B;](/help/forms/assets/adc-home.png)

3. 右上隅の **プロジェクトを編集** をクリックします

   ![&#x200B; プロジェクトを編集 &#x200B;](/help/forms/assets/adc-edit-project.png)

4. 意味のある名前を指定（例：「formsproject」）
5. 「**保存**」をクリックします。

   ![&#x200B; プロジェクト名を編集 &#x200B;](/help/forms/assets/adc-edit-projectname.png)

>[!TAB  既存のプロジェクトに移動するには ]

1. Adobe Developer Consoleで **すべてのプロジェクト** をクリックします

   ![&#x200B; プロジェクトの検索 &#x200B;](/help/forms/assets/search-adc-project.png)

2. プロジェクトを見つけて、クリックして開きます。

   ![&#x200B; プロジェクトの検索 &#x200B;](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

### &#x200B;2. Forms API を追加する

実行したい内容に基づいてForms API を追加します。

* **AEM Forms Communications API**: ドキュメント（PDFおよび関連するフォーマット）を生成、変換、アセンブリ、または保護する必要がある場合に使用します。
* **アダプティブFormsランタイム API** – 実行時にアダプティブFormsをレンダリング、送信または処理する必要がある場合に使用します。

>[!BEGINTABS]

>[!TAB AEM Forms Communications API の場合 ]

1. 「**API を追加**」をクリックします。

   ![API を追加 &#x200B;](/help/forms/assets/adc-add-api.png)

2. **Forms Communication API** を選択
   1. _API を追加_ ダイアログで、**Experience Cloudでフィルタリングします**
   2. 「Forms Communication API **を選択し** す。

      ![Forms Communication API の追加 &#x200B;](/help/forms/assets/adc-add-forms-api.png)

   3. 「**次へ**」をクリックします。
   4. **OAuth サーバー間** 認証方法を選択します

      ![&#x200B; 認証方法の選択 &#x200B;](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB  アダプティブ Forms ランタイム API の場合 ]

1. **「API を追加」をクリック**

   ![API を追加 &#x200B;](/help/forms/assets/adc-add-api.png)

2. **AEM Forms配信およびランタイム API を選択**
   1. _API を追加_ ダイアログで、**Experience Cloudでフィルタリングします**
   2. **AEM Forms配信およびランタイム API」を選択** ます。
      ![Forms Communication API の追加 &#x200B;](/help/forms/assets/adc-add-runtime-api.png)

   3. 「**次へ**」をクリックします。
   4. **OAuth サーバー間**&#x200B;認証方式を選択します。
      ![&#x200B; 認証方法の選択 &#x200B;](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

また、**プロジェクトに追加**/**API** をクリックして、既存のプロジェクトに API と認証方法を追加することもできます\
![&#x200B; 既存のプロジェクトへの API の追加 &#x200B;](/help/forms/assets/add-api-existing-project.png)

### 3.製品プロファイルの追加

製品プロファイルは、AEM リソースにアクセスするための資格情報に対する権限（または認証）を提供します。

1. お使いのAEM インスタンス URL （**）に一致する** 製品プロファイル `https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com` を選択します。

   * **サービスタイプ** - AEM インスタンスに関連付けられたサービスまたは権限を指定します。

   * **環境タイプ** – 環境がオーサーサービス用かパブリッシュサービス用かを指定します

   * **プログラム XXX** - Cloud Manager プログラム ID を識別します。

   * **環境 XXX** - プログラム内の特定の環境 ID を識別します。

   >[!NOTE]
   >
   > 製品プロファイルは、特定のAEM インスタンス（プログラム +環境）に関連付けられています。 インスタンスの URL に一致するプロファイルを常に選択します。

2. 「**設定済み API を保存**」をクリックします。API と製品プロファイルがプロジェクトに追加されます

   ![&#x200B; プロジェクト設定の選択 &#x200B;](/help/forms/assets/adc-add-product-profile.png)

### 4.認証情報の生成と保存

1. Adobe Developer Consoleでプロジェクトに移動します
2. **OAuth サーバー間** 資格情報をクリックします
3. 「**資格情報の詳細** セクションを表示します

   ![資格情報の表示](/help/forms/assets/adc-view-credential.png)

**レコード API 資格情報**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

### &#x200B;5. アクセストークンの生成

アクセストークンを手動またはプログラムで生成します。

>[!BEGINTABS]

>[!TAB  テスト用 ]

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
   > アクセストークンは **24 時間** のみ有効です

>[!TAB  実稼動用 ]

[Adobe IMS](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) API を使用してプログラムでトークンを生成します：

**必要な資格情報：**

* クライアント ID
* クライアントの秘密鍵
* 範囲（通常：`openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

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

>[!ENDTABS]

生成されたアクセストークンを使用して、開発、ステージ、実稼動環境の API 呼び出しを行えるようになりました。

## ベストプラクティス：開発、ステージングおよび実稼動用の認証情報の管理

* 開発、ステージングおよび実稼動用に、常に別々の資格情報を使用します。

* 正しいAEM環境 URL に各資格情報をマッピングします。

* 秘密鍵は安全に保存し、ソース管理にコミットしないでください。

* トークンは 24 時間のみ有効なので、アクセストークンの有効性を追跡します。

## 次の手順

同期Forms通信 API 用に環境を設定する方法については、[AEM Forms as a Cloud Service通信同期処理 &#x200B;](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md) を参照してください。


## 関連記事

同期（オンデマンド）および非同期（バッチ）Forms通信 API の環境を設定する方法について説明します。

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同期 API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同期 API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms通信 API – 同期">AEM Forms通信 API – 同期 </a>
                    </p>
                    <p class="is-size-6">ドキュメントを即座に生成または処理する、同期（オンデマンド）Forms Communications API の環境を設定する方法を説明します。 </p>
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
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms通信 API – 非同期" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="非同期 API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="非同期 API">AEM Forms通信 API – 非同期（バッチ） </a>
                    </p>
                    <p class="is-size-6">複数のドキュメントをスケジュールに従って生成または処理する、非同期（バッチ）Forms通信 API の環境を設定する方法について説明します。</p>
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
>* [Forms Communications API - チュートリアル &#x200B;](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
