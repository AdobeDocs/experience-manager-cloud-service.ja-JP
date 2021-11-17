---
title: インストール [!DNL Workfront for Experience Manager enhanced connector]
description: インストール [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8ca25f86a8d0d61b40deaff0af85e56e438efbdc
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 2%

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

1. 追加 `pom.xml` 依存関係：

   1. 親に依存関係を追加 `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. すべてのモジュールに依存関係を追加 [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. 追加 `pom.xml` 認証。

   1. 以下のリポジトリ設定を adobe-public プロファイル内の pom.xml に含めると、（上記の）コネクタの依存関係を（ローカルでも Cloud Manager でも）ビルド時に解決できます。 リポジトリアクセスの資格情報は、ライセンスの購入時に提供されます。 資格情報は、servers セクションの settings.xml ファイルに追加する必要があります。

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. という名前のファイルを作成します。 `./cloudmanager/maven/settings.xml` 」と入力します。 パスワードで保護された Maven リポジトリをサポートするには、 [プロジェクトの設定方法](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). また、例 `settings.xml` ファイルを参照してください。 最後に、ローカルの `settings.xml` ローカルでコンパイルする場合。

      ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
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

1. システムユーザー設定を作成するには、 `wf-workfront-users` in [!DNL Experience Manager] ユーザーグループと権限の割り当て `jcr:all` から `/content/dam`. システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。 からのすべてのユーザー [!DNL Workfront] 拡張コネクタを使用するユーザーは、このグループの一部として自動的に追加されます。

## 次の間の接続を設定 [!DNL Experience Manager] as a [!DNL Cloud Service] および [!DNL Workfront] {#configure-connection}

との接続を作成するには [!DNL Workfront]を使用する場合は、次の手順に従います。

1. In [!DNL Experience Manager]を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront Tools Configuration]**.

1. 選択 `workfront-tools` を選択し、 **[!UICONTROL 作成]** 」オプションを使用して、ページの右上に表示されます。

1. 内 **[!UICONTROL Workfront Connection]** ダイアログで、 [!DNL Workfront] 配置、選択 **[!UICONTROL Workfrontに接続]** オプション。 正常に接続されると、 [!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境。

   ![接続 [!DNL Experience Manager] および [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 次に移動： **[!UICONTROL 詳細]** 」タブに移動してオプションを選択します。 **[!UICONTROL Server AEM as a Cloud Service]**.
