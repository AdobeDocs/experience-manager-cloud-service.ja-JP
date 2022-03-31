---
title: Adobe Targetとの統合時に使用する IMS 設定
description: Adobe Targetとの統合時に使用する IMS 設定について説明します
source-git-commit: 444673c443d048db16e6ebc196b1498f553ef07b
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 4%

---

# Adobe Targetとの統合時に使用する IMS 設定{#ims-configuration-for-integration-with-adobe-target}

Target Standard API を使用してAEMとAdobe Targetを統合するには、Adobe IMS(Identity Managementシステム ) の設定が必要です。 この設定は、開発者コンソールでAdobeで実現します。

>[!NOTE]
>
>AEMaaCS では、Adobe Target Standard API のサポートが新しく追加されました。 Target Standard API は IMS 認証を使用します。
>
>API の選択は、AEM/Target 統合に使用される認証方法によって実行されます。

## 前提条件 {#prerequisites}

この手順を開始する前に、以下を実行します。

* [Adobeサポート](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) は次のアカウントをプロビジョニングする必要があります。

   * Adobeコンソール
   * Adobe 開発者コンソール
   * Adobe Targetと
   * Adobe IMS(Identity Management System)

* 組織のシステム管理者は、Admin Consoleを使用して、組織内の必要な開発者を関連する製品プロファイルに追加する必要があります。

   * これにより、特定の開発者に、開発者コンソールを使用して統合を有効にする権限をAdobeに与えます。
   * 詳しくは、 [開発者の管理](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## IMS 設定の指定 — 公開鍵の生成 {#configuring-an-ims-configuration-generating-a-public-key}

設定の最初の段階は、AEMで IMS 設定を作成し、公開鍵を生成することです。

1. AEMで、 **ツール** メニュー
1. 内 **セキュリティ** セクション選択 **Adobe IMS設定**.
1. 選択 **作成** 開く **Adobe IMSテクニカルアカウント設定**.
1. 下のドロップダウンを使用 **クラウド設定**&#x200B;を選択します。 **Adobe Target**.
1. 有効化 **新しい証明書を作成** 新しいエイリアスを入力します。
1. 次で確認： **証明書を作成**.

   ![証明書を作成](assets/integrate-target-ims-01.png)

1. 選択 **ダウンロード** ( または **公開鍵をダウンロード**) をクリックして、ファイルをローカルドライブにダウンロードし、 [AEMとのAdobe Target統合用の IMS の設定](#configuring-ims-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >この設定を開いたままにします。 [AEMでの IMS 設定の完了](#completing-the-ims-configuration-in-aem).

   ![証明書をダウンロード](assets/integrate-target-ims-02.png)

## AEMとのAdobe Target統合用の IMS の設定 {#configuring-ims-adobe-target-integration-with-aem}

Adobe開発者コンソールプロジェクト（統合）とAdobe Target(AEMで使用する ) を組み合わせ、必要な権限を割り当てます。

### プロジェクトの作成 {#creating-the-project}

Adobe開発者コンソールを開き、AEMが使用するAdobe Targetでプロジェクトを作成します。

1. プロジェクト用のAdobe開発者コンソールを開きます。

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 既に作成したプロジェクトが表示されます。 選択 **新規プロジェクトを作成**  — 場所と使用方法は、次のものに依存します。

   * まだプロジェクトがない場合は、 **新規プロジェクトを作成** 中央、下に配置します。
      ![新規プロジェクトを作成 — 最初のプロジェクト](assets/integration-target-ims-02.png)
   * 既存のプロジェクトがある場合は、それらがリストされ、 **新規プロジェクトを作成** が右上に表示されます。
      ![新規プロジェクトを作成 — 複数のプロジェクト](assets/integration-target-ims-03.png)


1. 選択 **プロジェクトに追加** 続いて **API**:

   ![プロジェクトに追加](assets/integration-target-ims-10.png)

1. 選択 **Adobe Target**&#x200B;を、 **次へ**:

   >[!NOTE]
   >
   >Adobe Targetを購読しているが、リストに表示されない場合は、 [前提条件](#prerequisites).

   ![](assets/integration-target-ims-12.png)

1. **公開鍵をアップロード**&#x200B;をクリックし、完了したら次の操作を続行します。 **次へ**:

   ![公開鍵をアップロード](assets/integration-target-ims-13.png)

1. 資格情報を確認し、次に進みます。 **次へ**:

   ![資格情報の確認](assets/integration-target-ims-15.png)

1. 必要な製品プロファイルを選択し、次に進みます。 **設定済み API を保存**:

   >[!NOTE]
   >
   >と共に表示される製品プロファイルは、次の条件によって異なります。
   >
   >* Adobe Target Standard — のみ **デフォルトのワークスペース** 使用可能な
   >* Adobe Target Premium — 使用可能なすべてのワークスペースが、次に示すようにリストされます


   ![製品プロファイルを選択し、設定済み API を保存する](assets/integration-target-ims-16.png)

1. 作成が確定されます。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-ims-07.png)
-->

<!-- could not verify - only saw Adobe Target Classic -->

### 統合への権限の割り当て {#assigning-privileges-to-the-integration}

次に、必要な権限を統合に割り当てる必要があります。

1. Adobeを開く **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. に移動します。 **製品** （上部のツールバー）、「 **Adobe Target - &lt;*your-tenant-id*>** （左のパネルから）。
1. 選択 **製品プロファイル**&#x200B;を選択し、表示されるリストから必要なワークスペースを選択します。 例えば、「デフォルトのワークスペース」などです。
1. 選択 **API 資格情報**&#x200B;を選択し、必要な統合設定を選択します。
1. 選択 **編集者** を **製品の役割**;の代わりに **監視者**.

## 開発者コンソール統合プロジェクト用にAdobeされた詳細 {#details-stored-for-the-ims-integration-project}

Adobe開発者コンソールのプロジェクトコンソールで、すべての統合プロジェクトのリストを表示できます。

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

選択 **表示** （特定のプロジェクトエントリの右側）をクリックして、設定に関する詳細を表示します。 次の機能が含まれます。

* プロジェクトの概要
* インサイト
* 秘密鍵証明書
   * サービスアカウント (JWT)
      * 資格情報の詳細
      * JWT を生成
* API
   * 例： Adobe Target

これらの一部は、IMS に基づいてAEMでAdobe Targetの統合を完了する必要があります。

## AEMでの IMS 設定の完了 {#completing-the-ims-configuration-in-aem}

AEMに戻ると、Target の IMS 統合から必要な値を追加することで、IMS 設定を完了できます。

1. に戻る [AEMで IMS 設定を開く](#configuring-an-ims-configuration-generating-a-public-key).
1. 「**次へ**」を選択します。

1. ここで、 [Adobe開発者コンソールのプロジェクト設定の詳細](#details-stored-for-the-ims-integration-project):

   * **タイトル**:テキスト。
   * **認証サーバー**:次の場所からコピー&amp;ペースト `aud` 行 **ペイロード** の下のセクション、例： `https://ims-na1.adobelogin.com` 以下の例では
   * **API キー**:これをプロジェクトからコピー [概要](#details-stored-for-the-ims-integration-project) セクション
   * **クライアント秘密鍵**:プロジェクトで生成 [概要](#details-stored-for-the-ims-integration-project) セクションとコピー
   * **ペイロード**:これを [JWT を生成](#details-stored-for-the-ims-integration-project) セクション

   ![Adobe IMS テクニカルアカウント設定](assets/integrate-target-ims-10.png)

1. 「**作成**」で確定します。

1. Adobe Targetの設定がAEMコンソールに表示されます。

   ![IMS 設定](assets/integrate-target-ims-11.png)

## IMS 設定の確認 {#confirming-the-ims-configuration}

設定が期待どおりに動作していることを確認するには：

1. 次を開きます。

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   次に例を示します。

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 設定を選択します。
1. 選択 **ヘルスチェック** ツールバーから、 **チェック**.

   ![正常性をチェック](assets/integrate-target-ims-12.png)

1. 成功した場合は、確認メッセージが表示されます。

## Adobe Targetとの統合の完了 {#complete-the-integration-with-adobe-target}

これで、この IMS 設定を使用して [Adobe Targetとの統合](/help/sites-cloud/integrating/integrating-adobe-target.md).

<!--

## Configuring the Adobe Target Cloud Service {#configuring-the-adobe-target-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Target Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Target** and select **Configure now**.

   The **Create Configuration** dialog will open.

1. Enter a **Title** and, if you want, a **Name** (if left blank this will be generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog will open.

1. Enter the details in the **Adobe Target Settings** tab:

    * **Authentication**: IMS

    * **Client Code**: See the [Tenant ID and Client Code](#tenant-client) section.

    * **Tenant ID**: the Adobe IMS Tenant ID. See also the [Tenant ID and Client Code](#tenant-client) section.

      >[!NOTE]
      >
      >For IMS this value needs to be taken from Target itself. You can log into Target and extract the Tenant ID from the URL.
      >
      >For example, if the URL is:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Then you would use `yourtenantid`.

    * **IMS Configuration**: select the name of the IMS Configuration

    * **API Type**: REST

    * **A4T Analytics Cloud Configuration**: Select the Analytics cloud configuration that is used for target activity goals and metrics. You need this if you are using Adobe Analytics as the reporting source when targeting content.   

      <!--
      If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
      -- >

    * **Use accurate targeting**: By default this check box is selected. If selected, the cloud service configuration will wait for the context to load before loading content. See note that follows.

    * **Synchronize segments from Adobe Target**: Select this option to download segments that are defined in Target to use them in AEM. You must select this option when the API Type property is REST, because inline segments are not supported and you always need to use segments from Target. (Note that the AEM term of 'segment' is equivalent to the Target 'audience'.)

    * **Client library**: Select whether you want the AT.js client library, or mbox.js (deprecated).

    * **Use Tag Management System to deliver client library**: Use DTM (deprecated), Adobe Launch or any other tag management system.

    * **Custom AT.js**: Leave blank if you checked the Tag Management box or to use the default AT.js. Alternatively upload your custom AT.js. Only appears if you have selected AT.js.

   <!--
   >[!NOTE]
   >
   >[Configuration of a Cloud Service to use the Target Classic API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) has been deprecated (uses the Adobe Recommendations Settings tab).
   -- >

1. Click **Connect to Adobe Target** to initialize the connection with Adobe Target.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding a Target Framework](/help/sites-administering/target-configuring.md#adding-a-target-framework) to configure ContextHub or ClientContext parameters that will be sent to Target. Note this may not be required for exporting AEM Experience Fragments to Target.

### Tenant ID and Client Code {#tenant-client}

With [Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md), the Client Code field had been added to the Target configuration window.

When configuring the Tenant ID and Client Code fields, please be aware of that for most customers, the **Tenant ID** and the **Client Code** are the same. This means that both fields contain the same information and are identical. Make sure you enter the Tenant ID in both fields.

>[!NOTE]
>
>For legacy purposes, you can also enter different values in the Tenant ID and the Client Code fields.

In both cases, be aware that:

* By default, the Client Code (if added first) will also be automatically copied into the Tenant ID field.
* You have the option to change the default Tenant ID set.
* Accordingly, the backend calls to Target will be based on the **Tenant ID** and the client side calls to Target will be based on the **Client Code**.

As stated previously, the default case is the most common for AEM as a Cloud Service. Either way, make sure **both** fields contain the correct information depending on your requirements.

>[!NOTE]
>
> If you want to change an existing Target Configuration:
>
> 1. Re-enter the Tenant ID.
> 2. Re-connect to Target.
> 3. Save the configuration.
-->
