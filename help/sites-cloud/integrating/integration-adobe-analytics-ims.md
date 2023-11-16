---
title: Adobe Analytics との統合時に使用する IMS 設定
description: Adobe Analytics との統合時に使用する IMS 設定について説明します
exl-id: 12bd1573-373a-4001-be71-c8f155ef6896
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 94%

---

# Adobe Analytics との統合時に使用する IMS 設定 {#ims-configuration-for-integration-with-adobe-analytics}

Analytics Standard API を使用して Adobe Experience Manager as a Cloud Service（AEMaaCS）と Adobe Analytics を統合するには、Adobe IMS（Identity Management System）を設定する必要があります。この設定は、Adobe Developer コンソールで行います。

>[!NOTE]
>
>AEMaaCS 2022.2.0 で、Adobe Analytics Standard API 2.0 のサポートが新しく追加されました。このバージョンの API は、IMS 認証をサポートしています。
>
>API の選択は、AEM／Analytics 統合に使用される認証方法によって決定されます。
>
>詳しくは、[2.0 API への移行](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/)でも参照できます。

## 前提条件 {#prerequisites}

この手順を開始する前に、以下を実行します。

* [アドビサポート](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html)は、次のアカウントをプロビジョニングする必要があります。

   * アドビコンソール
   * Adobe 開発者コンソール
   * Adobe Analytics と
   * Adobe IMS（Identity Management System）

* 組織のシステム管理者は、Admin Console を使用して、組織内で必要な開発者を関連する製品プロファイルに追加する必要があります。

   * これにより、Adobe Developer Console 使用して統合を有効にする権限が特定の開発者に付与されます。
   * 詳しくは、[開発者の管理](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)を参照してください。


## IMS 設定の指定 - 公開鍵の生成 {#configuring-ims-generating-a-public-key}

設定の最初の段階は、AEMで IMS 設定を作成し、公開鍵を生成することです。

1. AEM で、**ツール**&#x200B;メニューを開きます。
1. **セキュリティ**&#x200B;セクションで、**Adobe IMS 設定**&#x200B;を選択します。
1. **作成**&#x200B;を選択して、**Adobe IMS テクニカルアカウント設定**&#x200B;を開きます。
1. **クラウド設定**&#x200B;の下のドロップダウンを使用して、**Adobe Analytics** を選択します。
1. **新しい証明書の作成**&#x200B;をアクティブにして、新しいエイリアスを入力します。
1. 「**証明書の作成**」で確認します。

   ![証明書を作成](assets/integrate-analytics-ims-01.png)

1. **ダウンロード**（または&#x200B;**公開鍵のダウンロード**）を選択してファイルをローカルドライブにダウンロードし、[AEM との Adobe Analytics 統合用の IMS の設定](#configuring-ims-adobe-analytics-integration-with-aem)時に使用できるようにします。

   >[!CAUTION]
   >
   >この設定は、[AEM で IMS 設定を完了する](#completing-the-ims-configuration-in-aem)ときに再び必要になるため、開いたままにしてください。

   ![証明書をダウンロード](assets/integrate-analytics-ims-02.png)

## AEM との Adobe Analytics 統合用の IMS の設定 {#configuring-ims-adobe-analytics-integration-with-aem}

Adobe Developer Console を使用する場合は、Adobe Analytics でプロジェクト（統合）を作成し、AEM で使用するための権限を割り当てる必要があります。

### プロジェクトの作成 {#creating-the-project}

Adobe Developer Console を開いて、AEM が使用する Adobe Analytics でプロジェクトを作成します。

>[!CAUTION]
>
>現在、Adobe Developer Console の **サービスアカウント (JWT)** 資格情報のタイプ。
>
>次を使用しない **OAuth サーバー間通信** 秘密鍵証明書のタイプ。今後サポートされる予定です。

1. Adobe Developer Console を開いて、プロジェクトを表示します。

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 自分が持つプロジェクトが表示されます。**新規プロジェクトの作成**&#x200B;を選択 - 場所と使用方法は、以下に依存します。

   * まだプロジェクトがない場合は、「**新規プロジェクトを作成**」が中央の下に表示されます。
     ![新規プロジェクトの作成 - 最初のプロジェクト](assets/integration-analytics-ims-02.png)
   * 既存のプロジェクトがある場合は、それらがリストされ、「**新規プロジェクトを作成**」が右上に表示されます。
     ![新規プロジェクトの作成 - 複数のプロジェクト](assets/integration-analytics-ims-03.png)


1. **プロジェクトに追加**&#x200B;を選択し、続いて **API** を選択します。

   ![新しいプロジェクトの基本を学ぶ](assets/integration-analytics-ims-10.png)

1. **Adobe Analytics** を選択し、「**次へ**」を選択します。

   >[!NOTE]
   >
   >Adobe Analytics を購読しているが、リストに表示されない場合は、[前提条件](#prerequisites)を確認する必要があります。

   ![API を追加](assets/integration-analytics-ims-12.png)

1. 認証のタイプとして、「**サービスアカウント（JWT）**」を選択し、「**次へ**」をクリックして進みます。

   ![認証のタイプを選択](assets/integration-analytics-ims-12a.png)

1. **公開鍵**&#x200B;をアップロードして、完了したら&#x200B;**次へ**&#x200B;をクリックして進みます。

   ![公開鍵をアップロード](assets/integration-analytics-ims-13.png)

1. 資格情報を確認して、**次へ**&#x200B;をクリックして進みます。

   ![資格情報を確認](assets/integration-analytics-ims-15.png)

1. 必要な製品プロファイルを選択して、**設定済み API を保存**&#x200B;に進みます。

   ![必要な製品プロファイルを選択](assets/integration-analytics-ims-16.png)

1. 設定が完了しました。

### 統合への権限の割り当て {#assigning-privileges-to-the-integration}

次に、必要な権限を統合に割り当てる必要があります。

1. Adobe **Admin Console** を開きます。

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 上部のツールバーの&#x200B;**製品**&#x200B;に移動し、左のパネルから、**Adobe Analytics - &lt;*your-tenant-id*>**&#x200B;を選択します。
1. **製品プロファイル**&#x200B;を選択して、表示されるリストから必要なワークスペースを選択します（例：「デフォルトのワークスペース」）。
1. **API 資格情報**&#x200B;を選択して、必要な統合設定を選択します。
1. **製品の役割**&#x200B;として、**オブザーバー**&#x200B;の代わりに&#x200B;**編集者**&#x200B;を選択します。

## Adobe Developer Console 統合プロジェクト用に保存された詳細 {#details-stored-for-the-ims-integration-project}

Adobe Developer Console - プロジェクトから、すべての統合プロジェクトのリストを表示できます。

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

特定のプロジェクトエントリを選択して、設定の詳細を表示します。次のものが含まれます。

* プロジェクトの概要
* Insights
* 資格情報
   * サービスアカウント（JWT）
      * 資格情報の詳細
      * JWT の生成
* API
   * 例：Adobe Analytics

これらの一部は、IMS に基づいてAEMでAdobe Analyticsの統合を完了する必要があります。

## AEM での IMS 設定の完了 {#completing-the-ims-configuration-in-aem}

AEM に戻り、Analytics の IMS 統合から必要な値を追加して、IMS 設定を完了できます。

1. [AEM で IMS 設定を開く](#configuring-ims-generating-a-public-key)に戻ります。
1. 「**次へ**」を選択します。

1. ここで、[Adobe Developer Console のプロジェクト設定の詳細](#details-stored-for-the-ims-integration-project)を使用できます。

   * **タイトル**：テキスト。
   * **認証サーバー**：以下の&#x200B;**ペイロード**&#x200B;セクションの `aud` 行からこれをコピーして貼り付けます。例：以下の例では `https://ims-na1.adobelogin.com`　
   * **API キー**：これを[プロジェクトの概要](#details-stored-for-the-ims-integration-project)の「**資格情報**」セクションからコピーします。
   * **クライアント秘密鍵**：これを[「サービスアカウント（JWT）」セクションの「クライアント秘密鍵」タブ](#details-stored-for-the-ims-integration-project)で生成し、コピーします。
   * **ペイロード**：これを[「サービスアカウント（JWT）」セクションの「JWT を生成」タブ](#details-stored-for-the-ims-integration-project)からコピーします。

   ![AEM IMS 設定の詳細](assets/integrate-analytics-ims-10.png)

1. 「**作成**」で確定します。

1. Adobe Analytics の設定が AEM コンソールに表示されます。

   ![IMS 設定](assets/integrate-analytics-ims-11.png)

## IMS 設定の確認 {#confirming-the-ims-configuration}

設定が期待どおりに動作していることを確認するには：

1. 次を開きます。

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   次に例を示します。

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. 設定を選択します。
1. ツールバーから&#x200B;**ヘルスチェック**&#x200B;を選択し、次に&#x200B;**チェック**&#x200B;を選択します。

   ![IMS 設定 - ヘルスチェック](assets/integrate-analytics-ims-12.png)

1. 成功した場合は、確認メッセージが表示されます。

## Adobe Analytics との統合の完了 {#complete-the-integration-with-adobe-analytics}

これで、この IMS 設定を使用して [Adobe Analytics との統合](/help/sites-cloud/integrating/integrating-adobe-analytics.md)を完了できます。

<!--
## Configuring the Adobe Analytics Cloud Service {#configuring-the-adobe-analytics-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Analytics Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Analytics** and select **Configure now**.

   The **Create Configuration** dialog opens.

1. Enter a **Title** and, if you want, a **Name** (if left blank, it is generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog opens.

1. Enter the details in the **Analytics Settings** tab:

    * **Authentication**: IMS

    * **IMS Configuration**: select the name of the IMS Configuration

1. Click **Connect to Analytics** to initialize the connection with Adobe Analytics.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message.

1. Complete other parameters as required, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding an Analytics Framework](/help/sites-administering/adobeanalytics-connect.md) to configure parameters that are sent to Adobe Analytics. 
-->
