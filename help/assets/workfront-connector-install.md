---
title: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
description: ' [!DNL Workfront for Experience Manager enhanced connector] のインストール'
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 6e1408abde71c5400adaeaea130e4b7f9287169a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Workfront for Experience Manager enhanced connector] のインストール {#assets-integration-overview}

拡張コネクタのインストールは、[!DNL Cloud Service] として [!DNL Adobe Experience Manager] への管理者アクセス権を持つユーザーが行います。インストールする前に、プラットフォームのサポートとコネクタのその他の [前提条件](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience) を確認してください。

>[!IMPORTANT]
>
>* Adobeは、認定パートナーまたは [!DNL Adobe Professional Services] を介してのみ [!DNL Adobe Workfront for Experience Manager enhanced connector] のデプロイメントと構成を必要とします。認定パートナーなしでデプロイおよび設定した場合、または [!DNL Adobe Professional Services]の場合、Adobe ではサポートされません。
>
>* アドビは、このコネクターを冗長にする[!DNL Adobe Workfront]および [!DNL Adobe Experience Manager] の更新をリリースする可能性があります。この場合、お客様はこのコネクターの使用から移行する必要が生じることがあります。
>
>* Adobeは、拡張コネクタバージョン 1.7.4 以降をサポートしています。 以前のプレリリースおよびカスタムバージョンはサポートされていません。 拡張コネクタのバージョンを確認するには、次の手順 5(a) を参照してください： [コネクタのインストール手順の強化](workfront-connector-install.md).
>
>* 詳しくは、[Workfront for Experience Manager Assets 拡張コネクタに関するパートナー認定試験](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)を参照してください。試験について詳しくは、 [試験ガイド](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


コネクタをインストールする前に、次のプリインストール手順に従います。

1. [ファイアウォールの設定](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html?lang=ja)。[!DNL Workfront] の IP クラスターを調べるには、[!UICONTROL 設定]／[!UICONTROL システム]／[!UICONTROL 顧客情報]に移動します。

1. Dispatcher で、`authorization`、`username` および `apikey` という名前の HTTP ヘッダーを許可します。`/bin/workfront-tools` への `GET`、`POST` および `PUT` リクエストを許可します。

1. 次のパスが [!DNL Experience Manager] リポジトリーに存在しないことを確認します。

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. このインストールを行うには、[!DNL Experience Manager] の Maven プロジェクトを [!DNL Cloud Service] として設定するための知識が必要です。次のリソースを使用して、Maven プロジェクトにサードパーティパッケージを含める方法を理解します。

   * [Maven プロジェクトにサードパーティパッケージを含める](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=ja#including-third-party)。
   * [でのデプロイ [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=ja)。

アドオンを [!DNL Experience Manager] に [!DNL Cloud Service] としてインストールするには、次の手順に従います。

1. [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aemcloud.html?package=/content/software-distribution/ja/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip)から拡張コネクタをダウンロードします。

1. Cloud Manager から AEM as a Cloud Service リポジトリーに[アクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=ja)し、クローンを作成します。

1. 任意の IDE を使用して、AEM as a Cloud Service リポジトリーのクローンを開きます。

1. 手順 1 でダウンロードした拡張コネクタの zip ファイルを次のパスに配置します。

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >`resources` フォルダーが存在しない場合は作成します。


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
      >依存関係を親 `pom.xml` にコピーする前に、拡張コネクタのバージョン番号を必ず更新してください。

   1. `all module pom.xml` に依存関係を追加します。

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

   埋め込みセクションのターゲットが `/apps/<path-to-project-install-folder>/install` に設定されます。JCR パス `/apps/<path-to-project-install-folder>` を、`all/src/main/content/META-INF/vault/filter.xml` ファイルのフィルタールールに含める必要があります。リポジトリーのフィルタールールは、通常、プログラム名から派生します。フォルダーの名前を既存ルールのターゲットとして使用します。

1. 変更をリポジトリーにプッシュします。

1. パイプラインを実行して、[変更内容を Cloud Manager にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja)します。

1. システムユーザー設定を作成するには、[!DNL Experience Manager] ユーザーグループに `wf-workfront-users` を作成し、権限 `jcr:all` を `/content/dam` に割り当てます。システムユーザー `workfront-tools` が自動的に作成され、必要な権限が自動的に管理されます。拡張コネクタを使用する [!DNL Workfront] のすべてのユーザーは、このグループの一員として自動的に追加されます。

以前のバージョンから最新のバージョンに [!DNL Workfront for Experience Manager enhanced connector] を更新するための情報は、[こちら](update-workfront-enhanced-connector.md)にあります。

## [!DNL Experience Manager] 間の接続を [!DNL Cloud Service] と [!DNL Workfront] のように設定します。 {#configure-connection}

[!DNL Workfront] との接続を作成するには、次の手順に従います。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL Workfront ツール設定]** を選択します。 

1. 左パネルで `workfront-tools` を選択し、ページの右上の領域にある「**[!UICONTROL 作成]** 」オプションを選択します。

1. **[!UICONTROL Workfront 接続]**&#x200B;ダイアログで、[!DNL Workfront] デプロイメントの必須の詳細事項を入力して、「**[!UICONTROL Workfront に接続]**」オプションを選択します。正常に接続されると、[!DNL Workfront] ドキュメントのカスタム統合が [!DNL Workfront] 環境に自動的に作成されます。

   ![[!DNL Experience Manager] と [!DNL Workfront]](/help/assets/assets/wf-connection-config.png) の接続

1. 「**[!UICONTROL 詳細]**」タブに移動し、「**[!UICONTROL Is the Server AEM as a Cloud Service]**」オプションを選択します。
