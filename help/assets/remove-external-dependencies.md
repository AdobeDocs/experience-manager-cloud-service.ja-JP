---
title: 既存のインストールの外部依存関係の削除
description: 既存のインストールの外部依存関係の削除
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '104'
ht-degree: 100%

---

# 既存のインストールの外部依存関係の削除 {#remove-external-depedencies}

Workfront の既存の拡張コネクタインストールに対して設定手順を実行して、Hoodo 配布ポイントへの依存関係を削除することをお勧めします。

>[!NOTE]
>
>この設定手順は、2022年3月より前に Workfront の拡張コネクタをインストールした場合にのみ実行してください。2022年3月以降、Workfront の新しい拡張コネクタインストールについては、Hoodoo 配布ポイントへの依存関係はありません。

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
