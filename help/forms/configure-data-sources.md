---
title: データソースの設定方法
description: Experience Manager Forms のデータ統合機能により、複数の異なるデータソースを設定して接続できます。RESTful Web サービス、SOAP ベースの Web サービスおよび OData サービスをデータソースとして設定し、それらを使用してフォームデータモデルを作成する方法について説明します。
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: e353fd386d2dfbc39c76a0ab56b50c44f3c54afc
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 86%

---

# データソースの設定 {#configure-data-sources}

![データ統合](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。以下のタイプがサポートされています。これらのタイプは、すぐに使用することができます。

* リレーショナルデータベース — MySQL [!DNL Microsoft SQL Server], [!DNL IBM DB2]、および [!DNL Oracle RDBMS]
* RESTful Web サービス
* SOAP ベース Web サービス
* OData サービス(バージョン 4.0)
* Microsoft® Dynamics
* Salesforce
* Microsoft® Azure Blob ストレージ

データ統合では、すぐに使用できる認証タイプとして、OAuth2.0 認証、基本認証、API キー認証がサポートされています。また、Web サービスにアクセスするためのカスタムの認証タイプを実装することもできます。RESTful、SOAP ベース、OData の各サービスは [!DNL Experience Manager] as a Cloud Service<!--, JDBC for relational databases --> で設定されますが、[!DNL Experience Manager] ユーザープロファイル用のコネクタは [!DNL Experience Manager] web コンソールで設定されます。

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] はリレーショナルデータベースをサポートしていません。

## リレーショナルデータベースの設定 {#configure-relational-database}

### 前提条件

を使用してリレーショナルデータベースを設定する前に [!DNL Experience Manager] Web コンソール設定では、次の操作が必須です。
* [Cloud Manager API を使用した高度なネットワークの有効化](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)（ポートはデフォルトで無効になっているので）
* [Maven に JDBC ドライバーの依存関係を追加](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### リレーショナルデータベースを設定する手順

リレーショナルデータベースは、 [!DNL Experience Manager] Web コンソールの設定 次の手順を実行します。

1. に移動します。 [!DNL Experience Manager] web コンソールの場所： `https://server:host/system/console/configMgr`.
1. 場所 **[!UICONTROL Day Commons JDBC 接続プール]** 設定。 その設定をタップして編集モードで開きます。

   ![JDBC コネクタプール](/help/forms/assets/jdbc_connector.png)

1. 設定ダイアログで、設定するデータベースの詳細を指定します。例えば、以下のような詳細を指定します。

   * JDBC ドライバーの Java™クラス名
   * JDBC 接続 URI
   * JDBC ドライバーとの接続を確立するためのユーザー名とパスワード
   * 「**[!UICONTROL 検証クエリ]**」フィールドで SQL SELECT クエリを指定して、プールからの接続を検証します。このクエリでは、1 行以上の行が返される必要があります。使用しているデータベースに応じて、以下のいずれかを指定します。
      * SELECT 1（MySQL または MS SQL の場合）
      * SELECT 1 from dual（Oracle の場合）
   * データソースの名前

   リレーショナル・データベースを構成するための文字列の例：

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > 参照 [JDBC DataSourcePool を使用した SQL 接続](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) を参照してください。

1. 「**[!UICONTROL 保存]**」をタップして、設定内容を保存します。

これで、設定済みのリレーショナルデータベースをフォームデータモデルと共に使用できます。

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## クラウドサービス設定用フォルダーの構成 {#cloud-folder}

RESTful サービス、SOAP サービス、OData サービスのクラウドサービスを設定するには、クラウドサービス用のフォルダーを設定する必要があります。

[!DNL Experience Manager] のすべてのクラウドサービス設定は、[!DNL Experience Manager] リポジトリーの `/conf` フォルダー内に保存されます。デフォルトの場合、`conf` フォルダーには `global` フォルダーが含まれています。このフォルダーで、クラウドサービスの設定を作成することができます。ただし、このフォルダーを手動でクラウド設定用に有効にする必要があります。追加のフォルダーを `conf` フォルダー内に作成して、クラウドサービスの作成と編集を行うこともできます。

クラウドサービス設定用のフォルダーを構成するには、以下の手順を実行します。

1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   * 詳しくは、[設定ブラウザー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=ja)のドキュメントを参照してください。
1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

   1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、「`global`」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。

   1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。

   1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で「**[!UICONTROL 作成]**」をタップします。
1. 内 **[!UICONTROL 設定を作成]** ダイアログで、フォルダーのタイトルを指定し、有効にします。 **[!UICONTROL クラウド設定]**.
1. 「**[!UICONTROL 作成]**」をタップします。これで、クラウドサービス設定が有効になったフォルダーが作成されました。

## RESTful Web サービスの設定 {#configure-restful-web-services}

RESTful Web サービスは、[!DNL Swagger] の仕様に従い、JSON 形式または YAML 形式で [Swagger 定義ファイル](https://swagger.io/specification/v2/)内に記述できます。で RESTful Web サービスを設定するには、以下を実行します。 [!DNL Experience Manager] as a Cloud Service [!DNL Swagger] ファイル ([Swagger バージョン 2.0](https://swagger.io/specification/v2/)) または [!DNL Swagger] ファイル ([Swagger バージョン 3.0](https://swagger.io/specification/v3/)) をファイルシステムまたはファイルがホストされている URL に設定する必要があります。

### Open API 仕様バージョン 2.0 用の RESTful サービスの設定 {#configure-restful-services-open-api-2.0}

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL RESTful サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す RESTful サービスの詳細情報を指定します。

   * 「[!UICONTROL Swagger ソース]」ドロップダウンで「URL」または「ファイル」を選択します。「URL」を選択した場合は、[!DNL  Swagger] 定義ファイルに対する [!DNL Swagger URL] を指定し、「ファイル」を選択した場合は、ローカルのファイルシステムから [!DNL Swagger] ファイルをアップロードします。
   * 次に基づいて[!DNL  Swagger] ソース入力。次のフィールドには、値が事前に入力されています。

      * スキーム：REST API で使用される転送プロトコル。ドロップダウンリストに表示されるスキームの種類の数は、[!DNL Swagger] ソースで定義されているスキームによって異なります。
      * ホスト：REST API を提供するホストのドメイン名または IP アドレス。このフィールドは必須です。
      * 基本パス：すべての API パスの URL プリフィックス。これはオプションのフィールドです。\
         必要に応じて、これらのフィールドの事前入力された値を編集します。
   * RESTful サービスにアクセスするための認証タイプ（「なし」、「OAuth2.0 認証」、「基本認証」、「API キー認証」、「カスタム認証」）を選択し、その選択内容に応じて認証の詳細を指定します。

   認証タイプとして **[!UICONTROL API キー]**&#x200B;を選択した場合は、API キーの値を指定します。API キーは、リクエストヘッダーまたはクエリパラメーターとして送信できます。「**[!UICONTROL 場所]**」ドロップダウンリストから次のオプションの 1 つを選択し、それに応じて「**[!UICONTROL パラメーター名]**」フィールドにヘッダーまたはクエリパラメーターの名前を指定します。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 「**[!UICONTROL 作成]**」をタップして、RESTful サービス用のクラウド設定を作成します。

### Open API 仕様バージョン 3.0 用の RESTful サービスの設定 {#configure-restful-services-open-api-3.0}

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL RESTful サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す RESTful サービスの詳細情報を指定します。

   * 「[!UICONTROL Swagger ソース]」ドロップダウンで「URL」または「ファイル」を選択します。「URL」を選択した場合は、[!DNL  Swagger] 定義ファイルに対する [!DNL Swagger 3.0 URL] を指定し、「ファイル」を選択した場合は、ローカルのファイルシステムから [!DNL Swagger] ファイルをアップロードします。
   * 次に基づいて[!DNL  Swagger] ソース入力、ターゲットサーバとの接続情報が表示されます。
   * RESTful サービスにアクセスするための認証タイプ（「なし」、「OAuth2.0 認証」、「基本認証」、「API キー認証」、「カスタム認証」）を選択し、その選択内容に応じて認証の詳細を指定します。

   認証タイプとして **[!UICONTROL API キー]**&#x200B;を選択した場合は、API キーの値を指定します。API キーは、リクエストヘッダーまたはクエリパラメーターとして送信できます。「**[!UICONTROL 場所]**」ドロップダウンリストから次のオプションの 1 つを選択し、それに応じて「**[!UICONTROL パラメーター名]**」フィールドにヘッダーまたはクエリパラメーターの名前を指定します。

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 「**[!UICONTROL 作成]**」をタップして、RESTful サービス用のクラウド設定を作成します。

RESTful サービス Open API 仕様バージョン 3.0 でサポートされていない操作の一部は次のとおりです。
* コールバック
* 1/任意
* リモート参照
* リンク
* 1 回の操作に対する異なる MIME タイプに対する異なるリクエスト本文

以下を参照してください。 [OpenAPI 3.0 仕様](https://swagger.io/specification/v3/) を参照してください。

### パフォーマンスを最適化するためのフォームデータモデル HTTP クライアント設定 {#fdm-http-client-configuration}

データソースとして RESTful web サービスと統合する場合の [!DNL Experience Manager Forms] フォームデータモデルには、パフォーマンス最適化のための HTTP クライアント設定が含まれています。


**[!UICONTROL REST データソース設定のフォームデータモデル HTTP クライアント設定]**&#x200B;の次のプロパティを設定し、正規表現を指定します。

* `http.connection.max.per.route` プロパティを使用して、フォームデータモデルと RESTful web サービス間で許可される最大接続数を設定します。デフォルト値は 20 接続です。

* `http.connection.max` プロパティを使用して、各ルートに許可される最大接続数を指定します。デフォルト値は 40 接続です。

* `http.connection.keep.alive.duration` プロパティを使用して、永続的な HTTP 接続が有効に保たれる期間を指定します。デフォルト値は 15 秒です。

* `http.connection.timeout` プロパティを使用して、[!DNL Experience Manager Forms] 接続が確立するまでのサーバーの待機時間を指定します。デフォルト値は 10 秒です。

* `http.socket.timeout` プロパティを使用して、2 つのデータパケット間の無操作状態の最大期間を指定します。デフォルト値は 30 秒です。

以下の JSON ファイルにサンプルが表示されています。


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. 「**[!UICONTROL REST データソース用フォームデータモデル HTTP クライアント設定]**」をタップします。

1. [!UICONTROL REST データソース用フォームデータモデル HTTP クライアント設定]ダイアログで、

   * **[!UICONTROL 接続制限（合計）]**&#x200B;フィールドに、フォームデータモデルと RESTful web サービス間の接続許可数の上限を指定します。デフォルト値は 20 接続です。

   * **[!UICONTROL ルートごとの接続制限]**&#x200B;フィールドで、各ルートに許可される最大接続数を指定します。デフォルト値は 2 つの接続です。

   * **[!UICONTROL Keep Alive]** フィールドで、持続的な HTTP 接続を維持する期間を指定します。デフォルト値は 15 秒です。

   * **[!UICONTROL 接続タイムアウト]**&#x200B;フィールドで、[!DNL Experience Manager Forms] サーバーが接続を確立するまでの待ち時間を指定します。デフォルト値は 10 秒です。

   * **[!UICONTROL ソケットタイムアウト]**&#x200B;フィールドに、2 つのデータパケット間の非アクティブの最大時間を指定します。デフォルト値は 30 秒です。

## SOAP Web サービスの設定 {#configure-soap-web-services}

SOAP ベースの web サービスは、[Web Services Description Language（WSDL）の仕様](https://www.w3.org/TR/wsdl)に従って記述します。[!DNL Experience Manager Forms] は RPC スタイルの WSDL モデルをサポートしません。

[!DNL Experience Manager] as a Cloud Service で SOAP ベースの web サービスを設定するには、その web サービスの WSDL URL を確認して、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](configure-data-sources.md#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL SOAP Web サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す SOAP Web サービスの詳細情報を指定します。

   * Web サービスの WSDL URL を指定します。
   * サービスエンドポイント。WSDL で指定されているサービスエンドポイントを上書きするには、このフィールドの値を指定します。
   * SOAP サービスにアクセスするための認証タイプ（なし、OAuth2.0 認証、基本認証、カスタム認証）を選択し、その選択内容に応じて認証の詳細を指定します。

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. 「**[!UICONTROL 作成]**」をタップして、SOAP Web サービス用のクラウド設定を作成します。

### SOAP Web サービス WSDL でのインポート文の使用を有効にする {#enable-import-statements}

SOAP Web サービス WSDL のインポート文として許可される絶対 URL のフィルターとして機能する正規表現を指定できます。デフォルトでは、このフィールドに値はありません。その結果、[!DNL Experience Manager] は WSDL で使用可能なすべてのインポート文をブロックします。このフィールドの値として `.*` を指定すると、[!DNL Experience Manager] はすべてのインポート文を許可します。

**[!UICONTROL フォームデータモデル SOAP Web サービスインポート許可リスト]**&#x200B;の設定の `importAllowlistPattern` プロパティを設定して、正規表現を指定します。以下の JSON ファイルにサンプルが表示されています。


```json
{
  "importAllowlistPattern": ".*"
}
```


設定の値をセットするには、[AEM SDK を使用して OSGi 設定を生成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=ja#generating-osgi-configurations-using-the-aem-sdk-quickstart)し、Cloud Service インスタンスに[設定をデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja#deployment-process)します。

## OData サービスの設定 {#config-odata}

OData サービスは、そのサービスのルート URL によって識別されます。[!DNL Experience Manager] as a Cloud Service で OData サービスを設定するには、そのサービスのルート URL を確認して、以下の手順を実行します。

>[!NOTE]
>
> フォームデータモデルは [OData バージョン 4](https://www.odata.org/documentation/) をサポートします。
>オンライン環境またはオンプレミス環境で [!DNL Microsoft® Dynamics 365] を設定する詳しい手順については、[[!DNL Microsoft® Dynamics] OData 設定](ms-dynamics-odata-configuration.md)を参照してください。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](#cloud-folder)」を参照してください。

1. 「**[!UICONTROL 作成]**」をタップして、**[!UICONTROL データソース設定を作成]**&#x200B;ウィザードを開きます。設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL OData サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す OData サービスの詳細情報を指定します。

   * 設定する OData サービスのルート URL を指定します。
   * OData サービスにアクセスするための認証タイプ（なし、OAuth2.0 認証、基本認証、API キー認証、カスタム認証）を選択し、その選択内容に応じて認証の詳細を指定します。

   認証タイプとして **[!UICONTROL API キー]**&#x200B;を選択した場合は、API キーの値を指定します。API キーは、リクエストヘッダーまたはクエリパラメーターとして送信できます。「**[!UICONTROL 場所]**」ドロップダウンリストから次のオプションの 1 つを選択し、それに応じて「**[!UICONTROL パラメーター名]**」フィールドにヘッダーまたはクエリパラメーターの名前を指定します。

   >[!NOTE]
   >
   >OData エンドポイントをサービスルートとして使用して [!DNL Microsoft® Dynamics] サービスに接続する場合は、OAuth 2.0 認証を選択する必要があります。

1. 「**[!UICONTROL 作成]**」をタップして、OData サービス用のクラウド設定を作成します。

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## 次の手順 {#next-steps}

上記の手順により、データソースが設定されました。次に、フォームデータモデルを作成できます。データソースを持たないフォームデータモデルを既に作成している場合は、そのモデルを設定したデータソースに関連付けることができます。 詳しくは、「[フォームデータモデルの作成](create-form-data-models.md)」を参照してください。
