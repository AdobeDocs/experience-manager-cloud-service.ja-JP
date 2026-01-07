---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: e29f70aa1a8164787c7d310a05c24d7e501803e5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 16%

---

# アダプティブフォームの Azure SQL ストレージへの接続

Adobe Experience Manager（AEM）のアダプティブFormsは、外部データベースと統合してデータを保存または取得できます。
この記事では、AEM as a Cloud Serviceで JDBC を使用してアダプティブフォームを Azure SQL データベースに接続する方法について概説します。

>
> 
> このガイドは、高度なネットワーク機能が有効になっている、サンドボックス以外のAEM as a Cloud Service環境に適用されます。

## メリット

アダプティブFormsと Azure SQL の統合には、次のようないくつかの利点があります。

* **リアルタイムデータインタラクション：** フォームと Azure データベース間でデータのライブ読み取りと書き込みを有効にします。
* **スケーラビリティ：** Azure SQL は、エンタープライズレベルのアプリケーションに適したスケーラブルなデータベースパフォーマンスを提供します。
* **一元化されたデータストレージ：** フォーム送信および取得したデータを 1 か所に安全に保存します。
* **セキュリティコンプライアンス：** Azure の組み込みのネットワーク、ファイアウォール、暗号化オプションを活用して、安全な通信を確保します。
* **クラウドネイティブな統合：** AEM as a Cloud Serviceを使用する最新のクラウドファーストアーキテクチャに最適です。

## 前提条件

* [Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal) を作成し、**プロキシ接続** が有効になっていることを確認します。

  >[!NOTE]
  >
  > `Azure Portal → SQL Server → Security → Networking → Connectivity` に移動して、**プロキシ接続** を有効にします。

  ![Azure Db の作成 ](/help/forms/assets/create-azure-db.png)

* 作成した Azure データベースに対して、専用のエグレス IP を使用して設定された [ 高度なネットワーク ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address) を有効にします。

  >[!NOTE]
  >
  >    専用のエグレス IP を有効にした後。 `Azure Portal → SQL Server → Security → Networking → Public Access` に移動し、エグレス IP をファイアウォールルールに追加します。

  ![エグレス IP](/help/forms/assets/cretae-azure-db-egress-ip.png)

* 次を使用して、クラウド環境にポート転送を設定します。
   * **portOrigin**: `30000–30999` 間
   * **portDest**: `1433` （Azure SQL のデフォルトのポート）
例：`portOrigin: 30433 → portDest: 1433`

     >
     > 
     > ポート転送の設定については、Adobe Cloud Manager サポートにお問い合わせください。


## アダプティブFormsを Azure SQL に接続する手順

**手順 1:AEM as a Cloud Service Git リポジトリのクローン**

1. コマンドラインを開き、AEM as a Cloud Service リポジトリを保存するディレクトリ（例：`/cloud-service-repository/`）を選択します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **この情報はどこにありますか？**

   これらの詳細を見つける手順について詳しくは、Adobe Experience League の記事「[Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)」を参照してください。

   コマンドが正常に完了すると、ローカルディレクトリに新しいフォルダーが作成されます。このフォルダーの名前は、アプリケーションに合わせて指定します。

1. エディターでリポジトリフォルダーを開きます。

**手順 2：必要な JAR の追加**

[SQL ドライバーの依存関係 ](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true) を、`all` パッケージを介してAEM プロジェクトに含めます。

>[!NOTE]
>
> プロジェクトに SQL 依存関係を含めるには、[SQL ドライバーの依存関係 ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies) の節を参照してください。

**手順 3:JDBC 設定の追加**

1. `<application folder>` 内の次のディレクトリに移動します。このディレクトリには、JDBC プールの OSGi 設定を配置する必要があります。

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**手順 4:Azure SQL 接続設定ファイルを作成する**

1. 次のファイルを作成します。

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. 次のコード行を追加します。

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   >
   >
   > `jdbc.username` を実際の Azure ユーザー名に、`jdbc.password` を実際の安全なパスワードに置き換えます。

**手順 5：変更をコミットしてプッシュする**

ターミナルを開き、次のコマンドを実行します。

```bash
git add .
git commit -m "<commit message>"
git push 
```

**手順 6:Cloud Manager パイプラインを使用して変更をデプロイする**

1. **AEM Cloud Manager** にログインします。
1. プロジェクトに移動し、パイプラインを実行して変更をデプロイします。

**手順 7：フォームデータモデル（FDM）の作成**

AEMと Azure のセットアップが完了し、コードの変更がデプロイされたら、以下の操作を実行します。

1. AEM オーサーインスタンスに移動します。
1. **ツール**/**Forms**/**Data Integrations** に移動します。
1. 新規 **フォームデータモデル** を作成します。
1. 「**データソース**」タブで、作成した JDBC 設定を選択します。
1. **[!UICONTROL 作成]** をクリックし、接続を確認します。

![フォームデータモデルを作成](/help/forms/assets/create-azure-sql-fdm.png)

**手順 8：作成した FDM をアダプティブフォームで使用する**

1. アダプティブフォームを編集モードで開きます。
1. 前の手順で作成した FDM をデータモデルとして選択します。
1. [ データバインディングを使用して、フォームフィールドを Azure SQL データソースに接続し ](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services) 送信アクションを設定します。

## ベストプラクティス

* **シークレット管理** を使用して、設定ファイルにパスワードをハードコーディングしないようにします。
* データベース資格情報を定期的にローテーションし、設定を安全に更新します。
* JDBC 接続ログを監視して、障害と待ち時間を確認します。
* SQL データベースとファイアウォール設定を保護するための Azure のベストプラクティスに従います。
* フォームアクセスには高権限のデータベースアカウントを使用しないでください。

## 関連記事

{{af-submit-action}}