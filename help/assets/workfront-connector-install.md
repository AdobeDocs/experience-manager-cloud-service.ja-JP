---
title: インストール [!DNL Workfront for Experience Manager enhanced connector]
description: インストール [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 34f3cf925a3ea58de176521be459a61f4317eec3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 67%

---

# [!DNL Workfront for Experience Manager enhanced connector] のインストール {#assets-integration-overview}

拡張コネクタのインストールは、[!DNL Cloud Service] として [!DNL Adobe Experience Manager] への管理者アクセス権を持つユーザーが行います。インストールする前に、プラットフォームのサポートとコネクタのその他の [前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience) を確認してください。

>[!IMPORTANT]
>
>アドビは、[!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと設定を、認定パートナーまたは [!DNL Adobe Professional Services] を通じてのみ行うことを求めています。認定パートナーまたは [!DNL Adobe Professional Services] 以外がデプロイと設定を行った場合は、アドビのサポート対象外となります。
>
>アドビは、このコネクタを冗長にする [!DNL Adobe Workfront] および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクタの使用から移行する必要が生じることがあります。

コネクタをインストールする前に、次のプリインストール手順に従います。

1. [ファイアウォールの設定](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html?lang=ja)。[!DNL Workfront] の IP クラスターを調べるには、[!UICONTROL 設定]／[!UICONTROL システム]／[!UICONTROL 顧客情報]に移動します。

1. Dispatcher で、`authorization`、`username` および `apikey` という名前の HTTP ヘッダーを許可します。`GET`、`POST` および `PUT` リクエストを `/bin/workfront-tools` に許可します。

1. 次のパスが [!DNL Experience Manager] リポジトリに存在しないことを確認します。

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. このインストールを行うには、[!DNL Experience Manager] の Maven プロジェクトを [!DNL Cloud Service] として設定するための知識が必要です。次のリソースを使用して、Maven プロジェクトにサードパーティパッケージを含める方法を理解します。

   * [Maven プロジェクトにサードパーティパッケージを含める](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#including-third-party)。
   * [でのデプロイ [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)。

アドオンを [!DNL Experience Manager] に [!DNL Cloud Service] としてインストールするには、次の手順に従います。

1. から拡張コネクタをダウンロード [Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [アクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) Cloud Manager からAEM as a Cloud Serviceリポジトリのクローンを作成します。

1. 任意の IDE を使用して、クローンされたAEMas a Cloud Serviceリポジトリを開きます。

1. 手順 1 でダウンロードした拡張コネクタ zip ファイルを次のパスに配置します。

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >この `resources` フォルダーが存在しません。フォルダーを作成します。


1. `pom.xml` 依存関係を追加します。

   1. 親 `pom.xml` に依存関係を追加します。

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


1. `pom.xml` 埋め込みを追加します。すべてのサブプロジェクトの `pom.xml` の `embeddeds` セクションに [!DNL Workfront for Experience Manager enhanced connector] パッケージを追加します。すべてのモジュール `pom.xml` に組み込む必要があります。

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

1. システムユーザー設定を作成するには、[!DNL Experience Manager] ユーザーグループに `wf-workfront-users` を作成し、権限 `jcr:all` を `/content/dam` に割り当てます。システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。拡張コネクタを使用する [!DNL Workfront] のすべてのユーザーは、このグループの一員として自動的に追加されます。

## [!DNL Experience Manager] 間の接続を [!DNL Cloud Service] と [!DNL Workfront] のように設定します。 {#configure-connection}

[!DNL Workfront] との接続を作成するには、次の手順に従います。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Workfront ツール設定]** を選択します。 

1. 左側のパネルで `workfront-tools` を選択し、ページの右上の領域で **[!UICONTROL 作成]** オプションを選択します。

1. **[!UICONTROL Workfront 接続]** ダイアログで、[!DNL Workfront] デプロイメントに必要な詳細を入力し、 **[!UICONTROL Workfront への接続]** オプションを選択します。正常に接続すると、[!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境に自動作成されます。

   ![[!DNL Experience Manager] と [!DNL Workfront]](/help/assets/assets/wf-connection-config.png) の接続

1. 「**[!UICONTROL 詳細]**」タブに移動し、「**[!UICONTROL Is the Server AEM as a Cloud Service]**」オプションを選択します。
