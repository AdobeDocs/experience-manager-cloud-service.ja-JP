---
title: 既存のインストールの外部依存関係の削除
description: 既存のインストールの外部依存関係の削除
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: 230ca753bd5f3d5b26b30a962a526dc0edfc9bd4
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 100%

---

# 既存のインストールの外部依存関係の削除 {#remove-external-depedencies}

Workfront の既存の拡張コネクタインストールに対して設定手順を実行して、Hoodo 配布ポイントへの依存関係を削除することをお勧めします。

>[!NOTE]
>
>この設定手順は、2022年3月より前に Workfront の拡張コネクタをインストールした場合にのみ実行してください。 2022年3月以降、Workfront の新しい拡張コネクタインストールについては、Hoodoo 配布ポイントへの依存関係はありません。

外部の依存関係を削除するには：

1. 親の `pom.xml` から次の Hoodoo リポジトリー設定を削除します。

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. `settings.xml` ファイル（`./cloudmanager/maven/settings.xml`）から次のサーバー設定を削除します。

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

1. [新しいインストール手順](workfront-connector-install.md)を実行します。


**関連情報**

* [アセットを翻訳](/help/assets/translate-assets.md)
* [Assets HTTP API](/help/assets/mac-api-assets.md)
* [AEM Assets as a Cloud Service でサポートされているファイル形式](/help/assets/file-format-support.md)
* [アセットを検索](/help/assets/search-assets.md)
* [接続されたアセット](/help/assets/use-assets-across-connected-assets-instances.md)
* [アセットレポート](/help/assets/asset-reports.md)
* [メタデータスキーマ](/help/assets/metadata-schemas.md)
* [アセットをダウンロード](/help/assets/download-assets-from-aem.md)
* [メタデータを管理](/help/assets/manage-metadata.md)
* [Dynamic Media テンプレートの管理](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [レポートの管理](/help/assets/manage-reports-assets-view.md)
* [検索ファセット](/help/assets/search-facets.md)
* [コレクションを管理](/help/assets/manage-collections.md)
* [メタデータの一括読み込み](/help/assets/metadata-import-export.md)
* [AEM および Dynamic Media へのアセットの公開](/help/assets/publish-assets-to-aem-and-dm.md)
