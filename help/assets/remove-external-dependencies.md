---
title: 既存のインストールの外部依存関係の削除
description: 既存のインストールの外部依存関係の削除
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 17%

---

# 既存のインストールの外部依存関係の削除 {#remove-external-depedencies}

Adobeでは、Workfrontの既存の拡張コネクタインストールに対して設定手順を実行し、Hoodo 配布ポイントへの依存関係を削除することをお勧めします。

>[!NOTE]
>
>設定手順は、2022 年 3 月以前にWorkfront用拡張コネクタをインストールした場合にのみ実行してください。 2022 年 3 月以降、Workfrontの新しい拡張コネクタインストールに関しては、Hoodoo 配布ポイントに依存しません。

外部の依存関係を削除するには：

1. 親から次の Hoodoo リポジトリ設定を削除します。 `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 次のサーバー設定を `settings.xml` ファイル、次の場所にあります。 `./cloudmanager/maven/settings.xml`:

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

1. を実行します。 [新しいインストール手順](workfront-connector-install.md).
