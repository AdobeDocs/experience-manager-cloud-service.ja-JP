---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 34f3cf925a3ea58de176521be459a61f4317eec3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assetsas a Cloud Service] を使用すると、 [!DNL Workfront for Experience Manager enhanced connector] 以前のバージョンから最新のバージョンに移行する場合。

>[!TIP]
>
>次を検索していますか： [!DNL Workfront for Experience Manager enhanced connector] AEM 6.5 に関するドキュメントを更新しましたか？ クリック [ここ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


次の手順で [!DNL Workfront for Experience Manager enhanced connector] を最新バージョンに変更するには：

1. 拡張コネクタの最新バージョンをからダウンロードします。 [Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [アクセス](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) Cloud Manager からAEM as a Cloud Serviceリポジトリのクローンを作成します。

1. 任意の IDE を使用して、クローンExperience Manageras a Cloud Serviceリポジトリを開きます。

1. 手順 1 でダウンロードした拡張コネクタ zip ファイルを次のパスに配置します。

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >この `resources` フォルダーが存在しません。フォルダーを作成します。

1. 親の拡張コネクタのバージョンを更新 `pom.xml`.

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

1. の依存関係を更新します。 `all module pom.xml`.

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
   >必ず `<scope>` および `<systemPath>` を手順 5 と手順 6 の依存関係に追加します。

1. 更新 `pom.xml` 埋め込み すべてのサブプロジェクトの `pom.xml` の `embeddeds` セクションに [!DNL Workfront for Experience Manager enhanced connector] パッケージを追加します。すべてのモジュールに更新を組み込む `pom.xml`.

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

1. [Hoodoo 配布ポイントの依存関係を削除します](remove-external-dependencies.md)（存在する場合）

1. 変更をリポジトリにプッシュします。

1. 次の場所にパイプラインを実行 [Cloud Manager に変更をデプロイします。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
