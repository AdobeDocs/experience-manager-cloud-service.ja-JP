---
title: インストール [!DNL Workfront for Experience Manager enhanced connector]
description: インストール [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: a5776453b261e6f4e6c891763934b236bade8f7f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# インストール [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

で管理者アクセス権を持つユーザー [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 拡張コネクタをインストールします。 インストールする前に、プラットフォームのサポートとその他を確認してください [コネクタの前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>Adobeには、 [!DNL Adobe Workfront for Experience Manager enhanced connector] 認定パートナーまたは [!DNL Adobe Professional Services]. 認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobeではサポートされません。
>
>Adobeが次の更新をリリースする可能性がある： [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] このコネクタを冗長にするこの場合、お客様はこのコネクタの使用から移行する必要が生じる場合があります。

コネクタをインストールする前に、次のプリインストール手順に従います。

1. [ファイアウォールの設定](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). の IP クラスタを知るには、以下を実行します。 [!DNL Workfront]に移動します。 [!UICONTROL 設定] > [!UICONTROL システム] > [!UICONTROL 顧客情報].

1. Dispatcher で、という名前の HTTP ヘッダーを許可します。 `authorization`, `username`、および `apikey`. 許可 `GET`, `POST`、および `PUT` リクエスト： `/bin/workfront-tools`.

1. 次のパスがに存在しないことを確認してください。 [!DNL Experience Manager] リポジトリ：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. このインストールでは、で Maven プロジェクトを設定するための知識が必要です。 [!DNL Experience Manager] as a [!DNL Cloud Service]. Maven プロジェクトにサードパーティパッケージを含める方法については、次のリソースを参照してください。

   * [Maven プロジェクトにサードパーティパッケージを含める](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [でのデプロイ [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja).

アドオンをインストールするには、以下を実行します。 [!DNL Experience Manager] as a [!DNL Cloud Service]を使用する場合は、次の手順に従います。

1. から拡張コネクタをダウンロード [Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [アクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) Cloud Manager からAEM as a Cloud Serviceリポジトリのクローンを作成します。

1. 任意の IDE を使用して、クローンされたAEMas a Cloud Serviceリポジトリを開きます。

1. 手順 1 でダウンロードした拡張コネクタ zip ファイルを次のパスに配置します。

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >この `resources` フォルダーが存在しません。フォルダーを作成します。


1. 追加 `pom.xml` 依存関係：

   1. 親に依存関係を追加 `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >依存関係を親にコピーする前に、拡張コネクタのバージョン番号を必ず更新してください `pom.xml`.

   1. 依存関係をに追加 `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. 追加 `pom.xml` 埋め込み を [!DNL Workfront for Experience Manager enhanced connector] パッケージ `embeddeds` セクション `pom.xml` すべてのサブプロジェクトの すべてのモジュールに組み込まれている必要がある `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   埋め込みセクションのターゲットが `/apps/<path-to-project-install-folder>/install`. この JCR パス `/apps/<path-to-project-install-folder>` を `all/src/main/content/META-INF/vault/filter.xml` ファイル。 リポジトリのフィルター規則は、通常、プログラム名から派生します。 フォルダーの名前を既存のルールのターゲットとして使用します。

1. 変更をリポジトリにプッシュします。

1. 次の場所にパイプラインを実行 [Cloud Manager に変更をデプロイします。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. システムユーザー設定を作成するには、 `wf-workfront-users` in [!DNL Experience Manager] ユーザーグループと権限の割り当て `jcr:all` から `/content/dam`. システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。 からのすべてのユーザー [!DNL Workfront] 拡張コネクタを使用するユーザーは、このグループの一部として自動的に追加されます。

## 次の間の接続を設定 [!DNL Experience Manager] as a [!DNL Cloud Service] および [!DNL Workfront] {#configure-connection}

との接続を作成するには [!DNL Workfront]を使用する場合は、次の手順に従います。

1. In [!DNL Experience Manager]を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. 選択 `workfront-tools` を選択し、 **[!UICONTROL 作成]** 」オプションを使用して、ページの右上に表示されます。

1. 内 **[!UICONTROL Workfront Connection]** ダイアログで、 [!DNL Workfront] 配置、選択 **[!UICONTROL Workfrontに接続]** オプション。 正常に接続されると、 [!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境。

   ![接続 [!DNL Experience Manager] および [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 次に移動： **[!UICONTROL 詳細]** 」タブに移動してオプションを選択します。 **[!UICONTROL Server AEM as a Cloud Service]**.
