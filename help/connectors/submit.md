---
title: AEM Connectorの送信
description: AEM Connectorの送信
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


AEM Connectorの送信
===========================

以下に、AEM Connectorsの送信に役立つ情報を示します。コネクタの実装と管理に関する記事と共に参照 [し](implement.md) て [ください](maintain.md) 。

AEM Connectorsは [Adobe Exchangeに表示されます](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace.html)。

以前のAEMソリューションでは、Package Managerを使用して様々なAEMインスタンスにコネクターをインストールしていました。 ただし、AEMをクラウドサービスとして使用する場合、Cloud ManagerのCI/CDプロセス中にコネクターがデプロイされます。 コネクタをデプロイするには、Mavenプロジェクトのpom.xmlでコネクタを参照する必要があります。

プロジェクトにパッケージを含める方法には、様々なオプションがあります。

1. パートナーのパブリック・リポジトリ — パートナーは、公開アクセス可能なMavenリポジトリでコンテンツ・パッケージをホストします。
1. バンドルされたアーティファクト — この場合、コネクタパッケージは、お客様のMavenプロジェクトにローカルに含まれます。

パッケージは、ホストされている場所に関係なく、ベンダーが提供するpom.xmlの依存関係として参照する必要があります。

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

ISVパートナーがインターネットにアクセス可能なMavenリポジトリ（Cloud Managerにアクセス可能ななど）でコネクタをホストしている場合、ISVはpom.xmlを配置できるリポジトリ設定を提供し、上記のコネクタの依存関係をビルド時（ローカルでもCloud Managerでも解決できます）。

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

ISVパートナーがConnectorをダウンロード可能ファイルとして配布する場合、ISVは、AEMプロジェクトの一部としてGitにチェックインする必要があるローカルファイルシステムMavenリポジトリにファイルを展開する方法を指示する必要があります。
