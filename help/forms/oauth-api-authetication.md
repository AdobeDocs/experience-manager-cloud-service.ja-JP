---
title: OAuth サーバー間認証の設定方法
description: Adobe Experience Manager Forms as a Cloud Service用に OAuth サーバー間認証を設定する方法を説明します
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: fcc25eb44b485db69ec1c267f4cf8774c4279b24
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# OAuth サーバー間認証 – 推奨

OAuth サーバー間認証を使用すると、ユーザーの操作を必要とせずに、AEM Forms Communications API への安全なトークンベースのアクセスが可能になります。 この方法は、プログラムによる認証が必要な自動システム、バックエンドサービス、統合に最適です。

## 前提条件

開始する前に、次の前提条件が満たされていることを確認してください。

* 使用する環境に固有の [0}Adobe Developer Console} にアクセスできることを確認します。](https://developer.adobe.com/console)
* Adobe Admin Consoleでシステム管理者または開発者の役割を割り当てて、Adobe Developer Consoleへのアクセスを有効にします。

## OAuth サーバー間認証を使用してアクセストークンを生成する方法

以下の手順に従って、Adobe Developer コンソールからアクセストークンを生成し、OAuth サーバー間認証を使用して最初の API 呼び出しを行う方法を示します。


1. [Adobe Developer Console](https://developer.adobe.com/console) に移動します
2. Adobe IDでログイン

3. 新しいプロジェクトを作成するか、既存のプロジェクトに移動します

   **新しいプロジェクトを作成するには：**

   1. 「**クイックスタート**」セクションで、「**新規プロジェクトを作成**」をクリックします
   2. デフォルト名で新しいプロジェクトが作成されます

      ![ADC プロジェクトの作成 ](/help/forms/assets/adc-home.png)

   3. 右上隅の **プロジェクトを編集** をクリックします

      ![ プロジェクトを編集 ](/help/forms/assets/adc-edit-project.png)

   4. 意味のある名前を指定（例：「formsproject」）
   5. 「**保存**」をクリックします。

      ![ プロジェクト名を編集 ](/help/forms/assets/adc-edit-projectname.png)


   **既存のプロジェクトに移動するには、次の手順に従います。**

   1. Adobe Developer Consoleで **すべてのプロジェクト** をクリックします

      ![ プロジェクトの検索 ](/help/forms/assets/search-adc-project.png)

   2. プロジェクトを見つけて、クリックして開きます。

      ![ プロジェクトの検索 ](/help/forms/assets/locate-adc-project.png)


      >[!NOTE]
      >
      > **プロジェクトに追加**/**API** をクリックして、API と認証方法を既存のプロジェクトに追加できます\
      > ![ 既存のプロジェクトへの API の追加 ](/help/forms/assets/add-api-existing-project.png)
      > API と認証方法を追加するには、既存のプロジェクトに対して、以下に説明するのと同じ手順を実行します。

4. 要件に応じて、様々なAEM Forms通信 API を追加します。

   **A.ドキュメントサービス API の場合**

   1. 「**API を追加**」をクリックします。

      ![API を追加 ](/help/forms/assets/adc-add-api.png)

   2. **Forms Communication API** を選択
      1. _API を追加_ ダイアログで、**Experience Cloudでフィルタリングします**
      2. 「Forms Communication API **を選択し** す。

         ![Forms Communication API の追加 ](/help/forms/assets/adc-add-forms-api.png)


   3. **OAuth サーバー間** 認証方法を選択します

      ![ 認証方法の選択 ](/help/forms/assets/adc-add-authentication-method.png)


   **B.アダプティブ Forms ランタイム API**

   1. **「API を追加」をクリック**
プロジェクトで「**API を追加**」ボタンをクリックします

      ![API を追加 ](/help/forms/assets/adc-add-api.png)

   2. **AEM Forms配信およびランタイム API を選択**
      1. _API を追加_ ダイアログで、**Experience Cloudでフィルタリングします**
      2. **AEM Forms配信およびランタイム API」を選択** ます。
      3. 「**次へ**」をクリックします。

   3. **認証方法**
**OAuth サーバー間** 認証方法を選択します。


      ![ 認証方法の選択 ](/help/forms/assets/adc-add-authentication-method.png)

5. **製品プロファイルを追加**:

   1. 必要なアクセスレベルに基づいて適切な **製品プロファイル** を選択します。

      | アクセスタイプ | 製品プロファイル |
      |------------------|----------------------|
      | 読み取り専用アクセス | `AEM Users - author - Program XXX - Environment XXX` |
      | 読み取り/書き込みアクセス | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
      | 完全な管理アクセス | `AEM Administrators - author - Program XXX - Environment XXX` |

   2. オーサーサービス URL （**）に一致する** 製品プロファイル `https://author-pXXXXX-eYYYYY.adobeaemcloud.com` を選択します。 例：select `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`。

   3. 「**設定済み API を保存**」をクリックします。API と製品プロファイルがプロジェクトに追加されます

      ![ プロジェクト設定の選択 ](/help/forms/assets/adc-add-product-profile.png)

6. 資格情報の生成と保存

   1. Adobe Developer Consoleでプロジェクトに移動します
   2. **OAuth サーバー間** 資格情報をクリックします。
   3. 「**資格情報の詳細** セクションを表示します

      ![資格情報の表示](/help/forms/assets/adc-view-credential.png)

   4. レコード API 資格情報

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

7. アクセストークンの生成

   **A.テスト用**

   Adobe Developer Consoleで手動でアクセストークンを生成します。

   1. **プロジェクトへの移動**
      1. Adobe Developer Consoleで、プロジェクトを開きます
      2. **OAuth サーバー間** をクリックします。

   2. **アクセストークンの生成**
      1. プロジェクトの「API」セクションで **「アクセストークンを生成」** ボタンをクリックします
      2. 生成されたアクセストークンのコピー

      ![ アクセストークンの生成 ](/help/forms/assets/adc-access-token.png)

      >[!NOTE]
      >
      > アクセストークンは **24 時間** のみ有効です

   **B.実稼動の場合**

   Adobe IMSAPI を使用してプログラムでトークンを生成します。

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

生成されたアクセストークンを使用して、開発、ステージ、実稼動環境の API 呼び出しを行えるようになりました。

>[!NOTE]
>
> アクセストークンを生成して API 呼び出しをおこなう OAuth サーバー間実装について詳しくは、[ ここをクリック ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) を参照してください。

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


