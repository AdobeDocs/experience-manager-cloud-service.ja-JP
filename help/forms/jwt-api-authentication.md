---
title: JWT （JSON web トークン）認証の設定方法
description: Adobe Experience Manager Forms as a Cloud Serviceの JWT （JSON web トークン）認証を設定する方法について説明します
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: a9ef6553a7f480895f53f1240cd454c6f4fc7d24
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---


# JWT （JSON Web トークン）認証 – 非推奨

AEM Formsの JWT 認証、特にAEM as a Cloud Serviceのサーバーサイド統合の場合、AEM サービスと安全にやり取りするための特定のプロセスが必要になります。

## 考慮事項

JWT で生成されるアクセストークンは、現在の証明書の有効期限が切れた後か 2026 年 3 月 1 日（PT）のいずれか早い方が有効になりません。 したがって、新しい [OAuth サーバー間資格情報 ](/help/forms/oauth-api-authetication.md) を使用するには、統合を移行する必要があります。

プロジェクトを OAuth サーバー間資格情報に移行する手順は簡単で、アプリケーションと統合をダウンタイムなしで移行できます。 OAuth サーバー間資格情報に移行する場合は、[ 移行ガイド ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration) を参照してください。


## 前提条件

開始する前に、次の前提条件が満たされていることを確認してください。

* 使用する環境に固有の [Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html) へのアクセス権があることを確認します。
* Adobe Cloud Managerにアクセスするには、システム管理者または開発者の役割を割り当てます。

## JWT 資格情報を使用してアクセストークンを生成する方法

JWT 資格情報からアクセストークンを生成する方法を示す次の手順に従います。

1. **Adobe Cloud Manager**

   1. [Cloud Manager アカウント ](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html) にログインします。
   2. 選択したプログラムで、「**[!UICONTROL プログラムの概要]**」をクリックします。

      ![Cloud Manager アカウント ](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. プログラムで、3 ドットメニューをクリックし、「**[!UICONTROL Developer Console]**」を選択します。

      ![デベロッパーコンソール](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. AEM Developer Consoleにログインします。
   2. 上部メニューバーの「**[!UICONTROL 統合]**」をクリックします。

      ![統合](/help/forms/assets/jwt-integrations.png)

   3. オプションをクリックして **[!UICONTROL 新しいテクニカルアカウントを作成]** します。

      ![ 新しいテクニカルアカウントの作成 ](/help/forms/assets/jwt-creae-new-tech-account.png)

   「新しいテクニカルアカウントを作成」をクリックすると、アクセストークン（クライアント ID、クライアント秘密鍵など）および他のテクニカルアカウント情報（秘密鍵、公開鍵、有効期限が生成される）を生成するために必要な情報が表示されます。

   ![JWT 資格情報 ](/help/forms/assets/jwt-credentials.png)


3. 資格情報の生成と保存

   1. レコード API 資格情報

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. アクセストークンの生成

   cURL コマンドを使用してプログラムでトークンを生成します。

   **必要な資格情報：**

   * クライアント ID
   * クライアントの秘密鍵
   * 範囲（通常：`openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`）

   **トークン エンドポイント：**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **リクエストの例（cURL）:**

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


>[!NOTE]
>
> サービス資格情報と、Adobe IMSAPI を使用してアクセストークンを生成する方法について詳しくは、[ ここをクリック ](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials) を参照してください。

生成されたアクセストークンを使用して、開発、ステージ、実稼動環境の API 呼び出しを行えるようになりました。

## 次の手順

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


