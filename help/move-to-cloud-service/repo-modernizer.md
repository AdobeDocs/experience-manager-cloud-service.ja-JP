---
title: Repository Modenizer
description: Repository Modenizer
translation-type: tm+mt
source-git-commit: fd70f5b6a17666d411a64a8fb3961555a42a5430
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 3%

---


# Repository Modenizer {#repo-modernizer}

Repository Modenizerは、Cloud ServiceとしてAdobe Experience Managerに定義されたプロジェクト構造と互換性を持つように、コンテンツとコードを個別のパッケージに分割して、既存のプロジェクトパッケージを再構築するために開発されたユーティリティです。

## 概要 {#introduction}

Cloud ServiceとしてのAdobe Experience Managerは、AEMプロジェクトに多くの新機能と可能性を提供します。 ただし、AEMCloud Serviceとの互換性を保つために、Adobe Experience ManagerMavenプロジェクトにはいくつかの変更が必要です。 高レベルでは、AEMは、可変コンテンツと不変コンテンツの分割を考慮して **、** コンテンツ **と** コードを個別のサブパッケージに分離する必要があります。 Cloud Service用の新しいAEMプロジェクト構造の詳細は、 [AEMプロジェクト構造](https://docs.adobe.com/content/help/ja-JP/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.translate.html) （英語）を参照してください。

Repository Modenizerは、次の配置構造を作成することで、互換性のあるAEMCloud Serviceプロジェクト構造を作成します。

* `ui.apps` パッケージがすべてのコードに展開 `/apps` され、コードが含まれます

* `ui.content` 実行時に書き込み可能な領域(例： `/content`、 `/conf`、、 `/home`または何も含まない `/apps`)、およびすべてのコンテンツと設定が含まれます。

* `all` packageは、サブパッケージとを含むコンテナパッケージ `ui.apps` で `ui.content`す。

## リポジトリの最新化の使用 {#using-repo-modernizer}

* AdobeI/O CLIを使用：AdobeI/O CLIのCloud Serviceコードリファクタリングプラグインとして、 `aio-cli-plugin-aem-cloud-service-migration` AEMを介してRepository Modenizerを使用することをお勧めします。

   詳しくは、 **[Gitリソースを参照してください。aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 」を参照してください。

* スタンドアロンユーティリティとして、リポジトリ・モダナイザは、スタンドアロン・ユーティリティとして実行することもできます。

   詳しくは、 **[Gitリソースを参照してください。Repository Modenizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** （リポジトリの最新化）を参照してください。
