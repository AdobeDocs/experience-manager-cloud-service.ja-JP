---
title: ' [!DNL Assets] での [!DNL Adobe Stock] アセットの管理。'
description: ' [!DNL Adobe Experience Manager] 内から [!DNL Adobe Stock] アセットを、検索、取得、ライセンス、管理します。ライセンスされたアセットをその他のデジタルアセットとして使用します。'
contentOwner: Vishabh Gupta
feature: Search,Adobe Stock
role: Admin,User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 3761d399de29645ec62cabf50bf6b26a64f3c7be
workflow-type: tm+mt
source-wordcount: '2441'
ht-degree: 44%

---

# [!DNL Adobe Stock] での [!DNL Adobe Experience Manager Assets] アセットの使用  {#use-adobe-stock-assets-in-aem-assets}

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、何百万点もの質の高い選ばれた著作権使用料不要の写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。

[!DNL Adobe Stock] エンタープライズ版の場合は、デフォルトで、組織全体での共有権限が含まれます。 組織のユーザーがアセットのライセンスを取得すると、組織の他のユーザーがこのアセットを識別、ダウンロード、使用できるようになります。再度ライセンスを取得する必要はありません。 アセットが組織でライセンスされると、そのアセットを使用する権限は永続的に有効になります。

企業を統合できる [!DNL Adobe Stock] 計画する [!DNL Experience Manager Assets] の強力なアセット管理機能を使用して、ライセンスされたアセットをクリエイティブプロジェクトやマーケティングプロジェクトに幅広く利用できるようにする [!DNL Experience Manager]. [!DNL Experience Manager] に保存されているAdobe Stockアセットの検索、プレビュー、ライセンスの取得をすばやくおこなうことができます。 [!DNL Experience Manager]、 [!DNL Experience Manager] インターフェイス。

## [!DNL Experience Manager] と [!DNL Adobe Stock] の統合  {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] を使用すると、ユーザーは検索、プレビュー、保存、ライセンスを実行できます。 [!DNL Adobe Stock] から直接 [!DNL Experience Manager].

**前提条件**

統合には次の要件が必要です。

* 起動および実行 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] インスタンス
* An [enterprise [!DNL Adobe Stock] プラン](https://stockenterprise.adobe.com/)
* デフォルトの Stock 製品プロファイルにAdmin Consoleする権限を持つユーザー
* 統合開発者コンソールで統合を作成するための開発者アクセスプロファイルに対する権限を持つAdobe

企業 [!DNL Adobe Stock] 計画

* 次の製品の使用権限を提供 [!DNL Adobe Stock] ( 株式Experience Manager)
* に購入したクレジット [!DNL Adobe Admin Console] 在庫権限
* 内でのサービスアカウント (JWT) 認証を有効にします [!DNL Adobe Developer Console] 在庫権限
* 内からグローバルにクレジットとライセンスを管理できます [!DNL Adobe Admin Console]

権限内で、 [!DNL Adobe Stock] 次に存在する [!DNL Admin Console]. 複数のプロファイルを作成でき、これらのプロファイルによって Stock アセットのライセンスを取得できるユーザーが決まります。 製品プロファイルに直接アクセスできるユーザーは、 [https://stock.adobe.com/](https://stock.adobe.com/) および Stock アセットのライセンスを取得します。 一方、Developer Access を使用して統合 (API) を作成する方法もあります。 この統合により、 [!DNL Experience Manager Assets] および [!DNL Adobe Stock].

>[!NOTE]
>
>Stock サービスアカウント (JWT) 認証には、エンタープライズ Stock 使用権限が付与されます。
>
>この統合では、Enterprise Stock 使用権限の OAuth 認証をサポートしていません。


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

## 統合の手順 [!DNL Experience Manager] および [!DNL Adobe Stock] {#integration-steps}

統合する [!DNL Experience Manager] および [!DNL Adobe Stock]をクリックし、リストに表示された順序で次の手順を実行します。

1. [公開証明書の取得](#public-certificate)

   In [!DNL Experience Manager]、IMS アカウントを作成し、公開証明書（公開鍵）を生成します。

1. [サービスアカウント（JWT）接続の作成](#createnewintegration)

   In [!DNL Adobe Developer Console]、 [!DNL Adobe Stock] 組織。 そのプロジェクトで、公開鍵で API を設定して、サービスアカウント（JWT）接続を作成します。サービスアカウント資格情報と JWT ペイロード情報を取得します。

1. [IMS アカウントの設定](#create-ims-account-configuration)

   In [!DNL Experience Manager]の場合は、サービスアカウント資格情報と JWT ペイロードを使用して IMS アカウントを設定します。

1. [Cloud Service の設定](#configure-the-cloud-service)

   In [!DNL Experience Manager]、設定 [!DNL Adobe Stock] IMS アカウントを使用するクラウドサービス。


### IMS 設定の作成 {#create-an-ims-configuration}

IMS 設定により、 [!DNL Experience Manager Assets] オーサーインスタンスと [!DNL Adobe Stock] 使用権限

IMS 設定には、次の 2 つの手順が含まれます。

* [公開証明書の取得](#public-certificate)
* [IMS アカウントの設定](#create-ims-account-configuration)

### 公開証明書の取得 {#public-certificate}

公開鍵（証明書）は、製品開発者コンソールでAdobeプロファイルを認証します。

1. にログインします。 [!DNL Experience Manager Assets] クラウドインスタンス。

1. **[!UICONTROL ツール]**&#x200B;パネルで、**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。

1. Adobe IMS 設定ページで、「**[!UICONTROL 作成]**」をクリックします。この **[!UICONTROL Adobe IMSテクニカルアカウント設定]** ページが開きます。

1. 内 **[!UICONTROL 証明書]** タブ、選択 **[!UICONTROL Adobe Stock]** から **[!UICONTROL クラウドソリューション]** ドロップダウンリスト。

1. 証明書を作成するか、既存の証明書を設定に再利用できます。

   証明書を作成するには、 **[!UICONTROL 新しい証明書を作成]** チェックボックスをオンにして、 **エイリアス** 公開鍵の ここで入力したエイリアスが、公開鍵になります。

1. 「**[!UICONTROL 証明書を作成]**」をクリックします。「**[!UICONTROL OK]**」をクリックして公開証明書を生成します。

1. **[!UICONTROL 公開鍵をダウンロード]**&#x200B;アイコンをクリックして、公開鍵（.crt）ファイルをローカルマシンに保存します。この公開鍵を後で使用して、Brand Portal テナントの API を設定し、Adobe 開発者コンソールでサービスアカウント資格情報を生成が次の値である。

   「**[!UICONTROL 次へ]**」をクリックします。

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. 内 **アカウント** 「 」タブを選択すると、Adobe IMSアカウントが作成され、サービスアカウント資格情報が必要になります。

   新しいタブを開き、 [Adobe開発者コンソールでのサービスアカウント (JWT) 接続の作成](#createnewintegration).

### サービスアカウント（JWT）接続の作成 {#createnewintegration}

Adobe開発者コンソールで、プロジェクトと API を組織レベルで設定します。 API を設定すると、サービスアカウント（JWT）接続が作成されます。API を設定するには、キーペア（秘密鍵と公開鍵）を生成する方法と、公開鍵をアップロードする方法の 2 とおりがあります。この例では、サービスアカウント資格情報は公開鍵をアップロードすることで生成されます。

サービスアカウント資格情報と JWT ペイロードを生成するには：

1. システム管理者権限でAdobe開発者コンソールにログインします。 デフォルトの URL は [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui) です。


   ドロップダウン（組織）リストから正しい IMS 組織（Stock 使用権限）が選択されていることを確認します。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。システムで生成された名前を持つ空のプロジェクトが組織に対して作成されます。

   クリック **[!UICONTROL プロジェクトを編集]**. を更新します。 **[!UICONTROL プロジェクトタイトル]** および **[!UICONTROL 説明]**&#x200B;をクリックし、 **[!UICONTROL 保存]**.

1. 「**[!UICONTROL プロジェクトの概要]**」タブで、「**[!UICONTROL API を追加]**」をクリックします。

1. 内 **[!UICONTROL API ウィンドウを追加]**&#x200B;を選択します。 **[!UICONTROL Adobe Stock]**. 「**[!UICONTROL 次へ]**」をクリックします。

1. 内 **[!UICONTROL API の設定]** ウィンドウ：選択 **[!UICONTROL サービスアカウント (JWT)]** 認証。 「**[!UICONTROL 次へ]**」をクリックします。

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. クリック **[!UICONTROL 公開鍵をアップロード]**. クリック **[!UICONTROL ファイルを選択]** と、 [公開証明書を取得する](#public-certificate) 」セクションに入力します。 「**[!UICONTROL 次へ]**」をクリックします。

1. 公開鍵を確認し、「**[!UICONTROL 次へ]**」をクリックします。

1. デフォルトを選択 **[!UICONTROL Adobe Stock]** 製品プロファイルを選択し、 **[!UICONTROL 設定済み API を保存]**.

1. API が設定されると、API の概要ページにリダイレクトされます。左側のナビゲーションツリーで「**[!UICONTROL 資格情報]**」の下の「**[!UICONTROL サービスアカウント（JWT）]**」オプションをクリックします。ここで、資格情報を表示し、JWT トークンの生成、資格情報の詳細のコピー、クライアントの秘密鍵の取得などのアクションを実行できます。

1. 「**[!UICONTROL クライアント資格情報]**」タブから、**[!UICONTROL クライアント ID]** をコピーします。

   「**[!UICONTROL クライアント秘密鍵を取得]**」をクリックし、**[!UICONTROL クライアントの秘密鍵]**&#x200B;をコピーします。

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. 「**[!UICONTROL JWT を生成]**」タブに移動し、**[!UICONTROL JWT ペイロード]**&#x200B;情報をコピーします。

これで、クライアント ID（API キー）、クライアントの秘密鍵、JWT ペイロードを [IMS アカウントの設定](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### IMS アカウントの設定 {#create-ims-account-configuration}

次を持っている必要があります： [証明書](#public-certificate) および [サービスアカウント (JWT) 資格情報](#createnewintegration) をクリックして、IMS アカウントを設定します。

IMS アカウントを設定するには：

1. IMS 設定を開き、「**[!UICONTROL アカウント]**」タブに移動します。[公開証明書の取得](#public-certificate)中も、ページは開いたままになっています。

1. IMS アカウントの&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定します。

   内 **[!UICONTROL 認証サーバー]** フィールドに、URL を入力します。 [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   クライアント ID を **[!UICONTROL API キー]** フィールド **[!UICONTROL クライアント秘密鍵]**、および **[!UICONTROL ペイロード]** （JWT ペイロード） [サービスアカウント (JWT) 接続の作成](#createnewintegration).

1. 「**[!UICONTROL 作成]**」をクリックします。IMS アカウント設定が作成されます。

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. その IMS アカウント設定を選択し、「**[!UICONTROL 正常性をチェック]**」をクリックします。

   ダイアログボックスの「**[!UICONTROL チェック]**」をクリックします。正常に設定されると、*トークンが正常に取得されました*&#x200B;というメッセージが表示されます。

   ![ヘルスチェック](assets/aem-stock-healthcheck.png)


### Cloud Service の設定 {#configure-the-cloud-service}

次の手順で [!DNL Adobe Stock] クラウドサービス：

1. 内 [!DNL Experience Manager] ユーザーインターフェイス、に移動する **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. 内 [!DNL Adobe Stock Configurations] ページ、クリック **[!UICONTROL 作成]**.

1. を指定します。 **[!UICONTROL タイトル]** クラウド設定用。

   [IMS アカウントの設定](#create-ims-account-configuration)時に作成した IMS 設定を選択します。

   ドロップダウンリストからロケールを選択します。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   お使いの [!DNL Experience Manager Assets] オーサーインスタンスが [!DNL Adobe Stock]. 複数の [!DNL Adobe Stock] 設定（ロケールベースの設定など）。 これで、 [!DNL Adobe Stock] 内のアセット [!DNL Experience Manager] ユーザーインターフェイス。

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >統合のこの段階では、管理者のみが [!DNL Adobe Stock] アセットを検索し、（オムニサーチを使用して）Stock アセットを検索し、 [!DNL Adobe Stock] アセット。
   >
   >管理者は、 [!DNL Adobe Stock] クラウドサービスを使用して、 [!DNL Experience Manager] をクリックして、Stock 設定にアクセスします。

1. ユーザーまたはグループを追加するには、 [!DNL Adobe Stock] クラウド設定を開き、 **[!UICONTROL プロパティ]**.

1. Adobe Stock設定へのアクセス権を割り当てたユーザーまたはグループを検索して追加します。 詳しくは、 [ユーザーグループへの権限の割り当て](#assign-permissions-to-group).


## ユーザーグループに権限を割り当て {#assign-permissions-to-group}

管理者は、ユーザーグループを作成し、特定のユーザーまたはグループに対して、 [!DNL Adobe Stock] クラウドサービス。

Adobe Stockアセットの検索とライセンス取得に必要な権限は次のとおりです。

* パスを設定します。 `/conf/global/settings/stock`
* 権限: `jcr:read`
* 権限タイプ: `Allow`

ユーザーグループを作成したり、既存のユーザーグループに権限を割り当てたりできます。 権限は [!DNL Experience Manager Assets] インターフェイスまたは [!DNL User Admin] コンソール。

**次の場所からユーザーグループにアクセスできるようにする [!DNL Experience Manager]:**

1. 内 [!DNL Experience Manager] ユーザーインターフェイス、に移動する **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL グループ]**. のユーザーグループの作成 [!DNL Adobe Stock].

1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL 権限]**.

1. 左側のパネルでユーザーグループを検索し、新しい **[!UICONTROL アクセス制御エントリ (ACE)]** Adobe Stock

   * パスを設定します。 `/conf/global/settings/stock`
   * 権限: `jcr:read`
   * 権限タイプ: `Allow`

   「**[!UICONTROL 追加]**」をクリックします。

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. を選択します。 [!DNL Adobe Stock] クラウド設定を開き、 **[!UICONTROL プロパティ]**.

1. 新しく作成したユーザーグループを [!DNL Adobe Stock] 設定。 「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![assign-user](assets/aem-stock-adduser.png)

**次の場所からユーザーにアクセスを提供する [!DNL User Admin Console]:**

1. を開きます。 [!DNL Experience Manager] ユーザーAdmin Console。 デフォルトの URL は `http://localhost:4502/userdamin` です。

1. 左側のパネルで、 `user_id` または `name`. ダブルクリックして、ユーザープロパティを開きます。

1. 次に移動： **[!UICONTROL 権限]** タブと許可 `read` 権限 [!DNL Adobe Stock] クラウド設定： `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >クラウド設定が許可されていない場合、ユーザーは **[!UICONTROL Assets]** 内 [!DNL Experience Manager] インターフェイス。
   >
   >へのアクセスを許可するには [!UICONTROL Assets] および [!DNL Adobe Stock] アセットを使用する場合は、クラウド設定がユーザーに許可されていることを確認します。

1. クリック **[!UICONTROL 保存]** 権限を更新する場合。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. ユーザーまたはグループを [!DNL Adobe Stock] クラウド設定。


## Adobe Stock Assets へのアクセス {#access-stock-assets}

管理者以外のユーザーが [!DNL Adobe Stock] クラウド設定では、を検索してライセンスを取得できます [!DNL Adobe Stock] からのアセット [!DNL Experience Manager] インターフェイス。

ユーザーは、 [!DNL Adobe Stock] アクセス前のクラウド設定 [!DNL Adobe Stock] アセット。 これは 1 回限りのアクティビティです。 ユーザーに複数のに対する権限が割り当てられている場合 [!DNL Adobe Stock] クラウド設定の場合、ユーザーは、 **[!UICONTROL ユーザーの環境設定]**.

をアクティブにするには、以下を実行します。 [!DNL Adobe Stock] クラウド設定：

1. [!DNL Experience Manager] にログインします。

1. 右上隅のユーザーアイコンをクリックし、 **[!UICONTROL 環境設定]**. この **[!UICONTROL ユーザーの環境設定]** ウィンドウが開きます。

1. 目的のを選択します。 **[!UICONTROL 在庫設定]** ドロップダウンリストから、 **[!UICONTROL 確定]** をクリックして設定をアクティベートします。

   ![user-preferences](assets/aem-stock-preferences.png)

1. に移動します。 **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. 表示、検索、ライセンスが可能になりました [!DNL Adobe Stock] アセット。

次の表で、 [!DNL Adobe Stock] アセット：

| User | グループ | 権限 | ユーザーの環境設定で Stock 設定を受け入れる | アセットにアクセス | Adobe Stockにアクセス |
| --- | --- | --- | --- | --- | --- |
| admin | 該当なし | すべて | 該当なし | はい | はい |
| test-doc1 | DAM ユーザー | /conf/global/settings/stock/cloud-config | はい | 可 | はい |
| test-doc1 | DAM ユーザー | /conf/global/settings/stock/cloud-config | いいえ | エラー：データの読み込みに失敗しました | いいえ |
| test-doc1 | DAM ユーザー | **許可**:/conf/global/settings/stock **拒否**:/cloud-config | 在庫設定が表示されません | 可 | 不可 |

## [!DNL Adobe Stock] での [!DNL Experience Manager] アセットの使用と管理  {#usemanage}

この機能を使用すると、[!DNL Experience Manager Assets] で [!DNL Adobe Stock] アセットを操作できます。[!DNL Experience Manager] のユーザーインターフェイス内から [!DNL Adobe Stock] アセットを検索し、必要なアセットのライセンスを取得できます。

[!DNL Experience Manager] 内で [!DNL Adobe Stock] アセットのライセンスを取得すると、そのアセットを通常のアセットと同様に使用および管理できます。ユーザーは [!DNL Experience Manager] 内でアセットの検索およびプレビュー、アセットのコピーおよび公開、[!DNL Brand Portal] でのアセットの共有、[!DNL Experience Manager] デスクトップアプリケーション経由でのアセットのアクセスおよび使用を行うことができます。

![を検索 [!DNL Adobe Stock] アセットとフィルターの結果 [!DNL Adobe Experience Manager] workspace](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] 指定された ID のアセットと類似しているアセットを検索します。**B.** 選択した形状や向きと一致するアセットを検索します。**C.** サポートされているアセットタイプのいずれかを検索します。**D.** フィルターウィンドウを開く／折りたたみます。**E.** 選択したアセットのライセンスを取得して に保存します。[!DNL Experience Manager]**F.**[!DNL Experience Manager] アセットを透かし付きで に保存します。**G.**[!DNL Adobe Stock] 選択したアセットと類似したアセットを Web サイトで調べます。**H.**[!DNL Adobe Stock] 選択したアセットを Web サイトに表示します。**I.** 検索結果から選択したアセットの数。**J.** カード表示とリスト表示を切り替えます。

### アセットの検索 {#find-assets}

[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] と [!DNL Adobe Stock] の両方でアセットを検索できます。検索場所を [!DNL Adobe Stock] に限定しない場合は、[!DNL Experience Manager] と [!DNL Adobe Stock] からの検索結果が表示されます。

* [!DNL Adobe Stock] アセットを検索するには、**[!UICONTROL ナビゲーション]**／**[!UICONTROL アセット]**／**[!UICONTROL Adobe Stock を検索]**&#x200B;をクリックします。

* [!DNL Adobe Stock] と [!DNL Experience Manager Assets] にまたがるアセットを検索するには、「![検索](assets/do-not-localize/search_icon.png)」をクリックします。

また、アセットを選択するには、検索バーに「`Location: Adobe Stock`」と入力します。[!DNL Adobe Stock][!DNL Experience Manager] は、検索されたアセットに対する高度なフィルタリング機能を備えており、サポートされているアセットのタイプや画像の向き、ライセンスの状態などのフィルターを使用して、必要なアセットをすばやく見つけることができます。

>[!NOTE]
>
>検索元のアセット [!DNL Adobe Stock] が [!DNL Experience Manager]. [アセットを保存](/help/assets/aem-assets-adobe-stock.md#saveassets)するか、[アセットにライセンスを付与して保存](/help/assets/aem-assets-adobe-stock.md#licenseassets)した後でないと、[!DNL Adobe Stock] アセットを取得して [!DNL Experience Manager] リポジトリーに保存することはできません。既に [!DNL Experience Manager] に保存されているアセットが表示され、参照やアクセスが簡単にできるようにハイライトされます。また、[!DNL Stock] アセットは、ソースが [!DNL Stock] であることを示すいくつかの追加メタデータとともに保存されます。

![でフィルターを検索 [!DNL Experience Manager] およびハイライト [!DNL Adobe Stock] 検索結果内のアセット](assets/aem-search-filters2.jpg)

### 必要なアセットの保存と表示 {#saveassets}

[!DNL Experience Manager] に保存するアセットを選択します。上部ツールバーの「[!UICONTROL 保存]」をクリックし、アセットの名前と保存場所を指定します。ライセンスが不要なアセットはローカルに透かし付きで保存されます。

アセットの検索を次回実行すると、保存済みのアセットは、[!DNL Experience Manager Assets] で使用可能であることを示すバッジ付きでハイライトされます。

>[!NOTE]
>
>最近追加されたアセットには、ライセンスが許諾されていることを示すバッジではなく、新しいアセットであることを示すバッジが表示されます。

### アセットのライセンス取得 {#licenseassets}

[!DNL Adobe Stock] エンタープライズプランの割り当てを使用することで、[!DNL Adobe Stock] アセットのライセンスを取得できます。ライセンスを許諾されたアセットは透かしなしで保存され、[!DNL Experience Manager Assets] で検索することも使用することも可能になります。

![ライセンスを取得して保存するダイアログ [!DNL Adobe Stock] 内のアセット [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### メタデータおよびアセットプロパティへのアクセス {#access-metadata-and-asset-properties}

メタデータ（[!DNL Experience Manager] に保存されているアセットの [!DNL Adobe Stock] メタデータプロパティを含む）にアクセスしてプレビューし、アセットの&#x200B;**[!UICONTROL ライセンス参照]**&#x200B;を追加できます。ただし、ライセンス参照の更新は [!DNL Experience Manager] と [!DNL Adobe Stock] Web サイトの間で同期されません。

ユーザーは、ライセンスを許諾されたアセットとライセンスを許諾されていないアセットの両方を表示できます。

![保存されているアセットのメタデータとライセンス参照の表示、アクセス](assets/metadata_properties.jpg)


## 既知の制限事項 {#known-limitations}

* **ユーザーのライセンスを制限する機能が正しく機能しない**:次を持つすべてのユーザー： `read` stock 設定に対する権限で、 [!DNL Adobe Stock] アセット。

* **管理者以外のユーザーは、手動で [!DNL Adobe Stock] クラウド設定**:内 **[!UICONTROL ユーザーの環境設定]** ウィンドウ **[!UICONTROL 在庫設定]** には、 [!DNL Adobe Stock] クラウド設定が有効になっているが、管理者以外のユーザーに対しては機能しない。 ユーザーが **[!UICONTROL 確定]** ボタンをクリックして、Stock 設定を有効にします。 この手順がない場合、システムはにアクセスする際にエラーメッセージを反映します **[!UICONTROL Assets]**.

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

>[!MORELIKETHIS]
>
>* [Experience Manager Assets での Adobe Stock アセットの使用について説明するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=ja)
>* [Adobe Stock エンタープライズプランのヘルプ](https://helpx.adobe.com/jp/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock の FAQ](https://helpx.adobe.com/jp/stock/faq.html)

