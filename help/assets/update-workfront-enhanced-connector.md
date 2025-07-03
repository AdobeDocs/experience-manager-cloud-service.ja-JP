---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '226'
ht-degree: 100%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] を使用すると、以前のバージョンから最新のバージョンに [!DNL Workfront for Experience Manager enhanced connector] をアップデートできます。

>[!TIP]
>
>[!DNL Workfront for Experience Manager enhanced connector] の AEM 6.5 向けドキュメントをお探しですか？[ここをクリック](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=ja##update-enhanced-connector-for-workfront)してください。


[!DNL Workfront for Experience Manager enhanced connector] を最新バージョンにアップデートするには：

1. [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aemcloud.html?package=/content/software-distribution/ja/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip)から拡張コネクタの最新バージョンをダウンロードします。

1. Cloud Manager から AEM as a Cloud Service リポジトリーに[アクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=ja)し、クローンを作成します。

1. 任意の IDE を使用して、Experience Manager as a Cloud Service リポジトリーのクローンを開きます。

1. 手順 1 でダウンロードした拡張コネクタの zip ファイルを次のパスに配置します。

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >`resources` フォルダーが存在しない場合は作成します。

1. 親 `pom.xml`.の拡張コネクタのバージョンを更新します。

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. `all module pom.xml` の依存関係を更新します。

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >手順 5 と手順 6 の依存関係に、`<scope>` および `<systemPath>` を追加します。

1. `pom.xml` 埋め込みを更新します。すべてのサブプロジェクトの `pom.xml` の `embeddeds` セクションに [!DNL Workfront for Experience Manager enhanced connector] パッケージを追加します。すべてのモジュール `pom.xml` に更新を組み込みます。

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

1. [Hoodoo 配布ポイントの依存関係を削除します](remove-external-dependencies.md)（存在する場合）。

1. 変更をリポジトリーにプッシュします。

1. パイプラインを実行して、[変更内容を Cloud Manager にデプロイ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=ja)します。
