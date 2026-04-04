---
title: AEM アダプティブ FormsとAzure SQL ストレージを連携する方法
description: AEM FormsでAzure SQL Database接続を設定し、アダプティブFormsと統合して、JDBCを使用して効率的にデータを保存または取得する方法を説明します。
deywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="AEM Formsに適用）。"
exl-id: 111accf7-bf34-499c-832e-c001ea68f6d3
source-git-commit: e69201c40b72f4eaabe3da634ecf05bd04769f6b
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 15%

---

# アダプティブフォームをAzure SQL ストレージに接続する

Adobe Experience Manager（AEM）のアダプティブ Formsは、外部データベースと統合して、データを保存または取得できます。
この記事では、AEM as a Cloud Serviceを介してJDBCを使用してアダプティブフォームをAzure SQL データベースに接続する方法について説明します。

>[!NOTE]
> 
> このガイドは、高度なネットワーク機能が有効になっているサンドボックス以外のAEM as a Cloud Service環境に適用されます。

## メリット

アダプティブ FormsとAzure SQLを統合すると、次のようなメリットが得られます。

* **リアルタイム データ操作：** フォームとAzure データベース間のデータのライブ読み取りと書き込みを有効にします。
* **スケーラビリティ：** Azure SQLは、エンタープライズ レベルのアプリケーションに適したスケーラブルなデータベース パフォーマンスを提供します。
* **一元的なデータ保存：** フォーム送信と取得したデータを一元的な場所に安全に保存します。
* **セキュリティ コンプライアンス：** Azureの組み込みのネットワーク、ファイアウォール、暗号化オプションを活用して、安全なコミュニケーションを実現します。
* **クラウドネイティブ統合：** AEM as a Cloud Serviceを使用した最新のクラウドファーストアーキテクチャに最適です。

## 前提条件

* [Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal)を作成し、**プロキシ接続**&#x200B;が有効になっていることを確認します。

  >[!NOTE]
  >
  > `Azure Portal → SQL Server → Security → Networking → Connectivity`に移動して&#x200B;**プロキシ接続**&#x200B;を有効にします。

  ![Azure Dbを作成](/help/forms/assets/create-azure-db.png)

* 作成したAzure データベースの専用エグレス IP[を使用して設定された](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address)高度なネットワークを有効にします。

  >[!NOTE]
  >
  >    専用エグレス IPを有効にした後。 `Azure Portal → SQL Server → Security → Networking → Public Access`に移動し、エグレス IPをファイアウォール ルールに追加します。

  ![エグレス IP](/help/forms/assets/cretae-azure-db-egress-ip.png)

* クラウド環境でのポート転送を次のように設定します。
   * **portOrigin**: `30000–30999`の間
   * **portDest**: `1433` （Azure SQLのデフォルトポート）
例：`portOrigin: 30433 → portDest: 1433`

     >[!NOTE]
     > 
     > Adobe Cloud Manager サポートに連絡して、ポート転送を設定できます。


## アダプティブ FormsをAzure SQLに接続する手順

**手順1: AEM as a Cloud Service Git リポジトリを複製**

1. コマンドラインを開き、AEM as a Cloud Service リポジトリを保存するディレクトリ（例：`/cloud-service-repository/`）を選択します。

1. 次のコマンドを実行して、リポジトリのクローンを作成します。

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **この情報はどこにありますか？**

   これらの詳細を見つける手順について詳しくは、Adobe Experience League の記事「[Git へのアクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=ja#accessing-git)」を参照してください。

   コマンドが正常に完了すると、ローカルディレクトリに新しいフォルダーが作成されます。このフォルダーは、アプリケーションの名前にちなんで作成されます。

1. エディターでリポジトリフォルダーを開きます。

**手順2：必要なJARを追加**

[ パッケージを使用して、AEM プロジェクトに](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true)SQL ドライバー依存関係`all`を含めます。

>[!NOTE]
>
> プロジェクトにSQL依存関係を含めるには、[SQL ドライバーの依存関係](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies)の節を参照してください。

**手順3: JDBC設定を追加**

1. JDBC プールのOSGi設定を配置する`<application folder>`内の次のディレクトリに移動します。

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**手順4: Azure SQL Connection Configuration ファイルを作成する**

1. ファイルを作成します。

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. 以下のコード行を追加します。

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

   >[!NOTE]
   >
   > `jdbc.username`を実際のAzureのユーザー名に、`jdbc.password`を実際のセキュアパスワードに置き換えます。

**手順5：変更をコミットしてプッシュ**

ターミナルを開き、次のコマンドを実行します。

```bash
git add .
git commit -m "<commit message>"
git push 
```

**手順6: Cloud Manager パイプラインを介した変更内容のデプロイ**

1. **AEM Cloud Manager**&#x200B;にログインします。
1. プロジェクトに移動し、パイプラインを実行して変更をデプロイします。

**手順7: フォームデータモデル （FDM）の作成**

AEMとAzureの設定が完了し、コードの変更がデプロイされると、次のようになります。

1. AEM オーサーインスタンスに移動します。
1. **ツール** > **Forms** > **データインテグレーション**&#x200B;に移動します。
1. 新しい&#x200B;**フォームデータモデル**&#x200B;を作成します。
1. 「**データソース**」タブで、作成したJDBC設定を選択します。
1. 「**[!UICONTROL 作成]**」をクリックし、接続を確認します。

![フォームデータモデルを作成](/help/forms/assets/create-azure-sql-fdm.png)

**手順8：作成したFDMをアダプティブフォームで使用**

1. アダプティブフォームを編集モードで開きます。
1. 前の手順で作成したFDMをデータモデルとして選択します。
1. [ データバインディングを使用して、フォームフィールドをAzure SQL データソース ](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services)に接続し、送信アクションを設定します。

## ベストプラクティス

* **シークレット管理**&#x200B;を使用して、設定ファイル内のパスワードをハードコーディングしないようにします。
* データベースの資格情報を定期的にローテーションし、設定を安全に更新します。
* JDBC接続ログでエラーと遅延を監視します。
* SQL データベースとファイアウォール設定を保護するためのAzureのベストプラクティスに従います。
* フォームアクセスに高権限のデータベースアカウントを使用することは避けてください。

## 関連記事

{{af-submit-action}}
