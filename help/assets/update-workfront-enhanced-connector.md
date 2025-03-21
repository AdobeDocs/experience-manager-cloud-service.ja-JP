---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 89%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup>Dynamic Media Prime<a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM AssetsUltimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM AssetsとEdge Delivery Servicesの統合 </b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i> 新規 </i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 拡張機能 </b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Dynamic Media Prime</i></sup>Ultimateの新 <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b> 能 </b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>検索のベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>メタデータのベストプラクティス</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>コンテンツハブ</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>OpenAPI 機能を備えた Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開発者向けドキュメント</b></a>
        </td>
    </tr>
</table>

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
