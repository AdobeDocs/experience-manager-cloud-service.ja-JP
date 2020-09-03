---
title: AEM コネクタの登録
description: AEM コネクタの登録
translation-type: tm+mt
source-git-commit: d4e376ab30bb3e1fb533ed32f6ac43580775787c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 91%

---


AEM コネクタの登録
===========================

AEM コネクタの登録に役立つ情報を以下に示します。コネクタの[実装](implement.md)と[管理](maintain.md)に関する記事と共に参照してください。

AEM コネクタは [Adobe Exchange](https://partners.adobe.com/jp/exchangeprogram/experiencecloud) に一覧表示されています。

これまでの AEM ソリューションでは、パッケージマネージャーを使用して様々な AEM インスタンスにコネクタをインストールしていました。しかし、AEM as a Cloud Service では、Cloud Manager の CI/CD プロセスでコネクタがデプロイされます。コネクタをデプロイするには、Maven プロジェクトの pom.xml でコネクタを参照する必要があります。

パッケージをプロジェクトに組み込む方法には、様々な選択肢があります。

1. パートナーの公開リポジトリ - 公にアクセス可能な Maven リポジトリでパートナーがコンテンツパッケージをホストします。
1. パートナーのパスワードで保護されたリポジトリ — パートナーは、パスワードで保護されたMavenリポジトリでコンテンツパッケージをホストします。 手順については、 [パスワードで保護されたMavenリポジトリ](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories) (「」)を参照してください。
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

インターネットでアクセス可能な Maven リポジトリ（Cloud Manager を通じてアクセス可能な場合など）で ISV パートナーがコネクタをホストする場合、ISV は、pom.xml を配置できるリポジトリ設定を提供して、上記のコネクタ依存関係をビルド時に（ローカルでも Cloud Manager でも）解決できるようにする必要があります。

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

ISV パートナーがコネクタをダウンロード可能なファイルとして配布する場合、ISV は、Cloud Manager がこれらの依存関係を解決できるように、AEM プロジェクトの一部として Git にチェックインする必要があるローカルファイルシステム Maven リポジトリにファイルをデプロイする方法を指示する必要があります。
