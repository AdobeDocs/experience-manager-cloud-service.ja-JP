---
title: AEM コネクタの登録
description: AEM コネクタの登録
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 94%

---

AEM コネクタの登録
===========================

AEM コネクタの登録に役立つ情報を以下に示します。コネクタの[実装](implement.md)と[管理](maintain.md)に関する記事と共に参照してください。

AEM コネクタは [Adobe Exchange](https://partners.adobe.com/jp/exchangeprogram/experiencecloud) に一覧表示されています。

以前のAEMソリューションでは、 [パッケージマネージャー](/help/implementing/developing/tools/package-manager.md) は、様々なAEMインスタンスにコネクタをインストールするために使用されていました。 しかし、AEM as a Cloud Service では、Cloud Manager の CI/CD プロセスでコネクタがデプロイされます。コネクタをデプロイするには、Maven プロジェクトの pom.xml でコネクタを参照する必要があります。

パッケージをプロジェクトに組み込む方法には、様々な選択肢があります。

1. パートナーの公開リポジトリー - 公にアクセス可能な Maven リポジトリーでパートナーがコンテンツパッケージをホストします。
1. パスワードで保護されたパートナーのリポジトリー - パスワードで保護された Maven リポジトリーでパートナーがコンテンツパッケージをホストします。手順については、[パスワードで保護された Maven リポジトリーのサポート](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=ja#password-protected-maven-repositories)を参照してください。
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

インターネットでアクセス可能な Maven リポジトリー（Cloud Manager を通じてアクセス可能な場合など）で ISV パートナーがコネクタをホストする場合、ISV は、pom.xml を配置できるリポジトリー設定を提供して、上記のコネクタ依存関係をビルド時に（ローカルでも Cloud Manager でも）解決できるようにする必要があります。

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

ISV パートナーがコネクタをダウンロード可能なファイルとして配布する場合、ISV は、Cloud Manager がこれらの依存関係を解決できるように、AEM プロジェクトの一部として Git にチェックインする必要があるローカルファイルシステム Maven リポジトリーにファイルをデプロイする方法を指示する必要があります。
