---
title: AEM コネクタの登録
description: Adobe Experience Manager（AEM）as a Cloud Service でコネクタを正しく参照およびデプロイする方法を説明します。
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
feature: Operations
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 100%

---

# AEM コネクタの登録

以下に、Adobe Experience Manager（AEM）Connectors の送信に役立つ便利な情報を示します。コネクタの[実装](implement.md)と[保守](maintain.md)に関する記事と併せてお読みください。

AEM コネクタは [Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html) に一覧表示されています。

これまでの AEM ソリューションでは、 [パッケージマネージャー](/help/implementing/developing/tools/package-manager.md) を使用して様々な AEM インスタンスにコネクタをインストールしていました。しかし、AEM as a Cloud Service では、Cloud Manager の CI/CD プロセスでコネクタがデプロイされます。コネクタをデプロイするには、Maven プロジェクトの pom.xml でコネクタを参照する必要があります。

パッケージをプロジェクトに組み込む方法には、様々な選択肢があります。

1. パートナーの公開リポジトリー - 公にアクセス可能な Maven リポジトリーでパートナーがコンテンツパッケージをホストします。
1. パートナーのパスワードで保護されたリポジトリ - パスワードで保護された Maven リポジトリでパートナーがコンテンツパッケージをホストします。手順について詳しくは、[パスワードで保護された Maven リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=ja#password-protected-maven-repositories)を参照してください。
1. アーティファクトのバンドル - ユーザーの Maven プロジェクトにコネクタパッケージがローカルに含まれます。

パッケージは、ホストされている場所に関係なく、ベンダーから提供されるとおりに、パッケージを依存関係として pom.xml で参照する必要があります。

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

ISV パートナーがインターネットにアクセス可能な（Cloud Manager でアクセス可能な）Maven リポジトリでコネクタをホストする場合、ISV は `pom.xml` を配置できるリポジトリ設定を提供する必要があります。その理由は、ローカルでも Cloud Manager でも、コネクタの依存関係（上記）をビルド時に解決できるからです。

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

ISV パートナーがコネクタをダウンロード可能ファイルとして配布することを選択した場合、ISV が手順を提供する必要があります。手順では、AEM プロジェクトの一環として Git にチェックインする必要があるローカルファイルシステムの Maven リポジトリに、ファイルをデプロイする方法を説明する必要があります。これにより、Cloud Manager はこれらの依存関係を解決できます。
