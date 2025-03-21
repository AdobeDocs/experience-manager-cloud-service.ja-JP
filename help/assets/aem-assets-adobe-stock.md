---
title: ' [!DNL Assets] での [!DNL Adobe Stock] アセットの管理。'
description: ' [!DNL Adobe Experience Manager] 内から [!DNL Adobe Stock] アセットを、検索、取得、ライセンス、管理します。ライセンスされたアセットをその他のデジタルアセットとして使用します。'
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 98%

---

# [!DNL Adobe Experience Manager Assets] での [!DNL Adobe Stock] アセットの使用 {#use-adobe-stock-assets-in-aem-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=ja) |
| AEM as a Cloud Service | この記事 |

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。

[!DNL Adobe Stock] エンタープライズ版の場合は、デフォルトで、組織全体での共有権限が含まれます。組織のユーザーがアセットのライセンスを取得すると、組織の他のユーザーがこのアセットを識別、ダウンロード、使用できるようになります。再度ライセンスを取得する必要はありません。組織でアセットのライセンスを取得すると、そのアセットの使用権限が永続的に有効になります。

[!DNL Adobe Stock] エンタープライズ版プランと [!DNL Experience Manager Assets] を統合すると、[!DNL Experience Manager] の強力なアセット管理機能を使用して、ライセンスを取得したアセットをクリエイティブプロジェクトやマーケティングプロジェクトに幅広く活用できます。[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] に保存されている Adobe Stock アセットの検索、プレビューおよびライセンス取得を、[!DNL Experience Manager] インターフェイスから画面を切り替えることなく、すばやく実行できます。

## [!DNL Experience Manager] と [!DNL Adobe Stock] の統合  {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] を使用すると、ユーザーは [!DNL Experience Manager] から直接、[!DNL Adobe Stock] アセットの検索、プレビュー、保存、ライセンス取得を実行できます。

**前提条件**

統合には次の要件が必要です。

* 実行中の [!DNL Experience Manager Assets] as a [!DNL Cloud Service] インスタンス
* [エンタープライズ [!DNL Adobe Stock] プラン](https://stockenterprise.adobe.com/jp/)
* Admin Console でデフォルトの Stock 製品プロファイルにアクセスする権限を持つユーザー
* Adobe Developer Console で統合を作成するための開発者アクセスプロファイルに対する権限を持つユーザー

[!DNL Adobe Stock] エンタープライズ版プラン

* [!DNL Adobe Stock]（Experience Manager と統合された Stock）製品を使用するための権利付与
* Stock の権利付与のために [!DNL Adobe Admin Console] で購入したクレジット
* Stock の権利付与のために [!DNL Adobe Developer Console] 内でのサービスアカウント（JWT）認証を有効にする
* [!DNL Adobe Admin Console] 内からのクレジットとライセンスのグローバルな管理を有効にする

権利付与において、[!DNL Adobe Stock] のデフォルトの製品プロファイルは [!DNL Admin Console] に存在します。複数のプロファイルを作成でき、これらのプロファイルによって、誰が Stock アセットのライセンスを取得できるかが決まります。製品プロファイルに直接アクセスできるユーザーは、[https://stock.adobe.com/jp](https://stock.adobe.com/jp/) にアクセスして、Stock アセットのライセンスを取得できます。一方、Developer Access を使用して統合（API）を作成する方法もあります。この統合により、[!DNL Experience Manager Assets] と [!DNL Adobe Stock] 間の通信が認証されます。

>[!NOTE]
>
>Stock サービスアカウント（JWT）認証には、エンタープライズ Stock 使用権が付属しています。
>
>この統合では、Stock エンタープライズ版の権利付与のための OAuth 認証をサポートしていません。


<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->
<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->

## [!DNL Experience Manager] と [!DNL Adobe Stock] を統合する手順 {#integration-steps}

[!DNL Experience Manager] と [!DNL Adobe Stock] を統合するには、リストに示された順序で次の手順を実行します。

1. [公開証明書の取得](#public-certificate)

   [!DNL Experience Manager] で IMS アカウントを作成し、公開証明書（公開鍵）を生成します。

1. [サービスアカウント（JWT）接続の作成](#createnewintegration)

   [!DNL Adobe Developer Console] で、[!DNL Adobe Stock] 組織のプロジェクトを作成します。そのプロジェクトで、公開鍵を使用して API を設定し、サービスアカウント（JWT）接続を作成します。サービスアカウント資格情報と JWT ペイロード情報を取得します。

1. [IMS アカウントの設定](#create-ims-account-configuration)

   [!DNL Experience Manager] で、サービスアカウント資格情報と JWT ペイロードを使用して IMS アカウントを設定します。

1. [Cloud Service の設定](#configure-the-cloud-service)

   [!DNL Experience Manager] で、IMS アカウントを使用して [!DNL Adobe Stock] クラウドサービスを設定します。


### IMS 設定の作成 {#create-an-ims-configuration}

IMS 設定により [!DNL Experience Manager Assets] オーサーインスタンスが認証され、[!DNL Adobe Stock] が権利付与されます。

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、Adobe 開発者コンソールでプロファイルを認証します。

1. [!DNL Experience Manager Assets] クラウドインスタンスにログインします。

1. **[!UICONTROL ツール]**&#x200B;パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。「**[!UICONTROL Adobe IMS テクニカルアカウント設定]**」ページが表示されます。

1. 「**[!UICONTROL 証明書]**」タブで、**[!UICONTROL クラウドソリューション]**&#x200B;ドロップダウンリストから「**[!UICONTROL Adobe Stock]**」を選択します。

1. 証明書を作成するか、既存の証明書を設定に再利用できます。

   証明書を作成するには、「**[!UICONTROL 新しい証明書を作成]**」チェックボックスをオンにして、公開鍵の&#x200B;**エイリアス**&#x200B;を指定します。ここで入力したエイリアスが、公開鍵になります。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

1. **[!UICONTROL 公開鍵をダウンロード]**&#x200B;アイコンをクリックして、公開鍵（.crt）ファイルをローカルマシンに保存します。この公開鍵を後で使用して、Brand Portal テナントの API を設定し、Adobe 開発者コンソールでサービスアカウント資格情報を生成します。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. 「**アカウント**」タブで、サービスアカウント資格情報を必要とする Adobe IMS アカウントが作成されます。

   新しいタブを開き、[Adobe 開発者コンソールでのサービスアカウント (JWT) 接続を作成します](#createnewintegration)。

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobe 開発者コンソールで、プロジェクトと API を組織レベルで設定します。API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。この例では、サービスアカウント資格情報は公開鍵をアップロードすることで生成されます。

サービスアカウント資格情報と JWT ペイロードを生成するには、次の操作を実行します。

1. システム管理者権限で Adobe 開発者コンソールにログインします。デフォルトの URL は [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui) です。


   ドロップダウン（組織）リストで正しい IMS 組織（Stock 使用権限）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   **[!UICONTROL プロジェクトを編集]**&#x200B;をクリックします。**[!UICONTROL プロジェクトタイトル]**&#x200B;および&#x200B;**[!UICONTROL 説明]**&#x200B;を更新し、「**[!UICONTROL 保存]**」をクリックします。

1. 「**[!UICONTROL プロジェクトの概要]**」タブで、「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API ウィンドウを追加ウィンドウ]**&#x200B;で、「**[!UICONTROL Adobe Stock]**」を選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL API の設定]**&#x200B;ウィンドウで、「**[!UICONTROL サービスアカウント (JWT)]**」認証を選択します。「**[!UICONTROL 次へ]**」をクリックします。

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. 「**[!UICONTROL 公開鍵をアップロード]**」をクリックします。「**[!UICONTROL ファイルを選択]**」をクリックし、[公開証明書の取得](#public-certificate)節でダウンロードした公開鍵（.crt ファイル）をアップロードします。「**[!UICONTROL 次へ]**」をクリックします。

1. 公開鍵を確認し、「**[!UICONTROL 次へ]**」をクリックします。

1. デフォルトの **[!UICONTROL Adobe Stock]** 製品プロファイルを選択し、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

1. API が設定されると、API の概要ページにリダイレクトされます。左側のナビゲーションで「**[!UICONTROL 資格情報]**」の下の「**[!UICONTROL サービスアカウント（JWT）]**」オプションをクリックします。ここで資格情報を表示し、JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得などのアクションを実行できます。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. 「**[!UICONTROL JWT を生成]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;情報をコピーします。

[!DNL Experience Manager Assets] で [IMS アカウントを設定](#create-ims-account-configuration)をするためのクライアント ID（API キー）、クライアントの秘密鍵、JWT ペイロードを使用できるようになりました。

### IMS アカウントの設定 {#create-ims-account-configuration}

IMS アカウントを設定するには、[証明書](#public-certificate)と[サービスアカウント（JWT）資格情報](#createnewintegration)が必要です。

IMS アカウントを設定するには：

1. IMS 設定を開き、「**[!UICONTROL アカウント]**」タブに移動します。[公開証明書の取得](#public-certificate)中も、ページは開いたままになっています。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   「**[!UICONTROL 認証サーバー]**」フィールドに、URL を [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/) と入力します。

   [サービスアカウント（JWT）接続の作成](#createnewintegration)時にコピーしたクライアント ID を「**[!UICONTROL API キー]**」フィールド、**[!UICONTROL クライアントの秘密鍵]**&#x200B;および&#x200B;**[!UICONTROL ペイロード]**（JWT ペイロード）に入力します。

1. 「**[!UICONTROL 作成]**」をクリックします。IMS アカウントの設定が作成されます。

   ![configure-ims-acount](assets/aem-stock-ims-config.png)

1. その IMS アカウント設定を選択し、「**[!UICONTROL 正常性をチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![ヘルスチェック](assets/aem-stock-healthcheck.png)


### Cloud Service の設定 {#configure-the-cloud-service}

[!DNL Adobe Stock] Cloud Service を設定するには：

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／ **[!UICONTROL Cloud Services]** ／ **[!UICONTROL Adobe Stock]** に移動します。

1. [!DNL Adobe Stock Configurations] ページで、「**[!UICONTROL 作成]**」をクリックします。

1. クラウド設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力します。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   ドロップダウンリストからご自身のロケールを選択します。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   お使いの[!DNL Experience Manager Assets]オーサーインスタンスは、[!DNL Adobe Stock] に統合されています。複数の [!DNL Adobe Stock] 設定（例えばロケールベースの設定など）を作成できます。これで、[!DNL Experience Manager] ユーザーインターフェイスの中から [!DNL Adobe Stock] アセットにアクセス、検索およびライセンス付与ができます。

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >統合の現段階で、[!DNL Adobe Stock] アセットへのアクセス、Stock アセットの検索（オムニサーチによる）および[!DNL Adobe Stock] アセットへのライセンス付与が許可されるのは、管理者のみです。
   >
   >管理者は、[!DNL Adobe Stock] Cloud Service に別のユーザーまたはグループを追加したり、[!DNL Experience Manager] で管理者以外のユーザーに Stock 設定にアクセスする権限を付与できます。

1. ユーザーまたはグループを追加するには、[!DNL Adobe Stock]クラウド設定を選択し、「**[!UICONTROL プロパティ]**」をクリックします。

1. Adobe Stock 設定にアクセスする権限を割り当てられたユーザーまたはグループを検索して追加します。詳しくは、[ユーザーグループへの権限の割り当て](#assign-permissions-to-group)を参照してください。


## ユーザーグループへの権限の割り当て {#assign-permissions-to-group}

管理者は、ユーザーグループを作成し、特定のユーザーやグループに対して、[!DNL Adobe Stock] Cloud Service へのアクセス権を付与することができます。

ユーザーが Adobe Stock アセットを検索し、ライセンスを付与する場合は、次の権限が必要になります。

* 次のパスを設定します。 `/conf/global/settings/stock`
* 権限： `jcr:read`
* 権限タイプ: `Allow`

ユーザーグループを作成したり、既存のユーザーグループに権限を割り当てることができます。権限は、[!DNL Experience Manager Assets] インターフェイスまたは [!DNL User Admin] コンソールを使用して割り当てられます。

**[!DNL Experience Manager] からユーザーグループにアクセスを許可するには：**

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL グループ]**&#x200B;に移動します。[!DNL Adobe Stock] のユーザーグループを作成します。

1. **[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL 権限]**&#x200B;に移動します。

1. 左側のパネルでユーザーグループを検索し、Adobe Stock の新規の&#x200B;**[!UICONTROL アクセス制御エントリ（ACE）]**&#x200B;を追加します。

   * 次のパスを設定します。 `/conf/global/settings/stock`
   * 権限： `jcr:read`
   * 権限タイプ：`Allow`

   「**[!UICONTROL 追加]**」をクリックします。

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／ **[!UICONTROL Adobe Stock]** に移動します。[!DNL Adobe Stock] クラウド設定を選択し、「**[!UICONTROL プロパティ]**」をクリックします。

1. 作成したユーザーグループを [!DNL Adobe Stock] 設定に追加します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![assign-user](assets/aem-stock-adduser.png)

**[!DNL User Admin Console] からユーザーにアクセスを提供する：**

1. [!DNL Experience Manager] ユーザー Admin Console を開きます。デフォルトの URL は `http://localhost:4502/userdamin` です。

1. 左側のパネルで、`user_id` または `name` を入力して、ユーザーを検索します。ダブルクリックして、ユーザープロパティを開きます。

1. 「**[!UICONTROL 権限]**」タブに移動し、[!DNL Adobe Stock] クラウド設定の `read` 権限を許可します。`/conf/global/settings/stock`

   >[!CAUTION]
   >
   >クラウド設定が許可されていない場合、ユーザーは [!DNL Experience Manager] インターフェイスで **[!UICONTROL Assets]** のみアクセスできます。
   >
   >[!UICONTROL Assets] および [!DNL Adobe Stock] アセットへのアクセスを許可するには、クラウド設定がユーザーに許可されていることを確認します。

1. 「**[!UICONTROL 保存]**」をクリックして、権限を更新します。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. ユーザーまたはグループを [!DNL Adobe Stock] クラウド設定に追加します。


## Adobe Stock Assets へのアクセス {#access-stock-assets}

管理者以外のユーザーが [!DNL Adobe Stock] クラウド設定の権限がある場合、[!DNL Experience Manager] インターフェイスから [!DNL Adobe Stock] アセットの検索やライセンスの取得ができます。

ユーザーは、[!DNL Adobe Stock] アセットへのアクセス前に [!DNL Adobe Stock] クラウド設定をアクティベートする追加のステップを行う必要があります。これは 1 回限りのアクティビティです。ユーザーが複数の [!DNL Adobe Stock] クラウド設定に対する権限が割り当てられている場合、ユーザーは&#x200B;**[!UICONTROL ユーザーの環境設定]**&#x200B;から必要な設定を選択することができます。

[!DNL Adobe Stock] クラウド設定をアクティベートするには、次の操作を実行します。

1. [!DNL Experience Manager] にログインします。

1. 右上隅のユーザーアイコンをクリックし、「**[!UICONTROL 環境設定]**」をクリックします。**[!UICONTROL ユーザー管理]**&#x200B;ウィンドウが開きます。

1. ドロップダウンリストから目的の&#x200B;**[!UICONTROL 在庫設定]**&#x200B;を選択し、「**[!UICONTROL 承諾]**」をクリックして設定をアクティベートします。

   ![user-preferences](assets/aem-stock-preferences.png)

1. **[!UICONTROL Assets]** ／ **[!UICONTROL Adobe Stock]** に移動します。[!DNL Adobe Stock] アセットの表示、検索、ライセンスの取得が可能になりました。

次の表では、[!DNL Adobe Stock] アセットにアクセスする際のユーザー権限の仕組みについて説明します。

| ユーザー | グループ | 権限 | ユーザーの環境設定で Stock 設定を受け入れる | Assets にアクセス | Adobe Stock にアクセス |
| --- | --- | --- | --- | --- | --- |
| admin | 該当なし | すべて | 該当なし | はい | はい |
| test-doc1 | DAM ユーザー | /conf/global/settings/stock/cloud-config | はい | はい | はい |
| test-doc1 | DAM ユーザー | /conf/global/settings/stock/cloud-config | いいえ | エラー：データの読み込みに失敗しました | 不可 |
| test-doc1 | DAM ユーザー | **許可**：/conf/global/settings/stock **拒否**：/cloud-config | Stock 設定が表示されません | はい | いいえ |

## [!DNL Adobe Stock] での [!DNL Experience Manager] アセットの使用と管理  {#usemanage}

この機能を使用すると、[!DNL Experience Manager Assets] で [!DNL Adobe Stock] アセットを操作できます。[!DNL Experience Manager] のユーザーインターフェイス内から [!DNL Adobe Stock] アセットを検索し、必要なアセットのライセンスを取得できます。

[!DNL Experience Manager] 内で [!DNL Adobe Stock] アセットのライセンスを取得すると、そのアセットを通常のアセットと同様に使用および管理できます。ユーザーは [!DNL Experience Manager] 内でアセットの検索およびプレビュー、アセットのコピーおよび公開、[!DNL Brand Portal] でのアセットの共有、[!DNL Experience Manager] デスクトップアプリケーション経由でのアセットのアクセスおよび使用を行うことができます。

![[!DNL Adobe Experience Manager] Workspace から [!DNL Adobe Stock] アセットを検索して結果を絞り込む](assets/adobe-stock-search-results-workspace.png)

**A.** [!DNL Adobe Stock] ID が指定されているアセットと類似しているアセットを検索します。**B.** 選択した形状や向きと一致するアセットを検索します。**C.** サポートされているアセットタイプのいずれかを検索します。**D.** フィルターウィンドウを開く／折りたたみます。**E.** 選択したアセットのライセンスを取得して [!DNL Experience Manager] に保存します。**F.** アセットを透かし付きで [!DNL Experience Manager] に保存します。**G.** 選択したアセットと類似したアセットを [!DNL Adobe Stock] の web サイトで調べます。**H.** 選択したアセットを [!DNL Adobe Stock] の web サイトに表示します。**I.** 検索結果から選択したアセットの数。**J.** カード表示とリスト表示を切り替えます。

### アセットの検索 {#find-assets}

[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] と [!DNL Adobe Stock] の両方でアセットを検索できます。検索場所を [!DNL Adobe Stock] に限定しない場合は、[!DNL Experience Manager] と [!DNL Adobe Stock] からの検索結果が表示されます。

* [!DNL Adobe Stock] アセットを検索するには、**[!UICONTROL ナビゲーション]**／**[!UICONTROL アセット]**／**[!UICONTROL Adobe Stock を検索]**&#x200B;をクリックします。

* [!DNL Adobe Stock] と [!DNL Experience Manager Assets] にまたがるアセットを検索するには、「![検索](assets/do-not-localize/search_icon.png)」をクリックします。

また、アセットを選択するには、検索バーに「`Location: Adobe Stock`」と入力します。[!DNL Adobe Stock][!DNL Experience Manager] は、検索されたアセットに対する高度なフィルタリング機能を備えており、サポートされているアセットのタイプや画像の向き、ライセンスの状態などのフィルターを使用して、必要なアセットをすばやく見つけることができます。

>[!NOTE]
>
>[!DNL Adobe Stock] から検索されたアセットは [!DNL Experience Manager] に表示されます。[アセットを保存](/help/assets/aem-assets-adobe-stock.md#saveassets)するか、[アセットにライセンスを付与して保存](/help/assets/aem-assets-adobe-stock.md#licenseassets)した後でないと、[!DNL Adobe Stock] アセットを取得して [!DNL Experience Manager] リポジトリーに保存することはできません。既に [!DNL Experience Manager] に保存されているアセットが表示され、参照やアクセスが簡単にできるようにハイライトされます。また、[!DNL Stock] アセットは、ソースが [!DNL Stock] であることを示すいくつかの追加メタデータとともに保存されます。

![[!DNL Experience Manager] の検索フィルターと、検索結果内でハイライトされている [!DNL Adobe Stock] アセット](assets/aem-search-filters2.jpg)

### 必要なアセットの保存と表示 {#saveassets}

[!DNL Experience Manager] に保存するアセットを選択します。上部ツールバーの「[!UICONTROL 保存]」をクリックし、アセットの名前と保存場所を指定します。ライセンスが不要なアセットはローカルに透かし付きで保存されます。

アセットの検索を次回実行すると、保存済みのアセットは、[!DNL Experience Manager Assets] で使用可能であることを示すバッジ付きでハイライトされます。

>[!NOTE]
>
>最近追加されたアセットには、ライセンスが許諾されていることを示すバッジではなく、新しいアセットであることを示すバッジが表示されます。

### アセットのライセンス取得 {#licenseassets}

[!DNL Adobe Stock] エンタープライズプランの割り当てを使用することで、[!DNL Adobe Stock] アセットのライセンスを取得できます。ライセンスを許諾されたアセットは透かしなしで保存され、[!DNL Experience Manager Assets] で検索することも使用することも可能になります。

![[!DNL Adobe Stock] アセットのライセンスを取得して [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg) に保存するダイアログ


### メタデータおよびアセットプロパティへのアクセス {#access-metadata-and-asset-properties}

メタデータ（[!DNL Experience Manager] に保存されているアセットの [!DNL Adobe Stock] メタデータプロパティを含む）にアクセスしてプレビューし、アセットの&#x200B;**[!UICONTROL ライセンス参照]**&#x200B;を追加できます。ただし、ライセンス参照の更新は [!DNL Experience Manager] と [!DNL Adobe Stock] Web サイトの間で同期されません。

ユーザーは、ライセンスを許諾されたアセットとライセンスを許諾されていないアセットの両方を表示できます。

![保存されているアセットのメタデータとライセンス参照の表示、アクセス](assets/metadata_properties.jpg)


## 既知の制限事項 {#known-limitations}

* **ユーザーのライセンスを制限する機能が正しく機能しない**：Stock 設定に対する `read` 権限を持つすべてのユーザーは、[!DNL Adobe Stock] アセットを検索してライセンスを取得できます。

* **管理者以外のユーザーは、[!DNL Adobe Stock] クラウド設定を手動でアクティベートする必要がある**：**[!UICONTROL ユーザー環境設定]**&#x200B;ウィンドウで、**[!UICONTROL Stock 設定]**&#x200B;に [!DNL Adobe Stock] クラウド設定は有効になっていますが、管理者以外のユーザーには機能しません。ユーザーは、「**[!UICONTROL 同意する]**」ボタンをクリックして、Stock 設定をアクティベートする必要があります。この手順がない場合、システムは **[!UICONTROL Assets]** にアクセスする際にエラーメッセージを反映します。

* **編集画像の警告が表示されない**：画像のライセンスを取得する場合、ユーザーは画像が「編集のみ使用」かどうか確認できません。管理者は誤用を防ぐために、Admin Console から編集用アセットへのアクセスをオフにできます。

* **間違ったライセンスの種類が表示される**：[!DNL Experience Manager] で、アセットに対して正しくないライセンスタイプが表示される可能性があります。[!DNL Adobe Stock] Web サイトにログインすると、ライセンスタイプを確認できます。

* **参照フィールドとメタデータが同期されない**：ユーザーがライセンス参照フィールドを更新すると、そのライセンス参照情報は [!DNL Experience Manager] で更新されますが、[!DNL Adobe Stock] Web サイト上では更新されません。同様に、[!DNL Adobe Stock] Web サイトで参照フィールドを更新すると、更新情報が [!DNL Experience Manager] には反映されません。

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
-->

**関連情報**

* [アセットを翻訳](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](file-format-support.md)
* [アセットを検索](search-assets.md)
* [接続されたアセット](use-assets-across-connected-assets-instances.md)
* [アセットレポート](asset-reports.md)
* [メタデータスキーマ](metadata-schemas.md)
* [アセットをダウンロード](download-assets-from-aem.md)
* [メタデータを管理](manage-metadata.md)
* [検索ファセット](search-facets.md)
* [コレクションを管理](manage-collections.md)
* [メタデータの一括読み込み](metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Experience Manager Assets での Adobe Stock アセットの使用について説明するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=ja)
>* [Adobe Stock エンタープライズプランのヘルプ](https://helpx.adobe.com/jp/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock の FAQ](https://helpx.adobe.com/jp/stock/faq.html)
